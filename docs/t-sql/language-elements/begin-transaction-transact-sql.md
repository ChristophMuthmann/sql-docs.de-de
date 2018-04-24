---
title: BEGIN TRANSACTION (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BEGIN_TRANSACTION_TSQL
- TRANSACTION_TSQL
- TRANSACTION
- BEGIN TRANSACTION
- BEGIN TRAN
- BEGIN_TRAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction logs [SQL Server], BEGIN TRANSACTION statement
- marked transactions [SQL Server], BEGIN TRANSACTION statement
- BEGIN TRANSACTION statement
- local transactions [SQL Server]
- marking transactions [SQL Server]
- transactions [SQL Server], starting
- transaction names [SQL Server]
- starting point marked for transactions
- starting transactions
ms.assetid: c6258df4-11f1-416a-816b-54f98c11145e
caps.latest.revision: 56
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a084c264195d48e0f0d8a5aae538c0a50e75c23c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="begin-transaction-transact-sql"></a>BEGIN TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Markiert den Anfang einer expliziten lokalen Transaktion. Explizite Transaktionen beginnen mit der BEGIN TRANSACTION-Anweisung und enden mit der COMMIT- oder ROLLBACK-Anweisung.  

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
--Applies to SQL Server and Azure SQL Database
 
BEGIN { TRAN | TRANSACTION }   
    [ { transaction_name | @tran_name_variable }  
      [ WITH MARK [ 'description' ] ]  
    ]  
[ ; ]  
```  
 
```  
--Applies to Azure SQL Data Warehouse and Parallel Data Warehouse
 
BEGIN { TRAN | TRANSACTION }   
[ ; ]  
```  

  
## <a name="arguments"></a>Argumente  
 *transaction_name*  
 **GILT FÜR:** SQL Server (ab 2008), Azure SQL-Datenbank
 
 Der Name, der der Transaktion zugewiesen ist. *transaction_name* muss den Regeln für Bezeichner entsprechen. Bezeichner mit mehr als 32 Zeichen sind jedoch nicht zulässig. Verwenden Sie Transaktionsnamen nur beim äußersten Paar von geschachtelten BEGIN...COMMIT- bzw. BEGIN...ROLLBACK-Anweisungen. *transaction_name* berücksichtigt immer die Groß-/Kleinschreibung, auch wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht zwischen Groß- und Kleinschreibung unterscheidet.  
  
 @*tran_name_variable*  
 **GILT FÜR:** SQL Server (ab 2008), Azure SQL-Datenbank
 
 Ist der Name einer benutzerdefinierten Variablen, die einen gültigen Transaktionsnamen enthält. Die Variable muss mit einem der folgenden Datentypen deklariert werden: **char**, **varchar**, **nchar** oder **nvarchar**. Werden mehr als 32 Zeichen an die Variable übergeben, werden nur die ersten 32 Zeichen verwendet; alle übrigen Zeichen werden abgeschnitten.  
  
 WITH MARK [ '*Beschreibung*' ]  
**GILT FÜR:** SQL Server (ab 2008), Azure SQL-Datenbank

Gibt an, dass die Transaktion im Protokoll markiert wird. Eine *Beschreibung* ist eine Zeichenfolge, die die Markierung beschreibt. Wenn die *Beschreibung* länger als 128 Zeichen ist, wird sie bei 128 Zeichen abgeschnitten, bevor sie in der Tabelle „msdb.dbo.logmarkhistory“ gespeichert wird.  
  
 Wenn WITH MARK verwendet wird, muss ein Transaktionsname angegeben sein. WITH MARK ermöglicht es, ein Transaktionsprotokoll bis zu einer benannten Markierung wiederherzustellen.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise
BEGIN TRANSACTION erhöht @@TRANCOUNT um den Wert 1.
  
BEGIN TRANSACTION stellt einen Punkt dar, an dem die Daten, auf die eine Verbindung verweist, logisch und physisch konsistent sind. Werden Fehler entdeckt, kann für alle Datenänderungen, die nach der BEGIN TRANSACTION-Anweisung vorgenommen wurden, ein Rollback ausgeführt werden, um die Daten auf diesen bekannten Konsistenzstatus zurückzusetzen. Jede Transaktion dauert so lange, bis sie entweder fehlerfrei abgeschlossen und COMMIT TRANSACTION zum dauerhaften Speichern der Änderungen in der Datenbank ausgegeben wird oder bis Fehler festgestellt und alle Änderungen mit der ROLLBACK TRANSACTION-Anweisung gelöscht werden.  
  
Mit BEGIN TRANSACTION wird eine lokale Transaktion für die Verbindung gestartet, die die Anweisung ausgibt. Abhängig von den aktuellen Einstellungen der Transaktionsisolationsstufe werden viele Ressourcen, die zur Unterstützung der von der Verbindung ausgegebenen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen abgerufen werden, so lange von der Transaktion gesperrt, bis diese entweder mit einer COMMIT TRANSACTION- oder einer ROLLBACK TRANSACTION-Anweisung abgeschlossen wurde. Längere Zeit ausstehende Transaktionen können verhindern, dass andere Anwender auf diese gesperrten Ressourcen zugreifen und dass Protokolle abgeschnitten werden.  
  
 BEGIN TRANSACTION startet zwar eine lokale Transaktion, es erfolgt jedoch so lange keine Aufzeichnung im Transaktionsprotokoll, bis die Anwendung nachfolgend eine Aktion ausführt, die im Protokoll aufgezeichnet werden muss, wie z. B. das Ausführen einer INSERT-, UPDATE- oder DELETE-Anweisung. Eine Anwendung kann Aktionen ausführen (wie z. B. das Aktivieren von Sperren, um die Transaktionsisolationsstufe von SELECT-Anweisungen zu schützen), ohne dass irgendwelche Einträge im Protokoll aufgezeichnet werden. Dies geschieht erst, wenn die Anwendung eine Änderungsaktion ausführt.  
  
 Das Benennen mehrerer Transaktionen in einer Reihe von geschachtelten Transaktionen mit einem Transaktionsnamen hat kaum Auswirkungen auf die Transaktion. Nur der erste (äußerste) Transaktionsname wird im System registriert. Ein Rollback zu einem anderen Namen (der kein gültiger Sicherungspunktname ist) erzeugt einen Fehler. Für keine der Anweisungen, die vor dem Rollback ausgeführt werden, wird zum Zeitpunkt des Auftretens dieses Fehlers ein Rollback ausgeführt. Für die Anweisungen wird erst dann ein Rollback ausgeführt, wenn für die äußere Transaktion ein Rollback ausgeführt wird.  
  
 Die von der BEGIN TRANSACTION-Anweisung gestartete lokale Transaktion wird zu einer verteilten Transaktion ausgeweitet, wenn folgende Aktionen vor einem Commit oder Rollback der Transaktion ausgeführt werden:  
  
-   Es wird eine INSERT-, DELETE- oder UPDATE-Anweisung ausgeführt, die auf eine Remotetabelle auf einem Verbindungsserver verweist. Bei der Anweisung INSERT, UPDATE oder DELETE tritt ein Fehler auf, wenn der für den Zugriff auf den Verbindungsserver verwendete OLE DB-Anbieter die ITransactionJoin-Schnittstelle nicht unterstützt.  
  
-   Eine remote gespeicherte Prozedur wird aufgerufen, wenn die Option REMOTE_PROC_TRANSACTIONS auf ON festgelegt ist.  
  
 Die lokale Kopie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird zum Transaktionscontroller und verwendet [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC), um die verteilte Transaktion zu verwalten.  
  
 Eine Transaktion kann mithilfe von BEGIN DISTRIBUTED TRANSACTION explizit als verteilte Transaktion ausgeführt werden. Weitere Informationen finden Sie unter [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md).  
  
 Wenn SET IMPLICIT_TRANSACTIONS auf ON festgelegt ist, werden durch eine BEGIN TRANSACTION-Anweisung zwei geschachtelte Transaktionen erstellt. Weitere Informationen finden Sie unter [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
## <a name="marked-transactions"></a>Markierte Transaktionen  
 Die Option WITH MARK bewirkt, dass der Transaktionsname im Transaktionsprotokoll abgelegt wird. Wenn eine Datenbank in einem früheren Status wiederhergestellt wird, kann die markierte Transaktion statt eines Datums und einer Uhrzeit verwendet werden. Weitere Informationen finden Sie unter [Wiederherstellen von verwandten Datenbanken mithilfe von markierten Transaktionen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md) und [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
 Transaktionsprotokollmarkierungen sind außerdem erforderlich, wenn Sie eine Gruppe von zusammenhängenden Datenbanken in einem logisch konsistenten Status wiederherstellen müssen. Markierungen können von einer verteilten Transaktion in den Transaktionsprotokollen der zusammenhängenden Datenbanken abgelegt werden. Das Wiederherstellen der Gruppe von zusammenhängenden Datenbanken entsprechend diesen Markierungen ergibt eine Gruppe von Datenbanken, die hinsichtlich der Transaktionen konsistent sind. Das Ablegen von Markierungen in zusammenhängenden Datenbanken erfordert spezielle Prozeduren.  
  
 Die Markierung wird nur dann im Transaktionsprotokoll abgelegt, wenn die Datenbank durch die markierte Transaktion aktualisiert wird. Transaktionen, die keine Daten ändern, werden nicht markiert.  
  
 BEGIN TRAN *new_name* WITH MARK kann innerhalb einer vorhandenen Transaktion, die nicht markiert ist, geschachtelt werden. Ist dies der Fall, wird *new_name* der Markierungsname der Transaktion, und zwar unabhängig von dem Namen, den die Transaktion möglicherweise bereits hat. Im folgenden Beispiel ist `M2` der Name der Markierung.  
  
```  
BEGIN TRAN T1;  
UPDATE table1 ...;  
BEGIN TRAN M2 WITH MARK;  
UPDATE table2 ...;  
SELECT * from table1;  
COMMIT TRAN M2;  
UPDATE table3 ...;  
COMMIT TRAN T1;  
```  
  
 Beim Schachteln von Transaktionen führt der Versuch, eine bereits markierte Transaktion zu markieren, zu einer Warnmeldung (nicht zu einer Fehlermeldung):  
  
 "BEGIN TRAN T1 WITH MARK ...;"  
  
 "UPDATE table1 ...;"  
  
 "BEGIN TRAN M2 WITH MARK ...;"  
  
 "Server: Meldung 3920, Ebene 16, Status 1, Zeile 3"  
  
 "Die Option WITH MARK gilt nur für die erste BEGIN TRAN WITH MARK-Anweisung."  
  
 "Die Option wird ignoriert."  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-an-explicit-transaction"></a>A. Verwenden expliziter Transaktionen
**GILT FÜR:** SQL Server (ab 2008), Azure SQL-Datenbank, Azure SQL Data Warehouse, Parallel Data Warehouse

In diesem Beispiel wird AdventureWorks verwendet. 

```
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```

### <a name="b-rolling-back-a-transaction"></a>B. Ausführen eines Rollbacks für eine Transaktion
**GILT FÜR:** SQL Server (ab 2008), Azure SQL-Datenbank, Azure SQL Data Warehouse, Parallel Data Warehouse

Im folgenden Beispiel werden die Auswirkungen des Rollbacks einer Transaktion veranschaulicht. In diesem Beispiel führt die ROLLBACK-Anweisung ein Rollback der INSERT-Anweisung aus, die erstellte Tabelle bleibt jedoch weiterhin vorhanden.

```
 
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  

```

### <a name="c-naming-a-transaction"></a>C. Benennen einer Transaktion 
**GILT FÜR:** SQL Server (ab 2008), Azure SQL-Datenbank

Im folgenden Beispiel wird gezeigt, wie eine Transaktion benannt wird.  
  
```  
DECLARE @TranName VARCHAR(20);  
SELECT @TranName = 'MyTransaction';  
  
BEGIN TRANSACTION @TranName;  
USE AdventureWorks2012;  
DELETE FROM AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
  
COMMIT TRANSACTION @TranName;  
GO  
```  
  
### <a name="d-marking-a-transaction"></a>D. Markieren einer Transaktion  
**GILT FÜR:** SQL Server (ab 2008), Azure SQL-Datenbank

Im folgenden Beispiel wird gezeigt, wie eine Transaktion markiert wird. Die Transaktion `CandidateDelete` wird markiert.  
  
```  
BEGIN TRANSACTION CandidateDelete  
    WITH MARK N'Deleting a Job Candidate';  
GO  
USE AdventureWorks2012;  
GO  
DELETE FROM AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
GO  
COMMIT TRANSACTION CandidateDelete;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  
