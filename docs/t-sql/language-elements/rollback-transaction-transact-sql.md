---
title: ROLLBACK TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROLLBACK TRANSACTION
- ROLLBACK
- ROLLBACK_TSQL
- ROLLBACK_TRANSACTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction rollbacks [SQL Server]
- ROLLBACK TRANSACTION statement
- erasing data modifications [SQL Server]
- rolling back transactions, ROLLBACK TRANSACTION
- roll back transactions [SQL Server]
- savepoints [SQL Server]
ms.assetid: 6882c5bc-ff74-476a-984b-164aeb036c66
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0df2fdf3d3e4aa7915fbfef3ff921d12b2851044
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="rollback-transaction-transact-sql"></a>ROLLBACK TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Führt für eine explizite oder implizite Transaktion ein Rollback zum Anfang der Transaktion oder auf einen Sicherungspunkt innerhalb der Transaktion aus. Mit ROLLBACK TRANSACTION können Sie alle Datenänderungen löschen, die seit dem letzten Start der Transaktion oder bis zu einem Sicherungspunkt vorgenommen wurden. Die Anweisung gibt auch Ressourcen frei, die von der Transaktion beansprucht werden.  
  

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ROLLBACK { TRAN | TRANSACTION }   
     [ transaction_name | @tran_name_variable  
     | savepoint_name | @savepoint_variable ]   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *transaction_name*  
 Der bei BEGIN TRANSACTION der Transaktion zugewiesene Name. *Transaction_name* muss den Regeln für Bezeichner entsprechen, aber nur die ersten 32 Zeichen des Transaktionsnamens verwendet werden. Wenn Transaktionen geschachtelt *Transaction_name* muss der Name der äußersten BEGIN TRANSACTION-Anweisung sein. *Transaction_name* wird immer Groß-/Kleinschreibung beachtet, selbst wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist nicht in der Groß-/Kleinschreibung beachtet.  
  
 **@** *tran_name_variable*  
 Ist der Name einer benutzerdefinierten Variablen, die einen gültigen Transaktionsnamen enthält. Die Variable muss deklariert werden, mit einem **Char**, **Varchar**, **Nchar**, oder **Nvarchar** -Datentyp.  
  
 *savepoint_name*  
 Ist *Savepoint_name* aus einer SAVE TRANSACTION-Anweisung. *Savepoint_name* muss den Regeln für Bezeichner entsprechen. Verwendung *Savepoint_name* Wann sollte ein bedingtes Rollback nur einen Teil der Transaktion auswirken.  
  
 **@** *savepoint_variable*  
 Dies ist der Name einer benutzerdefinierten Variablen, die einen gültigen Sicherungspunktnamen enthält. Die Variable muss deklariert werden, mit einem **Char**, **Varchar**, **Nchar**, oder **Nvarchar** -Datentyp.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Eine ROLLBACK TRANSACTION-Anweisung erzeugt keine Meldung für den Benutzer. Falls Warnungen in gespeicherten Prozeduren oder Triggern benötigt werden, verwenden Sie die RAISERROR- oder die PRINT-Anweisung. Die RAISERROR-Anweisung wird beim Anzeigen von Fehlern bevorzugt.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 ROLLBACK TRANSACTION-Anweisung eine *Savepoint_name* oder *Transaction_name* führt einen Rollback bis an den Anfang der Transaktion. Wenn Transaktionen geschachtelt werden, führt diese Anweisung ein Rollback für alle inneren Transaktionen bis zur äußersten BEGIN TRANSACTION-Anweisung aus. In beiden Fällen setzt ROLLBACK TRANSACTION die @@TRANCOUNT -Systemfunktion auf 0. ROLLBACK TRANSACTION *Savepoint_name* verringert nicht@TRANCOUNT.  
  
 ROLLBACK TRANSACTION kann nicht verwiesen. eine *Savepoint_name* verteilte Transaktionen entweder explizit mit BEGIN DISTRIBUTED TRANSACTION gestartet oder aus einer lokalen Transaktion ausgeweitet.  
  
 Ein Rollback kann nicht für eine Transaktion ausgeführt werden, nachdem eine COMMIT TRANSACTION-Anweisung ausgeführt wurde, es sei denn, COMMIT TRANSACTION ist einer geschachtelten Transaktion zugeordnet, die in der Transaktion enthalten ist, für die ein Rollback ausgeführt wird. In diesem Fall wird die geschachtelte Transaktion wird ein Rollback, auch wenn Sie eine COMMIT TRANSACTION hierfür ausgegeben haben.  
  
 Innerhalb einer Transaktion sind doppelte Sicherungspunktnamen zulässig; jedoch führt eine ROLLBACK TRANSACTION-Anweisung, die die doppelten Sicherungspunktnamen verwendet, das Rollback nur für die letzte SAVE TRANSACTION-Anweisung aus, die diesen Sicherungspunktnamen verwendet hat.  
  
## <a name="interoperability"></a>Interoperabilität  
 In gespeicherten Prozeduren, ROLLBACK TRANSACTION-Anweisungen ohne eine *Savepoint_name* oder *Transaction_name* Rollback für alle Anweisungen aus, bis zur äußersten BEGIN TRANSACTION. Eine ROLLBACK TRANSACTION-Anweisung in einer gespeicherten Prozedur, die bewirkt, dass @@TRANCOUNT auf einen anderen Wert aufweist, nach Abschluss der gespeicherten Prozedur als der @@TRANCOUNT Wert, wenn die gespeicherte Prozedur aufgerufen wurde, erzeugt eine informationsmeldung. Die Meldung beeinträchtigt nachfolgende Verarbeitungsvorgänge nicht.  
  
 Beim Ausgeben von ROLLBACK TRANSACTION in einem Trigger erfolgt Folgendes:  
  
-   Alle datenänderungen, die an diesem Punkt in der aktuellen Transaktion vorgenommen werden, ein Rollback einschließlich der vom Trigger vorgenommen.  
  
-   Der Trigger setzt die Ausführung aller verbleibenden Anweisungen nach der ROLLBACK-Anweisung fort. Wenn durch eine dieser Anweisungen Daten geändert werden, wird für die Änderungen kein Rollback ausgeführt. Es werden keine geschachtelten Trigger durch die Ausführung der verbleibenden Anweisungen ausgelöst.  
  
-   Die Anweisungen im Batch, die auf die Anweisung folgen, die den Trigger ausgelöst hat, werden nicht ausgeführt.  
  
@@TRANCOUNT wird um eins erhöht, bei der Eingabe eines Triggers, sogar im Autocommit-Modus. (Das System behandelt einen Trigger als implizite, geschachtelte Transaktion.)  
  
ROLLBACK TRANSACTION-Anweisungen in einer gespeicherten Prozedur wirken sich nicht auf nachfolgende Anweisungen in dem Batch aus, der die Prozedur aufgerufen hat; nachfolgende Anweisungen im Batch werden ausgeführt. ROLLBACK TRANSACTION-Anweisungen in Triggern beenden den Batch mit der Anweisung, die den Trigger ausgelöst hat; nachfolgende Anweisungen im Batch werden nicht ausgeführt.  
  
Die Auswirkung von ROLLBACK auf Cursor wird durch diese drei Regeln definiert:  
  
1.  Wenn CURSOR_CLOSE_ON_COMMIT auf ON festgelegt ist, schließt ROLLBACK alle offenen Cursor, hebt die Zuordnung aber nicht auf.  
  
2.  Wenn für CURSOR_CLOSE_ON_COMMIT OFF festgelegt ist, hat ROLLBACK keine Auswirkungen auf geöffnete synchrone STATIC- oder INSENSITIVE-Cursor oder asynchrone STATIC-Cursor, die vollständig aufgefüllt wurden. Offene Cursor anderer Typen werden geschlossen, ihre Zuordnungen aber nicht aufgehoben.  
  
3.  Ein Fehler, der einen Batch beendet und ein internes Rollback generiert, hebt die Zuordnung alle Cursor auf, die in dem Batch deklariert wurden, der die Fehleranweisung enthält. Die Zuordnung aller Cursor wird unabhängig von ihrem Typ oder der Einstellung von CURSOR_CLOSE_ON_COMMIT aufgehoben. Dazu gehören auch die Cursor, die in gespeicherten Prozeduren deklariert sind, die von dem Fehlerbatch aufgerufen wurden. In einem Batch vor dem Fehlerbatch deklarierte Cursor unterliegen den Regeln 1 und 2. Ein Beispiel für diese Art von Fehler ist ein Deadlockfehler. Eine in einem Trigger ausgegebene ROLLBACK-Anweisung generiert ebenfalls automatisch diese Art von Fehler.  
  
## <a name="locking-behavior"></a>Sperrverhalten  
 Eine ROLLBACK TRANSACTION-Anweisung angeben einer *Savepoint_name* hebt alle Sperren, die außerhalb des Sicherungspunkts, mit Ausnahme von ausweitungen und Konvertierungen erworben wurden. Diese Sperren werden nicht aufgehoben, und sie werden nicht in ihren vorherigen Sperrmodus zurückkonvertiert.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Auswirkungen des Rollbacks einer benannten Transaktion veranschaulicht. Nach dem Erstellen einer Tabellenstatus, die folgenden Anweisungen benannten Transaktion startet, zwei Zeilen eingefügt, und klicken Sie dann den Rollback der Transaktion, die mit dem Namen in der Variablen @TransactionName. Eine andere Anweisung außerhalb der benannten Transaktion zwei Zeilen eingefügt. Die Abfrage gibt die Ergebnisse der vorherigen Anweisungen zurück.   
  
```sql    
USE tempdb;  
GO  
CREATE TABLE ValueTable ([value] int);  
GO  
  
DECLARE @TransactionName varchar(20) = 'Transaction1';  
  
BEGIN TRAN @TransactionName  
       INSERT INTO ValueTable VALUES(1), (2);  
ROLLBACK TRAN @TransactionName;  
  
INSERT INTO ValueTable VALUES(3),(4);  
  
SELECT [value] FROM ValueTable;  
  
DROP TABLE ValueTable;  
```  
[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]  
```  
value  
-----   
3    
4  
```  
  
  
## <a name="see-also"></a>Siehe auch  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  
