---
title: DBCC SQLPERF (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/07/2018
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
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: cd615cd56860138d2e9afa7e2d7090ed27ba8e3a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-sqlperf-transact-sql"></a>DBCC SQLPERF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Stellt Statistiken bezüglich der Nutzung von Speicherplatz für das Transaktionsprotokoll in allen Datenbanken bereit. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann auch zum Zurücksetzen von Wartezeiten-und latchstatistiken verwendet werden.
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([Vorschau in einigen Regionen](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))
  
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
Gibt die aktuelle Größe des Transaktionsprotokolls und den für jede Datenbank genutzten Protokollspeicher in Prozent an. Verwenden Sie diese Informationen, die in einem Transaktionsprotokoll genutzten Speicherplatz überwachen.

> [!IMPORTANT]
> Weitere Informationen zu den Informationen zur Speicherplatzverwendung für das Transaktionsprotokoll ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], finden Sie in der ["Hinweise"](#Remarks) Abschnitt dieses Themas.
  
**"sys.dm_os_latch_stats"**, CLEAR  
Setzt die Statistik für Latches zurück. Weitere Informationen finden Sie unter [dm_os_latch_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md). Diese Option steht in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]nicht zur Verfügung.  
  
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
|**Protokollspeicherplatz verwendet (%)**|Prozentsatz der Protokolldatei aktuell in Verwendung zum Speichern von Informationen zu Transaktionsprotokollen.|  
|**Status**|Status der Protokolldatei. Immer 0.|  
  
## <a name="Remarks"></a> Hinweise  
Beginnend mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], verwenden Sie die [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md) DMV anstelle von `DBCC SQLPERF(LOGSPACE)`, um Informationen zur Speicherplatzverwendung für das Transaktionsprotokoll pro Datenbank zurückzugeben.    
 
Im Transaktionsprotokoll wird jede in der Datenbank vorgenommene Transaktion aufgezeichnet. Weitere Informationen finden Sie unter [das Transaktionsprotokoll &#40; SQLServer &#41; ](../../relational-databases/logs/the-transaction-log-sql-server.md) und [Transaktionsprotokollarchitektur für SQL Server- und-managementhandbuch](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auszuführende `DBCC SQLPERF(LOGSPACE)` erfordert `VIEW SERVER STATE` Berechtigung auf dem Server. Zurücksetzen der Warte-und latchstatistiken erfordert `ALTER SERVER STATE` Berechtigung auf dem Server.
  
Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Administratorkonto ein. Das Zurücksetzen der Warte- und Latchstatistiken wird nicht unterstützt.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-displaying-log-space-information-for-all-databases"></a>A. Anzeigen von Informationen zum Protokollspeicherplatz für alle Datenbanken  
Das folgende Beispiel zeigt `LOGSPACE` Informationen für alle Datenbanken in der Instanz enthaltenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
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
Das folgende Beispiel setzt die wartestatistik für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
```sql  
DBCC SQLPERF("sys.dm_os_wait_stats",CLEAR);  
```  
  
## <a name="see-also"></a>Siehe auch  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
[sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)    
[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
[sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)    
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)     
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)     

