---
title: SYSPUBLICATIONS (Systemsicht) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- syspublications
- syspublications_TSQL
dev_langs: TSQL
helpviewer_keywords: syspublications view
ms.assetid: e5f57c32-efc0-4455-a74f-684dc2ae51f8
caps.latest.revision: "20"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: afd6e57ed8c17dc74b24320808e8502a679bf152
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="syspublications-system-view-transact-sql"></a>syspublications (Systemsicht) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **Syspublications** -Sicht macht Veröffentlichungsinformationen verfügbar. Diese Sicht wird in der distribution-Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Beschreibung**|**nvarchar(255)**|Der beschreibende Eintrag für die Veröffentlichung.|  
|**name**|**sysname**|Der eindeutige der Veröffentlichung zugeordnete Name.|  
|**pubid**|**int**|Die Identitätsspalte mit einer eindeutigen ID für die Veröffentlichung.|  
|**repl_freq**|**tinyint**|Replikationshäufigkeit:<br /><br /> **0** = transaktionsbasiert (Transaktion).<br /><br /> **1** = Geplantes tabellenupdate (Snapshot).|  
|**status**|**tinyint**|Veröffentlichungsstatus:<br /><br /> **0** = inaktiv.<br /><br /> **1** = aktiv.|  
|**sync_method**|**tinyint**|Synchronisierungsmethode:<br /><br /> **0** = Hilfsprogramm Programm zum systemeigene Massenkopieren (BCP).<br /><br /> **1** = BCP-Zeichenmodus.<br /><br /> **3** = gleichzeitig, was bedeutet, dass das systemeigene BCP verwendet, aber Tabellen werden während der Erstellung der Momentaufnahme nicht gesperrt.<br /><br /> **4** = Concurrent_c, dies bedeutet, dass die Zeichen, BCP verwendet wird, aber Tabellen während der Erstellung der Momentaufnahme nicht gesperrt sind.|  
|**snapshot_jobid**|**Binary(16)**|Identifiziert den Agentauftrag, der die Anfangsmomentaufnahme generieren soll.|  
|**independent_agent**|**bit**|Gibt an, ob ein eigenständiger Verteilungs-Agent für diese Veröffentlichung vorhanden ist.<br /><br /> **0** = die Veröffentlichung verwendet einen freigegebenen Verteilungs-Agent, und jedes Verlegerdatenbank und Abonnentendatenbank-Paar besitzt einen einzelnen freigegebenen Agent.<br /><br /> **1** = es ist ein eigenständiger Verteilungs-Agent für diese Veröffentlichung.|  
|**immediate_sync**|**bit**|Gibt an, ob die Synchronisierungsdateien erstellt oder neu bei jeder Ausführung der Momentaufnahme-Agent erstellt werden, in denen **1** bedeutet, dass sie erstellt wurden, jedes Mal, wenn der Agent ausgeführt wird.|  
|**enabled_for_internet**|**bit**|Gibt an, ob die Synchronisierungsdateien für die Veröffentlichung im Internet über das Dateiübertragungsprotokoll (FTP) und andere Dienste bereitgestellt werden, in denen **1** bedeutet, dass sie über das Internet zugegriffen werden kann.|  
|**allow_push**|**bit**|Gibt an, ob Pushabonnements für die Veröffentlichung zulässig sind, in denen **1** bedeutet, dass sie zulässig sind.|  
|**allow_pull**|**bit**|Gibt an, ob Pullabonnements für die Veröffentlichung zulässig sind, in denen **1** bedeutet, dass sie zulässig sind.|  
|**allow_anonymous**|**bit**|Gibt an, ob anonyme Abonnements für die Veröffentlichung zulässig sind, in denen **1** bedeutet, dass sie zulässig sind.|  
|**immediate_sync_ready**|**bit**|Zeigt an, ob die Momentaufnahme vom Momentaufnahme-Agent generiert wurde und dieser zum Verwenden durch neue Abonnements bereit ist. Dies ist nur für sofort aktualisierbare Veröffentlichungen von Bedeutung. **1** gibt an, dass die Momentaufnahme bereit ist.|  
|**allow_sync_tran**|**bit**|Gibt an, ob Abonnements mit sofortiger Aktualisierung für die Veröffentlichung zulässig sind. **1** bedeutet, dass Abonnements mit sofortigem Update zulässig sind.|  
|**autogen_sync_procs**|**bit**|Gibt an, ob die synchronisierende gespeicherte Prozedur für Abonnements mit sofortiger Aktualisierung beim Verleger generiert wird. **1** bedeutet, dass es auf dem Verleger generiert wird.|  
|**Beibehaltungsdauer**|**int**|Der Zeitraum (in Stunden), in dem Änderungen an der Veröffentlichung in der Verteilungsdatenbank beibehalten werden.|  
|**allow_queued_tran-Eigenschaft**|**bit**|Gibt an, ob das Einreihen von Änderungen auf dem Abonnenten in Warteschlangen, bis diese Änderungen auf dem Verleger angewendet werden können, aktiviert wurde. Wenn **1**, Änderungen auf dem Abonnenten in der Warteschlange.|  
|**snapshot_in_defaultfolder**|**bit**|Gibt an, ob momentaufnahmedateien im Standardordner gespeichert werden. Wenn **0**, sind momentaufnahmedateien im alternativen vom angegebenen Speicherort gespeichert *Alternate_snapshot_folder*. Bei 1 befinden sich die Momentaufnahmedateien im Standardordner.|  
|**alt_snapshot_folder**|**nvarchar(510)**|Gibt den Speicherort des anderen Ordners für die Momentaufnahme an.|  
|**pre_snapshot_script**|**nvarchar(510)**|Gibt einen Zeiger auf eine **.sql** Dateispeicherort. Der Verteilungs-Agent führt das vor der Momentaufnahme ausgeführte Skript vor allen Skripts für replizierte Objekte aus, wenn die Momentaufnahme auf einem Abonnenten angewendet wird.|  
|**post_snapshot_script**|**nvarchar(510)**|Gibt einen Zeiger auf eine **.sql** Dateispeicherort. Der Verteilungs-Agent führt post_snapshot_script aus, nachdem alle anderen Skripts für replizierte Objekte und Daten während der erstsynchronisierung angewendet wurden.|  
|**compress_snapshot**|**bit**|Gibt an, dass die Momentaufnahme, die geschrieben wird die *Alt_snapshot_folder* Speicherort ist in komprimiert die [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB-Format. **1** bedeutet, dass die Momentaufnahme komprimiert wird.|  
|**ftp_address**|**sysname**|Die Netzwerkadresse des FTP-Diensts für den Verteiler. Gibt an, wo die Veröffentlichungsmomentaufnahmedateien zum Aufnehmen durch den Verteilungs-Agent gespeichert sind.|  
|**ftp_port**|**int**|Die Portnummer des FTP-Diensts für den Verteiler. Gibt an, wo die veröffentlichungsmomentaufnahmedateien für den Verteilungs-Agent zum Abholen befinden.|  
|**ftp_subdirectory**|**nvarchar(510)**|Gibt an, wo die Momentaufnahmedateien für den Verteilungs-Agent zum Aufnehmen verfügbar sind, wenn die Veröffentlichung das Weitergeben von Momentaufnahmen mithilfe von FTP unterstützt.|  
|**ftp_login**|**nvarchar(256)**|Der Benutzername, der für die Verbindung mit dem FTP-Dienst verwendet wird.|  
|**ftp_password**|**nvarchar(1048)**|Das Benutzerkennwort für die Verbindung mit dem FTP-Dienst verwendet wird.|  
|**allow_dts nicht**|**bit**|Gibt an, ob die Veröffentlichung DTS-Transformationen (Data Transformation Services) für [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] zulässt. **1** gibt an, dass DTS-Transformationen zulässig sind.|  
|**allow_subscription_copy**|**bit**|Gibt an, ob die Möglichkeit zum Kopieren der Abonnementdatenbanken aktiviert wurde, die diese Veröffentlichung abonniert haben. **1** bedeutet, dass das Kopieren zulässig ist.|  
|**centralized_conflicts**|**bit**|Gibt an, ob Konfliktdatensätze auf dem Verleger gespeichert werden:<br /><br /> **0** = die Konfliktdatensätze gespeichert werden auf dem Verleger und dem Abonnenten, die den Konflikt verursacht hat.<br /><br /> **1** = die Konfliktdatensätze auf dem Verleger gespeichert werden.|  
|**conflict_retention**|**int**|Gibt die Beibehaltungsdauer für Konfliktdatensätze in Tagen an.|  
|**conflict_policy**|**int**|Gibt die Richtlinie zur Konfliktlösung an, die für die Option zur verzögerten Aktualisierung über eine Warteschlange verwendet wird. Einer der folgenden Werte sind möglich:<br /><br /> **1** = der Verleger gewinnt den Konflikt.<br /><br /> **2** = der Abonnent gewinnt den Konflikt.<br /><br /> **3** = Abonnement wird erneut initialisiert.|  
|**Warteschlangentyp**|**int**|Gibt an, welcher Wartenschlangentyp verwendet wird. Einer der folgenden Werte sind möglich:<br /><br /> **1** = .MSMQ, d. verwendet h. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing zum Speichern von Transaktionen.<br /><br /> **2** = SQL; es wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Speichern von Transaktionen.<br /><br /> Hinweis: Mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing wurde als veraltet markiert und wird nicht mehr unterstützt.|  
|**ad_guidname**|**sysname**|Gibt an, ob die Veröffentlichung in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory veröffentlicht wird. Ein gültiger GUID (Globally Unique Identifier) gibt an, dass die Veröffentlichung in Active Directory veröffentlicht wird, und der GUID ist das entsprechende Active Directory-Veröffentlichungsobjekt objectGUID. Wenn dieser Wert NULL ist, wird die Veröffentlichung nicht in Active Directory veröffentlicht.<br /><br /> Hinweis: Die Veröffentlichung in Active Directory wird nicht mehr unterstützt.|  
|**backward_comp_level**|**int**|Datenbankkompatibilitätsgrad, der einen der folgenden Werte annehmen kann:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|**allow_initialize_from_backup**|**bit**|Gibt an, ob Abonnenten ein Abonnement für diese Veröffentlichung aus einer Sicherung anstatt einer anfangsmomentaufnahme initialisieren können. **1** bedeutet, dass Abonnements aus einer Sicherung initialisiert werden können und **0** bedeutet, die sie nicht. Weitere Informationen finden Sie unter [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)initialisiert wird.|  
|**min_autonosync_lsn**|**Binary(1)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|Gibt an, ob die Schemareplikation für die Veröffentlichung unterstützt wird.<br /><br /> **1** = DDL-Anweisungen auf dem Verleger ausgeführt werden repliziert.<br /><br /> **0** = gibt an, dass die DDL-Anweisungen nicht repliziert werden. Weitere Informationen finden Sie unter [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).|  
|**Optionen**|**int**|Ein Bitmuster, mit dem zusätzliche Veröffentlichungsoptionen angegeben werden. Dabei gibt es folgende bitweise Optionswerte:<br /><br /> **0 x 1** – für die Peer-zu-Peer-Replikation aktiviert.<br /><br /> **0 x 2** -nur lokale Änderungen für die Peer-zu-Peer-Replikation veröffentlichen.<br /><br /> **0 x 4** - aktiviert für nicht -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten.<br /><br /> **0 x 8** – für die Peer-zu-Peer-konflikterkennung aktiviert.|  
|**originator_id**|**smallint**|Kennzeichnet jeden Knoten in einer Peer-zu-Peer-Replikationstopologie zum Zweck der Konflikterkennung. Weitere Informationen finden Sie unter [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Gespeicherte Replikationsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Sp_addpublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [Sp_helppublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)  
  
  
