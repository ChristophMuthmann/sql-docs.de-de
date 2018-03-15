---
title: DBCC INPUTBUFFER (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC INPUTBUFFER
- INPUTBUFFER
- DBCC_INPUTBUFFER_TSQL
- INPUTBUFFER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- input buffers [SQL Server]
- last statement from client
- displaying last statement sent
- statements [SQL Server], last statement
- DBCC INPUTBUFFER statement
ms.assetid: a44d702b-b3fb-4950-8c8f-1adcf3f514ba
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0d36f0e25c0f5959053e028cdfc95babf69c4e48
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-inputbuffer-transact-sql"></a>DBCC INPUTBUFFER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Zeigt die letzte Anweisung an, die von einem Client an eine Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gesendet wurde.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC INPUTBUFFER ( session_id [ , request_id ])  
[WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumente  
*session_id*  
Die Sitzungs-ID, die jeweils einer aktiven primären Verbindung zugeordnet ist.  
  
*request_id*  
Die genaue Anforderung (Batch), nach der in der aktuellen Sitzung gesucht werden soll.  

Die folgende Abfrage gibt *request_id*zurück:  
```sql
SELECT request_id   
FROM sys.dm_exec_requests   
WHERE session_id = @@spid;  
```  
mit  
Aktiviert anzugebende Optionen.  
  
NO_INFOMSGS  
Unterdrückt alle Informationsmeldungen mit einem Schweregrad von 0 bis 10.  
  
## <a name="result-sets"></a>Resultsets  
DBCC INPUTBUFFER gibt ein Rowset mit folgenden Spalten zurück.
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**EventType**|**nvarchar(30)**|Der Ereignistyp. Dies kann **RPC Event** oder **Language Event**sein. Wurde kein letztes Ereignis erkannt, wird **No Event** ausgegeben.|  
|**Parameter**|**smallint**|0 = Text<br /><br /> 1- *n* = Parameter|  
|**EventInfo**|**nvarchar(4000)**|Wenn **EventType** gleich RPC, enthält **EventInfo** nur den Namen der Prozedur. Wenn **EventType** gleich Language, werden nur die ersten 4000 Zeichen des Ereignisses angezeigt.|  
  
Beispielsweise gibt DBCC INPUTBUFFER das folgende Resultset zurück, wenn das letzte Ereignis im Puffer DBCC INPUTBUFFER(11) war:
  
```
EventType      Parameters EventInfo               
-------------- ---------- ---------------------   
Language Event 0          DBCC INPUTBUFFER (11)  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  

> [!NOTE]
> Verwenden Sie ab [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 [sys.dm_exec_input_buffer](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md), um Informationen zu Anweisungen zurückzugeben, die an eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gesendet werden.

## <a name="permissions"></a>Berechtigungen  
Bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss eine der folgenden Bedingungen erfüllt sein:
-   Der Benutzer muss ein Mitglied der festen Serverrolle **sysadmin** sein.  
-   Der Benutzer muss über die VIEW SERVER STATE-Berechtigung verfügen.  
-   *session_id* muss mit der ID der Sitzung identisch sein, in der der Befehl ausgeführt wird. Führen Sie die folgende Abfrage aus, um die Sitzungs-ID zu bestimmen:  
  
```sql
SELECT @@spid;  
```
  
Für [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Premium-Tarife ist die VIEW DATABASE STATE-Berechtigung in der Datenbank erforderlich. Für die [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Tarife Standard und Basic ist das [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Administratorkonto erforderlich.
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird `DBCC INPUTBUFFER` auf einer zweiten Verbindung ausgeführt, während eine vorherige Verbindung durch die Ausführung einer langwierigen Transaktion beansprucht wird.
  
```sql
CREATE TABLE dbo.T1 (Col1 int, Col2 char(3));  
GO  
DECLARE @i int = 0;  
BEGIN TRAN  
SET @i = 0;  
WHILE (@i < 100000)  
BEGIN  
INSERT INTO dbo.T1 VALUES (@i, CAST(@i AS char(3)));  
SET @i += 1;  
END;  
COMMIT TRAN;  
--Start new connection #2.  
DBCC INPUTBUFFER (52);  
```  

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
[sys.dm_exec_input_buffer &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md)
  
  
