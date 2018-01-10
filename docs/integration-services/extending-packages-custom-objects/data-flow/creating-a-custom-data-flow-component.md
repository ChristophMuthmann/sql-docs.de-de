---
title: Erstellen einer benutzerdefinierten Datenflusskomponente | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- design-time component interface [Integration Services]
- custom data flow components [Integration Services], about data flow components
- custom data flow components [Integration Services]
- data flow components [Integration Services]
- data flow components [Integration Services], developing
ms.assetid: 9d96bcf5-eba8-44bd-b113-ed51ad0d0521
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2ef59aa198958341e6349118ce200feadf2d88ed
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="creating-a-custom-data-flow-component"></a>Erstellen einer benutzerdefinierten Datenflusskomponente
  In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] stellt der Datenflusstask ein Objektmodell zur Verfügung, das Entwicklern das Erstellen von benutzerdefinierten Datenflusskomponenten (Quellen, Transformationen und Ziele) anhand von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] und verwaltetem Code ermöglicht.  
  
 Ein Datenflusstask besteht aus Komponenten, die eine <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>-Schnittstelle und eine Auflistung von <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100>-Objekten enthalten, die die Verschiebung von Daten zwischen Komponenten definieren.  
  
> [!NOTE]  
>  Wenn Sie einen benutzerdefinierten Anbieter erstellen, müssen Sie die Datei "ProviderDescriptors.xml" mit den Metadatenspaltenwerten aktualisieren.  
  
## <a name="design-time-and-run-time"></a>Entwurfszeit und Laufzeit  
 Vor der Ausführung befindet sich der Datenflusstask im so genannten Entwurfszeitstatus, während er inkrementelle Änderungen durchläuft. Zu den Änderungen kann das Hinzufügen oder Entfernen von Komponenten, das Hinzufügen oder Entfernen von Pfadobjekten zur Verbindung von Komponenten sowie Änderungen an den Metadaten der Komponenten gehören. Wenn Metadaten-Änderungen auftreten, kann die Komponente die Änderungen überwachen und darauf reagieren. Zum Beispiel kann eine Komponente bestimmte Änderungen nicht zulassen oder zusätzliche Änderungen als Reaktion auf eine Änderung vornehmen. Zur Entwurfszeit interagiert der Designer mit einer Komponente durch die Entwurfszeitschnittstelle <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100>.  
  
 Zur Ausführungszeit wird vom Datenflusstask die Reihenfolge von Komponenten überprüft, ein Ausführungsplan vorbereitet und ein Pool von Arbeitsthreads verwaltet, die den Arbeitsplan ausführen. Auch wenn jeder Arbeitsthread einige interne Arbeiten im Datenflusstask ausführt, besteht die Hauptaufgabe des Arbeitsthread darin, die Methoden der Komponenten über die Laufzeitschnittstelle <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100> aufzurufen.  
  
## <a name="creating-a-component"></a>Erstellen einer Komponente  
 Zum Erstellen einer Datenflusskomponente leiten Sie eine Klasse von der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>-Basisklasse ab, wenden die <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>-Klasse an und überschreiben dann die entsprechenden Methoden der Basisklasse. Mit <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> werden die Schnittstellen <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> und <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100> implementiert und die Methoden zum Überschreiben in der Komponente zur Verfügung gestellt.  
  
 Abhängig von den in der Komponente verwendeten Objekten erfordert Ihr Projekt Verweise auf einige oder alle der folgenden Assemblys:  
  
|Funktion|Verweis auf Assembly|Zu importierender Namespace|  
|-------------|---------------------------|-------------------------|  
|Datenfluss|Microsoft.SqlServer.PipelineHost|<xref:Microsoft.SqlServer.Dts.Pipeline>|  
|Datenfluss-Wrapper|Microsoft.SqlServer.DTSPipelineWrap|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>|  
|Typ|Microsoft.SQLServer.ManagedDTS|<xref:Microsoft.SqlServer.Dts.Runtime>|  
|Laufzeit-Wrapper|Microsoft.SqlServer.DTSRuntimeWrap|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper>|  
  
 Im folgenden Codebeispiel werden eine einfache, von der Basisklasse abgeleitete Komponente veranschaulicht und <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> angewendet. Sie müssen einen Verweis auf die Microsoft.SqlServer.DTSPipelineWrap-Assembly hinzufügen.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "SampleComponent", ComponentType = ComponentType.Transform )]  
    public class BasicComponent: PipelineComponent  
    {  
        // TODO: Override the base class methods.  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
<DtsPipelineComponent(DisplayName:="SampleComponent", ComponentType:=ComponentType.Transform)> _  
Public Class BasicComponent  
  
    Inherits PipelineComponent  
  
    ' TODO: Override the base class methods.  
  
End Class  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Entwickeln einer Benutzeroberfläche für eine Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-user-interface-for-a-data-flow-component.md)  
  
  
