---
title: DBCC OPENTRAN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_OPENTRAN_TSQL
- DBCC OPENTRAN
- OPENTRAN_TSQL
- OPENTRAN
dev_langs: TSQL
helpviewer_keywords:
- status information [SQL Server], transactions
- transactions [SQL Server], status information
- DBCC OPENTRAN statement
- open transactions
- displaying transaction information
- checking open transactions
- oldest transactions [SQL Server]
ms.assetid: 63163843-226f-42d3-9e2c-b634fbf06943
caps.latest.revision: "40"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 6a0d7dba4272f39dcbd23c9f0f2aed6706b745f6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="dbcc-opentran-transact-sql"></a>DBCC OPENTRAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Mithilfe von DBCC OPENTRAN können aktive Transaktionen identifiziert werden, die die Protokollkürzung möglicherweise verhindern. DBCC OPENTRAN zeigt Informationen zur ältesten aktiven Transaktion sowie zu den ältesten verteilten und nicht verteilten replizierten Transaktionen (sofern vorhanden) im Transaktionsprotokoll der angegebenen Datenbank an. Ergebnisse werden nur angezeigt, wenn im Protokoll eine aktive Transaktion vorhanden ist oder die Datenbank Replikationsinformationen enthält. Wenn keine aktiven Transaktionen im Protokoll enthalten sind, wird eine Informationsmeldung angezeigt.
  
> [!NOTE]  
>  DBCC OPENTRAN wird ausschließlich für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger unterstützt.  
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC OPENTRAN   
[   
    ( [ database_name | database_id | 0 ] ) ]  
    { [ WITH TABLERESULTS ]  
      [ , [ NO_INFOMSGS ] ]  
    }  
]   
```  
  
## <a name="arguments"></a>Argumente  
 *Database_name* | *Database_id*| 0  
 Der Name oder die ID der Datenbank, für die Informationen zur ältesten Transaktion angezeigt werden sollen. Erfolgt keine Eingabe, oder wird 0 angegeben, wird die aktuelle Datenbank verwendet. Datenbanknamen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 TABLERESULTS  
 Gibt die Ergebnisse, die in eine Tabelle geladen werden können, im Tabellenformat an. Verwenden Sie diese Option, um eine Tabelle mit Ergebniswerten zu erhalten, die zum Durchführen von Vergleichen in eine Tabelle eingefügt werden können. Wenn diese Option nicht angegeben ist, werden die Ergebnisse zwecks besserer Lesbarkeit formatiert.  
  
 NO_INFOMSGS  
 Alle Informationsmeldungen werden unterdrückt.  
  
## <a name="remarks"></a>Hinweise  
Verwenden Sie DBCC OPENTRAN, um zu ermitteln, ob eine offene Transaktion innerhalb des Transaktionsprotokolls vorhanden ist. Wenn Sie die BACKUP LOG-Anweisung verwenden, kann nur der inaktive Teil des Protokolls abgeschnitten werden. Eine offene Transaktion kann verhindern, dass das Protokoll vollständig abgeschnitten wird. Zum Identifizieren einer geöffneten Transaktion können Sie mit sp_who die Systemprozess-ID abrufen.
  
## <a name="result-sets"></a>Resultsets  
DBCC OPENTRAN gibt folgendes Resultset zurück, wenn keine offenen Transaktionen vorhanden sind:
  
```sql
No active open transactions.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** oder der festen Datenbankrolle **db_owner** .
  
## <a name="examples"></a>Beispiele  
### <a name="a-returning-the-oldest-active-transaction"></a>A. Zurückgeben der ältesten aktiven Transaktion  
Im folgenden Beispiel werden Transaktionsinformationen für die aktuelle Datenbank abgerufen. Die Ergebnisse können variieren.
  
```sql  
CREATE TABLE T1(Col1 int, Col2 char(3));  
GO  
BEGIN TRAN  
INSERT INTO T1 VALUES (101, 'abc');  
GO  
DBCC OPENTRAN;  
ROLLBACK TRAN;  
GO  
DROP TABLE T1;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Transaction information for database 'master'.
Oldest active transaction:
SPID (server process ID) : 52
UID (user ID) : -1
Name          : user_transaction
LSN           : (518:1576:1)
Start time    : Jun  1 2004  3:30:07:197PM
SID           : 0x010500000000000515000000a065cf7e784b9b5fe77c87709e611500
DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```
  
> [!NOTE]  
>  Das "UID (user ID)"-Ergebnis ist bedeutungslos und wird in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt.  
  
### <a name="b-specifying-the-with-tableresults-option"></a>B. Angeben der WITH TABLERESULTS-Option  
Im folgenden Beispiel werden die Ergebnisse des DBCC OPENTRAN-Befehls in eine temporäre Tabelle geladen.
  
```sql  
-- Create the temporary table to accept the results.  
CREATE TABLE #OpenTranStatus (  
   ActiveTransaction varchar(25),  
   Details sql_variant   
   );  
-- Execute the command, putting the results in the table.  
INSERT INTO #OpenTranStatus   
   EXEC ('DBCC OPENTRAN WITH TABLERESULTS, NO_INFOMSGS');  
  
-- Display the results.  
SELECT * FROM #OpenTranStatus;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
[BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)  
[COMMIT der Transaktion &#40; Transact-SQL &#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Db_id &#40; Transact-SQL &#41;](../../t-sql/functions/db-id-transact-sql.md)  
[ROLLBACK TRANSACTION &#40; Transact-SQL &#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)
  
  
