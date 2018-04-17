---
title: SqlPipe-Objekt | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- custom result sets [CLR integration]
- SqlPipe object
- tabular results
ms.assetid: 3e090faf-085f-4c01-a565-79e3f1c36e3b
caps.latest.revision: 54
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eeeb65173b29ab5e0e441789d1c0033a2a59b369
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlpipe-object"></a>SqlPipe-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]war es üblich, eine gespeicherte Prozedur (oder eine erweiterte gespeicherte Prozedur) zu schreiben, die Ergebnisse oder Ausgabeparameter an den aufrufenden Client sendet.  
  
 In einer [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherten Prozedur sendet jede **SELECT** -Anweisung, die NULL oder mehr Zeilen zurückgibt, die Ergebnisse an die "Pipe" des verbundenen Aufrufers.  
  
 Für CLR-Datenbankobjekte (Common Language Runtime), die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt werden, können Sie die Ergebnisse mit der **Send** -Methode des **SqlPipe** -Objekts an die verbundene Pipe senden. Greifen Sie auf die **Pipe** -Eigenschaft des **SqlContext** -Objekts zu, um das **SqlPipe** -Objekt abzurufen. Die **SqlPipe** -Klasse gleicht konzeptionell der **Response** -Klasse in ASP.NET. Weitere Informationen finden Sie in der Referenzdokumentation zur SqlPipe-Klasse im .NET Framework Software Development Kit.  
  
## <a name="returning-tabular-results-and-messages"></a>Zurückgeben von Tabellenergebnissen und Meldungen  
 **SqlPipe** verfügt über eine **Send** -Methode, die drei Überladungen besitzt. Die Überladungen sind:  
  
-   `void Send(string message)`  
  
-   `void Send(SqlDataReader reader)`  
  
-   `void Send(SqlDataRecord record)`  
  
 Die **Send** -Methode sendet Daten direkt an den Client oder Aufrufer. Normalerweise verwendet der Client die Ausgabe der **SqlPipe**-Methode, im Fall von geschachtelten gespeicherten CLR-Prozeduren kann es sich beim Consumer der Ausgabe jedoch auch um eine gespeicherte Prozedur handeln. Beispiel: Procedure1 ruft SqlCommand.ExecuteReader() mit dem Befehlstext "EXEC Procedure2" auf. Bei Procedure2 handelt es sich ebenfalls um eine verwaltete gespeicherte Prozedur. Wenn Procedure2 jetzt SqlPipe.Send( SqlDataRecord ) aufruft, wird die Zeile an den Reader von Procedure1 und nicht an den Client gesendet.  
  
 Die **senden** Methode sendet eine zeichenfolgenmeldung, die auf dem Client angezeigt, als eine informationsmeldung ähnlich wie PRINT in wird [!INCLUDE[tsql](../../includes/tsql-md.md)]. Die Methode kann mit **SqlDataRecord**auch ein einzeiliges Resultset oder mit **SqlDataReader**ein mehrzeiliges Resultset senden.  
  
 Das **SqlPipe** -Objekt stellt außerdem eine **ExecuteAndSend** -Methode bereit. Mit dieser Methode kann ein Befehl (der als **SqlCommand** -Objekt übergeben wird) ausgeführt und Ergebnisse direkt zurück an den Aufrufer gesendet werden. Wenn im übermittelten Befehl Fehler vorhanden sind, werden Ausnahmen an die Pipe gesendet. Es wird jedoch auch eine Kopie an den aufrufenden verwalteten Code gesendet. Wenn der aufrufende Code die Ausnahme nicht abfängt, wird sie in der Liste aufwärts weitergeleitet an den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code und dann zweimal in der Ausgabe angezeigt. Wenn der aufrufende Code die Ausnahme abfängt, wird dem Client der Fehler angezeigt, es gibt jedoch keinen doppelten Fehler.  
  
 Es kann nur ein **SqlCommand** -Befehl, der mit der kontextabhängigen Verbindung verknüpft ist, akzeptiert werden. Ein Befehl, der mit der nicht kontextabhängigen Verbindung verknüpft ist, kann nicht akzeptiert werden.  
  
## <a name="returning-custom-result-sets"></a>Zurückgeben von benutzerdefinierten Resultsets  
 Verwaltete gespeicherte Prozeduren können Resultsets senden, die nicht von einem **SqlDataReader**stammen. Die **SendResultsStart** -Methode ermöglicht es gespeicherten Prozeduren zusammen mit **SendResultsRow** und **SendResultsEnd**, benutzerdefinierte Resultsets an den Client zu senden.  
  
 **SendResultsStart** akzeptiert einen **SqlDataRecord** als Eingabe. Die Methode kennzeichnet den Anfang eines Resultsets und erstellt mithilfe der Datensatzmetadaten die Metadaten zur Beschreibung des Resultsets. Der Wert des Datensatzes wird nicht mit **SendResultsStart**gesendet. Alle nachfolgenden Zeilen, die mit der **SendResultsRow**-Methode gesendet werden, müssen dieser Metadatendefinition entsprechen.  
  
> [!NOTE]  
>  Nach dem Aufruf der **SendResultsStart** -Methode können nur **SendResultsRow** und **SendResultsEnd** aufgerufen werden. Ein Aufruf einer beliebigen anderen Methode in der gleichen Instanz von **SqlPipe** verursacht eine **InvalidOperationException**. **SendResultsEnd** setzt **SqlPipe** auf den Ausgangszustand zurück, in dem andere Methoden aufgerufen werden können.  
  
### <a name="example"></a>Beispiel  
 Die gespeicherte **uspGetProductLine** -Prozedur gibt den Namen, die Produktnummer, die Farbe und den Listenpreis aller Produkte innerhalb einer bestimmten Produktlinie zurück. Diese gespeicherte Prozedur nimmt genaue Übereinstimmungen für *prodLine*an.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
  
public partial class StoredProcedures  
{  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void uspGetProductLine(SqlString prodLine)  
{  
    // Connect through the context connection.  
    using (SqlConnection connection = new SqlConnection("context connection=true"))  
    {  
        connection.Open();  
  
        SqlCommand command = new SqlCommand(  
            "SELECT Name, ProductNumber, Color, ListPrice " +  
            "FROM Production.Product " +   
            "WHERE ProductLine = @prodLine;", connection);  
  
        command.Parameters.AddWithValue("@prodLine", prodLine);  
  
        try  
        {  
            // Execute the command and send the results to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command);  
        }  
        catch (System.Data.SqlClient.SqlException ex)  
        {  
            // An error occurred executing the SQL command.  
        }  
     }  
}  
};  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Partial Public Class StoredProcedures  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub uspGetProductLine(ByVal prodLine As SqlString)  
    Dim command As SqlCommand  
  
    ' Connect through the context connection.  
    Using connection As New SqlConnection("context connection=true")  
        connection.Open()  
  
        command = New SqlCommand( _  
        "SELECT Name, ProductNumber, Color, ListPrice " & _  
        "FROM Production.Product " & _  
        "WHERE ProductLine = @prodLine;", connection)  
        command.Parameters.AddWithValue("@prodLine", prodLine)  
  
        Try  
            ' Execute the command and send the results   
            ' directly to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command)  
        Catch ex As System.Data.SqlClient.SqlException  
            ' An error occurred executing the SQL command.  
        End Try  
    End Using  
End Sub  
End Class  
```  
  
 Die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung führt die **uspGetProduct** -Prozedur aus, die eine Liste mit Touringräderprodukten zurückgibt.  
  
```  
EXEC uspGetProductLineVB 'T';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SqlDataRecord-Objekt](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)   
 [CLR-gespeicherte Prozeduren](http://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [Von SQL Server verwendete prozessinterne spezifische Erweiterungen für ADO.NET](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
