---
title: SET TRANSACTION ISOLATION LEVEL (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- LEVEL
- LEVEL_TSQL
- SET TRANSACTION ISOLATION LEVEL
- ISOLATION
- ISOLATION_TSQL
- SET_TRANSACTION_ISOLATION_LEVEL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET TRANSACTION ISOLATION LEVEL statement
- row versioning [SQL Server], isolation levels
- TRANSACTION ISOLATION LEVEL option
- isolation levels [SQL Server], setting
- locking [SQL Server], isolation levels
- transactions [SQL Server], isolation levels
ms.assetid: 016fb05e-a702-484b-bd2a-a6eabd0d76fd
caps.latest.revision: 80
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b02c7d741c03fb25aa6d4afd4048f3b67c77da45
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="set-transaction-isolation-level-transact-sql"></a>SET TRANSACTION ISOLATION LEVEL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Steuert das Verhalten von Sperren und der Zeilenversionsverwaltung von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die von einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgestellt wurden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>Syntax

```
-- Syntax for SQL Server and Azure SQL Database
  
SET TRANSACTION ISOLATION LEVEL
    { READ UNCOMMITTED
    | READ COMMITTED
    | REPEATABLE READ
    | SNAPSHOT
    | SERIALIZABLE
    }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse
  
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED
```

## <a name="arguments"></a>Argumente  
 READ UNCOMMITTED  
 Gibt an, dass Anweisungen Zeilen lesen können, die von anderen Transaktionen geändert wurden, für die jedoch noch kein Commit ausgeführt wurde.  
  
 Transaktionen, die auf der READ UNCOMMITTED-Ebene ausgeführt werden, geben keine gemeinsamen Sperren aus, die verhindern würden, dass andere Transaktionen Daten ändern, die von der aktuellen Transaktion gelesen werden. READ UNCOMMITTED-Transaktionen werden darüber hinaus nicht durch exklusive Sperren blockiert, die verhindern würden, dass die aktuelle Transaktion Zeilen liest, die von anderen Transaktionen geändert wurden, für die jedoch kein Commit ausgeführt wurde. Wenn diese Option festgelegt wird, können Änderungen gelesen werden, für die kein Commit ausgeführt wurde (so genannte Dirty Reads). Datenwerte können geändert werden, und Zeilen können vor dem Transaktionsende im Dataset hinzugefügt oder entfernt werden. Diese Option hat dieselbe Auswirkung wie das Festlegen von NOLOCK für die Tabellen in allen SELECT-Anweisungen in einer Transaktion. Von allen Isolationsstufen ist diese am wenigsten restriktiv.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Sie auch Konflikte zwischen Sperren minimieren und zugleich Transaktionen vor Dirty Reads von Datenänderungen, für die kein Commit ausgeführt wurde, folgendermaßen schützen:  
  
-   Verwendung der READ COMMITTED-Isolationsstufe und gleichzeitiges Festlegen der Datenbankoption READ_COMMITTED_SNAPSHOT auf ON.  
  
-   Verwendung der SNAPSHOT-Isolationsstufe.  
  
 READ COMMITTED  
 Gibt an, dass Anweisungen Zeilen nicht lesen können, die von anderen Transaktionen geändert wurden, für die jedoch noch kein Commit ausgeführt wurde. Dadurch werden Dirty Reads verhindert. Daten können von anderen Transaktionen zwischen einzelnen Anweisungen innerhalb der aktuellen Transaktion geändert werden, was zu nicht wiederholbaren Lesevorgängen oder Phantomdaten führt. Diese Option ist die Standardeinstellung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Das Verhalten von READ COMMITTED hängt von der Einstellung der Datenbankoption READ_COMMITTED_SNAPSHOT ab:  
  
-   Wenn READ_COMMITTED_SNAPSHOT auf OFF (Standardeinstellung) festgelegt wird, verwendet [!INCLUDE[ssDE](../../includes/ssde-md.md)] freigegebene Sperren, um zu verhindern, dass andere Transaktionen Zeilen ändern, während die aktuelle Transaktion einen Lesevorgang ausführt. Durch freigegebene Sperren wird außerdem verhindert, dass die Anweisung Zeilen, die von anderen Transaktionen geändert werden, erst nach Abschluss der anderen Transaktion lesen kann. Mit dem Typ der gemeinsamen Sperre wird festgelegt, wann die Sperre aufgehoben wird. Zeilensperren werden aufgehoben, bevor die nächste Zeile verarbeitet wird. Seitensperren werden aufgehoben, wenn die nächste Seite gelesen wird, und Tabellensperren werden aufgehoben, nachdem die Ausführung der Anweisung beendet wurde.  
  
    > [!NOTE]  
    >  Wenn READ_COMMITTED_SNAPSHOT auf ON festgelegt wird, verwendet [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Zeilenversionsverwaltung, um jede Anweisung mit einer hinsichtlich der Transaktionen konsistenten Momentaufnahme der Daten so darzustellen, wie sie zu Beginn der Anweisung vorhanden waren. Es werden keine Sperren verwendet, um die Daten vor Updates durch andere Transaktionen zu schützen.  
    >   
    >  Die Momentaufnahmeisolation unterstützt FILESTREAM-Daten. Im Momentaufnahmeisolationsmodus entsprechen die von einer beliebigen Anweisung in einer Transaktion gelesenen FILESTREAM-Daten der im Hinblick auf Transaktionen konsistenten Version der Daten, die zu Beginn der Transaktion vorhanden waren.  
  
 Wenn die Datenbankoption READ_COMMITTED_SNAPSHOT auf ON festgelegt wird, können Sie mithilfe des READCOMMITTEDLOCK-Tabellenhinweises freigegebene Sperren anstelle der Zeilenversionsverwaltung für einzelne Anweisungen in Transaktionen anfordern, die auf der READ COMMITTED-Isolationsstufe ausgeführt werden.  
  
> [!NOTE]  
>  Wenn Sie die Option READ_COMMITTED_SNAPSHOT festlegen, wird in der Datenbank nur die Verbindung zugelassen, die den ALTER DATABASE-Befehl ausführt. So lange ALTER DATABASE nicht abgeschlossen ist, darf keine andere offene Verbindung in der Datenbank bestehen. Die Datenbank muss sich nicht im Einzelbenutzermodus befinden.  
  
 REPEATABLE READ  
 Gibt an, dass Anweisungen keine Daten lesen können, die geändert wurden, für die jedoch noch kein Commit von anderen Transaktionen ausgeführt wurde. Darüber hinaus können von der aktuellen Transaktion gelesene Daten erst nach Abschluss der aktuellen Transaktion von anderen Transaktionen geändert werden.  
  
 Freigegebene Sperren werden auf alle Daten angewendet, die von den Anweisungen in der Transaktion gelesen werden, und werden bis zum Abschluss der Transaktion aufrecht erhalten. Dadurch wird verhindert, dass andere Transaktionen Zeilen ändern, die von der aktuellen Transaktion gelesen wurden. Andere Transaktionen können neue Zeilen in Übereinstimmung mit den Suchbedingungen von Anweisungen einfügen, die von der aktuellen Transaktion ausgegeben wurden. Wenn die aktuelle Transaktion dann die Anweisung wiederholt, werden die neuen Zeilen abgerufen, was Phantomlesezugriffe zur Folge hat. Da freigegebene Sperren nicht am Ende jeder Anweisung aufgehoben werden, sondern bis zum Ende einer Transaktion aufrechterhalten werden, ist die Parallelität geringer als die der READ COMMITTED-Standardisolationsstufe. Verwenden Sie diese Option nur, wenn sie wirklich erforderlich ist.  
  
 SNAPSHOT  
 Gibt an, dass von Anweisungen in einer Transaktion gelesene Daten der im Hinblick auf Transaktionen konsistenten Version der Daten entsprechen, die zu Beginn der Transaktion vorhanden waren. Die Transaktion kann nur Datenänderungen erkennen, für die vor dem Beginn der Transaktion ein Commit ausgeführt wurde. Datenänderungen, die nach Beginn der aktuellen Transaktion von anderen Transaktionen vorgenommen wurden, sind für in der aktuellen Transaktion ausgeführte Anweisungen nicht sichtbar. So entsteht der Eindruck, als ob die Anweisungen in einer Transaktion eine Momentaufnahme der Daten erhalten, für die ein Commit ausgeführt wurde, wie sie zu Beginn der Transaktion vorhanden waren.  
  
 Außer bei der Wiederherstellung einer Datenbank fordern SNAPSHOT-Transaktionen beim Lesen von Daten keine Sperren an. SNAPSHOT-Transaktionen, die Daten lesen, halten andere Transaktionen nicht vom Schreiben von Daten ab. Transaktionen, die Daten schreiben, halten SNAPSHOT-Transaktionen nicht vom Lesen von Daten ab.  
  
 Während des Rollbacks einer Datenbankwiederherstellung fordern SNAPSHOT-Transaktionen eine Sperre an, wenn das Lesen von Daten versucht wird, die von einer anderen Transaktion gesperrt sind, für die gerade ein Rollback ausgeführt wird. Die SNAPSHOT-Transaktion bleibt so lange gesperrt, bis der Rollback der Transaktion ausgeführt ist. Die Sperre wird unmittelbar nach dem Erteilen aufgehoben.  
  
 Die Datenbankoption ALLOW_SNAPSHOT_ISOLATION muss auf ON festgelegt werden, bevor Sie eine Transaktion auf der SNAPSHOT-Isolationsstufe starten können. Greift eine Transaktion auf der SNAPSHOT-Isolationsstufe auf Daten in mehreren Datenbanken zu, muss ALLOW_SNAPSHOT_ISOLATION in jeder Datenbank auf ON festgelegt werden.  
  
 Die SNAPSHOT-Isolationsstufe kann nicht für Transaktionen festgelegt werden, die sich zu Beginn auf einer anderen Isolationsstufe befanden. Dies hat den Abbruch der Transaktion zur Folge. Wenn sich eine Transaktion zu Beginn auf der SNAPSHOT-Isolationsstufe befindet, ist der Wechsel zu einer anderen Isolationsstufe und dem anschließenden Wechsel zurück zu SNAPSHOT möglich. Eine Transaktion wird mit dem erstmaligen Zugriff auf Daten gestartet.  
  
 Eine Transaktion, die auf der SNAPSHOT-Isolationsstufe ausgeführt wird, kann Änderungen anzeigen, die von dieser Transaktion vorgenommen wurden. Führt die Transaktion beispielsweise eine UPDATE-Anweisung für eine Tabelle aus und gibt dann eine SELECT-Anweisung für dieselbe Tabelle aus, werden die geänderten Daten in das Resultset eingeschlossen.  
  
> [!NOTE]  
>  Im Momentaufnahmeisolationsmodus entsprechen die von einer beliebigen Anweisung in einer Transaktion gelesenen FILESTREAM-Daten der im Hinblick auf Transaktionen konsistenten Version der Daten, die zu Beginn der Transaktion und nicht zu Beginn der Anweisung vorhanden waren.  
  
 SERIALIZABLE  
 Gibt Folgendes an:  
  
-   Anweisungen können keine Daten lesen, die geändert wurden, für die jedoch noch kein Commit von anderen Transaktionen ausgeführt wurde.  
  
-   Andere Transaktionen können Daten, die von der aktuellen Transaktion gelesen werden, erst dann ändern, wenn die aktuelle Transaktion abgeschlossen ist.  
  
-   Andere Transaktionen können erst nach Abschluss der aktuellen Transaktion neue Zeilen mit Schlüsselwerten einfügen, die in den von Anweisungen in der aktuellen Transaktion gelesenen Schlüsselbereich fallen.  
  
 Bereichssperren werden in den Schlüsselwertbereichen eingerichtet, die die Suchbedingungen der in einer Transaktion ausgeführten Anweisungen erfüllen. Dadurch wird verhindert, dass andere Transaktionen Zeilen aktualisieren oder einfügen, die den von der aktuellen Transaktion ausgeführten Anweisungen entsprechen würden. Werden also Anweisungen in einer Transaktion ein zweites Mal ausgeführt, lesen diese dieselbe Zeilengruppe. Die Bereichssperren werden bis zum Abschluss der Transaktion aufrechterhalten. Diese Isolationsstufe ist am restriktivsten, da gesamte Schlüsselbereiche gesperrt werden, und die Sperren bis zum Abschluss der Transaktion aufrechterhalten werden. Da die Parallelität geringer ist, verwenden Sie diese Option nur, wenn es notwendig ist. Diese Option hat dieselbe Auswirkung wie das Festlegen von HOLDLOCK für die Tabellen in allen SELECT-Anweisungen in einer Transaktion.  
  
## <a name="remarks"></a>Remarks  
 Es können nicht mehrere Isolationsstufenoptionen gleichzeitig festgelegt werden; eine Option bleibt für die Dauer der Verbindung festgelegt, wenn sie nicht explizit geändert wird. Alle Lesevorgänge innerhalb der Transaktion unterliegen den Regeln der angegebenen Isolationsstufe, es sei denn, ein Tabellenhinweis in der FROM-Klausel einer Anweisung gibt ein anderes Sperr- oder Versionsverwaltungsverhalten für eine Tabelle an.  
  
 Die Transaktionsisolationsstufen definieren die Typen von Sperren, die für Lesevorgänge angefordert werden. Freigegebene Sperren für READ COMMITTED oder REPEATABLE READ sind im Allgemeinen Zeilensperren, die jedoch auf Seiten- oder Tabellensperren ausgeweitet werden können, wenn beim Lesevorgang auf viele Zeilen auf einer Seite oder in einer Tabelle verwiesen wird. Wenn eine Zeile nach dem Lesen durch die Transaktion geändert wird, fordert die Transaktion eine exklusive Sperre an, um diese Zeile zu schützen. Die exklusive Sperre wird bis zum Abschluss der Transaktion aufrechterhalten. Verfügt beispielsweise eine REPEATABLE READ-Transaktion über eine freigegebene Sperre für eine Zeile, und die Zeile wird dann durch die Transaktion geändert, wird die freigegebene Zeilensperre in eine exklusive Zeilensperre konvertiert.  
  
 Mit einer Ausnahme können Sie während einer Transaktion jederzeit von einer Isolationsstufe zu einer anderen wechseln. Die Ausnahme tritt auf, wenn von einer beliebigen Isolationsstufe zur SNAPSHOT-Isolation gewechselt wird. Dadurch erzeugt die Transaktion einen Fehler und führt ein Rollback aus. Sie können jedoch bei einer mit SNAPSHOT-Isolation gestarteten Transaktion zu einer beliebigen anderen Isolationsstufe wechseln.  
  
 Beim Wechsel der Isolationsstufe einer Transaktion werden Ressourcen, die nach dem Wechsel gelesen werden, gemäß den Regeln der neuen Isolationsstufe geschützt. Für Ressourcen, die vor dem Wechsel gelesen werden, gelten weiterhin die Regeln der bisherigen Isolationsstufe. Wenn eine Transaktion beispielsweise von READ COMMITTED nach SERIALIZABLE wechselt, werden die nach dem Wechsel angeforderten freigegebenen Sperren nun bis zum Ende der Transaktion aufrechterhalten.  
  
 Wenn Sie SET TRANSACTION ISOLATION LEVEL in einer gespeicherten Prozedur oder einem Trigger ausgeben, wird die Isolationsstufe auf die Stufe zurückgesetzt, die beim Aufrufen des Objekts Gültigkeit hatte, wenn das Objekt die Steuerung zurückgibt. Wenn Sie beispielsweise REPEATABLE READ in einem Batch festlegen und der Batch dann eine gespeicherte Prozedur aufruft, die die Isolationsstufe auf SERIALIZABLE festlegt, wird die Einstellung der Isolationsstufe auf REPEATABLE READ zurückgesetzt, wenn die gespeicherte Prozedur die Steuerung an den Batch zurückgibt.  
  
> [!NOTE]  
>  Benutzerdefinierte Funktionen und CLR-benutzerdefinierte Typen (Common Language Runtime) können SET TRANSACTION ISOLATION LEVEL nicht ausführen. Sie können die Isolationsstufe jedoch mithilfe eines Tabellenhinweises überschreiben. Weitere Informationen finden Sie unter [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Wird sp_bindsession zum Binden zweier Sitzungen verwendet, behält jede Sitzung die eigene Isolationsstufeneinstellung bei. Das Verwenden von SET TRANSACTION ISOLATION LEVEL zum Ändern der Isolationsstufeneinstellung einer Sitzung wirkt sich nicht auf die Einstellung anderer gebundener Sitzungen aus.  
  
 SET TRANSACTION ISOLATION LEVEL wird zur Ausführungszeit und nicht zur Analysezeit wirksam.  
  
 Durch optimierte Massenladevorgänge für Heaps werden Abfragen blockiert, die unter den folgenden Isolationsstufen ausgeführt werden:  
  
-   SNAPSHOT  
  
-   READ UNCOMMITTED  
  
-   READ COMMITTED mithilfe der Zeilenversionsverwaltung  
  
 Umgekehrt werden durch Abfragen, die unter diesen Isolationsstufen ausgeführt werden, optimierte Massenladevorgänge für Heaps blockiert. Weitere Informationen zu Massenladevorgängen finden Sie unter [Massenimport und -export von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
 FILESTREAM-aktivierte Datenbanken unterstützen die folgenden Transaktionsisolationsstufen.  
  
|Isolationsstufe|Transact-SQL-Zugriff|Dateisystemzugriff|  
|---------------------|-------------------------|------------------------|  
|Read Uncommitted|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|Nicht unterstützt|  
|Read Committed|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|Repeatable Read|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|Nicht unterstützt|  
|Serializable|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|Nicht unterstützt|  
|Read committed snapshot|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|Momentaufnahme|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `TRANSACTION ISOLATION LEVEL` für die Sitzung festgelegt. Für alle folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen erhält [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle freigegebenen Sperren bis zum Abschluss der Transaktion aufrecht.  
  
```  
USE AdventureWorks2012;  
GO  
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;  
GO  
BEGIN TRANSACTION;  
GO  
SELECT *   
    FROM HumanResources.EmployeePayHistory;  
GO  
SELECT *   
    FROM HumanResources.Department;  
GO  
COMMIT TRANSACTION;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [DBCC USEROPTIONS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
