---
title: Programmgesteuertes Erstellen von Paketen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: building-packages-programmatically
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: e44bcc70-32d3-43e8-a84b-29aef819d5d3
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a31311c4ab21e2862758da3f08c9649e72e4090d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="creating-a-package-programmatically"></a>Programmgesteuertes Erstellen eines Pakets
  Das <xref:Microsoft.SqlServer.Dts.Runtime.Package>-Objekt ist der Container oberster Ebene für alle anderen Objekte in einer [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Projektmappe. Als Container der obersten Ebene ist das Paket das erste Objekt, das erstellt wird. Nachfolgende Objekte werden diesem hinzugefügt und dann in dem Kontext des Pakets ausgeführt. Das Paket selbst verschiebt oder transformiert keine Daten. Das Paket ist zur Ausführung der Arbeit auf die Tasks angewiesen, die es enthält. Tasks führen den Großteil der von einem Paket ausgeführten Arbeit aus und definieren die Funktionalität eines Pakets. Ein Paket wird mit nur drei Codezeilen erstellt und ausgeführt. Um dem Paket zusätzliche Funktionalität zu verleihen, können jedoch verschiedene Tasks und <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>-Objekte hinzugefügt werden. In diesem Abschnitt wird erläutert, wie ein Paket programmgesteuert erstellt wird. Er enthält keine Informationen zum Erstellen der Tasks oder des <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>. Diese Themen werden in späteren Abschnitten behandelt.  
  
## <a name="example"></a>Beispiel  
 Zum Schreiben von Code mithilfe der Visual Studio-IDE ist ein Verweis auf Microsoft.SqlServer.ManagedDTS.DLL erforderlich, um eine `using`-Anweisung (`Imports` in Visual Basic .NET) für Microsoft.SqlServer.Dts.Runtime zu erstellen. Im folgenden Codebeispiel wird das Erstellen eines leeren Pakets veranschaulicht.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package package;  
      package = new Package();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Package  
    package = New Package  
  
  End Sub  
  
End Module  
```  
  
 Drücken Sie F5 in Visual Studio, um das Beispiel zu kompilieren und auszuführen. Verwenden Sie zum Erstellen des Codes mithilfe des C#-Compilers, **csc.exe**, an der Eingabeaufforderung für die Kompilierung den folgenden Befehl sowie die folgenden Dateiverweise, und ersetzen Sie *\<Dateiname>* durch den Namen der CS- oder VB-Datei. Legen Sie einen *\<Ausgabedateiname>* Ihrer Wahl fest.  
  
 **csc /target:library /out: \<Ausgabedateiname>.dll \<Dateiname>.cs /r:Microsoft.SqlServer.Managed DTS.dll" /r:System.dll**  
  
 Verwenden Sie zum Erstellen des Codes mithilfe des Visual Basic .NET-Compilers, **vbc.exe**, an der Eingabeaufforderung für die Kompilierung den folgenden Befehl sowie die folgenden Dateiverweise.  
  
 **vbc /target:library /out: \<Ausgabedateiname>.dll \<Dateiname>.vb /r:Microsoft.SqlServer.Managed DTS.dll" /r:System.dll**  
  
 Sie können auch ein Paket erstellen, indem Sie ein vorhandenes Paket, das auf der Festplatte gespeichert wurde, in das Dateisystem oder in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] laden. Der Unterschied besteht darin, dass das <xref:Microsoft.SqlServer.Dts.Runtime.Application>-Objekt zuerst erstellt wird und dann das Paketobjekt mit einer der überlasteten Methoden der Anwendung gefüllt wird: **LoadPackage** für Flatfiles, **LoadFromSQLServer** für Pakete, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert sind, oder <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A> für Pakete, die im Dateisystem gespeichert sind. Im folgenden Beispiel wird ein vorhandenes Paket von der Festplatte geladen. Anschließend werden die verschiedenen Eigenschaften des Pakets betrachtet.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class ApplicationTests  
  {  
    static void Main(string[] args)  
    {  
      // The variable pkg points to the location of the  
      // ExecuteProcess package sample that was installed with  
      // the SSIS samples.  
      string pkg = @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\ExecuteProcess Sample\ExecuteProcess\UsingExecuteProcess.dtsx";  
  
      Application app = new Application();  
      Package p = app.LoadPackage(pkg, null);  
  
      // Now that the package is loaded, we can query on  
      // its properties.  
      int n = p.Configurations.Count;  
      DtsProperty p2 = p.Properties["VersionGUID"];  
      DTSProtectionLevel pl = p.ProtectionLevel;  
  
      Console.WriteLine("Number of configurations = " + n.ToString());  
      Console.WriteLine("VersionGUID = " + (string)p2.GetValue(p));  
      Console.WriteLine("ProtectionLevel = " + pl.ToString());  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module ApplicationTests  
  
  Sub Main()  
  
    ' The variable pkg points to the location of the  
    ' ExecuteProcess package sample that was installed with  
    ' the SSIS samples.  
    Dim pkg As String = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\ExecuteProcess Sample\ExecuteProcess\UsingExecuteProcess.dtsx"  
  
    Dim app As Application = New Application()  
    Dim p As Package = app.LoadPackage(pkg, Nothing)  
  
    ' Now that the package is loaded, we can query on  
    ' its properties.  
    Dim n As Integer = p.Configurations.Count  
    Dim p2 As DtsProperty = p.Properties("VersionGUID")  
    Dim pl As DTSProtectionLevel = p.ProtectionLevel  
  
    Console.WriteLine("Number of configurations = " & n.ToString())  
    Console.WriteLine("VersionGUID = " & CType(p2.GetValue(p), String))  
    Console.WriteLine("ProtectionLevel = " & pl.ToString())  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **Beispielausgabe:**  
  
 `Number of configurations = 2`  
  
 `VersionGUID = {09016682-89B8-4406-AAC9-AF1E527FF50F}`  
  
 `ProtectionLevel = DontSaveSensitive`  
  
## <a name="external-resources"></a>Externe Ressourcen  
  
-   Blogeintrag, [API Sample – OleDB source and OleDB destination](http://go.microsoft.com/fwlink/?LinkId=220824), (API-Beispiel – OleDB-Quelle und OleDB-Ziel) auf blogs.msdn.com.  
  
-   Blogeintrag, [EzAPI – Updated for SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=243223) (EzAPI – aktualisiert für SQL Server 2012), auf blogs.msdn.com.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Programmgesteuertes Hinzufügen von Tasks](../../integration-services/building-packages-programmatically/adding-tasks-programmatically.md)  
  
  
