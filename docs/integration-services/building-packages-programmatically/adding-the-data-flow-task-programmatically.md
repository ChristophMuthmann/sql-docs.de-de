---
title: "Programmgesteuertes Hinzufügen von Datenflusstasks | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
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
- adding Data Flow task
- SSIS data flow
- data flow task [Integration Services], adding
- MainPipe object
ms.assetid: 0ca03712-a82e-4aa7-949b-f869a8936ddf
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0a7b0c3e51d7df76689f16ed91f60972d171bd9a
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="adding-the-data-flow-task-programmatically"></a>Programmgesteuertes Hinzufügen des Datenflusstasks
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] umfasst einen Task namens Datenflusstask, der durch den <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>-Namespace im Objektmodell dargestellt wird. Der Datenflusstask ist ein spezialisierter Hochleistungstask, der dem Transformieren und Verschieben von Daten bei der Paketausführung dient. Genau wie andere Tasks ist der Datenflusstask vom <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>-Objekt umschlossen, und aus Sicht des Laufzeitmoduls ist dieser Task nur einer der Tasks im Paket. Der Datenfluss enthält jedoch zusätzliche Objekte, die so genannten Datenflusskomponenten. Diese Komponenten bewirken, dass Daten von einer Quelle an ein Ziel verschoben werden, was manchmal durch eine Transformation erfolgt. Die Komponenten definieren sowohl die Richtung des Verschiebens als auch die Art der Datentransformation. Zum Konfigurieren des Datenflusstasks müssen dem Task Komponenten hinzugefügt und anschließend verbunden werden, damit der Datenfluss eingerichtet und die beabsichtigte Transformation erzielt wird.  
  
 Es gibt drei Arten von Komponenten in einem Datenflusstask: **Datenflussquellen**, **Datenflusstransformationen**, und **Datenflussziele**wie in dieser Reihenfolge in die [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer-Toolbox. Diese Typen werden auch einfacher als Quellen, Transformationen oder Ziele bezeichnet. Wie die Namen nahe legen, fließen Daten von einer Quelle zu einer Transformation und dann zu einem Ziel. Dies ist eine vereinfachte Beschreibung des Datenflusses zur Veranschaulichung des Konzepts. Der Datenflusstask ist jedoch flexibel und leistungsfähig genug, um mehrere Quellen zu verarbeiten und zahlreiche Transformationen miteinander zu verbinden, die Ausgabe an mehrere Ziele senden.  
  
 Der Datenflusstask wird einem Paket auf die gleiche Weise wie andere Tasks hinzugefügt. Nachdem der Task hinzugefügt wurde, wird er durch Hinzufügen von Komponenten zum Datenflusstask sowie Konfigurieren und Verbinden von Komponenten im Task konfiguriert.  
  
## <a name="sample"></a>Beispiel  
 Im folgenden Codebeispiel wird gezeigt, wie einem Paket ein Datenflusstask hinzugefügt wird. Für dieses Beispiel ist ein Verweis auf die Microsoft.SqlServer.PipelineHost-, Microsoft.SqlServer.DTSPipelineWrap- und Microsoft.SqlServer.ManagedDTS-Assemblys erforderlich.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      Executable e = p.Executables.Add("STOCK:PipelineTask");  
      TaskHost thMainPipe = e as TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;   
    }  
  }  
}  
```  
  
```vb  
Imports System.IO  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    Dim e As Executable = p.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As TaskHost = CType(e, TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>Externe Ressourcen  
 Blogeintrag, [EzAPI – Updated for SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=243223), auf blogs.msdn.com.  
  
## <a name="see-also"></a>Siehe auch  
 [Programmgesteuertes Auffinden von Datenflusskomponenten](../../integration-services/building-packages-programmatically/discovering-data-flow-components-programmatically.md)  
  
  
