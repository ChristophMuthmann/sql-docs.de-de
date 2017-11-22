---
title: "Erstellen, ändern und Löschen von Regeln | Microsoft Docs"
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
helpviewer_keywords: rules [SMO]
ms.assetid: 16981459-524e-4b39-a899-4370eaf763cc
caps.latest.revision: "46"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 57d816026ea3824860d49dff974139a8284f9342
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="creating-altering-and-removing-rules"></a>Erstellen, Ändern und Löschen von Regeln
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]In SMO werden Regeln dargestellt werden, durch die <xref:Microsoft.SqlServer.Management.Smo.Rule> Objekt. Die Regel wird durch die <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A>-Eigenschaft definiert, wobei es sich um eine Textzeichenfolge handelt, die einen Bedingungsausdruck enthält, der Operatoren oder Prädikate wie IN, LIKE oder BETWEEN verwendet. Eine Regel kann nicht auf Spalten oder andere Datenbankobjekte verweisen. Integrierte Funktionen, die nicht auf Datenbankobjekte verweisen, dürfen in einer Regel eingeschlossen sein.  
  
 Die Definition in der <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> Eigenschaft muss eine Variable enthalten, die auf den eingegebenen Datenwert verweist. Wenn Sie die Regel erstellen, können Sie den Wert durch einen beliebigen Namen bzw. ein Symbol darstellen; das erste Zeichen muss jedoch ein @-Zeichen sein.  
  
## <a name="example"></a>Beispiel  
 Zum Verwenden eines angegebenen Codebeispiels müssen Sie die Programmierumgebung, Programmiervorlage und die zu verwendende Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [Erstellen eines Visual C &#35; SMO-Projekts in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-basic"></a>Erstellen, Ändern und Entfernen einer Regel in Visual Basic  
 Dieses Codebeispiel zeigt, wie eine Regel erstellt und an eine Spalte angefügt wird, wie Eigenschaften des <xref:Microsoft.SqlServer.Management.Smo.Rule>-Objekts geändert werden, die Regel von der Spalte getrennt und anschließend gelöscht wird.  
  
 Die **Dim** -Anweisung für die <xref:Microsoft.SqlServer.Management.Smo.Rule> Objekt wurde angegeben, mit dem vollständigen Assemblypfad zur Vermeidung von Mehrdeutigkeiten mit einer <xref:Microsoft.SqlServer.Management.Smo.Rule> Objekt in der System.Data-Assembly.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Product table.
Dim tb As Table
tb = db.Tables("Product", "Production")
'Define a Rule object variable by supplying the parent database, name and schema in the constructor. 
'Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.
Dim ru As Microsoft.SqlServer.Management.Smo.Rule
ru = New Rule(db, "TestRule", "Production")
'Set the TextHeader and TextBody properties to define the rule.
ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"
ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"
'Create the rule on the instance of SQL Server.
ru.Create()
'Bind the rule to a column in the Product table by supplying the table, schema, and 
'column as arguments in the BindToColumn method.
ru.BindToColumn("Product", "SellEndDate", "Production")
'Unbind from the column before removing the rule from the database.
ru.UnbindFromColumn("Product", "SellEndDate", "Production")
ru.Drop()
```
  
## <a name="creating-altering-and-removing-a-rule-in-visual-c"></a>Erstellen, Ändern und Löschen einer Regel in Visual C#  
 Dieses Codebeispiel zeigt, wie eine Regel erstellt und an eine Spalte angefügt wird, wie Eigenschaften des <xref:Microsoft.SqlServer.Management.Smo.Rule>-Objekts geändert werden, die Regel von der Spalte getrennt und anschließend gelöscht wird.  
  
 Die **Dim** -Anweisung für die <xref:Microsoft.SqlServer.Management.Smo.Rule> Objekt wurde angegeben, mit dem vollständigen Assemblypfad zur Vermeidung von Mehrdeutigkeiten mit einer <xref:Microsoft.SqlServer.Management.Smo.Rule> Objekt in der System.Data-Assembly.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
            //Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.   
            Microsoft.SqlServer.Management.Smo.Rule ru;  
            ru = new Rule(db, "TestRule", "Production");  
            //Set the TextHeader and TextBody properties to define the rule.   
            ru.TextHeader = "CREATE RULE [Production].[TestRule] AS";  
            ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())";  
            //Create the rule on the instance of SQL Server.   
            ru.Create();  
            //Bind the rule to a column in the Product table by supplying the table, schema, and   
            //column as arguments in the BindToColumn method.   
            ru.BindToColumn("Product", "SellEndDate", "Production");  
            //Unbind from the column before removing the rule from the database.   
            ru.UnbindFromColumn("Product", "SellEndDate", "Production");  
            ru.Drop();  
  
        }  
```  
  
## <a name="creating-altering-and-removing-a-rule-in-powershell"></a>Erstellen, Ändern und Löschen einer Regel in PowerShell  
 Dieses Codebeispiel zeigt, wie eine Regel erstellt und an eine Spalte angefügt wird, wie Eigenschaften des <xref:Microsoft.SqlServer.Management.Smo.Rule>-Objekts geändert werden, die Regel von der Spalte getrennt und anschließend gelöscht wird.  
  
 Die **Dim** -Anweisung für die <xref:Microsoft.SqlServer.Management.Smo.Rule> Objekt wurde angegeben, mit dem vollständigen Assemblypfad zur Vermeidung von Mehrdeutigkeiten mit einer <xref:Microsoft.SqlServer.Management.Smo.Rule> Objekt in der System.Data-Assembly.  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
$ru = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Rule `  
-argumentlist $db, "TestRule", "Production"  
  
#Set the TextHeader and TextBody properties to define the rule.   
$ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"  
$ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"  
  
#Create the rule on the instance of SQL Server.   
$ru.Create()  
  
# Bind the rule to a column in the Product table by supplying the table, schema, and   
# column as arguments in the BindToColumn method.   
$ru.BindToColumn("Product", "SellEndDate", "Production")  
  
#Unbind from the column before removing the rule from the database.   
$ru.UnbindFromColumn("Product", "SellEndDate", "Production")  
$ru.Drop()  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.SqlServer.Management.Smo.Rule>  
  
  
