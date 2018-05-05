---
title: Aufrufen von Methoden | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- methods [SMO]
- calling methods
- SQL Server Management Objects, method calling
- SMO [SQL Server], method calling
ms.assetid: c88d5c5f-9ff0-4f84-b2b6-24c6b90fa15e
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a3629f2f5d5905ce17df7a5aa15936edaa876ef4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="calling-methods"></a>Aufrufen von Methoden
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Methoden führen bestimmte Tasks im Zusammenhang mit dem Objekt, z. B. die Ausgabe einer **Prüfpunkt** auf einer Datenbank oder die Anforderung einer Aufzählungsliste mit Anmeldungen für die Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Methoden führen Vorgänge an Objekten aus. Methoden können Parameter enthalten, und sie verfügen häufig über einen Rückgabewert. Bei dem Rückgabewert kann es sich um einen einfachen Datentyp, ein komplexes Objekt oder eine Struktur handeln, die mehrere Elemente enthält.  
  
 Mithilfe der Ausnahmebehandlung können Sie feststellen, ob die Methode erfolgreich war. Weitere Informationen finden Sie unter [Handling SMO Exceptions](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-exceptions.md).  
  
## <a name="examples"></a>Beispiele  
Zum Verwenden eines angegebenen Codebeispiels müssen Sie die Programmierumgebung, Programmiervorlage und die zu verwendende Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [Erstellen eines Visual C&#35; SMO-Projekts in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
 
  
## <a name="using-a-simple-smo-method-in-visual-basic"></a>Verwenden einer einfachen SMO-Methode in Visual Basic  
 In diesem Beispiel enthält die <xref:Microsoft.SqlServer.Management.Smo.Database.Create%2A>-Methode keine Parameter und hat keinen Rückgabewert.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Define a Database object variable by supplying the parent server and the database name arguments in the constructor.
Dim db As Database
db = New Database(srv, "Test_SMO_Database")
'Call the Create method to create the database on the instance of SQL Server. 
db.Create()
```
  
## <a name="using-a-simple-smo-method-in-visual-c"></a>Verwenden einer einfachen SMO-Methode in Visual C#  
 In diesem Beispiel enthält die <xref:Microsoft.SqlServer.Management.Smo.Database.Create%2A>-Methode keine Parameter und hat keinen Rückgabewert.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Define a Database object variable by supplying the parent server and the database name arguments in the constructor.   
Database db;   
db = new Database(srv, "Test_SMO_Database");   
//Call the Create method to create the database on the instance of SQL Server.   
db.Create();   
```  
  
 }  
  
## <a name="using-an-smo-method-with-a-parameter-in-visual-basic"></a>Verwenden einer SMO-Methode mit einem Parameter in Visual Basic  
 Die <xref:Microsoft.SqlServer.Management.Smo.Table> Objekt verfügt über eine Methode namens <xref:Microsoft.SqlServer.Management.Smo.Table.RebuildIndexes%2A>. Diese Methode benötigt einen numerischen Parameter, der **FillFactor**angibt.  
  
```VBNET
Dim srv As Server  
srv = New Server  
Dim tb As Table  
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources")  
tb.RebuildIndexes(70)  
```  
  
## <a name="using-an-smo-method-with-a-parameter-in-visual-c"></a>Verwenden einer SMO-Methode mit einem Parameter in Visual C#  
 Die <xref:Microsoft.SqlServer.Management.Smo.Table> Objekt verfügt über eine Methode namens <xref:Microsoft.SqlServer.Management.Smo.Table.RebuildIndexes%2A>. Diese Methode benötigt einen numerischen Parameter, der `FillFactor`angibt.  
  
```csharp  
{   
Server srv = default(Server);   
srv = new Server();   
Table tb = default(Table);   
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources");   
tb.RebuildIndexes(70);   
}   
```  
  
## <a name="using-an-enumeration-method-that-returns-a-datatable-object-in-visual-basic"></a>Verwenden einer Enumerationsmethode in Visual Basic, die ein "DataTable"-Objekt zurückgibt  
 In diesem Abschnitt wird beschrieben, wie eine Enumerationsmethode aufgerufen und wie die Daten in der zurückgegebenen behandelt <xref:System.Data.DataTable> Objekt.  
  
 Die <xref:Microsoft.SqlServer.Management.Smo.Server.EnumCollations%2A>-Methode gibt ein <xref:System.Data.DataTable>-Objekt zurück, für das weitere Navigation erforderlich ist, auf alle verfügbaren Sortierungsinformationen zu der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] zuzugreifen.  
  
```VBNET
'Connect to the local, default instance of SQL Server.  
Dim srv As Server  
srv = New Server  
'Call the EnumCollations method and return collation information to DataTable variable.  
Dim d As DataTable  
'Select the returned data into an array of DataRow.  
d = srv.EnumCollations  
'Iterate through the rows and display collation details for the instance of SQL Server.  
Dim r As DataRow  
Dim c As DataColumn  
For Each r In d.Rows  
    Console.WriteLine("==")  
    For Each c In r.Table.Columns  
        Console.WriteLine(c.ColumnName + " = " + r(c).ToString)  
    Next  
Next  
```  
  
## <a name="using-an-enumeration-method-that-returns-a-datatable-object-in-visual-c"></a>Verwenden einer Enumerationsmethode in Visual C#, die ein "DataTable"-Objekt zurückgibt  
 In diesem Abschnitt wird beschrieben, wie eine Enumerationsmethode aufgerufen und wie die Daten in der zurückgegebenen behandelt <xref:System.Data.DataTable> Objekt.  
  
 Die <xref:Microsoft.SqlServer.Management.Smo.Server.EnumCollations%2A> Methodenrückgabe ein System <xref:System.Data.DataTable> Objekt. Die <xref:System.Data.DataTable> -Objekt ist Weitere Navigation auf alle verfügbaren Sortierungsinformationen zu der Instanz von erforderlich [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
//Call the EnumCollations method and return collation information to DataTable variable.   
DataTable d = default(DataTable);   
//Select the returned data into an array of DataRow.   
d = srv.EnumCollations;   
//Iterate through the rows and display collation details for the instance of SQL Server.   
DataRow r = default(DataRow);   
DataColumn c = default(DataColumn);   
foreach ( r in d.Rows) {   
  Console.WriteLine("=========");   
  foreach ( c in r.Table.Columns) {   
    Console.WriteLine(c.ColumnName + " = " + r(c).ToString);   
  }   
}   
}   
```  
  
## <a name="constructing-an-object-in-visual-basic"></a>Erstellen eines Objekts in Visual Basic  
 Der Konstruktor eines Objekts kann mit dem **New** -Operator aufgerufen werden. Der <xref:Microsoft.SqlServer.Management.Smo.Database>-Objektkonstruktor ist überladen, und die Version des im Beispiel verwendeten <xref:Microsoft.SqlServer.Management.Smo.Database>-Objektkonstruktors akzeptiert zwei Parameter: das übergeordnete <xref:Microsoft.SqlServer.Management.Smo.Server>-Objekt, zu dem die Datenbank gehört, und eine Zeichenfolge, die den Namen der neuen Datenbank darstellt.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Declare and define a Database object by supplying the parent server and the database name arguments in the constructor.
Dim d As Database
d = New Database(srv, "Test_SMO_Database")
'Create the database on the instance of SQL Server.
d.Create()
Console.WriteLine(d.Name)
```
  
## <a name="constructing-an-object-in-visual-c"></a>Erstellen eines Objekts in Visual C#  
 Der Konstruktor eines Objekts kann mit dem **New** -Operator aufgerufen werden. Der <xref:Microsoft.SqlServer.Management.Smo.Database>-Objektkonstruktor ist überladen, und die Version des im Beispiel verwendeten <xref:Microsoft.SqlServer.Management.Smo.Database>-Objektkonstruktors akzeptiert zwei Parameter: das übergeordnete <xref:Microsoft.SqlServer.Management.Smo.Server>-Objekt, zu dem die Datenbank gehört, und eine Zeichenfolge, die den Namen der neuen Datenbank darstellt.  
  
```csharp  
{   
Server srv;   
srv = new Server();   
Table tb;   
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources");   
tb.RebuildIndexes(70);   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Declare and define a Database object by supplying the parent server and the database name arguments in the constructor.   
Database d;   
d = new Database(srv, "Test_SMO_Database");   
//Create the database on the instance of SQL Server.   
d.Create();   
Console.WriteLine(d.Name);   
}  
```  
  
## <a name="copying-an-smo-object-in-visual-basic"></a>Kopieren eines SMO-Objekts in Visual Basic  
 Dieses Codebeispiel verwendet die <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> Methode zum Erstellen einer Kopie der <xref:Microsoft.SqlServer.Management.Smo.Server> Objekt. Die <xref:Microsoft.SqlServer.Management.Smo.Server> Objekt stellt eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```VBNET  
'Connect to the local, default instance of SQL Server.
Dim srv1 As Server
srv1 = New Server()
'Modify the default database and the timeout period for the connection.
srv1.ConnectionContext.DatabaseName = "AdventureWorks2012"
srv1.ConnectionContext.ConnectTimeout = 30
'Make a second connection using a copy of the ConnectionContext property and verify settings.
Dim srv2 As Server
srv2 = New Server(srv1.ConnectionContext.Copy)
Console.WriteLine(srv2.ConnectionContext.ConnectTimeout.ToString)
```
  
## <a name="copying-an-smo-object-in-visual-c"></a>Kopieren eines SMO-Objekts in Visual C#  
 Dieses Codebeispiel verwendet die <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> Methode zum Erstellen einer Kopie der <xref:Microsoft.SqlServer.Management.Smo.Server> Objekt. Die <xref:Microsoft.SqlServer.Management.Smo.Server> Objekt stellt eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv1;   
srv1 = new Server();   
//Modify the default database and the timeout period for the connection.   
srv1.ConnectionContext.DatabaseName = "AdventureWorks2012";   
srv1.ConnectionContext.ConnectTimeout = 30;   
//Make a second connection using a copy of the ConnectionContext property and verify settings.   
Server srv2;   
srv2 = new Server(srv1.ConnectionContext.Copy);   
Console.WriteLine(srv2.ConnectionContext.ConnectTimeout.ToString);   
}  
```  
  
## <a name="monitoring-server-processes-in-visual-basic"></a>Überwachen von Serverprozessen in Visual Basic  
 Sie erhalten die aktuellen Informationen zu der Instanz von Statustyp [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] über Enumerationsmethoden. Im Beispielcode wird die <xref:Microsoft.SqlServer.Management.Smo.Server.EnumProcesses%2A>-Methode zum Ermitteln von Informationen zu den aktuellen Prozessen verwendet. Dieses Beispiel zeigt auch, wie mit den Spalten und Zeilen im zurückgegebenen <xref:System.Data.DataTable>-Objekt gearbeitet wird.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Call the EnumCollations method and return collation information to DataTable variable.
Dim d As DataTable
'Select the returned data into an array of DataRow.
d = srv.EnumProcesses
'Iterate through the rows and display collation details for the instance of SQL Server.
Dim r As DataRow
Dim c As DataColumn
For Each r In d.Rows
    Console.WriteLine("============================================")
    For Each c In r.Table.Columns
        Console.WriteLine(c.ColumnName + " = " + r(c).ToString)
    Next
Next
```
  
## <a name="monitoring-server-processes-in-visual-c"></a>Überwachen von Serverprozessen in Visual C#  
 Sie erhalten die aktuellen Informationen zu der Instanz von Statustyp [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] über Enumerationsmethoden. Im Beispielcode wird die <xref:Microsoft.SqlServer.Management.Smo.Server.EnumProcesses%2A>-Methode zum Ermitteln von Informationen zu den aktuellen Prozessen verwendet. Dieses Beispiel zeigt auch, wie mit den Spalten und Zeilen im zurückgegebenen <xref:System.Data.DataTable>-Objekt gearbeitet wird.  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
//Call the EnumCollations method and return collation information to DataTable variable.   
DataTable d = default(DataTable);   
//Select the returned data into an array of DataRow.   
d = srv.EnumProcesses;   
//Iterate through the rows and display collation details for the instance of SQL Server.   
DataRow r = default(DataRow);   
DataColumn c = default(DataColumn);   
foreach ( r in d.Rows) {   
  Console.WriteLine("=====");   
  foreach ( c in r.Table.Columns) {   
    Console.WriteLine(c.ColumnName + " = " + r(c).ToString);   
  }   
}   
}   
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
