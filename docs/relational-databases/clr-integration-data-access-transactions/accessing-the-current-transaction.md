---
title: Zugriff auf die aktuelle Transaktion | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- current transaction access
- Current property
- Transaction class
ms.assetid: 1a4e2ce5-f627-4c81-8960-6a9968cefda2
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 550455ead049191d94de93a40a55aa3b064602a6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="accessing-the-current-transaction"></a>Zugriff auf die aktuelle Transaktion
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Wenn eine Transaktion aktiv ist, an die Stelle, an die common Language Runtime (CLR)-Code auf ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist eingegeben haben, wird die Transaktion durch verfügbar gemacht der **"System.Transactions.Transaction"** Klasse. Mit der **Transaction.Current** -Eigenschaft wird auf die aktuelle Transaktion zugegriffen. In den meisten Fällen ist es nicht notwendig, explizit auf die Transaktion zuzugreifen. Bei Datenbankverbindungen überprüft ADO.NET **Transaction.Current** automatisch beim Aufruf der **Connection.Open** -Methode, und trägt die Verbindung automatisch in diese Transaktion ein (sofern für das Schlüsselwort **Enlist** in der Verbindungszeichenfolge nicht false angegeben wurde).  
  
 In den folgenden Szenarien sollten Sie das **Transaction** -Objekt direkt verwenden:  
  
-   Wenn Sie eine Ressource eintragen möchten, die nicht automatisch eingetragen wird oder die aus irgendeinem Grund während der Initialisierung nicht eingetragen wurde.  
  
-   Wenn Sie eine Ressource explizit in die Transaktion eintragen möchten.  
  
-   Wenn Sie die externe Transaktion aus einer gespeicherten Prozedur oder Funktion heraus beenden möchten. In diesem Fall verwenden Sie <xref:System.Transactions.TransactionScope>. Beispielsweise wird mit dem folgenden Code die aktuelle Transaktion rückgängig gemacht.  
  
    ```  
    using(TransactionScope transactionScope = new TransactionScope(TransactionScopeOptions.Required)) { }  
    ```  
  
 Im weiteren Verlauf dieses Themas werden andere Möglichkeiten beschrieben, eine externe Transaktion abzubrechen.  
  
## <a name="canceling-an-external-transaction"></a>Abbrechen einer externen Transaktion  
 Sie können externe Transaktionen wie folgt von einer verwalteten Prozedur oder einer Funktion aus abbrechen:  
  
-   Die verwaltete Prozedur oder die Funktion kann in einem Ausgabeparameter einen Wert zurückgeben. Die aufrufende [!INCLUDE[tsql](../../includes/tsql-md.md)] Prozedur kann den zurückgegebenen Wert überprüfen und ggf. ausführen **ROLLBACK TRANSACTION**.  
  
-   Die verwaltete Prozedur oder die Funktion kann eine benutzerdefinierte Ausnahme auslösen. Die aufrufende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Prozedur kann die Ausnahme wird von der verwalteten Prozedur oder Funktion in einem Try/Catch-Block ausgelöst, und führen Sie **ROLLBACK TRANSACTION**.  
  
-   Die verwaltete Prozedur oder die Funktion kann die aktuelle Transaktion durch einen Aufruf der **Transaction.Rollback** -Methode abbrechen, wenn eine bestimmte Bedingung erfüllt wird.  
  
 Beim Aufruf innerhalb einer verwalteten Prozedur oder Funktion löst die **Transaction.Rollback** -Methode eine Ausnahme mit einer nicht eindeutigen Fehlermeldung aus und kann in einen try/catch-Block eingebunden werden. Die Fehlermeldung lautet wie folgt oder ähnlich:  
  
```  
Msg 3994, Level 16, State 1, Procedure uspRollbackFromProc, Line 0  
Transaction is not allowed to roll back inside a user defined routine, trigger or aggregate because the transaction is not started in that CLR level. Change application logic to enforce strict transaction nesting.  
```  
  
 Diese Ausnahme wird erwartet und der try/catch-Block ist notwendig, damit die Codeausführung fortgesetzt wird. Wenn kein try/catch-Block vorhanden ist, wird die Ausnahme sofort der aufrufenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur übergeben und der verwaltete Code wird zu Ende ausgeführt. Wenn die Ausführung des verwalteten Codes beendet ist, wird eine andere Ausnahme ausgelöst.  
  
```  
Msg 3991, Level 16, State 1, Procedure uspRollbackFromProc, Line 1   
The context transaction which was active before entering user defined routine, trigger or aggregate " uspRollbackFromProc " has been ended inside of it, which is not allowed. Change application logic to enforce strict transaction nesting. The statement has been terminated.  
```  
  
 Diese Ausnahme ist ebenfalls zu erwarten, und die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung, welche die den Trigger auslösenden Aktion ausführt, muss in einen try/catch-Block eingeschlossen werden, damit die Ausführung fortgesetzt wird. Trotz der zwei ausgelösten Ausnahmen wird ein Rollback für die Transaktion ausgeführt, und für die Änderungen in der Tabelle wird kein Commit ausgeführt.  
  
### <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird von der verwalteten Prozedur für eine Transaktion mit der **Transaction.Rollback** -Methode ein Rollback für die Transaktion ausgeführt. Beachten Sie den try/catch-Block um die **Transaction.Rollback** -Methode im verwalteten Code. Das [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skript erstellt eine Assembly und eine verwaltete gespeicherte Prozedur. Beachten Sie, dass die **EXEC uspRollbackFromProc** -Anweisung in einen try/catch-Block eingebunden ist, sodass die Ausnahme abgefangen wird, die ausgelöst wird, sobald die Ausführung der verwalteten Prozedur beendet wurde.  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Transactions;  
  
public partial class StoredProcedures  
{  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void uspRollbackFromProc()  
{  
   using (SqlConnection connection = new SqlConnection(@"context connection=true"))  
   {  
      // Open the connection.  
      connection.Open();  
  
      bool successCondition = true;  
  
      // Success condition is met.  
      if (successCondition)  
      {  
         SqlContext.Pipe.Send("Success condition met in procedure.");   
         // Perform other actions here.  
      }  
  
      //  Success condition is not met, the transaction will be rolled back.  
      else  
      {  
         SqlContext.Pipe.Send("Success condition not met in managed procedure. Transaction rolling back...");  
         try  
         {  
               // Get the current transaction and roll it back.  
               Transaction trans = Transaction.Current;  
               trans.Rollback();  
         }  
         catch (SqlException ex)  
         {  
            // Catch the expected exception.   
            // This allows the connection to close correctly.                      
         }    
      }  
  
      // Close the connection.  
      connection.Close();  
   }  
}  
};  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Transactions  
  
Partial Public Class StoredProcedures  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  uspRollbackFromProc ()  
   Using connection As New SqlConnection("context connection=true")  
  
   ' Open the connection.  
   connection.Open()  
  
   Dim successCondition As Boolean  
   successCondition = False  
  
   ' Success condition is met.  
   If successCondition Then  
  
      SqlContext.Pipe.Send("Success condition met in procedure.")  
  
      ' Success condition is not met, the transaction will be rolled back.  
  
   Else  
      SqlContext.Pipe.Send("Success condition not met in managed procedure. Transaction rolling back...")  
      Try  
         ' Get the current transaction and roll it back.  
         Dim trans As Transaction  
         trans = Transaction.Current  
         trans.Rollback()  
  
      Catch ex As SqlException  
         ' Catch the exception instead of throwing it.    
         ' This allows the connection to close correctly.                      
      End Try  
  
   End If  
  
   ' Close the connection.  
   connection.Close()  
  
End Using  
End Sub  
End Class  
```  
  
 **Transact-SQL**  
  
```  
--Register assembly.  
CREATE ASSEMBLY TestProcs FROM 'C:\Programming\TestProcs.dll'   
Go  
CREATE PROCEDURE uspRollbackFromProc AS EXTERNAL NAME TestProcs.StoredProcedures.uspRollbackFromProc  
Go  
  
-- Execute procedure.  
BEGIN TRY  
BEGIN TRANSACTION   
-- Perform other actions.  
Exec uspRollbackFromProc  
-- Perform other actions.  
PRINT N'Commiting transaction...'  
COMMIT TRANSACTION  
END TRY  
  
BEGIN CATCH  
SELECT ERROR_NUMBER() AS ErrorNum, ERROR_MESSAGE() AS ErrorMessage  
PRINT N'Exception thrown, rolling back transaction.'  
ROLLBACK TRANSACTION  
PRINT N'Transaction rolled back.'   
END CATCH  
Go  
  
-- Clean up.  
DROP Procedure uspRollbackFromProc;  
Go  
DROP ASSEMBLY TestProcs;  
Go  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CLR-Integration und -Transaktionen](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
