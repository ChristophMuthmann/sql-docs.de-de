---
title: "Teilen eines Datasets mithilfe der Transformation für bedingtes Teilen | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Conditional Split transformation
- splitting dataset
- datasets [Integration Services], splitting
ms.assetid: 23b3e84f-9296-4dc9-81c0-c7f06ae3f1ff
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 8248e068541c6bd72b21f78d121811f4851850bb
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="split-a-dataset-by-using-the-conditional-split-transformation"></a>Teilen eines Datasets mithilfe der Transformation für bedingtes Teilen
  Das Paket muss bereits mindestens einen Datenflusstask und eine Quelle enthalten, damit Sie eine Transformation für bedingtes Teilen hinzufügen und konfigurieren können.  
  
### <a name="to-conditionally-split-a-dataset"></a>So führen Sie eine bedingte Teilung eines Datasets aus  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Datenfluss** , und ziehen Sie dann aus **Toolbox**die Transformation für bedingtes Teilen auf die Entwurfsoberfläche.  
  
4.  Verbinden Sie die Transformation für bedingtes Teilen mit dem Datenfluss, indem Sie den Konnektor von der Datenquelle oder der vorherigen Transformation auf die Transformation für bedingtes Teilen ziehen.  
  
5.  Doppelklicken Sie auf die Transformation für bedingtes Teilen.  
  
6.  Erstellen Sie in **Transformations-Editor für bedingtes Teilen**die Ausdrücke, die als Bedingungen verwendet werden sollen, indem Sie Variablen, Spalten, Funktionen und Operatoren in die **Bedingung** -Spalte im Raster ziehen. Sie können den Ausdruck auch in die **Bedingung** -Spalte eingeben.  
  
    > [!NOTE]  
    >  Eine Variable oder Spalte kann in mehreren Ausdrücken verwendet werden.  
  
    > [!NOTE]  
    >  Falls der Ausdruck ungültig ist, wird der Ausdruckstext hervorgehoben dargestellt, und die Fehler werden in einer QuickInfo in der Spalte beschrieben.  
  
7.  Optional können Sie die Werte in der **Ausgabename** -Spalte ändern. Die Standardnamen sind Fall 1, Fall 2 usw.  
  
8.  Klicken Sie auf den Pfeil nach oben oder den Pfeil nach unten, um die Reihenfolge zu ändern, in der die Bedingungen ausgewertet werden.  
  
    > [!NOTE]  
    >  Positionieren Sie die Bedingungen, die höchstwahrscheinlich vorhanden sind, am Anfang der Liste.  
  
9. Optional können Sie den Namen der Standardausgabe für Datenzeilen ändern, die mit keiner Bedingung übereinstimmen.  
  
10. Klicken Sie auf **Fehlerausgabe konfigurieren**, um die Fehlerausgabe zu konfigurieren. Weitere Informationen finden Sie unter [Debugging Data Flow](../../../integration-services/troubleshooting/debugging-data-flow.md).  
  
11. Klicken Sie auf **OK**.  
  
12. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="see-also"></a>Siehe auch  
 [Transformation für bedingtes Teilen](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)   
 [Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services-Pfade](../../../integration-services/data-flow/integration-services-paths.md)   
 [Integration Services-Datentypen](../../../integration-services/data-flow/integration-services-data-types.md)   
 [Datenflusstask](../../../integration-services/control-flow/data-flow-task.md)   
 [Integrationsservices &#40; SSIS &#41; Ausdrücke](../../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  

