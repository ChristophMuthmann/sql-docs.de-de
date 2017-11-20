---
title: "Ausführungsplan und Pufferzuordnung | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom data flow components [Integration Services], buffer allocations
- custom data flow components [Integration Services], execution plans
- buffer allocations [Integration Services]
- data flow components [Integration Services], buffer allocations
- data flow components [Integration Services], execution plans
- execution plans [Integration Services]
ms.assetid: 679d9ff0-641e-47c3-abb8-d1a7dcb279dd
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 931196de739980cb889f120b977b82bfb313ddd9
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="execution-plan-and-buffer-allocation"></a>Ausführungsplan und Pufferzuordnung
  Vor der Ausführung überprüft der Datenflusstask seine Komponenten und erstellt einen Ausführungsplan für jede Komponentensequenz. Dieser Abschnitt enthält Einzelheiten zum Ausführungsplan, zur Anzeige des Plans und zur Zuweisung von Eingabe- und Ausgabepuffern anhand des Plans.  
  
## <a name="understanding-the-execution-plan"></a>Grundlegendes zum Ausführungsplan  
 Ein Ausführungsplan enthält Quell- und Arbeitsthreads. Diese umfassen jeweils Arbeitslisten, die bei Quellthreads Ausgabearbeitslisten und bei Arbeitsthreads Eingabe- und Ausgabearbeitslisten festlegen. Die Quellthreads eines Ausführungsplans stellen die Quellkomponenten im Datenfluss dar und werden im Ausführungsplan von identifiziert *SourceThread**n*, wobei  *n*  die nullbasierte Nummer des Quellthreads ist.  
  
 Jeder Quellthread erstellt einen Puffer, legt eine Überwachung fest und ruft die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>-Methode der Quellkomponente auf. Dies ist der Punkt, an dem die Ausführung beginnt und von dem die Daten stammen. Die Quellkomponente beginnt, den Ausgabepuffern Zeilen hinzuzufügen, die vom Datenflusstask bereitgestellt werden. Sobald die Quellthreads ausgeführt werden, wird die Arbeitslast auf die Arbeitsthreads aufgeteilt.  
  
 Ein Arbeitsthread kann sowohl Eingabe- und Ausgabespalten Arbeitslisten enthalten und wird im Ausführungsplan als identifiziert *WorkThread**n*, wobei  *n*  ist die nullbasierte Nummer des Threads Arbeit. Diese Threads enthalten Ausgabearbeitslisten, wenn das Diagramm eine Komponente mit asynchronen Ausgaben enthält.  
  
 Das folgende Beispiel eines Ausführungsplans zeigt einen Datenfluss, der eine Quellkomponente umfasst, die mit einer Transformation mit einer asynchronen Ausgabe verbunden ist, die über eine Verbindung mit einer Zielkomponente verfügt. In diesem Beispiel enthält WorkThread0 eine Ausgabearbeitsliste, da die Transformationskomponente über eine asynchrone Ausgabe verfügt.  
  
```  
SourceThread0   
    Influences: 72 158   
    Output Work List   
        CreatePrimeBuffer of type 1 for output id 10   
        SetBufferListener: "WorkThread0" for input ID 73   
        CallPrimeOutput on component "OLE DB Source" (1)   
    End Output Work List   
    This thread drives 0 distributors   
End SourceThread0   
WorkThread0   
    Influences: 72 158   
    Input Work list, input ID 73   
        CallProcessInput on input ID 73 on component "Sort" (72) for view type 2   
    End Input Work list for input 73   
    Output Work List   
        CreatePrimeBuffer of type 3 for output id 74   
        SetBufferListener: "WorkThread1" for input ID 171with internal handoff   
        CallPrimeOutput on component "Sort" (72)   
    End Output Work List   
    This thread drives 0 distributors   
End WorkThread0   
WorkThread1   
    Influences: 158   
    Input Work list, input ID 171  
        CallProcessInput on input ID 171 on component "OLE DB Destination" (158) for view type 4  
    End Input Work list for input 171   
    Output Work List   
    End Output Work List   
    This thread drives 0 distributors   
End WorkThread1  
```  
  
> [!NOTE]  
>  Der Ausführungsplan generiert jedes Mal, wenn ein Paket ausgeführt wird und aufgezeichnet werden kann, durch Hinzufügen eines Protokollanbieters für das Paket, die Protokollierung aktivieren, und wählen die **PipelineExecutionPlan** Ereignis.  
  
## <a name="understanding-buffer-allocation"></a>Grundlegendes zur Pufferzuordnung  
 Der Datenflusstask erstellt anhand des Ausführungsplans Puffer, in denen die in den Ausgaben der Datenflusskomponenten definierten Spalten enthalten sind. Wenn der Datenfluss die Komponentensequenz durchläuft, wird der Puffer wiederverwendet, bis eine Komponente mit asynchroner Ausgabe auftritt. In diesem Fall wird ein neuer Puffer erstellt, der die Ausgabespalten der asynchronen Ausgabe sowie diejenigen der Downstreamkomponenten umfasst.  
  
 Während der Ausführung verfügen die Komponenten über Zugriff auf die Puffer im aktuellen Quell- oder Arbeitsthread. Bei dem Puffer handelt es sich entweder um einen Eingabepuffer, der von der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>-Methode bereitgestellt wird, oder um einen Ausgabepuffer, der von der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>-Methode bereitgestellt wird. Die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.Mode%2A>-Eigenschaft des <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> identifiziert jeden Puffer als Eingabe- oder Ausgabepuffer.  
  
 Transformationskomponenten mit asynchronen Ausgaben erhalten den vorhandenen Eingabepuffer von der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>-Methode sowie den neuen Ausgabepuffer von der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>-Methode. Transformationskomponenten mit asynchronen Ausgaben sind der einzige Datenflusskomponententyp, der sowohl Eingabe- als auch Ausgabepuffer erhält.  
  
 Ist der Puffer bereitgestellt, um eine Komponente enthalten wahrscheinlich mehr Spalten als die Komponente hat, in ihren Eingabe-oder Ausgabespalte Auflistungen, Komponentenentwickler rufen die <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> Methode zum Suchen einer Spalteninhalts im Puffer durch Angabe seiner **LineageID**.  
  

