---
title: Erstellen eines benutzerdefinierten Tasks | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: extending-packages-custom-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom tasks [Integration Services], creating
ms.assetid: 42965c09-1782-4cdb-9ce1-216af4c23e0a
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1160df297872da3bdbb8c09ffcbd99636865219a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="creating-a-custom-task"></a>Erstellen eines benutzerdefinierten Tasks
  Die Schritte zum Erstellen eines benutzerdefinierten Tasks ähneln denen jedes anderen benutzerdefinierten Objekts für [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]:  
  
-   Erstellen Sie eine neue Klasse, die von der Basisklasse erbt. Für einen Task ist die Basisklasse <xref:Microsoft.SqlServer.Dts.Runtime.Task>.  
  
-   Weisen Sie das Attribut zu, das den Typ des Objekts für die Klasse identifiziert. Für einen Task ist das Attribut <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>.  
  
-   Überschreiben Sie die Implementierung der Methoden und Eigenschaften der Basisklasse. Für einen Task sind dies die Methoden <xref:Microsoft.SqlServer.Dts.Runtime.Task.Validate%2A> und <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>.  
  
-   Entwickeln Sie optional eine individuelle Benutzeroberfläche. Für einen Task ist dazu eine Klasse erforderlich, die die <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>-Schnittstelle implementiert.  
  
## <a name="getting-started-with-a-custom-task"></a>Erste Schritte mit einem benutzerdefinierten Task  
  
### <a name="creating-projects-and-classes"></a>Erstellen von Projekten und Klassen  
 Da alle verwalteten Tasks von der <xref:Microsoft.SqlServer.Dts.Runtime.Task>-Basisklasse abgeleitet sind, besteht der erste Schritt beim Erstellen eines benutzerdefinierten Tasks darin, in Ihrer bevorzugten verwalteten Programmiersprache ein Klassenbibliotheksprojekt anzulegen und eine Klasse zu generieren, die von der Basisklasse erbt. In dieser abgeleiteten Klasse überschreiben Sie die Methoden und Eigenschaften der Basisklasse, um die benutzerdefinierten Funktionen zu implementieren.  
  
 Erstellen Sie in der gleichen Lösung ein zweites Klassenbibliotheksprojekt für die individuelle Benutzeroberfläche. Für eine einfache Bereitstellung sollten Sie eine eigene Assembly für die Benutzeroberfläche verwenden, da Sie so den Verbindungs-Manager oder seine Benutzeroberfläche unabhängig aktualisieren und erneut bereitstellen können.  
  
 Konfigurieren Sie beide Projekte für das Signieren der Assemblys, die bei der Erstellung erzeugt werden, mit einer Schlüsseldatei mit starkem Namen.  
  
### <a name="applying-the-dtstask-attribute"></a>Zuweisen des 'DtsTask'-Attributs  
 Weisen Sie das <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>-Attribut der Klasse zu, die Sie erstellt haben, um sie als Task zu kennzeichnen. Dieses Attribut stellt Entwurfszeitinformationen, z. B. Name, Beschreibung und Tasktyp des Tasks, bereit.  
  
 Verwenden Sie die <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.UITypeName%2A>-Eigenschaft, um den Task mit der individuellen Benutzeroberfläche zu verknüpfen. Um das für diese Eigenschaft erforderliche öffentliche Schlüsseltoken zu erhalten, können Sie **sn.exe -t** verwenden. Damit zeigen Sie das öffentliche Schlüsseltoken aus der Schlüsselpaardatei (.snk) an, die Sie für das Signieren der Benutzeroberflächenassembly verwenden möchten.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
namespace Microsoft.SSIS.Samples  
{  
  [DtsTask  
  (  
   DisplayName = "MyTask",  
   IconResource = "MyTask.MyTaskIcon.ico",  
   UITypeName = "My Custom Task," +  
   "Version=1.0.0.0," +  
   "Culture = Neutral," +  
   "PublicKeyToken = 12345abc6789de01",  
   TaskType = "PackageMaintenance",  
   TaskContact = "MyTask; company name; any other information",  
   RequiredProductLevel = DTSProductLevel.None  
   )]  
  public class MyTask : Task  
  {  
    // Your code here.  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsTask(DisplayName:="MyTask", _  
 IconResource:="MyTask.MyTaskIcon.ico", _  
 UITypeName:="My Custom Task," & _  
 "Version=1.0.0.0,Culture=Neutral," & _  
 "PublicKeyToken=12345abc6789de01", _  
 TaskType:="PackageMaintenance", _  
 TaskContact:="MyTask; company name; any other information", _  
 RequiredProductLevel:=DTSProductLevel.None)> _  
Public Class MyTask  
  Inherits Task  
  
  ' Your code here.  
  
End Class 'MyTask  
```  
  
## <a name="building-deploying-and-debugging-a-custom-task"></a>Erstellen, Bereitstellen und Debuggen eines benutzerdefinierten Tasks  
 Die Schritte zum Erstellen, Bereitstellen und Debuggen eines benutzerdefinierten Tasks in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] ähneln denen für andere Typen benutzerdefinierter Objekte. Weitere Informationen finden Sie unter [Building, Deploying, and Debugging Custom Objects](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md) (Erstellen, Bereitstellen und Debuggen von benutzerdefinierten Objekten).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen eines benutzerdefinierten Tasks](../../../integration-services/extending-packages-custom-objects/task/creating-a-custom-task.md)   
 [Codieren eines benutzerdefinierten Tasks](../../../integration-services/extending-packages-custom-objects/task/coding-a-custom-task.md)   
 [Entwickeln einer Benutzeroberfläche für einen benutzerdefinierten Task](../../../integration-services/extending-packages-custom-objects/task/developing-a-user-interface-for-a-custom-task.md)  
  
  
