---
title: "Übertragen von Daten | Microsoft Docs"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- data transfers [SMO]
- transferring data
ms.assetid: eea255c3-8251-40f0-973b-fe4ef6cb5261
caps.latest.revision: "50"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7a5be776cd4852c09ae6a3cbc2b344646f8504fc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="transferring-data"></a>Übertragen von Daten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Die <xref:Microsoft.SqlServer.Management.Smo.Transfer> Klasse ist eine Hilfsprogrammklasse, die Tools zur Übertragung von Objekten und Daten bereitstellt.  
  
 Objekte im Datenbankschema werden übertragen, indem auf dem Zielserver ein generiertes Skript ausgeführt wird. <xref:Microsoft.SqlServer.Management.Smo.Table>-Daten werden mit einem dynamisch erstellten DTS-Paket übertragen.  
  
 Die <xref:Microsoft.SqlServer.Management.Smo.Transfer> -Objekt verwendet die ["SqlBulkCopy"](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy.aspx) -API, um Daten zu übertragen. Zudem befinden sich die für die Durchführung von Datenübertragungen verwendeten Methoden und Eigenschaften im <xref:Microsoft.SqlServer.Management.Smo.Transfer>-Objekt statt im <xref:Microsoft.SqlServer.Management.Smo.Database>-Objekt. Das Verschieben von Funktionalität aus den Instanzenklassen in die Hilfsprogrammklassen entspricht einem weniger umfangreichen Objektmodell, da der Code für spezifische Aufgaben nur dann geladen wird, wenn er benötigt wird.  
  
 Das <xref:Microsoft.SqlServer.Management.Smo.Transfer>-Objekt unterstützt keine Datenübertragungen in eine Zieldatenbank, deren <xref:Microsoft.SqlServer.Management.Smo.Database.CompatibilityLevel%2A> geringer als die Version der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz ist.  
  
## <a name="example"></a>Beispiel  
Zum Verwenden eines angegebenen Codebeispiels müssen Sie die Programmierumgebung, Programmiervorlage und die zu verwendende Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [Erstellen eines Visual C &#35; SMO-Projekts in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
 
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-visual-basic"></a>Übertragen von Schema und Daten aus einer Datenbank in eine andere in Visual Basic  
 Dieses Codebeispiel stellt die Übertragung von Schema und Daten mithilfe des <xref:Microsoft.SqlServer.Management.Smo.Transfer>-Objekts von einer Datenbank in eine andere dar.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Create a new database that is to be destination database.
Dim dbCopy As Database
dbCopy = New Database(srv, "AdventureWorks2012Copy")
dbCopy.Create()
'Define a Transfer object and set the required options and properties.
Dim xfr As Transfer
xfr = New Transfer(db)
xfr.CopyAllTables = True
xfr.Options.WithDependencies = True
xfr.Options.ContinueScriptingOnError = True
xfr.DestinationDatabase = "AdventureWorks2012Copy"
xfr.DestinationServer = srv.Name
xfr.DestinationLoginSecure = True
xfr.CopySchema = True
'Script the transfer. Alternatively perform immediate data transfer with TransferData method.
xfr.ScriptTransfer()
```
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-visual-c"></a>Übertragen von Schema und Daten aus einer Datenbank in eine andere in Visual C#  
 Dieses Codebeispiel stellt die Übertragung von Schema und Daten mithilfe des <xref:Microsoft.SqlServer.Management.Smo.Transfer>-Objekts von einer Datenbank in eine andere dar.  
  
```csharp  
{  
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
            //Create a new database that is to be destination database.   
            Database dbCopy;  
            dbCopy = new Database(srv, "AdventureWorks2012Copy");  
            dbCopy.Create();  
            //Define a Transfer object and set the required options and properties.   
            Transfer xfr;  
            xfr = new Transfer(db);  
            xfr.CopyAllTables = true;  
            xfr.Options.WithDependencies = true;  
            xfr.Options.ContinueScriptingOnError = true;  
            xfr.DestinationDatabase = "AdventureWorks2012Copy";  
            xfr.DestinationServer = srv.Name;  
            xfr.DestinationLoginSecure = true;  
            xfr.CopySchema = true;  
            //Script the transfer. Alternatively perform immediate data transfer   
            // with TransferData method.   
            xfr.ScriptTransfer();  
        }   
```  
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-powershell"></a>Übertragen von Schema und Daten aus einer Datenbank in eine andere in PowerShell  
 Dieses Codebeispiel stellt die Übertragung von Schema und Daten mithilfe des <xref:Microsoft.SqlServer.Management.Smo.Transfer>-Objekts von einer Datenbank in eine andere dar.  
  
```powershell  
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Reference the AdventureWorks2012 database.  
$db = $srv.Databases["AdventureWorks2012"]  
  
#Create a database to hold the copy of AdventureWorks  
$dbCopy = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Database -argumentlist $srv, "AdventureWorksCopy"  
$dbCopy.Create()  
  
#Define a Transfer object and set the required options and properties.  
$xfr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Transfer -argumentlist $db  
  
#Set this objects properties  
$xfr.CopyAllTables = $true  
$xfr.Options.WithDependencies = $true  
$xfr.Options.ContinueScriptingOnError = $true  
$xfr.DestinationDatabase = "AdventureWorksCopy"  
$xfr.DestinationServer = $srv.Name  
$xfr.DestinationLoginSecure = $true  
$xfr.CopySchema = $true  
"Scripting Data Transfer"  
#Script the transfer. Alternatively perform immediate data transfer with TransferData method.  
$xfr.ScriptTransfer()  
```  
  
  
