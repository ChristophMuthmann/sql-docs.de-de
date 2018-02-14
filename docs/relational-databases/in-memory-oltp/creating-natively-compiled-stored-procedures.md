---
title: Erstellen systemintern kompilierter gespeicherter Prozeduren | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
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
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 108baf378ee99256bef1f3dd11aead8dac68307b
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="creating-natively-compiled-stored-procedures"></a>Erstellen systemintern kompilierter gespeicherter Prozeduren
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Von systemintern kompilierten gespeicherten Prozeduren wird nicht die vollständige [!INCLUDE[tsql](../../includes/tsql-md.md)] -Programmier- und -Abfrageoberfläche implementiert. Es gibt bestimmte [!INCLUDE[tsql](../../includes/tsql-md.md)] -Konstrukte, die innerhalb systemintern kompilierter gespeicherter Prozeduren nicht verwendet werden können. Weitere Informationen finden Sie unter [Unterstützte Funktionen für nativ kompilierte T-SQL-Module](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
 Allerdings gibt es auch mehrere [!INCLUDE[tsql](../../includes/tsql-md.md)] -Funktionen, die nur für systemintern kompilierte gespeicherte Prozeduren unterstützt werden:  
  
-   ATOMIC-Blöcke. Weitere Informationen finden Sie unter [ATOMIC-Blöcke](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).  
  
-   **NOT NULL**-Einschränkungen für Parameter und Variablen. Sie können als **NOT NULL** deklarierten Parametern oder Variablen keine **NULL**-Werte zuweisen. Weitere Informationen finden Sie unter [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).  
  
    -   CREATE PROCEDURE dbo.myproc (@myVarchar  varchar(32)  **nicht NULL**) ...  
  
    -   DECLARE @myVarchar  varchar(32)  **nicht NULL = "Hello"**; -- *(Muss mit einem Wert initialisiert werden.)*  
  
    -   SET @myVarchar **= null**; -- *(Wird kompiliert, schlägt jedoch während der Laufzeit fehl.)*  
  
-   Schemabindung von systemintern kompilierten gespeicherten Prozeduren.  
  
 Systemintern kompilierte gespeicherte Prozeduren werden mithilfe von [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md) erstellt. Das folgende Beispiel zeigt eine speicheroptimierte Tabelle und eine systemintern kompilierte gespeicherte Prozedur, die zum Einfügen von Zeilen in die Tabelle verwendet wird.  
  
```sql  
create table dbo.Ord  
(OrdNo integer not null primary key nonclustered,   
 OrdDate datetime not null,   
 CustCode nvarchar(5) not null)   
 with (memory_optimized=on)  
go  
  
create procedure dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
with native_compilation, schemabinding  
as   
begin atomic with  
(transaction isolation level = snapshot,  
language = N'English')  
  
  declare @OrdDate datetime = getdate();  
  insert into dbo.Ord (OrdNo, CustCode, OrdDate) values (@OrdNo, @CustCode, @OrdDate);  
end  
go  
```  
  
 Im Codebeispiel ist an **NATIVE_COMPILATION** erkennbar, dass diese gespeicherte [!INCLUDE[tsql](../../includes/tsql-md.md)] -Prozedur eine systemintern kompilierte gespeicherte Prozedur ist. Die folgenden Optionen sind erforderlich:  
  
|Option|Description|  
|------------|-----------------|  
|**SCHEMABINDING**|Eine systemintern kompilierte gespeicherte Prozedur muss an das Schema der Objekte gebunden werden, auf die sie verweist. Dies bedeutet, dass Tabellen, auf die von der Prozedur verwiesen wird, nicht gelöscht werden können. Die Tabellen, auf die in der Prozedur verwiesen wird, müssen den Schemanamen enthalten, und Platzhalterzeichen (\*) sind in Abfragen nicht zulässig (also ohne `SELECT * from...`). **SCHEMABINDING** wird nur in dieser Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]für systemintern kompilierte gespeicherte Prozeduren unterstützt.|  
|**BEGIN ATOMIC**|Der Text einer systemintern kompilierten gespeicherten Prozedur muss genau ein ATOMIC-Block sein. ATOMIC-Blöcke gewährleisten die unteilbare Ausführung der gespeicherten Prozedur. Wenn die Prozedur außerhalb des Kontexts einer aktiven Transaktion aufgerufen wird, wird eine neue Transaktion gestartet, für die am Ende des ATOMIC-Blocks ein Commit ausgeführt wird. ATOMIC-Blöcke in systemintern kompilierten gespeicherten Prozeduren weisen zwei erforderliche Optionen auf:<br /><br /> **TRANSACTION ISOLATION LEVEL**. Informationen zu unterstützten Isolationsstufen finden Sie unter [Transaktionsisolationsstufen für speicheroptimierte Tabellen](http://msdn.microsoft.com/library/8a6a82bf-273c-40ab-a101-46bd3615db8a) .<br /><br /> **LANGUAGE**. Die Sprache der gespeicherten Prozedur muss auf eine der verfügbaren Sprachen bzw. einen der verfügbaren Sprachenaliase festgelegt werden.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Systemintern kompilierte gespeicherte Prozeduren](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
