---
title: DBCC SQLPERF (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
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
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 41f854ce5ff1261829df621931d3a736426f32c8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-sqlperf-transact-sql"></a>DBCC SQLPERF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Stellt Statistiken bezüglich der Nutzung von Speicherplatz für das Transaktionsprotokoll in allen Datenbanken bereit. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann auch zum Zurücksetzen von Wartezeiten-und latchstatistiken verwendet werden.
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([Vorschau in einigen Regionen](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC SQLPERF   
(  
     [ LOGSPACE ]  
     |  
          [ "sys.dm_os_latch_stats" , CLEAR ]  
     |  
     [ "sys.dm_os_wait_stats" , CLEAR ]  
)   
     [WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumente  
LOGSPACE  
Gibt die aktuelle Größe des Transaktionsprotokolls und den für jede Datenbank genutzten Protokollspeicher in Prozent an. Anhand dieser Informationen können Sie den in einem Transaktionsprotokoll genutzten Speicherplatz überwachen.  
  
**"** **sys.dm_os_latch_stats" ,** CLEAR  
Setzt die Statistik für Latches zurück. Weitere Informationen finden Sie unter [dm_os_latch_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md). Diese Option steht in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]nicht zur Verfügung.  
  
**"sys.dm_os_wait_stats" ,** CLEAR  
Setzt die Wartestatistik zurück. Weitere Informationen finden Sie unter [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). Diese Option steht in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]nicht zur Verfügung.  
  
WITH NO_INFOMSGS  
Unterdrückt alle Informationsmeldungen mit einem Schweregrad von 0 bis 10.  
  
## <a name="result-sets"></a>Resultsets  
 In der folgenden Tabelle werden die Spalten des Resultsets beschrieben:  
  
|Spaltenname|Definition|  
|---|---|
|**Datenbankname**|Der Name der Datenbank, für die die Protokollstatistiken angezeigt werden.|  
|**Protokollgröße (MB)**|Dem Protokoll aktuell zugeordnete Größe. Es steht weniger Speicherplatz zur Verfügung, als dem Protokollspeicher ursprünglich zugeordnet wurde, da [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen kleinen Bereich an Datenträgerspeicher für interne Headerinformationen reserviert.|  
|**Protokollspeicherplatz verwendet (%)**|Prozentsatz der Protokolldatei aktuell in Verwendung zum Speichern von Informationen zu Transaktionsprotokollen.|  
|**Status**|Status der Protokolldatei. Immer 0.|  
  
## <a name="remarks"></a>Hinweise  
Im Transaktionsprotokoll wird jede in der Datenbank vorgenommene Transaktion aufgezeichnet. Weitere Informationen finden Sie unter [das Transaktionsprotokoll &#40; SQLServer &#41; ](../../relational-databases/logs/the-transaction-log-sql-server.md).
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Ausführen von DBCC SQLPERF(LOGSPACE) erfordert VIEW SERVER STATE-Berechtigung auf dem Server. Zum Zurücksetzen der Warte- und Latchstatistiken ist die ALTER SERVER STATE-Berechtigung auf dem Server erforderlich.
  
Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] benötigen Premium-Ebenen die VIEW DATABASE STATE-Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Administratorkonto ein. Das Zurücksetzen der Warte- und Latchstatistiken wird nicht unterstützt.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-displaying-log-space-information-for-all-databases"></a>A. Anzeigen von Informationen zum Protokollspeicherplatz für alle Datenbanken  
Das folgende Beispiel zeigt `LOGSPACE` Informationen für alle Datenbanken in der Instanz enthaltenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
```sql  
DBCC SQLPERF(LOGSPACE);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
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
[Sp_spaceused &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
  
  


