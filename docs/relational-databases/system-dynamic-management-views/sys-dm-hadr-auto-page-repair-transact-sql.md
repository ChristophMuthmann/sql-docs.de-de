---
title: "Sys. dm_hadr_auto_page_repair – (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_hadr_auto_page_repair_TSQL
- sys.dm_hadr_auto_page_repair
- sys.dm_hadr_auto_page_repair_TSQL
- dm_hadr_auto_page_repair
dev_langs: TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- automatic page repair
- sys.dm_hadr_auto_page_repair dynamic management view
ms.assetid: d7840adf-4a1b-41ac-bc94-102c07ad1c79
caps.latest.revision: "8"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9a29d92e0309ed4ff9379e0d3370f1f1a299e512
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmhadrautopagerepair-transact-sql"></a>sys.dm_hadr_auto_page_repair (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede versuchte automatische Seitenreparatur in einer beliebigen Verfügbarkeitsdatenbank auf einem Verfügbarkeitsreplikat zurück, das von der Serverinstanz für eine beliebige Verfügbarkeitsgruppe gehostet wird. Diese Sicht enthält Zeilen für die letzte automatische Seitenreparatur einer bestimmten primären oder sekundären Datenbank. Pro Datenbank können maximal 100 Zeilen angezeigt werden. Sobald das Maximum in der Datenbank erreicht ist, ersetzt die Zeile bei der nächsten automatischen Seitenreparatur einen der bereits vorhandenen Einträge. In der folgenden Tabelle wird die Bedeutung der einzelnen Spalten definiert.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID der Datenbank, der diese Zeile entspricht.|  
|**FILE_ID**|**int**|ID der Datei, in der sich diese Seite befindet.|  
|**Page_ID**|**bigint**|ID der Seite in der Datei.|  
|**error_type**|**int**|Typ des Fehlers. Folgende Werte sind möglich:<br /><br /> **-**1 = alle Hardwarefehler 823<br /><br /> 1 = 824 Fehler außer einer fehlerhaften Prüfsumme oder einer zerrissenen Seite (z. B. eine fehlerhafte Seiten-ID)<br /><br /> 2 = Fehlerhafte Prüfsumme<br /><br /> 3 = Zerrissene Seite|  
|**page_status**|**int**|Status einer Seitenreparatur:<br /><br /> 2 = In der Warteschlange für Partneranforderung.<br /><br /> 3 = Anforderung an Partner gesendet.<br /><br /> 4 = In der Warteschlange für automatische Seitenreparatur (Antwort von Partner empfangen).<br /><br /> 5 = Automatische Seitenreparatur erfolgreich ausgeführt. Die Seite sollte verwendbar sein.<br /><br /> 6 = Nicht zu reparieren. Dies weist darauf hin, dass bei der Seitenreparatur ein Fehler aufgetreten ist, weil beispielsweise die Partnerseite ebenfalls beschädigt ist, der Partner nicht verbunden ist oder ein Netzwerkproblem aufgetreten ist. Dieser Status ist nicht abschließend; wenn auf der Seite erneut eine Beschädigung festgestellt wird, wird sie nochmals vom Partner angefordert.|  
|**modification_time**|**datetime**|Zeitpunkt der letzten Seitenstatusänderung.|  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Automatische Seitenreparatur (Verfügbarkeitsgruppen: Datenbankspiegelung)](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [Suspect_pages &#40; Transact-SQL &#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [Verwalten der suspect_pages-Tabelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  

