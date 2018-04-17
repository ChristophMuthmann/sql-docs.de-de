---
title: IHpublications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHpublications_TSQL
- IHpublications
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublications system table
ms.assetid: b519a101-fa53-44be-bd55-6ea79245b5d1
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8041914733509d89ed6d17084ae30df5817e3505
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="ihpublications-transact-sql"></a>IHpublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **IHpublications** -Systemtabelle enthält eine Zeile für jede nicht - SQL Server-Veröffentlichung mithilfe des aktuellen Verteilers. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**pubid**|**int**|Die Identitätsspalte mit einer eindeutigen ID für die Veröffentlichung.|  
|**name**|**sysname**|Der eindeutige der Veröffentlichung zugeordnete Name.|  
|**repl_freq**|**tinyint**|Replikationshäufigkeit:<br /><br /> **0** = transaktionsbasiert.<br /><br /> **1** = Geplantes tabellenupdate.|  
|**status**|**tinyint**|Der Status der Veröffentlichung; dieser kann einen der folgenden Werte annehmen:<br /><br /> **0** = inaktiv.<br /><br /> **1** = aktiv.|  
|**sync_method**|**tinyint**|Synchronisierungsmethode:<br /><br /> **1** = Massenkopieren von Zeichen.<br /><br /> **4** = Concurrent_c, dies bedeutet, dass das Massenkopieren von Zeichen wird verwendet, aber Tabellen werden während der Erstellung der Momentaufnahme nicht gesperrt.|  
|**snapshot_jobid**|**binary**|Die ID des geplanten Tasks.|  
|**enabled_for_internet**|**bit**|Gibt an, ob die Synchronisierungsdateien für die Veröffentlichung im Internet über FTP oder andere Dienste bereitgestellt werden, in denen **1** bedeutet, dass sie über das Internet zugegriffen werden kann.|  
|**immediate_sync_ready**|**bit**|Gibt an, ob die Synchronisierungsdateien verfügbar sind; **1** bedeutet, dass sie verfügbar sind. *Nicht unterstützt für nicht - SQL-Verleger.*|  
|**allow_queued_tran**|**bit**|Gibt an, ob das Einreihen von Änderungen auf dem Abonnenten in Warteschlangen, bis diese Änderungen auf dem Verleger angewendet werden können, aktiviert wurde. Wenn **1**, Änderungen auf dem Abonnenten in der Warteschlange. *Nicht unterstützt für nicht - SQL-Verleger.*|  
|**allow_sync_tran**|**bit**|Gibt an, ob Abonnements mit sofortiger Aktualisierung für die Veröffentlichung zulässig sind. **1** bedeutet, dass Abonnements mit sofortigem Update zulässig sind. *Nicht unterstützt für nicht - SQL-Verleger.*|  
|**autogen_sync_procs**|**bit**|Gibt an, ob die synchronisierende gespeicherte Prozedur für Abonnements mit sofortiger Aktualisierung beim Verleger generiert wird. **1** bedeutet, dass es auf dem Verleger generiert wird. *Nicht unterstützt für nicht - SQL-Verleger.*|  
|**snapshot_in_defaultfolder**|**bit**|Gibt an, ob momentaufnahmedateien im Standardordner gespeichert werden. Wenn **0**, sind momentaufnahmedateien im alternativen vom angegebenen Speicherort gespeichert *Alternate_snapshot_folder*. Wenn **1**, momentaufnahmedateien im Standardordner gefunden werden können.|  
|**alt_snapshot_folder**|**nvarchar(510)**|Gibt den Speicherort des anderen Ordners für die Momentaufnahme an.|  
|**pre_snapshot_script**|**nvarchar(510)**|Gibt einen Zeiger auf eine **.sql** Dateispeicherort. Der Verteilungs-Agent führt das vor der Momentaufnahme ausgeführte Skript vor allen Skripts für replizierte Objekte aus, wenn die Momentaufnahme auf einem Abonnenten angewendet wird.|  
|**post_snapshot_script**|**nvarchar(510)**|Gibt einen Zeiger auf eine **.sql** Dateispeicherort. Der Verteilungs-Agent führt post_snapshot_script aus, nachdem alle anderen Skripts für replizierte Objekte und Daten während der erstsynchronisierung angewendet wurden.|  
|**compress_snapshot**|**bit**|Gibt an, dass die Momentaufnahme, die geschrieben wird die *Alt_snapshot_folder* Speicherort ist in komprimiert die [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB-Format. **0** gibt an, dass die Momentaufnahme nicht komprimiert wird.|  
|**ftp_address**|**sysname**|Die Netzwerkadresse des FTP-Diensts für den Verteiler. Gibt an, wo die Veröffentlichungsmomentaufnahmedateien zum Aufnehmen durch den Verteilungs-Agent gespeichert sind.|  
|**ftp_port**|**int**|Die Portnummer des FTP-Diensts für den Verteiler. Gibt an, wo die Veröffentlichungsmomentaufnahmedateien zur Aufnahme durch den Verteilungs-Agent gespeichert sind.|  
|**ftp_subdirectory**|**nvarchar(510)**|Gibt an, wo die Momentaufnahmedateien für den Verteilungs-Agent zum Aufnehmen verfügbar sind, wenn die Veröffentlichung das Weitergeben von Momentaufnahmen mithilfe von FTP unterstützt.|  
|**ftp_login**|**nvarchar(256)**|Der Benutzername, der für die Verbindung mit dem FTP-Dienst verwendet wird.|  
|**ftp_password**|**nvarchar(1048)**|Das Benutzerkennwort für die Verbindung mit dem FTP-Dienst verwendet wird.|  
|**allow_dts**|**bit**|Gibt an, dass die Veröffentlichung Datentransformationen zulässt. **1** gibt an, dass DTS-Transformationen zulässig sind. *Nicht unterstützt für nicht - SQL-Verleger.*|  
|**allow_anonymous**|**bit**|Gibt an, ob anonyme Abonnements für die Veröffentlichung zulässig sind, in denen **1** bedeutet, dass sie zulässig sind.|  
|**centralized_conflicts**|**bit**|Gibt an, ob Konfliktdatensätze auf dem Verleger gespeichert werden:<br /><br /> **0** = die Konfliktdatensätze gespeichert werden auf dem Verleger und dem Abonnenten, die den Konflikt verursacht hat.<br /><br /> **1** = die Konfliktdatensätze auf dem Verleger gespeichert werden.<br /><br /> *Nicht unterstützt für nicht - SQL-Verleger.*|  
|**conflict_retention**|**int**|Gibt die Konfliktaufbewahrungsdauer in Tagen an. *Nicht unterstützt für nicht - SQL-Verleger.*|  
|**conflict_policy**|**int**|Gibt die Richtlinie zur Konfliktlösung an, die für die Option zur verzögerten Aktualisierung über eine Warteschlange verwendet wird. Einer der folgenden Werte sind möglich:<br /><br /> **1** = der Verleger gewinnt den Konflikt.<br /><br /> **2** = der Abonnent gewinnt den Konflikt.<br /><br /> **3** = Abonnement wird erneut initialisiert.<br /><br /> *Nicht unterstützt für nicht - SQL-Verleger.*|  
|**queue_type**|**int**|Gibt an, welcher Wartenschlangentyp verwendet wird. Einer der folgenden Werte sind möglich:<br /><br /> **1** = Msmq; es wird [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing zum Speichern von Transaktionen.<br /><br /> **2** = Sql; es wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Speichern von Transaktionen.<br /><br /> Diese Spalte wird nicht verwendet, von nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber.<br /><br /> Hinweis: Mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing wurde als veraltet markiert und wird nicht mehr unterstützt.<br /><br /> *Diese Spalte wird für nicht - SQL-Verleger nicht unterstützt.*|  
|**ad_guidname**|**sysname**|Gibt an, ob die Veröffentlichung in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory veröffentlicht wird. Ein gültiger globally unique Identifier (GUID) gibt an, dass die Veröffentlichung, in veröffentlicht wird der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory und die GUID ist das entsprechende Active Directory-Veröffentlichungsobjekt **"objectGUID"**. Wenn dieser Wert NULL ist, wird die Veröffentlichung nicht in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory veröffentlicht. *Nicht unterstützt für nicht - SQL-Verleger.*|  
|**backward_comp_level**|**int**|Datenbankkompatibilitätsgrad, der einen der folgenden Werte annehmen kann:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].<br /><br /> *Nicht unterstützt für nicht - SQL-Verleger.*|  
|**description**|**nvarchar(255)**|Beschreibender Eintrag für die Veröffentlichung.|  
|**independent_agent**|**bit**|Gibt an, ob ein eigenständiger Verteilungs-Agent für diese Veröffentlichung vorhanden ist.<br /><br /> **0** = die Veröffentlichung verwendet einen freigegebenen Verteilungs-Agent, und jedes Verlegerdatenbank und Abonnentendatenbank-Paar besitzt einen einzelnen freigegebenen Agent.<br /><br /> **1** = es ist ein eigenständiger Verteilungs-Agent für diese Veröffentlichung.|  
|**immediate_sync**|**bit**|Gibt an, ob die Synchronisierungsdateien erstellt oder neu bei jeder Ausführung der Momentaufnahme-Agent erstellt werden, in denen **1** bedeutet, dass sie erstellt wurden, jedes Mal, wenn der Agent ausgeführt wird.|  
|**allow_push**|**bit**|Gibt an, ob Pushabonnements für die Veröffentlichung zulässig sind, in denen **1** bedeutet, dass sie zulässig sind.|  
|**allow_pull**|**bit**|Gibt an, ob Pullabonnements für die Veröffentlichung zulässig sind, in denen **1** bedeutet, dass sie zulässig sind.|  
|**Beibehaltungsdauer**|**int**|Der Änderungsumfang in Stunden, der für die angegebene Veröffentlichung eingespart werden soll.|  
|**allow_subscription_copy**|**bit**|Gibt an, ob die Möglichkeit zum Kopieren der Abonnementdatenbanken aktiviert wurde, die diese Veröffentlichung abonniert haben. **1** bedeutet, dass das Kopieren zulässig ist.|  
|**allow_initialize_from_backup**|**bit**|Gibt an, ob Abonnenten ein Abonnement für diese Veröffentlichung über eine Sicherung anstelle einer Anfangsmomentaufnahme initialisieren können. **1** bedeutet, dass Abonnements aus einer Sicherung initialisiert werden können und **0** bedeutet, die sie nicht. Weitere Informationen finden Sie unter [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)initialisiert wird. *Nicht unterstützt für nicht - SQL-Verleger.*|  
|**min_autonosync_lsn**|**Binary(1)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|Gibt an, ob für die Veröffentlichung die Schemareplikation unterstützt wird. **1** gibt an, dass auf dem Verleger ausgeführte DDL-Anweisungen repliziert werden, und **0** gibt an, dass die DDL-Anweisungen nicht repliziert werden. Weitere Informationen finden Sie unter [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md). *Nicht unterstützt für nicht - SQL-Verleger.*|  
|**options**|**int**|Bitmuster, mit dem zusätzliche Veröffentlichungsoptionen angegeben werden, mit den folgenden bitweisen Optionswerten:<br /><br /> **0 x 1** – für die Peer-zu-Peer-Replikation aktiviert.<br /><br /> **0 x 2** -nur lokale Änderungen veröffentlichen.<br /><br /> **0 x 4** – für nicht - SQL Server-Abonnenten aktiviert.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [SYSPUBLICATIONS &#40;Systemsicht&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)   
 [SYSPUBLICATIONS &#40;Transact-SQL&#41;](../../relational-databases/system-tables/syspublications-transact-sql.md)  
  
  
