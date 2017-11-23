---
title: BEGIN TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BEGIN_TRANSACTION_TSQL
- TRANSACTION_TSQL
- TRANSACTION
- BEGIN TRANSACTION
- BEGIN TRAN
- BEGIN_TRAN_TSQL
dev_langs: TSQL
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
caps.latest.revision: "56"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: d1e327dc8e5ce590ee3d2123b6049bbfc470d7b6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="begin-transaction-transact-sql"></a>BEGIN TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Markiert den Anfang einer expliziten lokalen Transaktion. Explizite Transaktionen mit der BEGIN TRANSACTION-Anweisung beginnen und enden die Commit- oder ROLLBACK-Anweisung.  

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
 **GILT für:** SQL Server (ab 2008), Azure SQL-Datenbank
 
 Der Name, der der Transaktion zugewiesen ist. *Transaction_name* entsprechen den Regeln für Bezeichner jedoch Bezeichner mit mehr als 32 Zeichen nicht zulässig sind. Verwenden Sie Transaktionsnamen nur beim äußersten Paar von geschachtelten BEGIN...COMMIT- bzw. BEGIN...ROLLBACK-Anweisungen. *Transaction_name* wird immer Groß-/ Kleinschreibung, auch wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist nicht in der Groß-/Kleinschreibung beachtet.  
  
 @*tran_name_variable*  
 **GILT für:** SQL Server (ab 2008), Azure SQL-Datenbank
 
 Ist der Name einer benutzerdefinierten Variablen, die einen gültigen Transaktionsnamen enthält. Die Variable muss deklariert werden, mit einem **Char**, **Varchar**, **Nchar**, oder **Nvarchar** -Datentyp. Werden mehr als 32 Zeichen an die Variable übergeben, werden nur die ersten 32 Zeichen verwendet; alle übrigen Zeichen werden abgeschnitten.  
  
 WITH MARK ["*Beschreibung*"]  
**GILT für:** SQL Server (ab 2008), Azure SQL-Datenbank

Gibt an, dass die Transaktion im Protokoll markiert wird. *Beschreibung* ist eine Zeichenfolge, die die Markierung beschreibt. Ein *Beschreibung* länger als 128 Zeichen ist auf 128 Zeichen abgeschnitten, bevor Sie in der msdb.dbo.logmarkhistory-Tabelle gespeichert wird.  
  
 Wenn WITH MARK verwendet wird, muss ein Transaktionsname angegeben sein. WITH MARK ermöglicht es, ein Transaktionsprotokoll bis zu einer benannten Markierung wiederherzustellen.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise
BEGIN TRANSACTION erhöht@TRANCOUNT um 1.
  
BEGIN TRANSACTION stellt einen Punkt dar, an dem die Daten, auf die eine Verbindung verweist, logisch und physisch konsistent sind. Werden Fehler entdeckt, kann für alle Datenänderungen, die nach der BEGIN TRANSACTION-Anweisung vorgenommen wurden, ein Rollback ausgeführt werden, um die Daten auf diesen bekannten Konsistenzstatus zurückzusetzen. Jede Transaktion dauert so lange, bis sie entweder fehlerfrei abgeschlossen und COMMIT TRANSACTION zum dauerhaften Speichern der Änderungen in der Datenbank ausgegeben wird oder bis Fehler festgestellt und alle Änderungen mit der ROLLBACK TRANSACTION-Anweisung gelöscht werden.  
  
Mit BEGIN TRANSACTION wird eine lokale Transaktion für die Verbindung gestartet, die die Anweisung ausgibt. Abhängig von den aktuellen Einstellungen der Transaktionsisolationsstufe werden viele Ressourcen, die zur Unterstützung der von der Verbindung ausgegebenen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen abgerufen werden, so lange von der Transaktion gesperrt, bis diese entweder mit einer COMMIT TRANSACTION- oder einer ROLLBACK TRANSACTION-Anweisung abgeschlossen wurde. Längere Zeit ausstehende Transaktionen können verhindern, dass andere Anwender auf diese gesperrten Ressourcen zugreifen und dass Protokolle abgeschnitten werden.  
  
 BEGIN TRANSACTION startet zwar eine lokale Transaktion, es erfolgt jedoch so lange keine Aufzeichnung im Transaktionsprotokoll, bis die Anwendung nachfolgend eine Aktion ausführt, die im Protokoll aufgezeichnet werden muss, wie z. B. das Ausführen einer INSERT-, UPDATE- oder DELETE-Anweisung. Eine Anwendung kann Aktionen ausführen (wie z. B. das Aktivieren von Sperren, um die Transaktionsisolationsstufe von SELECT-Anweisungen zu schützen), ohne dass irgendwelche Einträge im Protokoll aufgezeichnet werden. Dies geschieht erst, wenn die Anwendung eine Änderungsaktion ausführt.  
  
 Das Benennen mehrerer Transaktionen in einer Reihe von geschachtelten Transaktionen mit einem Transaktionsnamen hat kaum Auswirkungen auf die Transaktion. Nur der erste (äußerste) Transaktionsname wird im System registriert. Ein Rollback zu einem anderen Namen (der kein gültiger Sicherungspunktname ist) erzeugt einen Fehler. Für keine der Anweisungen, die vor dem Rollback ausgeführt werden, wird zum Zeitpunkt des Auftretens dieses Fehlers ein Rollback ausgeführt. Für die Anweisungen wird erst dann ein Rollback ausgeführt, wenn für die äußere Transaktion ein Rollback ausgeführt wird.  
  
 Die von der BEGIN TRANSACTION-Anweisung gestartete lokale Transaktion wird zu einer verteilten Transaktion ausgeweitet, wenn folgende Aktionen vor einem Commit oder Rollback der Transaktion ausgeführt werden:  
  
-   Es wird eine INSERT-, DELETE- oder UPDATE-Anweisung ausgeführt, die auf eine Remotetabelle auf einem Verbindungsserver verweist. Die INSERT-, Update- oder DELETE-Anweisung schlägt fehl, wenn der OLE DB-Anbieter verwendet, um Zugriff auf den Verbindungsserver ITransactionJoin-Schnittstelle nicht unterstützt.  
  
-   Eine remote gespeicherte Prozedur wird aufgerufen, wenn die Option REMOTE_PROC_TRANSACTIONS auf ON festgelegt ist.  
  
 Die lokale Kopie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird zum Transaktionscontroller und verwendet [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC), um die verteilte Transaktion zu verwalten.  
  
 Eine Transaktion kann mithilfe von BEGIN DISTRIBUTED TRANSACTION explizit als verteilte Transaktion ausgeführt werden. Weitere Informationen finden Sie unter [BEGIN DISTRIBUTED TRANSACTION &#40; Transact-SQL &#41; ](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md).  
  
 Wenn SET IMPLICIT_TRANSACTIONS auf ON festgelegt ist, werden durch eine BEGIN TRANSACTION-Anweisung zwei geschachtelte Transaktionen erstellt. Weitere Informationen finden Sie unter [SET IMPLICIT_TRANSACTIONS &#40; Transact-SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)  
  
## <a name="marked-transactions"></a>Markierte Transaktionen  
 Die Option WITH MARK bewirkt, dass der Transaktionsname im Transaktionsprotokoll abgelegt wird. Wenn eine Datenbank in einem früheren Status wiederhergestellt wird, kann die markierte Transaktion statt eines Datums und einer Uhrzeit verwendet werden. Weitere Informationen finden Sie unter [mithilfe von markierten Transaktionen zum Wiederherstellen von verwandten Datenbanken &#40; Vollständiges Wiederherstellungsmodell &#41; ](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md) und [RESTORE &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-transact-sql.md).  
  
 Transaktionsprotokollmarkierungen sind außerdem erforderlich, wenn Sie eine Gruppe von zusammenhängenden Datenbanken in einem logisch konsistenten Status wiederherstellen müssen. Markierungen können von einer verteilten Transaktion in den Transaktionsprotokollen der zusammenhängenden Datenbanken abgelegt werden. Das Wiederherstellen der Gruppe von zusammenhängenden Datenbanken entsprechend diesen Markierungen ergibt eine Gruppe von Datenbanken, die hinsichtlich der Transaktionen konsistent sind. Das Ablegen von Markierungen in zusammenhängenden Datenbanken erfordert spezielle Prozeduren.  
  
 Die Markierung wird nur dann im Transaktionsprotokoll abgelegt, wenn die Datenbank durch die markierte Transaktion aktualisiert wird. Transaktionen, die keine Daten ändern, werden nicht markiert.  
  
 BEGIN TRAN *New_name* WITH MARK kann innerhalb einer bereits vorhandenen Transaktion, die nicht markiert ist geschachtelt werden. Dies der Fall, *New_name* der Markierungsname für die Transaktion, ungeachtet des Namens, der die Transaktion möglicherweise bereits zugewiesen wurde. Im folgenden Beispiel ist `M2` der Name der Markierung.  
  
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
  
### <a name="a-using-an-explicit-transaction"></a>A. Verwenden eine explizite Transaktion
**GILT für:** SQL Server (ab 2008), Azure SQL-Datenbank, Azure SQL Data Warehouse, Parallel Data Warehouse

In diesem Beispiel wird die AdventureWorks verwendet. 

```
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```

### <a name="b-rolling-back-a-transaction"></a>B. Rollback einer Transaktion
**GILT für:** SQL Server (ab 2008), Azure SQL-Datenbank, Azure SQL Data Warehouse, Parallel Data Warehouse

Das folgende Beispiel zeigt die Auswirkung von Rollback einer Transaktion. In diesem Beispiel wird die ROLLBACK-Anweisung wird ein Rollback der INSERT-Anweisung, die erstellte Tabelle sind jedoch weiterhin vorhanden.

```
 
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  

```

### <a name="c-naming-a-transaction"></a>C. Benennen einer Transaktion 
**GILT für:** SQL Server (ab 2008), Azure SQL-Datenbank

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
**GILT für:** SQL Server (ab 2008), Azure SQL-Datenbank

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
  
## <a name="see-also"></a>Siehe auch  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [COMMIT WORK &#40; Transact-SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40; Transact-SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  
