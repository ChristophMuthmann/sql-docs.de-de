---
title: Erste Schritte mit CLR-Integration | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- database objects [CLR integration]
- namespaces [CLR integration]
- database objects [CLR integration], about CLR integration
- stored procedures [CLR integration]
- common language runtime [SQL Server], about CLR integration
- building database objects [CLR integration], about CLR integration
- common language runtime [SQL Server], stored procedures
- common language runtime [SQL Server], namespaces
- Hello World example [CLR integration]
- library [CLR integration]
ms.assetid: c73e628a-f54a-411a-bfe3-6dae519316cc
caps.latest.revision: 62
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d79bafbd781b34d3f6fa4908f998775f37548cd9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getting-started-with-clr-integration"></a>Erste Schritte mit der CLR-Integration
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Dieses Thema bietet einen Überblick über die Namespaces und Bibliotheken, kompilieren Sie die Datenbankobjekte, die mit der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Integration mit der .NET Framework common Language Runtime (CLR). In diesem Thema wird außerdem erläutert, wie eine einfache gespeicherte CLR-Prozedur in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# geschrieben, kompiliert und ausgeführt wird.  
  
## <a name="required-namespaces"></a>Erforderliche Namespaces  
 Die Entwicklung einfacher CLR-Datenbankobjekte erforderlichen Komponenten installiert und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Die CLR-Integrationsfunktionalität wird in einer Assembly mit dem Namen system.data.dll verfügbar gemacht, die Teil von .NET Framework ist. Diese Assembly befindet sich im globalen Assemblycache (GAC) sowie im .NET Framework-Verzeichnis. Ein Verweis auf diese Assembly wird in der Regel sowohl von Befehlszeilentools als auch von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio automatisch hinzugefügt und muss daher nicht manuell hinzugefügt werden.  
  
 Die system.data.dll-Assembly enthält die folgenden Namespaces, die zum Kompilieren von CLR-Datenbankobjekten erforderlich sind:  
  
 `System.Data`  
  
 `System.Data.Sql`  
  
 `Microsoft.SqlServer.Server`  
  
 `System.Data.SqlTypes`  
  
## <a name="writing-a-simple-hello-world-stored-procedure"></a>Schreiben der einfachen gespeicherten Prozedur "Hello World"  
 Kopieren Sie den folgenden Visual C#- oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic-Code, fügen Sie ihn in einen Texteditor ein, und speichern Sie ihn in einer Datei mit dem Namen "helloworld.cs" oder "helloworld.vb".  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlTypes;  
  
public class HelloWorldProc  
{  
    [Microsoft.SqlServer.Server.SqlProcedure]  
    public static void HelloWorld(out string text)  
    {  
        SqlContext.Pipe.Send("Hello world!" + Environment.NewLine);  
        text = "Hello world!";  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlTypes  
Imports System.Runtime.InteropServices  
  
Public Class HelloWorldProc  
    \<Microsoft.SqlServer.Server.SqlProcedure> _   
    Public Shared  Sub HelloWorld(\<Out()> ByRef text as String)  
        SqlContext.Pipe.Send("Hello world!" & Environment.NewLine)  
        text = "Hello world!"  
    End Sub  
End Class  
  
```  
  
 Dieses einfache Programm enthält eine einzelne statische Methode in einer öffentlichen Klasse. Diese Methode verwendet zwei neue Klassen **[SqlContext](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.aspx)** und  **[SqlPipe](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx)**, zum Erstellen von verwalteten Datenbankobjekten für die Ausgabe von eines einfachen Texts Nachricht. Zudem weist die Methode die Zeichenfolge "Hello World!" als Wert des Out-Parameter. Diese Methode kann als gespeicherte Prozedur in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deklariert und anschließend auf dieselbe Weise wie eine gespeicherte [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Prozedur ausgeführt werden.  
  
 Dieses Programm als Bibliothek kompiliert, und Laden Sie ihn in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], und es als eine gespeicherte Prozedur ausführen.  
  
## <a name="compile-the-hello-world-stored-procedure"></a>Kompiliert die "Hello World" gespeicherte Prozedur  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] installiert die Redistributionsdateien von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework standardmäßig. Zu diesen Dateien zählen die Dateien csc.exe und vbc.exe, die Befehlszeilencompiler für Visual C# sowie Visual Basic-Programme. Zum Kompilieren des Beispiels müssen Sie die Pfadvariable so ändern, dass sie auf das Verzeichnis mit der Datei csc.exe oder mit der Datei vbc.exe zeigt. Der Standardinstallationspfad von .NET Framework lautet wie folgt:  
  
```  
C:\Windows\Microsoft.NET\Framework\(version)  
```  
  
 Diese Version enthält die Versionsnummer der installierten Redistributionsdatei von .NET Framework. Zum Beispiel:  
  
```  
C:\Windows\Microsoft.NET\Framework\v4.6.1  
```  
  
 Nach dem Hinzufügen des .NET Framework-Verzeichnises zum Pfad können Sie die gespeicherte Prozedur in diesem Beispiel mit dem folgenden Befehl in eine Assembly kompilieren. Die **/target** Option können Sie es in eine Assembly kompilieren.  
  
 Für Visual C#-Quelldateien gilt:  
  
```  
csc /target:library helloworld.cs   
```  
  
 Für Visual Basic-Quelldateien gilt:  
  
```  
vbc /target:library helloworld.vb  
```  
  
 Mit diesen Befehlen wird der Visual C# - bzw. Visual Basic-Compiler unter Angabe der /target-Option aufgerufen, die festlegt, dass eine Bibliotheks-DLL erstellt werden soll.  
  
## <a name="loading-and-running-the-hello-world-stored-procedure-in-sql-server"></a>Laden und Ausführen der gespeicherten Prozedur "Hello World" in SQL Server  
 Sobald die Beispielprozedur erfolgreich kompiliert wurde, können Sie sie in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] testen. Öffnen Sie hierzu [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], und erstellen Sie eine neue Abfrage zum Verbinden einer geeigneten Testdatenbank (z. B. der Beispieldatenbank AdventureWorks).  
  
 Die Funktion zum Ausführen von CLR-Code (Common Language Runtime) ist in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] standardmäßig deaktiviert. Der CLR-Code kann aktiviert werden, mithilfe der **Sp_configure** gespeicherten Systemprozedur. Weitere Informationen finden Sie unter [Enabling CLR Integration](../../../relational-databases/clr-integration/clr-integration-enabling.md).  
  
 Sie müssen die Assembly erstellen, um auf die gespeicherte Prozedur zugreifen zu können. Für dieses Beispiel wird vorausgesetzt, dass Sie die helloworld.dll-Assembly im Verzeichnis C:\ erstellt haben. Fügen Sie die folgende [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisung zur Abfrage hinzu:  
  
```  
CREATE ASSEMBLY helloworld from 'c:\helloworld.dll' WITH PERMISSION_SET = SAFE  
```  
  
 Nach dem Erstellen der Assembly können Sie mithilfe der CREATE PROCEDURE-Anweisung auf die HelloWorld-Methode zugreifen. Die gespeicherte Prozedur wird "hello" genannt:  
  
```  
  
CREATE PROCEDURE hello  
@i nchar(25) OUTPUT  
AS  
EXTERNAL NAME helloworld.HelloWorldProc.HelloWorld  
-- if the HelloWorldProc class is inside a namespace (called MyNS),  
-- the last line in the create procedure statement would be  
-- EXTERNAL NAME helloworld.[MyNS.HelloWorldProc].HelloWorld  
```  
  
 Nach dem Erstellen der Prozedur kann diese wie eine normale, in [!INCLUDE[tsql](../../../includes/tsql-md.md)] geschriebene gespeicherte Prozedur ausgeführt werden. Führen Sie den folgenden Befehl ein:  
  
```  
DECLARE @J nchar(25)  
EXEC hello @J out  
PRINT @J  
```  
  
 Daraufhin sollte im Meldungsfenster von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] folgende Ausgabe angezeigt werden.  
  
```  
Hello world!  
Hello world!  
```  
  
## <a name="removing-the-hello-world-stored-procedure-sample"></a>Entfernen des Beispiels der gespeicherten Prozedur "Hello World"  
 Wenn Sie die gespeicherte Beispielprozedur ausgeführt haben, können Sie die Prozedur und die Assembly aus der Testdatenbank entfernen.  
  
 Entfernen Sie zuerst die Prozedur. Verwenden Sie hierzu den drop procedure-Befehl.  
  
```  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'hello')  
   drop procedure hello  
```  
  
 Nach dem Löschen der Prozedur können Sie die Assembly entfernen, die den Beispielcode enthält.  
  
```  
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'helloworld')  
   drop assembly helloworld  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CLR-gespeicherte Prozeduren](http://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [SQL Server In-Process-spezifische Erweiterungen für ADO.NET](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)   
 [Debuggen von CLR-Datenbankobjekten](../../../relational-databases/clr-integration/debugging-clr-database-objects.md)   
 [Sicherheit der CLR-Integration](../../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
