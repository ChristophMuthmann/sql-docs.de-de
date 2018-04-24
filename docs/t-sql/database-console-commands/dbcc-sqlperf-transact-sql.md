---
title: DBCC SQLPERF (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|database-console-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SQLPERF
- DBCC_SQLPERF_TSQL
- SQLPERF_TSQL
- DBCC SQLPERF
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], transaction logs
- transaction logs [SQL Server], space usage
- space [SQL Server], transaction logs
- DBCC SQLPERF statement
ms.assetid: ec9225ce-e20f-4b03-8b3a-7bcad8a649df
caps.latest.revision: 43
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: bf29b53e16a0ebb90b7fc18f2a5d2eb745a7bc33
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dbcc-sqlperf-transact-sql"></a>DBCC SQLPERF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Stellt Statistiken bezüglich der Nutzung von Speicherplatz für das Transaktionsprotokoll in allen Datenbanken bereit. Der Befehl kann in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auch zum Zurücksetzen von Wartezeiten- und Latchstatistiken verwendet werden.
  
**Gilt für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([Vorschauversion in einigen Regionen](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```
DBCC SQLPERF   
(  
     [ LOGSPACE ]  
     | [ "sys.dm_os_latch_stats" , CLEAR ]  
     | [ "sys.dm_os_wait_stats" , CLEAR ]  
)   
     [WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumente  
LOGSPACE  
Gibt die aktuelle Größe des Transaktionsprotokolls und den für jede Datenbank genutzten Protokollspeicher in Prozent an. Anhand dieser Informationen können Sie den in einem Transaktionsprotokoll genutzten Speicherplatz überwachen.

> [!IMPORTANT]
> Weitere Informationen zu den Informationen zur Speicherplatznutzung für das Transaktionsprotokoll in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] finden Sie im Abschnitt [Hinweise](#Remarks) in diesem Thema.
  
**"sys.dm_os_latch_stats"**, CLEAR  
Setzt die Statistik für Latches zurück. Weitere Informationen finden Sie unter [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md). Diese Option steht in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]nicht zur Verfügung.  
  
**"sys.dm_os_wait_stats"**, CLEAR  
Setzt die Wartestatistik zurück. Weitere Informationen finden Sie unter [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). Diese Option steht in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]nicht zur Verfügung.  
  
WITH NO_INFOMSGS  
Unterdrückt alle Informationsmeldungen mit einem Schweregrad von 0 bis 10.  
  
## <a name="result-sets"></a>Resultsets  
 In der folgenden Tabelle werden die Spalten des Resultsets beschrieben:  
  
|Spaltenname|Definition|  
|---|---|
|**Database Name**|Der Name der Datenbank, für die die Protokollstatistiken angezeigt werden.|  
|**Protokollgröße (MB)**|Dem Protokoll aktuell zugeordnete Größe. Es steht weniger Speicherplatz zur Verfügung, als dem Protokollspeicher ursprünglich zugeordnet wurde, da [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen kleinen Bereich an Datenträgerspeicher für interne Headerinformationen reserviert.|  
|**Verwendeter Protokollspeicherplatz (%)**|Prozentsatz der Protokolldatei, in dem zurzeit Informationen zur Transaktionsprotokollen gespeichert ist.|  
|**Status**|Status der Protokolldatei. Immer 0.|  
  
## <a name="Remarks"></a> Hinweise  
Nutzen Sie ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] die [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)-DMV statt `DBCC SQLPERF(LOGSPACE)`, um Informationen zur Speicherplatzverwendung für das Transaktionsprotokoll pro Datenbank zurückzugeben.    
 
Im Transaktionsprotokoll wird jede in der Datenbank vorgenommene Transaktion aufgezeichnet. Weitere Informationen finden Sie unter [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md) und im [Handbuch zur Architektur und Verwaltung von Transaktionsprotokollen in SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).
  
## <a name="permissions"></a>Berechtigungen  
Um in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `DBCC SQLPERF(LOGSPACE)` auszuführen, ist die `VIEW SERVER STATE`-Berechtigung auf dem Server erforderlich. Wenn Sie Warte- und Latchstatistiken zurücksetzen möchten, ist die `ALTER SERVER STATE`-Berechtigung auf dem Server erforderlich.
  
In [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Premium-Tarifen und unternehmenskritischen Tarifen ist die `VIEW DATABASE STATE`-Berechtigung für die Datenbank erforderlich. Für die [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Tarife Standard, Basic und Universell ist das [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Administratorkonto erforderlich. Das Zurücksetzen der Warte- und Latchstatistiken wird nicht unterstützt.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-displaying-log-space-information-for-all-databases"></a>A. Anzeigen von Informationen zum Protokollspeicherplatz für alle Datenbanken  
Im folgenden Beispiel werden `LOGSPACE`-Informationen für alle in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]enthaltenen Datenbanken angezeigt.
  
```sql  
DBCC SQLPERF(LOGSPACE);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Database Name Log Size (MB) Log Space Used (%) Status        
------------- ------------- ------------------ -----------   
master         3.99219      14.3469            0   
tempdb         1.99219      1.64216            0   
model          1.0          12.7953            0   
msdb           3.99219      17.0132            0   
AdventureWorks 19.554688    17.748701          0  
```  
  
### <a name="b-resetting-wait-statistics"></a>B. Zurücksetzen der Wartestatistik  
Im folgenden Beispiel wird die Wartestatistik für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurückgesetzt.
  
```sql  
DBCC SQLPERF("sys.dm_os_wait_stats",CLEAR);  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
[sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)    
[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
[sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)    
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)     
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)     

