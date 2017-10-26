---
title: Programmgesteuertes Arbeiten mit Variablen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- System namespace
- scope [Integration Services]
- variables [Integration Services], programmatically
- configuration files [Integration Services]
- Variables collection
- User namespace
- custom variables [Integration Services]
- variables [Integration Services], customizing
ms.assetid: c4b76a3d-94ca-4a8e-bb45-cb8bd0ea3ec1
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 5c8968302f42e1b8fde55894810ecb77cf715ab6
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="working-with-variables-programmatically"></a>Programmgesteuertes Arbeiten mit Variablen
  Variablen bieten die Möglichkeit, Werte dynamisch festzulegen und Prozesse in Paketen, Containern, Tasks und Ereignishandlern zu steuern. Variablen können auch von Rangfolgeneinschränkungen verwendet werden, um die Richtung des Datenflusses an andere Tasks zu steuern. Variablen haben vielerlei Verwendungszwecke:  
  
-   Aktualisieren der Eigenschaften eines Pakets zur Laufzeit.  
  
-   Auffüllen von Parameterwerten für Transact-SQL-Anweisungen zur Laufzeit.  
  
-   Kontrollieren des Flusses einer Foreach-Schleife. Weitere Informationen finden Sie unter [Enumeration eine Ablaufsteuerung](http://msdn.microsoft.com/library/f212b5fb-3cc4-422e-9b7c-89eb769a812a).  
  
-   Steuern einer Rangfolgeneinschränkung durch ihre Verwendung in einem Ausdruck. Eine Rangfolgeneinschränkung kann Variablen in die Einschränkungsdefinition einschließen. Weitere Informationen finden Sie unter [Hinzufügen von Ausdrücken zu Rangfolgeneinschränkungen](http://msdn.microsoft.com/library/5574d89a-a68e-4b84-80ea-da93305e5ca1).  
  
-   Kontrollieren der bedingten Wiederholung eines For-Schleifencontainers. Weitere Informationen finden Sie unter [Iteration eine Ablaufsteuerung](http://msdn.microsoft.com/library/eb3a7494-88ae-4165-9d0f-58715eb1734a).  
  
-   Erstellen Sie Ausdrücke, die Variablenwerte einschließen.  
  
-   Sie können benutzerdefinierte Variablen für alle Containertypen erstellen: Pakete, **foreach-Schleife** Containern **For-Schleife** Container, **Sequenz** Container, Taskshosts und Ereignishandler. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) und [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="scope"></a>Scope  
 Jeder Container weist seine eigene <xref:Microsoft.SqlServer.Dts.Runtime.Variables>-Auflistung auf. Wenn eine neue Variable erstellt wird, liegt diese innerhalb des Bereichs seines übergeordneten Containers. Da sich der Paketcontainer ganz oben in der Containerhierarchie befindet, funktionieren Variablen mit Paketbereich wie globale Variablen und sind für alle Container innerhalb des Pakets sichtbar. Auf die Auflistung von Variablen für den Container kann über die <xref:Microsoft.SqlServer.Dts.Runtime.Variables>-Auflistung auch von untergeordneten Elementen des Containers zugegriffen werden, indem entweder der Variablenname oder der Index der Variablen in der Auflistung verwendet wird.  
  
 Da die Sichtbarkeit einer Variablen von oben nach unten verläuft, sind Variablen, die auf der Paketebene deklariert werden, für alle Container in dem Paket sichtbar. Die <xref:Microsoft.SqlServer.Dts.Runtime.Variables>-Auflistung in einem Container umfasst daher alle Variablen, die neben den eigenen Variablen des Containers auch zu seinem übergeordneten Element gehören.  
  
 Die Variablen, die in einem Task enthalten sind, sind dagegen hinsichtlich Bereich und Sichtbarkeit eingeschränkt und nur für den Task sichtbar.  
  
 Wenn ein Paket andere Pakete ausführt, sind die in dem Bereich des aufrufenden Pakets definierten Variablen für das aufgerufene Paket verfügbar. Die einzige Ausnahme tritt auf, wenn eine gleichnamige Variable im aufgerufenen Paket vorhanden ist. Bei diesem Konflikt wird der Wert des aufrufenden Pakets von dem Variablenwert des aufgerufenen Pakets überschrieben. Die in dem Bereich des aufgerufenen Pakets definierten Variablen sind niemals für das aufrufende Paket verfügbar.  
  
 Im folgenden Beispielcode wird eine Variable `myCustomVar` programmgesteuert in dem Paketbereich erstellt. Diese führt dann eine Iteration durch alle Variablen durch, die für das Paket sichtbar sind. Dabei wird der Name, der Datentyp und der Wert ausgedruckt.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Application app = new Application();  
      // Load a sample package that contains a variable that sets the file name.  
      Package pkg = app.LoadPackage(  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx",  
        null);  
      Variables pkgVars = pkg.Variables;  
      Variable myVar = pkg.Variables.Add("myCustomVar", false, "User", "3");  
      foreach (Variable pkgVar in pkgVars)  
      {  
        Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name,  
          pkgVar.DataType, pkgVar.Value.ToString());  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim app As Application = New Application()  
    ' Load a sample package that contains a variable that sets the file name.  
    Dim pkg As Package = app.LoadPackage( _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx", _  
      Nothing)  
    Dim pkgVars As Variables = pkg.Variables  
    Dim myVar As Variable = pkg.Variables.Add("myCustomVar", False, "User", "3")  
    Dim pkgVar As Variable  
    For Each pkgVar In pkgVars  
      Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name, _  
        pkgVar.DataType, pkgVar.Value.ToString())  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **Beispielausgabe:**  
  
 `Variable: CancelEvent, Int32, 0`  
  
 `Variable: CreationDate, DateTime, 4/18/2003 11:57:00 AM`  
  
 `Variable: CreatorComputerName, String,`  
  
 `Variable: CreatorName, String,`  
  
 `Variable: ExecutionInstanceGUID, String, {237AB5A4-7E59-4FC9-8D61-E8F20363DF25}`  
  
 `Variable: FileName, String, Junk`  
  
 `Variable: InteractiveMode, Boolean, False`  
  
 `Variable: LocaleID, Int32, 1033`  
  
 `Variable: MachineName, String, MYCOMPUTERNAME`  
  
 `Variable: myCustomVar, String, 3`  
  
 `Variable: OfflineMode, Boolean, False`  
  
 `Variable: PackageID, String, {F0D2E396-A6A5-42AE-9467-04CE946A810C}`  
  
 `Variable: PackageName, String, DTSPackage1`  
  
 `Variable: StartTime, DateTime, 1/28/2005 7:55:39 AM`  
  
 `Variable: UserName, String, <domain>\<userid>`  
  
 `Variable: VersionBuild, Int32, 198`  
  
 `Variable: VersionComments, String,`  
  
 `Variable: VersionGUID, String, {90E105B4-B4AF-4263-9CBD-C2050C2D6148}`  
  
 `Variable: VersionMajor, Int32, 1`  
  
 `Variable: VersionMinor, Int32, 0`  
  
 Beachten Sie, die alle Variablen in der bereichsbezogenen der **System** Namespace für das Paket verfügbar sind. Weitere Informationen finden Sie unter [System Variables](../../integration-services/system-variables.md).  
  
## <a name="namespaces"></a>Namespaces  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) stellt zwei Standardnamespaces Variablen originaldatenseiten; **Benutzer** und **System** Namespaces. Standardmäßig alle benutzerdefinierten Variablen, die vom Entwickler erstellten hinzugefügt wird die **Benutzer** Namespace. Systemvariablen befinden sich in der **System** Namespace. Sie können zusätzliche Namespaces außer erstellen die **Benutzer** Namespace zum Speichern von benutzerdefinierten Variablen, und Sie können den Namen ändern der **Benutzer** Namespace, jedoch keine hinzufügen oder Ändern von Variablen in der **System** -Namespace oder Systemvariablen einem anderen Namespace zuzuweisen.  
  
 Die verfügbaren Systemvariablen sind je nach Containertyp unterschiedlich. Eine Liste der auf Pakete, Container, Tasks und Ereignishandler verfügbaren Systemvariablen, finden Sie unter [Systemvariablen](../../integration-services/system-variables.md).  
  
## <a name="value"></a>Wert  
 Der Wert einer benutzerdefinierten Variablen kann ein Literal oder ein Ausdruck sein:  
  
-   Wenn die Variable einen Literalwert enthalten soll, legen Sie den Wert seiner <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A>-Eigenschaft fest.  
  
-   Wenn die Variable einen Ausdruck enthalten soll, damit Sie die Ergebnisse des Ausdrucks als Wert verwenden können, legen Sie die <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> Eigenschaft der Variablen, die **"true"**, und geben Sie einen Ausdruck in der <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Expression%2A> Eigenschaft. Zur Laufzeit wird der Ausdruck ausgewertet, und das Ergebnis des Ausdrucks wird als Wert der Variablen verwendet. Wenn z. B. die Ausdruckseigenschaft einer Variablen`"100 * 2""100 * 2"` ist, wird die Variable auf einen Wert von 200 ausgewertet.  
  
 Für eine Variable kann der Wert ihres <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> nicht explizit festgelegt werden. Der Wert <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> wird aus dem Startwert, der der Variablen zugewiesen ist, abgeleitet und kann nachträglich nicht geändert werden. Weitere Informationen zu Variablen Datentypen, finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Das folgende Codebeispiel erstellt eine neue Variable Sätze <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> auf **"true"**, weist der Ausdruck `"100 * 2"` der Ausdruckseigenschaft der Variablen an, und der Wert der Variablen ausgegeben.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package pkg = new Package();  
      Variable v100 = pkg.Variables.Add("myVar", false, "", 1);  
      v100.EvaluateAsExpression = true;  
      v100.Expression = "100 * 2";  
      Console.WriteLine("Expression for myVar: {0}",   
        v100.Properties["Expression"].GetValue(v100));  
      Console.WriteLine("Value of myVar: {0}", v100.Value.ToString());  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkg As Package = New Package  
    Dim v100 As Variable = pkg.Variables.Add("myVar", False, "", 1)  
    v100.EvaluateAsExpression = True  
    v100.Expression = "100 * 2"  
    Console.WriteLine("Expression for myVar: {0}", _  
      v100.Properties("Expression").GetValue(v100))  
    Console.WriteLine("Value of myVar: {0}", v100.Value.ToString)  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **Beispielausgabe:**  
  
 `Expression for myVar: 100 * 2`  
  
 `Value of myVar: 200`  
  
 Der Ausdruck muss ein gültiger Ausdruck sein, der die [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Ausdruckssyntax verwendet. Neben den Operatoren und Funktionen, die der Ausdruck bereitstellt, sind Literale in Variablenausdrücke zulässig, Ausdrücke können jedoch nicht auf andere Variablen oder Spalten verweisen. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md)ausgewertet wird.  
  
## <a name="configuration-files"></a>Konfigurationsdateien  
 Wenn eine Konfigurationsdatei eine benutzerdefinierte Variable einschließt, kann die Variable zur Laufzeit aktualisiert werden. Dies bedeutet, dass der Wert der ursprünglich in dem Paket enthaltenen Variablen beim Ausführen des Pakets durch einen neuen Wert aus der Konfigurationsdatei ersetzt wird. Diese Ersetzungstechnik ist hilfreich, wenn ein Paket für mehrere Server bereitgestellt wird, die unterschiedliche Variablenwerte erfordern. Eine Variable kann z. B. wie oft angeben einer **foreach-Schleife** -Schleifencontainer zugehörigen Workflow oder die Liste die Empfänger, die ein Ereignishandler sendet per e-mail an, wenn ein Fehler ausgelöst wird, oder ändern die Anzahl von Fehlern, die auftreten können, bevor das Paket fehlschlägt. Diese Variablen werden dynamisch in Konfigurationsdateien für jede Umgebung bereitgestellt. Daher sind nur Lese-/Schreibvariablen in Konfigurationsdateien zulässig. Weitere Informationen finden Sie unter [Erstellen von Paketkonfigurationen](../../integration-services/packages/create-package-configurations.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Integrationsservices &#40; SSIS &#41; Variablen](../../integration-services/integration-services-ssis-variables.md)   
 [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  

