---
title: "Erstellen, ändern und Löschen von Standardwerten | Microsoft Docs"
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
helpviewer_keywords: defaults [SMO]
ms.assetid: c30ac3b9-8150-4264-ba4c-c549f44261ab
caps.latest.revision: "46"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2ebd93c329c2ee25ca67cdd6e338e40a78e84330
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="creating-altering-and-removing-defaults"></a>Erstellen, Ändern und Löschen von Standardwerten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), die Default-Einschränkung wird dargestellt, durch die <xref:Microsoft.SqlServer.Management.Smo.Default> Objekt.  
  
 Die <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> Eigenschaft von der <xref:Microsoft.SqlServer.Management.Smo.Default> Objekt dient zum Festlegen des Werts eingefügt werden. Dies kann eine Konstante oder eine [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisung sein, die einen konstanten Wert zurückgibt, z. B. GETDATE(). Die <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A>-Eigenschaft kann über die <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>-Methode nicht geändert werden. Stattdessen die <xref:Microsoft.SqlServer.Management.Smo.Default> Objekt muss gelöscht und neu erstellt werden.  
  
## <a name="example"></a>Beispiel  
 Zum Verwenden eines angegebenen Codebeispiels müssen Sie die Programmierumgebung, Programmiervorlage und die zu verwendende Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [Erstellen eines Visual C &#35; SMO-Projekts in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-default-in-visual-basic"></a>Erstellen, Ändern und Löschen eines Standardwerts in Visual Basic  
 Dieses Codebeispiel zeigt, wie erstellt ein Standard, der einfachen Text ist, und ein anderer Standardwert, der eine [!INCLUDE[tsql](../../../includes/tsql-md.md)] Anweisung. Der Standard muss mithilfe der Spalte angefügt werden die <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> Methode und getrennt werden, mithilfe der <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A> Methode.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a Default object variable by supplying the parent database and the default name 
'in the constructor.
Dim def As [Default]
def = New [Default](db, "Test_Default2")
'Set the TextHeader and TextBody properties that define the default.
def.TextHeader = "CREATE DEFAULT [Test_Default2] AS"
def.TextBody = "GetDate()"
'Create the default on the instance of SQL Server.
def.Create()
'Declare a Column object variable and reference a column in the AdventureWorks2012 database.
Dim col As Column
col = db.Tables("SpecialOffer", "Sales").Columns("StartDate")
'Bind the default to the column.
def.BindToColumn("SpecialOffer", "StartDate", "Sales")
'Unbind the default from the column and remove it from the database.
def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales")
def.Drop()
```
  
## <a name="creating-altering-and-removing-a-default-in-visual-c"></a>Erstellen, Ändern und Löschen eines Standardwerts in Visual C#  
 Dieses Codebeispiel zeigt, wie erstellt ein Standard, der einfachen Text ist, und ein anderer Standardwert, der eine [!INCLUDE[tsql](../../../includes/tsql-md.md)] Anweisung. Der Standard muss mithilfe der Spalte angefügt werden die <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> Methode und getrennt werden, mithilfe der <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A> Methode.  
  
```csharp  
{  
  
          Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database  db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Default object variable by supplying the parent database and the default name   
            //in the constructor.   
            Default def = new Default(db, "Test_Default2");  
  
            //Set the TextHeader and TextBody properties that define the default.   
            def.TextHeader = "CREATE DEFAULT [Test_Default2] AS";  
            def.TextBody = "GetDate()";  
  
            //Create the default on the instance of SQL Server.   
            def.Create();  
  
            //Bind the default to a column in a table in AdventureWorks2012  
            def.BindToColumn("SpecialOffer", "StartDate", "Sales");  
  
            //Unbind the default from the column and remove it from the database.   
            def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales");  
            def.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-default-in-powershell"></a>Erstellen, Ändern und Löschen eines Standardwerts in PowerShell  
 Dieses Codebeispiel zeigt, wie erstellt ein Standard, der einfachen Text ist, und ein anderer Standardwert, der eine [!INCLUDE[tsql](../../../includes/tsql-md.md)] Anweisung. Der Standard muss mithilfe der Spalte angefügt werden die <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> Methode und getrennt werden, mithilfe der <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A> Methode.  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
#Define a Default object variable by supplying the parent database and the default name in the constructor.  
$def = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Default `  
-argumentlist $db, "Test_Default2"  
  
#Set the TextHeader and TextBody properties that define the default.   
$def.TextHeader = "CREATE DEFAULT [Test_Default2] AS"  
$def.TextBody = "GetDate()"  
  
#Create the default on the instance of SQL Server.   
$def.Create()  
  
#Bind the default to the column.   
$def.BindToColumn("SpecialOffer", "StartDate", "Sales")  
  
#Unbind the default from the column and remove it from the database.   
$def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales")  
$def.Drop()  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 <xref:Microsoft.SqlServer.Management.Smo.Default>  
  
  
