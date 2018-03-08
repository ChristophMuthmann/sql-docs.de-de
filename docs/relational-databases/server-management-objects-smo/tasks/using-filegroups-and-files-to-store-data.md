---
title: Verwenden von Dateigruppen und Dateien zur Speicherung von Daten | Microsoft Docs
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- filegroups [SMO]
- storing data [SMO]
- files [SMO]
- files [SMO], about files
- storage [SMO]
ms.assetid: 7e2327ce-e1a6-4904-83d1-0944b24a7b43
caps.latest.revision: "31"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5622269022dcbf63d717fb2dec2efac7692f0e52
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2018
---
# <a name="using-filegroups-and-files-to-store-data"></a>Verwenden von Dateigruppen und Dateien zur Speicherung von Daten
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Datendateien werden zur Speicherung von Datenbankdateien verwendet. Die Datendateien werden in Dateigruppen unterteilt. Das <xref:Microsoft.SqlServer.Management.Smo.Database>-Objekt verfügt über eine <xref:Microsoft.SqlServer.Management.Smo.Database.FileGroups%2A>-Eigenschaft, die auf ein <xref:Microsoft.SqlServer.Management.Smo.FileGroupCollection>-Objekt verweist. Jedes <xref:Microsoft.SqlServer.Management.Smo.FileGroup>-Objekt in dieser Auflistung verfügt über eine <xref:Microsoft.SqlServer.Management.Smo.FileGroup.Files%2A>-Eigenschaft. Diese Eigenschaft bezieht sich auf eine <xref:Microsoft.SqlServer.Management.Smo.DataFileCollection>-Auflistung, die alle Datendateien enthält, die zur Datenbank gehören. Eine Dateigruppe wird prinzipiell verwendet, um Dateien zu gruppieren, die zur Speicherung eines Datenbankobjekts genutzt werden. Ein Grund für die Verteilung eines Datenbankobjekts über mehrere Dateien ist die Verbesserung der Leistung, insbesondere wenn die Dateien auf unterschiedlichen Laufwerken gespeichert sind.  
  
 Jede automatisch erstellte Datenbank verfügt über eine Dateigruppe mit dem Namen "Primary" und eine Datendatei, die den gleichen Namen hat wie die Datenbank. Den Auflistungen können weitere Dateien und Gruppen hinzugefügt werden.  
  
## <a name="examples"></a>Beispiele  
 Für die folgenden Codebeispiele müssen Sie die Programmierungsumgebung, die Programmiervorlage und die Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [Erstellen eines Visual C &#35; SMO-Projekts in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-basic"></a>Hinzufügen von Dateigruppen und Datendateien zu einer Datenbank in Visual Basic  
 Die primäre Dateigruppe und die Datendatei werden automatisch mit Standardeigenschaftswerten erstellt. Im Codebeispiel werden einige Eigenschaftswerte angegeben, die Sie verwenden können. Andernfalls werden die Standardeigenschaftswerte verwendet.  
  
```vbnet  
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a FileGroup object called SECONDARY on the database.
Dim fg1 As FileGroup
fg1 = New FileGroup(db, "SECONDARY")
'Call the Create method to create the file group on the instance of SQL Server.
fg1.Create()
'Define a DataFile object on the file group and set the FileName property.
Dim df1 As DataFile
df1 = New DataFile(fg1, "datafile1")
df1.FileName = "c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data\datafile2.ndf"
'Call the Create method to create the data file on the instance of SQL Server.
df1.Create()
```
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-c"></a>Hinzufügen von Dateigruppen und Datendateien zu einer Datenbank in Visual C#  
 Die primäre Dateigruppe und die Datendatei werden automatisch mit Standardeigenschaftswerten erstellt. Im Codebeispiel werden einige Eigenschaftswerte angegeben, die Sie verwenden können. Andernfalls werden die Standardeigenschaftswerte verwendet.  
  
```  
{  
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a FileGroup object called SECONDARY on the database.   
            FileGroup fg1 = default(FileGroup);  
            fg1 = new FileGroup(db, "SECONDARY");  
            //Call the Create method to create the file group on the instance of SQL Server.   
            fg1.Create();  
            //Define a DataFile object on the file group and set the FileName property.   
            DataFile df1 = default(DataFile);  
            df1 = new DataFile(fg1, "datafile1");  
            df1.FileName = "c:\\Program Files\\Microsoft SQL Server\\MSSQL.1\\MSSQL\\Data\\datafile2.ndf";  
            //Call the Create method to create the data file on the instance of SQL Server.   
            df1.Create();  
        }  
```  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-powershell"></a>Hinzufügen von Dateigruppen und Datendateien zu einer Datenbank in PowerShell  
 Die primäre Dateigruppe und die Datendatei werden automatisch mit Standardeigenschaftswerten erstellt. Im Codebeispiel werden einige Eigenschaftswerte angegeben, die Sie verwenden können. Andernfalls werden die Standardeigenschaftswerte verwendet.  
  
```powershell   
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012.  
$db = get-item AdventureWorks2012  
  
#Create a new filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "SECONDARY"  
$fg1.Create()  
  
#Define a DataFile object on the file group and set the FileName property.   
$df1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.DataFile -argumentlist $fg1, "datafile1"  
  
#Make sure to have a directory created to hold the designated data file  
$df1.FileName = "c:\\TestData\\datafile2.ndf"  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$df1.Create()  
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-basic"></a>Erstellen, Ändern und Löschen einer Protokolldatei in Visual Basic  
 Im Codebeispiel wird ein <xref:Microsoft.SqlServer.Management.Smo.LogFile>-Objekt erstellt, eine der Eigenschaften geändert und das Objekt dann aus der Datenbank gelöscht.  
  
```vbnet  
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a LogFile object and set the database, name, and file name properties in the constructor.
Dim lf1 As LogFile
lf1 = New LogFile(db, "logfile1", "c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data\logfile1.ldf")
'Set the file growth to 6%.
lf1.GrowthType = FileGrowthType.Percent
lf1.Growth = 6
'Run the Create method to create the log file on the instance of SQL Server.
lf1.Create()
'Alter the growth percentage.
lf1.Growth = 7
lf1.Alter()
'Remove the log file.
lf1.Drop()
```
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-c"></a>Erstellen, Ändern und Löschen einer Protokolldatei in Visual C#  
 Im Codebeispiel wird ein <xref:Microsoft.SqlServer.Management.Smo.LogFile>-Objekt erstellt, eine der Eigenschaften geändert und das Objekt dann aus der Datenbank gelöscht.  
  
```  
//Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a LogFile object and set the database, name, and file name properties in the constructor.   
            LogFile lf1 = default(LogFile);  
            lf1 = new LogFile(db, "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf");  
            //Set the file growth to 6%.   
            lf1.GrowthType = FileGrowthType.Percent;  
            lf1.Growth = 6;  
            //Run the Create method to create the log file on the instance of SQL Server.   
            lf1.Create();  
            //Alter the growth percentage.   
            lf1.Growth = 7;  
            lf1.Alter();  
            //Remove the log file.   
            lf1.Drop();  
  
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-powershell"></a>Erstellen, Ändern und Löschen einer Protokolldatei in PowerShell  
 Im Codebeispiel wird ein <xref:Microsoft.SqlServer.Management.Smo.LogFile>-Objekt erstellt, eine der Eigenschaften geändert und das Objekt dann aus der Datenbank gelöscht.  
  
```powershell  
#Load the assembly containing the enums used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.SqlEnum")  
  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012  
$db = get-item AdventureWorks2012  
  
#Create a filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Secondary"  
  
#Call the Create method to create the file group on the instance of SQL Server.   
$fg1.Create()  
  
#Define a LogFile object on the file group and set the FileName property.   
$lf1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LogFile -argumentlist $db, "LogFile2"  
  
#Set a location for it - make sure the directory exists  
$lf1.FileName = "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf"  
  
#Set file growth to 6%  
$lf1.GrowthType = [Microsoft.SqlServer.Management.Smo.FileGrowthType]::Percent  
$lf1.Growth = 6.0  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$lf1.Create()  
  
#Alter a value and drop the log file  
$lf1.Growth = 7.0  
$lf1.Alter()  
$lf1.Drop()  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.SqlServer.Management.Smo.FileGroup>   
 [Datenbankdateien und Dateigruppen](../../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
