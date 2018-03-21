---
title: "Atomic-Blöcke | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 40e0e749-260c-4cfc-a848-444d30c09d85
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f70a9c85cf6a4341f6c92674a046bff11c7a077a
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/19/2018
---
# <a name="atomic-blocks-in-native-procedures"></a>ATOMIC-Blöcke in nativen Prozeduren
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  **BEGIN ATOMIC** ist Teil des ANSI SQL-Standards. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt ATOMIC-Blöcke auf der obersten Ebene der nativ kompilierten gespeicherten Prozeduren sowie für nativ kompilierte, skalare benutzerdefinierte Funktionen. Weitere Informationen zu diesen Funktionen finden Sie unter [Benutzerdefinierte Skalarfunktionen für In-Memory-OLTP](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
-   Jede systemintern kompilierte gespeicherte Prozedur enthält genau einen Block mit [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen. Dies ist ein ATOMIC-Block.  
  
-   Nicht systemeigene interpretierte gespeicherte [!INCLUDE[tsql](../../includes/tsql-md.md)] -Prozeduren und Ad-hoc-Batches unterstützen keine ATOMIC-Blöcke.  
  
 ATOMIC-Blöcke werden (unteilbar) innerhalb der Transaktion ausgeführt. Entweder werden alle Anweisungen im Block erfolgreich ausgeführt, oder für den gesamten Block wird ein Rollback zu dem Sicherungspunkt ausgeführt, der beim Starten des Blocks erstellt wurde. Darüber hinaus sind die Sitzungseinstellungen für den ATOMIC-Block fest definiert. Wird derselbe ATOMIC-Block in Sitzungen mit unterschiedlichen Einstellungen ausgeführt, ergibt sich unabhängig von den Einstellungen der aktuellen Sitzung dasselbe Verhalten.  
  
## <a name="transactions-and-error-handling"></a>Transaktionen und Fehlerbehandlung  
 Wenn in einer Sitzung bereits eine Transaktion vorhanden ist (da von einem Batch eine **BEGIN TRANSACTION** -Anweisung ausgeführt wurde und die Transaktion aktiv bleibt), wird durch das Starten eines ATOMIC-Blocks in der Transaktion ein Sicherungspunkt erstellt. Wenn der Block ohne Ausnahme beendet wird, wird der erstellte Sicherungspunkt für den Block festgeschrieben. Für die Transaktion wird jedoch erst ein Commit ausgeführt, wenn für die Transaktion auf Sitzungsebene ein Commit erfolgt. Wenn der Block eine Ausnahme auslöst, wird für den ausgeführten Teil des Blocks ein Rollback ausgeführt, die Transaktion auf Sitzungsebene wird jedoch weiterhin ausgeführt, sofern die Ausnahme nicht zum Fehlschlagen der Transaktion führt. Beispielsweise kann ein Schreibkonflikt zum Fehlschlagen einer Transaktion führen, ein Typumwandlungsfehler jedoch nicht.  
  
 Wenn eine Sitzung keine aktive Transaktion enthält, wird durch **BEGIN ATOMIC** eine neue Transaktion gestartet. Wenn außerhalb des Blockbereichs keine Ausnahme ausgelöst wird, wird für die Transaktion am Ende des Blocks ein Commit ausgeführt. Wenn der Block eine Ausnahme auslöst (d. h., die Ausnahme wird nicht innerhalb des Blocks abgefangen und behandelt), wird ein Rollback für die Transaktion ausgeführt. Bei Transaktionen, die einen einzelnen ATOMIC-Block (eine einzelne nativ kompilierte gespeicherte Prozedur) umfassen, ist es nicht notwendig, explizite **BEGIN TRANSACTION** und **COMMIT** oder **ROLLBACK** -Anweisungen zu schreiben.  
  
 Systemintern kompilierte gespeicherte Prozeduren unterstützen **TRY**-, **CATCH**- und **THROW** -Konstrukte zur Fehlerbehandlung. **RAISERROR** wird nicht unterstützt.  
  
 Das folgende Beispiel veranschaulicht das Fehlerbehandlungsverhalten bei ATOMIC-Blöcken und systemintern kompilierten gespeicherten Prozeduren:  
  
```sql  
-- sample table  
CREATE TABLE dbo.t1 (  
  c1 int not null primary key nonclustered  
)  
WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- sample proc that inserts 2 rows  
CREATE PROCEDURE dbo.usp_t1 @v1 bigint not null, @v2 bigint not null  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS  
BEGIN ATOMIC  
WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english', DELAYED_DURABILITY = ON)  
  
  INSERT dbo.t1 VALUES (@v1)  
  INSERT dbo.t1 VALUES (@v2)  
  
END  
GO  
  
-- insert two rows  
EXEC dbo.usp_t1 1, 2  
GO  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify the rows 1 and 2 were committed  
SELECT c1 FROM dbo.t1  
GO  
  
-- execute proc with arithmetic overflow  
EXEC dbo.usp_t1 3, 4444444444444  
GO  
-- expected error message:  
-- Msg 8115, Level 16, State 0, Procedure usp_t1  
-- Arithmetic overflow error converting bigint to data type int.  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify rows 3 was not committed; usp_t1 has been rolled back  
SELECT c1 FROM dbo.t1  
GO  
  
-- start a new transaction  
BEGIN TRANSACTION  
  -- insert rows 3 and 4  
  EXEC dbo.usp_t1 3, 4  
  
  -- verify there is still an active transaction  
  SELECT @@TRANCOUNT  
  
  -- verify the rows 3 and 4 were inserted  
  SELECT c1 FROM dbo.t1 WITH (SNAPSHOT)   
  ORDER BY c1  
  
  -- catch the arithmetic overflow error  
  BEGIN TRY  
    EXEC dbo.usp_t1 5, 4444444444444  
  END TRY  
  BEGIN CATCH  
    PRINT N'Error occurred: ' + error_message()  
  END CATCH  
  
  -- verify there is still an active transaction  
  SELECT @@TRANCOUNT  
  
  -- verify rows 3 and 4 are still in the table, and row 5 has not been inserted  
  SELECT c1 FROM dbo.t1 WITH (SNAPSHOT)   
  ORDER BY c1  
  
COMMIT  
GO  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify rows 3 and 4 has been committed  
SELECT c1 FROM dbo.t1  
ORDER BY c1  
GO  
```  
  
 Bei folgenden, für speicheroptimierte Tabellen spezifischen Fehlern schlägt eine Transaktion fehl. Wenn sie im Bereich eines ATOMIC-Blocks auftreten, wird die Transaktion abgebrochen: 10772, 41301, 41302, 41305, 41325, 41332, 41333, und 41839.  
  
## <a name="session-settings"></a>Sitzungseinstellungen  
 Die Sitzungseinstellungen in ATOMIC-Blöcken werden bei der Kompilierung der gespeicherte Prozedur fest definiert. Einige Einstellungen können mit **BEGIN ATOMIC** angegeben werden, während andere immer denselben festen Wert aufweisen.  
  
 Die folgenden Optionen sind für **BEGIN ATOMIC**erforderlich:  
  
|Erforderliche Einstellung|Description|  
|----------------------|-----------------|  
|**TRANSACTION ISOLATION LEVEL**|Unterstützte Werte sind **SNAPSHOT**, **REPEATABLEREAD**und **SERIALIZABLE**.|  
|**LANGUAGE**|Bestimmt Datums- und Uhrzeitformate sowie Systemmeldungen. Alle Sprachen und Aliase in [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) werden unterstützt.|  
  
 Die folgenden Einstellungen sind optional:  
  
|Optionale Einstellung|Description|  
|----------------------|-----------------|  
|**DATEFORMAT**|Alle Datumsformate von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden unterstützt. Falls angegeben, überschreibt **DATEFORMAT** das Standarddatumsformat, das **LANGUAGE**zugeordnet ist.|  
|**DATEFIRST**|Falls angegeben, überschreibt **DATEFIRST** den Standardwert, der **LANGUAGE**zugeordnet ist.|  
|**DELAYED_DURABILITY**|Unterstützte Werte sind **OFF** und **ON**.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Transaktionscommits können entweder vollständig dauerhaft (Standardeinstellung) oder verzögert dauerhaft sein. Weitere Informationen finden Sie unter [Steuern der Transaktionsdauerhaftigkeit](../../relational-databases/logs/control-transaction-durability.md).|  
  
 Die folgenden SET-Optionen verfügen für alle ATOMIC-Blöcke in allen systemintern kompilierten gespeicherten Prozeduren über denselben Systemstandardwert:  
  
|SET-Option|Systemstandard für ATOMIC-Blöcke|  
|----------------|--------------------------------------|  
|ANSI_NULLS|ON|  
|ANSI_PADDING|ON|  
|ANSI_WARNING|ON|  
|ARITHABORT|ON|  
|ARITHIGNORE|OFF|  
|CONCAT_NULL_YIELDS_NULL|ON|  
|IDENTITY_INSERT|OFF|  
|NOCOUNT|ON|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|ON|  
|ROWCOUNT|0|  
|TEXTSIZE|0|  
|XACT_ABORT|OFF<br /><br /> Nicht abgefangene Ausnahmen bewirken ein Rollback für den ATOMIC-Block, führen jedoch nicht zu einem Abbruch der Transaktion, solange die Transaktion durch den Fehler nicht fehlschlägt.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Systemintern kompilierte gespeicherte Prozeduren](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
