---
title: Programmgesteuertes Verbinden von Datenflusskomponenten | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- data flow task [Integration Services], components
- paths [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 404ecab7-7698-447b-93d6-dd256beb11ff
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 40869328965e049b5981e94655226bc0a78dc37f
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="connecting-data-flow-components-programmatically"></a>Programmgesteuertes Verbinden von Datenflusskomponenten
  Nachdem Sie dem Datenflusstask Komponenten hinzugefügt haben, verbinden Sie diese, um eine Ausführungsstruktur zu erstellen. Diese spiegelt den Datenfluss von den Quellen über Transformationen bis hin zu den Zielen wider. Sie verwenden <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100>-Objekte, um die Komponenten im Datenfluss zu verbinden.  
  
## <a name="creating-a-path"></a>Erstellen eines Pfads  
 Rufen Sie die neue Methode von der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.PathCollection%2A> Eigenschaft von der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipe> Benutzeroberfläche zum Erstellen eines neuen Pfads und der Auflistung der pfadauflistung im Datenflusstask hinzuzufügen. Diese Methode gibt ein neues, getrenntes <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100>-Objekt zurück. Sie verwenden dieses anschließend, um zwei Komponenten zu verbinden.  
  
 Rufen Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100.AttachPathAndPropagateNotifications%2A>-Methode auf, um den Pfad zu verbinden und die Komponenten im Pfad über die Verbindung in Kenntnis zu setzen. Diese Methode akzeptiert eine <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> der Upstreamkomponente sowie eine <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> der Downstreamkomponente als Parameter. Standardmäßig wird durch den Aufruf der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>-Methode der Komponente eine einzelne Eingabe für Komponenten, die über Eingaben verfügen, und eine einzelne Ausgabe für Komponenten, die über Ausgaben verfügen, erstellt. Im folgenden Beispiel wird diese Standardeinstellung für die Ausgabe der Quelle und die Eingabe des Ziels verwendet.  
  
## <a name="next-step"></a>Nächster Schritt  
 Nachdem Sie einen Pfad zwischen zwei Komponenten eingerichtet haben, ist der nächste Schritt Eingabespalten in der downstreamkomponente zuzuordnen, der im nächsten Thema erläutert wird, [Eingabe Spalten programmgesteuert auswählen](../../integration-services/building-packages-programmatically/selecting-input-columns-programmatically.md).  
  
## <a name="sample"></a>Beispiel  
 Im folgenden Codebeispiel wird die Einrichtung eines Pfads zwischen zwei Komponenten veranschaulicht.  
  
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
      Package package = new Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      TaskHost thMainPipe = e as TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;  
  
      // Create the source component.    
      IDTSComponentMetaData100 source =  
        dataFlowTask.ComponentMetaDataCollection.New();  
      source.ComponentClassID = "DTSAdapter.OleDbSource";  
      CManagedComponentWrapper srcDesignTime = source.Instantiate();  
      srcDesignTime.ProvideComponentProperties();  
  
      // Create the destination component.  
      IDTSComponentMetaData100 destination =  
        dataFlowTask.ComponentMetaDataCollection.New();  
      destination.ComponentClassID = "DTSAdapter.OleDbDestination";  
      CManagedComponentWrapper destDesignTime = destination.Instantiate();  
      destDesignTime.ProvideComponentProperties();  
  
      // Create the path.  
      IDTSPath100 path = dataFlowTask.PathCollection.New();  
      path.AttachPathAndPropagateNotifications(source.OutputCollection[0],  
        destination.InputCollection[0]);  
    }  
  }  
```  
  
 }  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' Create the source component.    
    Dim source As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    source.ComponentClassID = "DTSAdapter.OleDbSource"  
    Dim srcDesignTime As CManagedComponentWrapper = source.Instantiate()  
    srcDesignTime.ProvideComponentProperties()  
  
    ' Create the destination component.  
    Dim destination As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    destination.ComponentClassID = "DTSAdapter.OleDbDestination"  
    Dim destDesignTime As CManagedComponentWrapper = destination.Instantiate()  
    destDesignTime.ProvideComponentProperties()  
  
    ' Create the path.  
    Dim path As IDTSPath100 = dataFlowTask.PathCollection.New()  
    path.AttachPathAndPropagateNotifications(source.OutputCollection(0), _  
      destination.InputCollection(0))  
  
  End Sub  
  
End Module  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Programmgesteuertes auswählen von Eingabespalten](../../integration-services/building-packages-programmatically/selecting-input-columns-programmatically.md)  
  
  

