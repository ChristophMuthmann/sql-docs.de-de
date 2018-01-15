---
title: Behandlung von Ereignissen SMO | Microsoft Docs
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
- events [SMO]
- SQL Server Management Objects, events
- SMO [SQL Server], events
- events [SMO], about events
ms.assetid: b4f120dd-ba78-46ff-99c5-e47effac8544
caps.latest.revision: "48"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee676a0f3eca14164b44b19f3e5a1dfc7258c997
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2018
---
# <a name="handling-smo-events"></a>Behandeln von SMO-Ereignissen
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Es gibt Serverereignistypen, die über einen Ereignishandler und das <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Objekt abonniert werden können.  
  
 Viele der Instanzklassen in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO) können Ereignisse auslösen, wenn bestimmte Aktionen auf dem Server auftreten.  
  
 Diese Ereignisse können programmgesteuert behandelt werden, indem ein Ereignishandler eingerichtet und ein Abonnement für die zugehörigen Ereignisse vorgenommen wird. Diese Art der Ereignisbehandlung ist vorübergehend, da alle Abonnements gelöscht werden, sobald das SMO-Clientprogramm beendet wird.  
  
## <a name="connectioncontext-event-handling"></a>ConnectionContext-Ereignisbehandlung  
 Das <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Objekt unterstützt mehrere Ereignistypen. Die Ereigniseigenschaft muss auf die Instanz eines geeigneten Ereignishandlers gesetzt sein, und das Ereignishandlerobjekt muss als geschützte Funktion definiert sein, die das Ereignis behandelt.  
  
## <a name="event-subscription"></a>Ereignisabonnement  
 Sie behandeln Ereignisse, indem Sie eine Ereignishandlerklasse schreiben, eine Instanz dieser Klasse erstellen, den Ereignishandler dem übergeordneten Objekt zuordnen und dann das Ereignis abonnieren.  
  
 Eine Ereignishandlerklasse muss geschrieben werden, um Ereignisse zu behandeln. Die Ereignishandlerklasse kann mehr als eine Ereignishandlerfunktion enthalten und muss für die zu behandelnden Ereignisse installiert sein. Die Ereignishandlerfunktionen erhalten Informationen über das Ereignis aus der *ServerEventNotificatificationArgs* Parameter, der verwendet werden kann, um Informationen über das Ereignis zu melden.  
  
 Die Typen der Datenbank- und Serverereignisse, die behandelt werden können werden angezeigt, der <xref:Microsoft.SqlServer.Management.Smo.DatabaseEventSet> Klasse und die <xref:Microsoft.SqlServer.Management.Smo.ServerEventSet>Klasse.  
  
## <a name="example"></a>Beispiel  
Zum Verwenden eines angegebenen Codebeispiels müssen Sie die Programmierumgebung, Programmiervorlage und die zu verwendende Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [Erstellen eines Visual C &#35; SMO-Projekts in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  

  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-basic"></a>Registrieren von Ereignishandlern und Abonnieren der Ereignisbehandlung in Visual Basic  
 Dieses Codebeispiel zeigt, wie der Ereignishandler eingerichtet wird und wie die Datenbankereignisse abonniert werden.  
  
```VBNET
'Create an event handler subroutine that runs when a table is created.
Private Sub MyCreateEventHandler(ByVal sender As Object, ByVal e As ServerEventArgs)
    Console.WriteLine("A table has just been added to the AdventureWorks2012 2008 database.")
End Sub
'Create an event handler subroutine that runs when a table is deleted.
Private Sub MyDropEventHandler(ByVal sender As Object, ByVal e As ServerEventArgs)
    Console.WriteLine("A table has just been dropped from the AdventureWorks2012 2008 database.")
End Sub
Sub Main()
    'Connect to the local, default instance of SQL Server.
    Dim srv As Server
    srv = New Server
    'Reference the AdventureWorks2012 database.
    Dim db As Database
    db = srv.Databases("AdventureWorks2012")
    'Create a database event set that contains the CreateTable event only.
    Dim databaseCreateEventSet As New DatabaseEventSet
    databaseCreateEventSet.CreateTable = True
    'Create a server event handler and set it to the first event handler subroutine.
    Dim serverCreateEventHandler As ServerEventHandler
    serverCreateEventHandler = New ServerEventHandler(AddressOf MyCreateEventHandler)
    'Subscribe to the first server event handler when a CreateTable event occurs.
    db.Events.SubscribeToEvents(databaseCreateEventSet, serverCreateEventHandler)
    'Create a database event set that contains the DropTable event only.
    Dim databaseDropEventSet As New DatabaseEventSet
    databaseDropEventSet.DropTable = True
    'Create a server event handler and set it to the second event handler subroutine.
    Dim serverDropEventHandler As ServerEventHandler
    serverDropEventHandler = New ServerEventHandler(AddressOf MyDropEventHandler)
    'Subscribe to the second server event handler when a DropTable event occurs.
    db.Events.SubscribeToEvents(databaseDropEventSet, serverDropEventHandler)
    'Start event handling.
    db.Events.StartEvents()
    'Create a table on the database.
    Dim tb As Table
    tb = New Table(db, "Test_Table")
    Dim mycol1 As Column
    mycol1 = New Column(tb, "Name", DataType.NChar(50))
    mycol1.Collation = "Latin1_General_CI_AS"
    mycol1.Nullable = True
    tb.Columns.Add(mycol1)
    tb.Create()
    'Remove the table.
    tb.Drop()
    'Wait until the events have occured.
    Dim x As Integer
    Dim y As Integer
    For x = 1 To 1000000000
        y = x * 2
    Next
    'Stop event handling.
    db.Events.StopEvents()

End Sub
``` 
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-c"></a>Registrieren von Ereignishandlern und Abonnieren der Ereignisbehandlung in Visual C#  
 Dieses Codebeispiel zeigt, wie der Ereignishandler eingerichtet wird und wie die Datenbankereignisse abonniert werden.  
  
```csharp  
//Create an event handler subroutine that runs when a table is created.   
private void MyCreateEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been added to the AdventureWorks2012 database.");   
}   
//Create an event handler subroutine that runs when a table is deleted.   
private void MyDropEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been dropped from the AdventureWorks2012 database.");   
}   
public void Main()   
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Create a database event set that contains the CreateTable event only.   
DatabaseEventSet databaseCreateEventSet = new DatabaseEventSet();   
databaseCreateEventSet.CreateTable = true;   
//Create a server event handler and set it to the first event handler subroutine.   
ServerEventHandler serverCreateEventHandler;   
serverCreateEventHandler = new ServerEventHandler(MyCreateEventHandler);   
//Subscribe to the first server event handler when a CreateTable event occurs.   
db.Events.SubscribeToEvents(databaseCreateEventSet, serverCreateEventHandler);   
    //Create a database event set that contains the DropTable event only.   
DatabaseEventSet databaseDropEventSet = new DatabaseEventSet();   
databaseDropEventSet.DropTable = true;   
//Create a server event handler and set it to the second event handler subroutine.   
ServerEventHandler serverDropEventHandler;   
serverDropEventHandler = new ServerEventHandler(MyDropEventHandler);   
//Subscribe to the second server event handler when a DropTable event occurs.   
db.Events.SubscribeToEvents(databaseDropEventSet, serverDropEventHandler);   
//Start event handling.   
db.Events.StartEvents();   
//Create a table on the database.   
Table tb;   
tb = new Table(db, "Test_Table");   
Column mycol1;   
mycol1 = new Column(tb, "Name", DataType.NChar(50));   
mycol1.Collation = "Latin1_General_CI_AS";   
mycol1.Nullable = true;   
tb.Columns.Add(mycol1);   
tb.Create();   
//Remove the table.   
tb.Drop();   
//Wait until the events have occured.   
int x;   
int y;   
for (x = 1; x <= 1000000000; x++) {   
    y = x * 2;   
}   
//Stop event handling.   
db.Events.StopEvents();   
}  
```  
  
  
