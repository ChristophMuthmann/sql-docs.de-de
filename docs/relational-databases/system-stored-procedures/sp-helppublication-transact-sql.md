---
title: Sp_helppublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helppublication_TSQL
- sp_helppublication
helpviewer_keywords:
- sp_helppublication
ms.assetid: e801c3f0-dcbd-4b4a-b254-949a05f63518
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9c9a1709d788ac12e927de909af3ea3a00574e90
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelppublication-transact-sql"></a>sp_helppublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu einer Veröffentlichung zurück. Für eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Veröffentlichung diese gespeicherte Prozedur auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt wird. Bei einer Veröffentlichung für Oracle wird diese gespeicherte Prozedur auf dem Verteiler für eine beliebige Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helppublication [ [ @publication = ] 'publication' ]  
    [ , [ @found=] found OUTPUT]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication =** ] **'***publication***'**  
 Entspricht dem Namen der anzuzeigenden Veröffentlichung. *Veröffentlichung* ist vom Datentyp Sysname und hat den Standardwert **%**, womit Informationen zu allen Veröffentlichungen zurückgegeben.  
  
 [  **@found =** ] **"***gefunden***"** Ausgabe  
 Ein Flag zur Angabe zurückgegebener Zeilen. *gefunden*ist **Int** und ein OUTPUT-Parameter hat den Standardwert **23456**. **1** gibt an, die Veröffentlichung gefunden wurde. **0** gibt an, die Veröffentlichung wurde nicht gefunden.  
  
 [ **@publisher** = ] **'***publisher***'**  
 Gibt einen nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger. *Publisher* ist vom Datentyp Sysname und hat den Standardwert NULL.  
  
> [!NOTE]  
>  *Publisher* sollte nicht angegeben werden, wenn Veröffentlichungsinformationen von Anfordern einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|pubid|**int**|ID für die Veröffentlichung.|  
|name|**sysname**|Name der Veröffentlichung.|  
|restricted|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|status|**tinyint**|Der aktuelle Status der Veröffentlichung.<br /><br /> **0** = inaktiv.<br /><br /> **1** = aktiv.|  
|Task (task)||Dieser Parameter wird aus Gründen der Abwärtskompatibilität verwendet.|  
|replication frequency|**tinyint**|Art der Replikationshäufigkeit:<br /><br /> **0** = transaktionsveröffentlichung<br /><br /> **1** = Momentaufnahme|  
|synchronization method|**tinyint**|Synchronisierungsmethode:<br /><br /> **0** = systemeigenes Massenkopierprogramm (**Bcp** Hilfsprogramm)<br /><br /> **1** = Massenkopieren von Zeichen<br /><br /> **3** = gleichzeitig, d., das systemeigene Massenkopieren h. (**Bcp**Dienstprogramm) wird verwendet, aber Tabellen werden während der Erstellung der Momentaufnahme nicht gesperrt.<br /><br /> **4** = Concurrent_c, dies bedeutet, dass das Massenkopieren von Zeichen wird verwendet, aber Tabellen werden während der Erstellung der Momentaufnahme nicht gesperrt.|  
|description|**nvarchar(255)**|Optionale Beschreibung für die Veröffentlichung.|  
|immediate_sync|**bit**|Gibt an, ob die Synchronisierungsdateien bei jeder Ausführung des Momentaufnahme-Agents erstellt oder neu erstellt werden.|  
|enabled_for_internet|**bit**|Gibt an, ob die Synchronisierungsdateien für die Veröffentlichung im Internet über FTP (File Transfer Protocol) oder andere Dienste bereitgestellt werden.|  
|allow_push|**bit**|Gibt an, ob Pushabonnements für die Veröffentlichung zulässig sind.|  
|allow_pull|**bit**|Gibt an, ob Pullabonnements für die Veröffentlichung zulässig sind.|  
|allow_anonymous|**bit**|Gibt an, ob anonyme Abonnements für die Veröffentlichung zulässig sind.|  
|independent_agent|**bit**|Ob ein eigenständiger Verteilungs-Agent für diese Veröffentlichung vorhanden ist.|  
|immediate_sync_ready|**bit**|Gibt an, ob der Momentaufnahme-Agent eine Momentaufnahme generiert, der zum Verwenden durch neue Abonnements bereitsteht. Dieser Parameter wird nur definiert, wenn die Veröffentlichung so festgelegt ist, dass sie immer eine Momentaufnahme für neue oder neu initialisierte Abonnements zur Verfügung hat.|  
|allow_sync_tran|**bit**|Gibt an, ob sofort aktualisierbare Abonnements für die Veröffentlichung zulässig sind.|  
|autogen_sync_procs|**bit**|Gibt an, ob gespeicherte Prozeduren automatisch generiert werden sollen, um sofort aktualisierbare Abonnements zu unterstützen.|  
|snapshot_jobid|**Binary(16)**|ID für geplanten Task.|  
|retention|**int**|Der Änderungsumfang (in Stunden), der für die angegebene Veröffentlichung eingespart werden soll.|  
|has subscription|**bit**|Gibt an, ob die Veröffentlichung über aktive Abonnements verfügt. **1** bedeutet, dass die Veröffentlichung über aktive Abonnements verfügt und **0** bedeutet, dass die Veröffentlichung keine Abonnements vorhanden sind.|  
|allow_queued_tran|**bit**|Gibt an, ob das Hinzufügen von Änderungen beim Abonnenten zu Warteschlangen, bis diese beim Verleger zugeordnet werden können, aktiviert wurde. Wenn **0**, Änderungen auf dem Abonnenten werden nicht in die Warteschlange eingereiht.|  
|snapshot_in_defaultfolder|**bit**|Gibt an, ob momentaufnahmedateien im Standardordner gespeichert werden. Wenn **0**, sind momentaufnahmedateien im alternativen vom angegebenen Speicherort gespeichert *Alternate_snapshot_folder*. Wenn **1**, momentaufnahmedateien im Standardordner gefunden werden können.|  
|alt_snapshot_folder|**nvarchar(255)**|Gibt den Speicherort des anderen Ordners für die Momentaufnahme an.|  
|pre_snapshot_script|**nvarchar(255)**|Gibt einen Zeiger auf eine **.sql** Dateispeicherort. Der Verteilungs-Agent führt das vor der Momentaufnahme ausgeführte Skript vor allen Skripts für replizierte Objekte aus, wenn die Momentaufnahme bei einem Abonnenten angewendet wird.|  
|post_snapshot_script|**nvarchar(255)**|Gibt einen Zeiger auf eine **.sql** Dateispeicherort. Der Verteilungs-Agent führt das nach der Momentaufnahme ausgeführte Skript aus, nachdem alle anderen Skripts für replizierte Objekte und Daten während der Erstsynchronisierung angewendet wurden.|  
|compress_snapshot|**bit**|Gibt an, dass die Momentaufnahme, die geschrieben wird die *Alt_snapshot_folder* Speicherort ist in komprimiert die [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB-Format. **0** gibt an, dass die Momentaufnahme nicht komprimiert wird.|  
|ftp_address|**sysname**|Die Netzwerkadresse des FTP-Diensts für den Verteiler. Gibt an, wo die Veröffentlichungsmomentaufnahmedateien für den Verteilungs-Agent oder Merge-Agent eines Abonnenten zum Abholen gespeichert sind.|  
|ftp_port|**int**|Die Portnummer des FTP-Diensts für den Verteiler.|  
|ftp_subdirectory|**nvarchar(255)**|Gibt an, wo die Momentaufnahmedateien für den Verteilungs-Agent oder Merge-Agent eines Abonnenten zum Abholen verfügbar sind, wenn die Veröffentlichung das Weitergeben von Momentaufnahmen mithilfe von FTP unterstützt.|  
|ftp_login|**sysname**|Der Benutzername, der für die Verbindung mit dem FTP-Dienst verwendet wird.|  
|allow_dts|**bit**|Gibt an, dass die Veröffentlichung Datentransformationen zulässt. **0** gibt an, dass DTS-Transformationen nicht zulässig sind.|  
|allow_subscription_copy|**bit**|Gibt an, ob die Möglichkeit zum Kopieren der Abonnementdatenbanken aktiviert wurde, die diese Veröffentlichung abonniert haben. **0** bedeutet, dass das Kopieren nicht zulässig ist.|  
|centralized_conflicts|**bit**|Gibt an, ob Konfliktdatensätze auf dem Verleger gespeichert werden:<br /><br /> **0** = die Konfliktdatensätze gespeichert werden auf dem Verleger und dem Abonnenten, die den Konflikt verursacht hat.<br /><br /> **1** = die Konfliktdatensätze auf dem Verleger gespeichert werden.|  
|conflict_retention|**int**|Gibt die Konfliktaufbewahrungsdauer in Tagen an.|  
|conflict_policy|**int**|Gibt die Richtlinie zur Konfliktlösung an, die für die Option zur verzögerten Aktualisierung über eine Warteschlange verwendet wird. Einer der folgenden Werte sind möglich:<br /><br /> **1** = der Verleger gewinnt den Konflikt.<br /><br /> **2** = der Abonnent gewinnt den Konflikt.<br /><br /> **3** = Abonnement wird erneut initialisiert.|  
|queue_type||Gibt an, welcher Wartenschlangentyp verwendet wird. Einer der folgenden Werte sind möglich:<br /><br /> **MSMQ** = verwenden [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing zum Speichern von Transaktionen.<br /><br /> **SQL** = verwenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Speichern von Transaktionen.<br /><br /> Hinweis: Unterstützung für Message Queuing wurde eingestellt.|  
|backward_comp_level||Der Datenbank-Kompatibilitätsgrad. Folgende Werte sind möglich:<br /><br /> **90** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_AD|**bit**|Gibt an, ob die Veröffentlichung in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory™ veröffentlicht wird. Der Wert **1** gibt an, dass es veröffentlicht wird, und der Wert **0** gibt an, dass sie nicht veröffentlicht wird.|  
|allow_initialize_from_backup|**bit**|Gibt an, ob Abonnenten ein Abonnement für diese Veröffentlichung über eine Sicherung anstelle einer Anfangsmomentaufnahme initialisieren können. **1** bedeutet, dass Abonnements aus einer Sicherung initialisiert werden können und **0** bedeutet, die sie nicht. Weitere Informationen finden Sie unter [Initialisieren einer Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) einen Transaktionsabonnenten ohne Momentaufnahme.|  
|replicate_ddl|**int**|Gibt an, ob für die Veröffentlichung die Schemareplikation unterstützt wird. **1** gibt an, dass die Anweisungen des Data Definition Language (DDL) wird auf dem Verleger ausgeführte repliziert werden, und **0** gibt an, dass die DDL-Anweisungen nicht repliziert werden. Weitere Informationen finden Sie unter [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).|  
|enabled_for_p2p|**int**|Gibt an, ob die Veröffentlichung in einer Peer-zu-Peer-Replikationstopologie verwendet werden kann. **1** gibt an, dass die Veröffentlichung Peer-zu-Peer-Replikation unterstützt. Weitere Informationen finden Sie unter [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
|publish_local_changes_only|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|enabled_for_het_sub|**int**|Gibt an, ob die Veröffentlichung Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten unterstützt. Der Wert **1** bedeutet, dass nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten unterstützt werden. Der Wert **0** bedeutet, dass nur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten unterstützt werden. Weitere Informationen finden Sie unter [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).|  
|enabled_for_p2p_conflictdetection|**int**|Gibt an, ob der Verteilungs-Agent Konflikte für eine Veröffentlichung erkennt, die für die Peer-zu-Peer-Replikation aktiviert ist. Der Wert **1** bedeutet, dass Konflikte erkannt werden. Weitere Informationen finden Sie unter [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|originator_id|**int**|Gibt eine ID für einen Knoten in einer Peer-zu-Peer-Topologie an. Diese ID wird für die konflikterkennung verwendet, wenn **enabled_for_p2p_conflictdetection** festgelegt ist, um **1**. Zum Anzeigen einer Liste der bereits verwendeten IDs fragen Sie die [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) -Systemtabelle ab.|  
|p2p_continue_onconflict|**int**|Gibt an, ob der Verteilungs-Agent bei Erkennung eines Konflikts die Verarbeitung von Änderungen fortsetzt. Der Wert **1** bedeutet, dass der Agent Verarbeitung von Änderungen fortsetzt.<br /><br /> **\*\* Vorsicht \* \***  es wird empfohlen, dass Sie den Standardwert verwenden **0**. Wenn diese Option festgelegt wird, um **1**, den Verteilungs-Agent versucht, die Datenkonvergenz in der Topologie herbeizuführen, indem die konfliktverursachende Zeile von dem Knoten mit der höchsten Absender-ID angewendet Bei dieser Methode ist keine Konvergenz garantiert. Sie sollten sicherstellen, dass die Topologie nach der Erkennung eines Konflikts konsistent ist. Weitere Informationen finden Sie im Abschnitt "Konfliktbehandlung" unter [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|alllow_partition_switch|**int**|Gibt an, ob ALTER TABLE…SWITCH-Anweisungen für die veröffentlichte Datenbank ausgeführt werden können. Weitere Informationen finden Sie unter [Replicate Partitioned Tables and Indexes](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
|replicate_partition_switch|**int**|Gibt an, ob ALTER TABLE…SWITCH-Anweisungen, die für die veröffentlichte Datenbank ausgeführt werden, auf Abonnenten repliziert werden sollen. Diese Option gilt nur, wenn *Allow_partition_switch* festgelegt ist, um **1**.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Sp_helppublication wird bei der Momentaufnahme- und Transaktionsreplikation verwendet.  
  
 Sp_helppublication gibt Informationen zu allen Veröffentlichungen zurück, die der Benutzer Ausführen dieser Prozedur gehören.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_helppublication](../../relational-databases/replication/codesnippet/tsql/sp-helppublication-trans_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle "Sysadmin" auf dem Verleger oder Mitglieder der Db_owner-Datenbankrolle behoben, für die Veröffentlichungsdatenbank oder der Benutzer in der veröffentlichungszugriffsliste (PAL) Sp_helppublication ausführen können.  
  
 Für einen nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger festen nur Mitglieder der Sysadmin-Serverrolle auf dem Verteiler oder Mitglied der festen Datenbankrolle "Db_owner" für die Verteilungsdatenbank oder der Benutzer in der VERÖFFENTLICHUNGSZUGRIFFSLISTE können Sp_helppublication ausführen.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [Sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
