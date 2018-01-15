---
title: "Erstellen, ändern und Löschen von Trigger | Microsoft Docs"
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
helpviewer_keywords: triggers [SMO]
ms.assetid: 8ddbe23b-6e31-4f8e-8a70-17bd5072413e
caps.latest.revision: "48"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc1849a9bd38af6cbca6d9ebcbea6a571af8816c
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2018
---
# <a name="creating-altering-and-removing-triggers"></a>Erstellen, Ändern und Löschen von Trigger
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]In SMO werden Trigger dargestellt werden, mithilfe der <xref:Microsoft.SqlServer.Management.Smo.Trigger> Objekt. Die [!INCLUDE[tsql](../../../includes/tsql-md.md)] Code, der ausgeführt wird, wenn der Trigger, die ausgelöst wird, festgelegt ist, indem Sie die <xref:Microsoft.SqlServer.Management.Smo.Trigger.TextBody%2A> Eigenschaft des Trigger-Objekts. Der Typ des Triggers wird über andere Eigenschaften des <xref:Microsoft.SqlServer.Management.Smo.Trigger>-Objekts gesetzt, beispielsweise durch die <xref:Microsoft.SqlServer.Management.Smo.Trigger.Update%2A>-Eigenschaft. Hierbei handelt es sich um eine boolesche Eigenschaft, die angibt, ob der Trigger durch ein **UPDATE** von Datensätzen auf der übergeordneten Tabelle ausgelöst wird.  
  
 Das <xref:Microsoft.SqlServer.Management.Smo.Trigger>-Objekt stellt herkömmlicherweise Datenbearbeitungssprachentrigger (DML) dar. In [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] und höhere Versionen werden Trigger Data Definition Language (DDL) werden ebenfalls unterstützt. DDL-Trigger werden durch das <xref:Microsoft.SqlServer.Management.Smo.DatabaseDdlTrigger>-Objekt und das <xref:Microsoft.SqlServer.Management.Smo.ServerDdlTrigger>-Objekt dargestellt.  
  
## <a name="example"></a>Beispiel  
Zum Verwenden eines angegebenen Codebeispiels müssen Sie die Programmierumgebung, Programmiervorlage und die zu verwendende Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [Erstellen eines Visual C &#35; SMO-Projekts in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
 
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-basic"></a>Erstellen, Ändern und Löschen eines Triggers in Visual Basic  
 In diesem Codebeispiel wird veranschaulicht, wie zum Erstellen und einfügen einen Update-Trigger für eine vorhandene Tabelle, die mit dem Namen `Sales`in der [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] Datenbank. Der Trigger sendet eine Erinnerungsmitteilung, wenn die Tabelle aktualisiert oder ein neuer Datensatz eingefügt wird.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim mysrv As Server
mysrv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim mydb As Database
mydb = mysrv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Customer table.
Dim mytab As Table
mytab = mydb.Tables("Customer", "Sales")
'Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.
Dim tr As Trigger
tr = New Trigger(mytab, "Sales")
'Set TextMode property to False, then set other properties to define the trigger.
tr.TextMode = False
tr.Insert = True
tr.Update = True
tr.InsertOrder = Agent.ActivationOrder.First
Dim stmt As String
stmt = " RAISERROR('Notify Customer Relations',16,10) "
tr.TextBody = stmt
tr.ImplementationType = ImplementationType.TransactSql
'Create the trigger on the instance of SQL Server.
tr.Create()
'Remove the trigger.
tr.Drop()
``` 
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-c"></a>Erstellen, Ändern und Löschen eines Triggers in Visual C#  
 In diesem Codebeispiel wird veranschaulicht, wie zum Erstellen und einfügen einen Update-Trigger für eine vorhandene Tabelle, die mit dem Namen `Sales`in der [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] Datenbank. Der Trigger sendet eine Erinnerungsmitteilung, wenn die Tabelle aktualisiert oder ein neuer Datensatz eingefügt wird.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server mysrv;  
            mysrv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database mydb;  
            mydb = mysrv.Databases["AdventureWorks2012"];  
            //Declare a Table object variable and reference the Customer table.   
            Table mytab;  
            mytab = mydb.Tables["Customer", "Sales"];  
            //Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.   
            Trigger tr;  
            tr = new Trigger(mytab, "Sales");  
            //Set TextMode property to False, then set other properties to define the trigger.   
            tr.TextMode = false;  
            tr.Insert = true;  
            tr.Update = true;  
            tr.InsertOrder = ActivationOrder.First;  
            string stmt;  
            stmt = " RAISERROR('Notify Customer Relations',16,10) ";  
            tr.TextBody = stmt;  
            tr.ImplementationType = ImplementationType.TransactSql;  
            //Create the trigger on the instance of SQL Server.   
            tr.Create();  
            //Remove the trigger.   
            tr.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-trigger-in-powershell"></a>Erstellen, Ändern und Löschen eines Triggers in PowerShell  
 In diesem Codebeispiel wird veranschaulicht, wie zum Erstellen und einfügen einen Update-Trigger für eine vorhandene Tabelle, die mit dem Namen `Sales`in der [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] Datenbank. Der Trigger sendet eine Erinnerungsmitteilung, wenn die Tabelle aktualisiert oder ein neuer Datensatz eingefügt wird.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server and to the  
#database tables in Adventureworks2012  
CD \sql\localhost\default\databases\AdventureWorks2012\Tables\  
  
#Get reference to the trigger's target table  
$mytab = get-item Sales.Customer  
  
# Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.  
$tr  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Trigger `  
-argumentlist $mytab, "Sales"  
  
# Set TextMode property to False, then set other properties to define the trigger.   
$tr.TextMode = $false  
$tr.Insert = $true  
$tr.Update = $true  
$tr.InsertOrder = [Microsoft.SqlServer.Management.SMO.Agent.ActivationOrder]::First  
$tr.TextBody = " RAISERROR('Notify Customer Relations',16,10) "  
$tr.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Create the trigger on the instance of SQL Server.   
$tr.Create()  
  
#Remove the trigger.   
$tr.Drop()  
```  
  
  
