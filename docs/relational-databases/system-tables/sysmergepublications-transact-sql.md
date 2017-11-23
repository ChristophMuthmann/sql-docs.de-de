---
title: Sysmergepublications (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sysmergepublications
- sysmergepublications_TSQL
dev_langs: TSQL
helpviewer_keywords: sysmergepublications system table
ms.assetid: 7f82c6c3-22d1-47c0-a92b-4d64b98cc455
caps.latest.revision: "42"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95059187ddd567212027d73dbd361e1ee9d2e7a7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysmergepublications-transact-sql"></a>sysmergepublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede in der Datenbank definierte Mergeveröffentlichung. Diese Tabelle wird in der Veröffentlichungs- und in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Entspricht dem Namen des Standardservers.|  
|**publisher_db**|**sysname**|Der Name der Standardverlegerdatenbank.|  
|**name**|**sysname**|Der Name der Veröffentlichung.|  
|**Beschreibung**|**nvarchar(255)**|Eine kurze Beschreibung der Veröffentlichung.|  
|**Beibehaltungsdauer**|**int**|Die Beibehaltungsdauer für den gesamten veröffentlichungssatz, in denen die Einheit ist durch den Wert von der **Retention_period_unit** Spalte.|  
|**publication_type**|**tinyint**|Zeigt an, ob die Veröffentlichung gefiltert wird.<br /><br /> **0** = nicht gefiltert.<br /><br /> **1** = gefiltert.|  
|**pubid**|**uniqueidentifier**|Die eindeutige ID für diese Veröffentlichung. Dieser Wert wird beim Hinzufügen der Veröffentlichung generiert.|  
|**DesignMasterID**|**uniqueidentifier**|Zur künftigen Verwendung reserviert.|  
|**parentid**|**uniqueidentifier**|Zeigt die übergeordnete Veröffentlichung an, aus der die aktuelle gleichgeordnete oder als Teilmenge verwendete Veröffentlichung erstellt wurde (wird für hierarchische Veröffentlichungstopologien verwendet).|  
|**sync_mode**|**tinyint**|Der Synchronisierungsmodus dieser Veröffentlichung:<br /><br /> **0** = Native.<br /><br /> **1** = Zeichen.|  
|**allow_push**|**int**|Zeigt an, ob die Veröffentlichung Pushabonnements zulässt.<br /><br /> **0** = Pushabonnements sind nicht zulässig.<br /><br /> **1** = Pushabonnements sind zulässig.|  
|**allow_pull**|**int**|Zeigt an, ob die Veröffentlichung Pullabonnements zulässt.<br /><br /> **0** = Pullabonnements sind nicht zulässig.<br /><br /> **1** = Pullabonnements sind zulässig.|  
|**allow_anonymous**|**int**|Zeigt an, ob die Veröffentlichung anonyme Abonnements zulässt.<br /><br /> **0** = anonyme Abonnements sind nicht zulässig.<br /><br /> **1** = anonyme Abonnements sind zulässig.|  
|**centralized_conflicts**|**int**|Zeigt an, ob die Konfliktdatensätze auf dem Verleger gespeichert werden:<br /><br /> **0** = die Konfliktdatensätze werden nicht auf dem Verleger gespeichert.<br /><br /> **1** = die Konfliktdatensätze auf dem Verleger gespeichert werden.|  
|**status**|**tinyint**|Zur künftigen Verwendung reserviert.|  
|**snapshot_ready**|**tinyint**|Zeigt den Status für die Momentaufnahme der Veröffentlichung an:<br /><br /> **0** = Momentaufnahme kann nicht für die Verwendung.<br /><br /> **1** = Momentaufnahme für die Verwendung bereit ist.<br /><br /> **2** = eine neue Momentaufnahme für diese Veröffentlichung erstellt werden muss.|  
|**enabled_for_internet**|**bit**|Zeigt an, ob die Synchronisierungsdateien für die Veröffentlichung im Internet, über FTP oder andere Dienste bereitgestellt werden.<br /><br /> **0** = Zugriff auf Synchronisierungsdateien Dateien aus dem Internet zugegriffen werden können.<br /><br /> **1** = Zugriff auf Synchronisierungsdateien Dateien können nicht aus dem Internet zugegriffen werden.|  
|**dynamic_filters**|**bit**|Gibt an, ob die Veröffentlichung mithilfe eines parametrisierten Zeilenfilters gefiltert wird.<br /><br /> **0** = für die Veröffentlichung wird kein Zeilenfilter verwendet.<br /><br /> **1** = für die Veröffentlichung wird ein Zeilenfilter verwendet.|  
|**snapshot_in_defaultfolder**|**bit**|Gibt an, ob Momentaufnahmedateien im Standardordner gespeichert werden:<br /><br /> **0** = momentaufnahmedateien im Standardordner speichern werden.<br /><br /> **1** = momentaufnahmedateien werden Dateien vom angegebenen Speicherort gespeichert **Alt_snapshot_folder**.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Der Speicherort des alternativen Ordners für die Momentaufnahme.|  
|**pre_snapshot_script**|**nvarchar(255)**|Zeiger auf ein. **Sql** -Datei, die der Merge-Agent vor allen replikationsobjektskripts ausführt Skripts beim Anwenden der Momentaufnahme auf dem Abonnenten.|  
|**post_snapshot_script**|**nvarchar(255)**|Der Zeiger auf ein. **Sql** Datei, die der Merge-Agent ausführt, nachdem alle anderen Skripts für Objekte und Daten während der erstsynchronisierung angewendet wurden.|  
|**compress_snapshot**|**bit**|Gibt an, ob die Momentaufnahme geschrieben der **Alt_snapshot_folder** Speicherort wird in komprimiert die [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB-Format. **0** gibt an, dass die Datei nicht komprimiert wird.|  
|**ftp_address**|**sysname**|Die Netzwerkadresse des Protokolls FTP (File Transfer)-Diensts für den Verteiler. Gibt an, wo die Veröffentlichungs-Momentaufnahmedateien zum Abholen durch den Merge-Agent gespeichert sind, wenn FTP aktiviert ist.|  
|**ftp_port**|**int**|Die Portnummer des FTP-Diensts für den Verteiler.|  
|**ftp_subdirectory**|**nvarchar(255)**|Das Unterverzeichnis, in dem die Momentaufnahmedateien zum Abholen durch den Merge-Agent verfügbar sind.|  
|**ftp_login**|**sysname**|Der Benutzername, der für die Verbindung mit dem FTP-Dienst verwendet wird.|  
|**ftp_password**|**nvarchar(524)**|Das Benutzerkennwort für die Verbindung mit dem FTP-Dienst verwendet wird.|  
|**conflict_retention**|**int**|Gibt die Aufbewahrungsdauer in Tagen an, für die Konflikte beibehalten werden. Danach wird die Konfliktzeile aus der Konflikttabelle gelöscht.|  
|**keep_before_values**|**int**|Gibt an, ob die Synchronisierungsoptimierung für diese Veröffentlichung erfolgt:<br /><br /> **0** = Synchronisierung wird nicht optimiert, und die an alle Abonnenten gesendeten Partitionen werden überprüft, wenn Daten in einer Partition ändern.<br /><br /> **1** = die Synchronisierung wird optimiert, und nur Abonnenten, die über Zeilen in der geänderten Partition verfügen betroffen sind.|  
|**allow_subscription_copy**|**bit**|Gibt an, ob die Möglichkeit zum Kopieren der Abonnementdatenbank aktiviert wurde. **0** bedeutet, dass das Kopieren ist nicht zulässig.|  
|**allow_synctoalternate**|**bit**|Gibt an, ob ein alternativer Synchronisierungspartner für die Synchronisierung mit diesem Verleger zulässig ist. **0** bedeutet, dass ein alternativer Synchronisierungspartner nicht zulässig ist.|  
|**validate_subscriber_info**|**nvarchar(500)**|Listet die Funktionen auf, die zum Abrufen der Abonnenteninformationen sowie zum Überprüfen der parametrisierten Zeilenfilterkriterien für den Abonnenten verwendet werden.|  
|**ad_guidname**|**sysname**|Gibt an, ob die Veröffentlichung in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory veröffentlicht wird. Eine gültige GUID gibt an, dass die Veröffentlichung in Active Directory veröffentlicht wird, und die GUID das entsprechende Active Directory-Veröffentlichungsobjekt ist **"objectGUID"**. Wenn dieser Wert NULL ist, wird die Veröffentlichung nicht in Active Directory veröffentlicht.|  
|**backward_comp_level**|**int**|Datenbankkompatibilitätsgrad. Folgende Werte sind möglich:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|**max_concurrent_merge**|**int**|Die maximal zulässige Anzahl gleichzeitiger Mergeprozesse. Der Wert **0** für diese Eigenschaft bedeutet, dass es keine Beschränkung der Anzahl gleichzeitiger Mergeprozesse, die einem bestimmten Zeitpunkt ausgeführt. Diese Eigenschaft legt eine Grenze für die Anzahl gleichzeitiger Mergeprozesse fest, die zu einem Zeitpunkt für eine Mergeveröffentlichung ausgeführt werden können. Wenn zum gleichen Zeitpunkt mehr Momentaufnahmeprozesse geplant sind, als der Wert für eine Ausführung zulässt, werden die überschüssigen Aufträge in eine Warteschlange eingereiht, in der diese darauf warten, dass ein aktuell ausgeführter Momentaufnahmeprozess beendet wird.|  
|**max_concurrent_dynamic_snapshots**|**int**|Die maximal zulässige Anzahl gleichzeitiger Datenfilterungs-Momentaufnahmesitzungen, die für die Mergeveröffentlichung ausgeführt werden können. Wenn **0**, besteht keine Einschränkung für die maximale Anzahl gleichzeitiger datenfilterungs-momentaufnahmesitzungen, die für die Veröffentlichung zu einem beliebigen Zeitpunkt ausgeführt werden können. Diese Eigenschaft legt eine Grenze für die Anzahl gleichzeitiger Momentaufnahmeprozesse fest, die zu einem Zeitpunkt für eine Mergeveröffentlichung ausgeführt werden können. Wenn zum gleichen Zeitpunkt mehr Momentaufnahmeprozesse geplant sind, als der Wert für eine Ausführung zulässt, werden die überschüssigen Aufträge in eine Warteschlange eingereiht, in der diese darauf warten, dass ein aktuell ausgeführter Momentaufnahmeprozess beendet wird.|  
|**use_partition_groups**|**smallint**|Gibt an, ob die Veröffentlichung vorausberechnete Partitionen verwendet.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|Eine durch Semikolons getrennte Liste der Funktionen, die in den parametrisierten Zeilenfiltern der Veröffentlichung verwendet werden.|  
|**partition_id_eval_proc**|**sysname**|Gibt den Namen der Prozedur an, die vom Merge-Agent eines Abonnenten ausgeführt wird, um die zugewiesene Partitions-ID zu bestimmen.|  
|**publication_number**|**smallint**|Gibt die Identitätsspalte, die eine 2-Byte-Zuordnung zu **Pubid**. **Pubid** ist ein global eindeutiger Bezeichner für eine Veröffentlichung, während die veröffentlichungsnummer nur in einer bestimmten Datenbank eindeutig ist.|  
|**replicate_ddl**|**int**|Gibt an, ob die Schemareplikation für die Veröffentlichung unterstützt wird.<br /><br /> **0** = DDL-Anweisungen werden nicht repliziert.<br /><br /> **1** = DDL-Anweisungen auf dem Verleger ausgeführt werden repliziert.<br /><br /> Weitere Informationen finden Sie unter [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).|  
|**allow_subscriber_initiated_snapshot**|**bit**|Gibt an, dass Abonnenten den Prozess initiieren können, mit dem die Momentaufnahme für eine Veröffentlichung mithilfe parametrisierter Filter generiert wird. **1** gibt an, dass Abonnenten den momentaufnahmeprozess initiieren können.|  
|**dynamic_snapshot_queue_timeout**|**int**|Gibt an, wie viele Minuten ein Abonnent in der Warteschlange warten muss, damit der Momentaufnahme-Generierungsprozess gestartet wird, wenn parametrisierte Filter verwendet werden.|  
|**dynamic_snapshot_ready_timeout**|**int**|Gibt an, wie viele Minuten ein Abonnent wartet, dass der Momentaufnahme-Generierungsprozess abgeschlossen wird, wenn parametrisierte Filter verwendet werden.|  
|**Verteiler**|**sysname**|Der Name des Verteilers für die Veröffentlichung.|  
|**snapshot_jobid**|**Binary(16)**|Identifiziert den Agentauftrag, der die Momentaufnahme generiert, wenn der Abonnent den Momentaufnahmeprozess initiieren kann.|  
|**allow_web_synchronization**|**bit**|Gibt an, ob die Veröffentlichung für die websynchronisierung aktiviert ist, in dem **1** bedeutet, dass die websynchronisierung für die Veröffentlichung aktiviert ist.|  
|**web_synchronization_url**|**nvarchar(500)**|Gibt den Standardwert für die Internet-URL an, die für die Websynchronisierung verwendet wird.|  
|**allow_partition_realignment**|**bit**|Gibt an, ob Löschvorgänge an den Abonnenten gesendet werden, wenn durch eine Änderung der Zeile auf dem Verleger die Partition geändert wird.<br /><br /> **0** = Daten einer alten Partition verbleiben auf dem Abonnenten, auf die Daten auf dem Verleger vorgenommene Änderungen nicht an diesen Abonnenten repliziert werden, wobei ein auf dem Abonnenten vorgenommene Änderungen an den Verleger repliziert werden.<br /><br /> **1** = Löschvorgänge auf dem Abonnenten, um die Ergebnisse einer partitionsänderung widerzuspiegeln, durch das Entfernen von Daten, die nicht mehr Bestandteil der Partition des Abonnenten ist.<br /><br /> Weitere Informationen finden Sie unter [Sp_addmergepublication &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).<br /><br /> Hinweis: Daten, die auf dem Abonnenten verbleiben, wenn dieser Wert ist **0** behandelt werden soll, als wäre er schreibgeschützt ist, dies wird jedoch nicht zwingend erzwungen vom Replikationssystem.|  
|**retention_period_unit**|**tinyint**|Definiert die Einheit, die beim Definieren von verwendet *Aufbewahrung*, was kann einen der folgenden Werte:<br /><br /> **0** = Tag.<br /><br /> **1** = Woche.<br /><br /> **2** = Monat.<br /><br /> **3** = Jahr.|  
|**decentralized_conflicts**|**int**|Gibt an, ob die Konfliktdatensätze auf dem Abonnenten gespeichert werden, der den Konflikt verursacht hat:<br /><br /> **0** = die Konfliktdatensätze werden auf dem Abonnenten nicht gespeichert.<br /><br /> **1** = die Konfliktdatensätze werden auf dem Abonnenten gespeichert.|  
|**generation_leveling_threshold**|**int**|Gibt die Anzahl der Änderungen an, die in einer Generierung enthalten sind. Eine Generierung ist eine Auflistung von Änderungen, die an einen Verleger oder Abonnenten übermittelt werden.|  
|**automatic_reinitialization_policy**|**bit**|Gibt an, ob Änderungen vom Abonnenten vor einer automatischen erneuten Initialisierung hochgeladen werden.<br /><br /> **1** = Änderungen werden vor einer automatischen neuinitialisierung vom Abonnenten hochgeladen.<br /><br /> **0** = Änderungen werden vor einer automatischen neuinitialisierung nicht hochgeladen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Sp_addmergepublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [Sp_helpmergepublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)  
  
  
