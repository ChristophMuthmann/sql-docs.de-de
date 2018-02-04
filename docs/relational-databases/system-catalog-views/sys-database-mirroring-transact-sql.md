---
title: Sys. database_mirroring (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring
- database_mirroring
- sys.database_mirroring_TSQL
- database_mirroring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_mirroring catalog view
ms.assetid: 480de2b0-2c16-497d-a6a3-bf7f52a7c9a0
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c17cf0f7b1ad2a5fd45dcd356546f5e91c4b610b
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdatabasemirroring-transact-sql"></a>sys.database_mirroring (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Datenbank in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz. Wenn die Datenbank nicht ONLINE ist, oder die datenbankspiegelung nicht aktiviert ist, werden die Werte aller Spalten mit Ausnahme von Database_id NULL sein.  
  
 Um die Zeile für eine Datenbank außer Master oder Tempdb anzuzeigen, müssen Sie der Datenbankbesitzer sein oder zumindest ALTER ANY DATABASE oder VIEW ANY DATABASE auf Serverebene-Berechtigung oder die CREATE DATABASE-Berechtigung in der master-Datenbank. Um Werte ungleich NULL für die Spiegeldatenbank anzuzeigen, muss ein Mitglied der **Sysadmin** festen Serverrolle "".  
  
> [!NOTE]  
>  Wenn eine Datenbank nicht an der Spiegelung beteiligt ist, enthalten alle Spalten mit dem Präfix "mirroring_" den Wert NULL.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Die ID der Datenbank. Ist eindeutig innerhalb einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**mirroring_guid**|**uniqueidentifier**|ID der Spiegelungspartnerschaft.<br /><br /> NULL = Datenbank ist nicht verfügbar oder wird nicht gespiegelt.<br /><br /> Hinweis: Wenn die Datenbank nicht an der Spiegelung beteiligt ist, werden alle Spalten, die mit dem Präfix "mirroring_"den Wert NULL.|  
|**mirroring_state**|**tinyint**|Status der Spiegeldatenbank und der Datenbank-Spiegelungssitzung.<br /><br /> 0 = angehalten<br /><br /> 1 = Getrennt vom anderen Partner<br /><br /> 2 = Wird synchronisiert<br /><br /> 3 = Ausstehendes Failover<br /><br /> 4 = Synchronisiert<br /><br /> 5 = Die Partner sind nicht synchronisiert. Failover ist jetzt nicht möglich.<br /><br /> 6 = Die Partner sind synchronisiert. Failover ist eventuell möglich. Informationen zu den Anforderungen für Failovercluster finden Sie unter [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).<br /><br /> NULL = Auf die Datenbank kann nicht zugegriffen werden, oder die Datenbank wird nicht gespiegelt.|  
|**mirroring_state_desc**|**nvarchar(60)**|Beschreibung des Status der Spiegeldatenbank und der Datenbankspiegelungssitzung. Folgende Werte sind möglich:<br /><br /> DISCONNECTED<br /><br /> SYNCHRONIZED<br /><br /> SYNCHRONIZING<br /><br /> PENDING_FAILOVER<br /><br /> SUSPENDED<br /><br /> UNSYNCHRONIZED<br /><br /> SYNCHRONIZED<br /><br /> NULL<br /><br /> Weitere Informationen finden Sie unter [Spiegelungsstatus &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md).|  
|**mirroring_role**|**tinyint**|Aktuelle Rolle der lokalen Datenbank in der Datenbank-Spiegelungssitzung.<br /><br /> 1 = Prinzipal<br /><br /> 2 = Spiegel<br /><br /> NULL = Auf die Datenbank kann nicht zugegriffen werden, oder die Datenbank wird nicht gespiegelt.|  
|**mirroring_role_desc**|**nvarchar(60)**|Beschreibung der Rolle der lokalen Datenbank im Rahmen der Spiegelung. Folgende Werte sind möglich:<br /><br /> PRINCIPAL<br /><br /> MIRROR|  
|**mirroring_role_sequence**|**int**|Die Anzahl von Rollenwechseln zwischen den Spiegelungspartnern (Prinzipal und Spiegel) aufgrund eines Failovers oder eines erzwungenen Diensts.<br /><br /> NULL = Auf die Datenbank kann nicht zugegriffen werden, oder die Datenbank wird nicht gespiegelt.|  
|**mirroring_safety_level**|**tinyint**|Sicherheitseinstellung für Updates in der Spiegeldatenbank:<br /><br /> 0 = Unbekannter Status<br /><br /> 1 = Deaktiviert [asynchron]<br /><br /> 2 = Vollständige Sicherheit [synchron]<br /><br /> NULL = Auf die Datenbank kann nicht zugegriffen werden, oder die Datenbank wird nicht gespiegelt.|  
|**mirroring_safety_level_desc**|**nvarchar(60)**|Transaktionssicherheitseinstellung für Updates in der Spiegeldatenbank. Folgende Werte sind möglich:<br /><br /> UNKNOWN<br /><br /> OFF<br /><br /> FULL<br /><br /> NULL|  
|**mirroring_safety_sequence**|**int**|Updatesequenznummer für Änderungen an der Transaktionssicherheitsstufe.<br /><br /> NULL = Auf die Datenbank kann nicht zugegriffen werden, oder die Datenbank wird nicht gespiegelt.|  
|**mirroring_partner_name**|**nvarchar(128)**|Servername des Datenbank-Spiegelungspartners.<br /><br /> NULL = Auf die Datenbank kann nicht zugegriffen werden, oder die Datenbank wird nicht gespiegelt.|  
|**mirroring_partner_instance**|**nvarchar(128)**|Instanzname und Computername des anderen Partners. Clients benötigen diese Information, um die Verbindung mit dem Partner herstellen zu können, wenn dieser zum Prinzipalserver wird.<br /><br /> NULL = Auf die Datenbank kann nicht zugegriffen werden, oder die Datenbank wird nicht gespiegelt.|  
|**mirroring_witness_name**|**nvarchar(128)**|Servername des Datenbank-Spiegelungszeugen.<br /><br /> NULL = Es gibt keinen Zeugen.|  
|mirroring_witness_state|**tinyint**|Status des Zeugen in der Datenbankspiegelungssitzung der Datenbank. Folgende Werte sind möglich:<br /><br /> 0 = Unbekannt<br /><br /> 1 = Verbunden<br /><br /> 2 = Getrennt<br /><br /> NULL = Es ist kein Zeuge vorhanden, die Datenbank befindet sich nicht online, oder die Datenbank wird nicht gespiegelt.|  
|**mirroring_witness_state_desc**|**nvarchar(60)**|Beschreibung des Status. Folgende Werte sind möglich:<br /><br /> UNKNOWN<br /><br /> CONNECTED<br /><br /> DISCONNECTED<br /><br /> NULL|  
|**mirroring_failover_lsn**|**numeric(25,0)**|Protokollsequenznummer (Log Sequence Number, LSN) des aktuellsten Transaktionsprotokoll-Datensatzes, für den das Festschreiben auf der Festplatte auf beiden Partnern garantiert wird. Nach einem Failover die **Mirroring_failover_lsn** , die von den Partnern als Vergleichspunkt, an dem der neue Spiegelserver synchronisiert die neue Spiegeldatenbank mit der neuen Prinzipaldatenbank beginnt, verwendet wird.|  
|**mirroring_connection_timeout**|**int**|Timeout für die Spiegelungsverbindung in Sekunden. Dieser Wert entspricht der Anzahl von Sekunden, die auf eine Antwort vom Partner oder Zeugen gewartet wird, bis dieser als nicht verfügbar eingestuft wird. Standardmäßig beträgt der Timeoutwert 10 Sekunden.<br /><br /> NULL = Auf die Datenbank kann nicht zugegriffen werden, oder die Datenbank wird nicht gespiegelt.|  
|**mirroring_redo_queue**|**int**|Maximaler Umfang des Protokolls für die Wiederholung auf dem Spiegel. Wenn Mirroring_redo_queue_type auf UNLIMITED festgelegt ist, also die Standardeinstellung ist diese Spalte NULL. Wenn die Datenbank nicht online ist, ist der Wert dieser Spalte ebenfalls NULL.<br /><br /> Andernfalls enthält diese Spalte den maximalen Protokollumfang in MB. Wenn das Maximum erreicht ist, wird das Protokoll auf dem Prinzipal vorübergehend angehalten, bis der Spiegelserver den aktuellen Stand erreicht hat. Durch diese Funktion wird die Failoverzeit begrenzt.<br /><br /> Weitere Informationen finden Sie unter [Einschätzen der Unterbrechung des Diensts während des Rollenwechsels &#40;Datenbankspiegelung&#41;](../../database-engine/database-mirroring/estimate-the-interruption-of-service-during-role-switching-database-mirroring.md).|  
|**mirroring_redo_queue_type**|**nvarchar(60)**|UNLIMITED zeigt an, dass die Wiederholungswarteschlange durch die Spiegelung nicht unterdrückt wird. Dies ist die Standardeinstellung.<br /><br /> MB zeigt an, dass die maximale Größe der Wiederholungswarteschlange (in MB) verwendet wird. Beachten Sie Folgendes: Wenn die Warteschlangengröße in KB oder GB angegeben wurde, wird der Wert vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] in MB konvertiert.<br /><br /> Wenn die Datenbank nicht online ist, ist der Wert dieser Spalte NULL.|  
|**mirroring_end_of_log_lsn**|**numeric(25,0)**|Das lokale Protokollende, das auf den Datenträger geleert wurde. Dies ist vergleichbar mit der festgeschriebenen LSN des Spiegelservers (finden Sie unter der **Mirroring_failover_lsn** Spalte).|  
|**mirroring_replication_lsn**|**numeric(25,0)**|Die maximale LSN, die von der Replikation gesendet werden kann.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.database_mirroring_endpoints (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [Datenbanken und Dateikatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
