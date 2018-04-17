---
title: Sp_addmergepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_addmergepublication
- sp_addmergepublication_TSQL
helpviewer_keywords:
- sp_addmergepublication
ms.assetid: 28a629a1-7374-4614-9b04-279d290a942a
caps.latest.revision: 72
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 350bb858beee315e45a63cb5d72ab05f45d70848
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spaddmergepublication-transact-sql"></a>sp_addmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine neue Mergeveröffentlichung. Diese gespeicherte Prozedur wird auf Verlegerebene für die Datenbank ausgeführt, die veröffentlicht wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addmergepublication [ @publication = ] 'publication'   
    [ , [ @description = ] 'description'   
    [ , [ @retention = ] retention ]   
    [ , [ @sync_mode = ] 'sync_mode' ]   
    [ , [ @allow_push = ] 'allow_push' ]   
    [ , [ @allow_pull = ] 'allow_pull' ]   
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]   
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]   
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @dynamic_filters = ] 'dynamic_filters' ]   
    [ , [ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder' ]   
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @pre_snapshot_script = ] 'pre_snapshot_script' ]   
    [ , [ @post_snapshot_script = ] 'post_snapshot_script' ]   
    [ , [ @compress_snapshot = ] 'compress_snapshot' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]   
    [ , [ @conflict_retention = ] conflict_retention ]   
    [ , [ @keep_partition_changes = ] 'keep_partition_changes' ]   
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]   
    [ , [ @allow_synctoalternate = ] 'allow_synctoalternate' ]   
    [ , [ @validate_subscriber_info = ] 'validate_subscriber_info' ]   
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]   
    [ , [ @max_concurrent_merge = ] maximum_concurrent_merge ]   
    [ , [ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots ]  
    [ , [ @use_partition_groups = ] 'use_partition_groups' ]  
    [ , [ @publication_compatibility_level = ] 'backward_comp_level' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot' ]   
    [ , [ @allow_web_synchronization = ] 'allow_web_synchronization' ]   
    [ , [ @web_synchronization_url = ] 'web_synchronization_url' ]  
    [ , [ @allow_partition_realignment = ] 'allow_partition_realignment' ]  
    [ , [ @retention_period_unit = ] 'retention_period_unit' ]  
    [ , [ @generation_leveling_threshold = ] generation_leveling_threshold ]  
    [ , [ @automatic_reinitialization_policy = ] automatic_reinitialization_policy ]  
    [ , [ @conflict_logging = ] 'conflict_logging' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication =** ] **'***publication***'**  
 Der Name der Mergeveröffentlichung, die erstellt werden soll. *Veröffentlichung* ist **Sysname**und hat keinen Standardwert und darf nicht das Schlüsselwort alle. Der Name der Veröffentlichung muss innerhalb der Datenbank eindeutig sein.  
  
 [ **@description =** ] **'***description***'**  
 Ist die Beschreibung der Veröffentlichung. *Beschreibung* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
 [  **@retention =** ] *Aufbewahrung*  
 Ist die Beibehaltungsdauer in Aufbewahrung Zeitraumeinheiten für das Speichern der Änderungen für den angegebenen *Veröffentlichung*. *Aufbewahrung* ist **Int**, hat den Standardwert 14 Einheiten. Einheiten für die Beibehaltungsdauer werden definiert, indem *Retention_period_unit*. Wenn das Abonnement nicht innerhalb der Beibehaltungsdauer synchronisiert wird und die ausstehenden Änderungen von einem Cleanupvorgang auf dem Verteiler entfernt wurden, läuft das Abonnement ab und muss erneut initialisiert werden. Die maximal zulässige Beibehaltungsdauer ist die Anzahl von Tagen zwischen dem 31. Dezember 9999 und dem aktuellen Datum.  
  
> [!NOTE]  
>  Für die Beibehaltungsdauer von Mergeveröffentlichungen gilt eine Kulanzfrist von 24 Stunden, um Abonnenten in verschiedenen Zeitzonen zu unterstützen. Wenn Sie beispielsweise eine Beibehaltungsdauer von einem Tag festgelegt haben, beträgt die tatsächliche Beibehaltungsdauer 48 Stunden.  
  
 [  **@sync_mode =** ] **"***Sync_mode***"**  
 Ist der Modus der Erstsynchronisierung der Abonnenten für die Veröffentlichung. *Sync_mode* ist **nvarchar(10)**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**systemeigene** (Standard)|Erstellt eine Massenkopierprogramm-Ausgabe aller Tabellen im einheitlichen Modus.|  
|**character**|Erstellt eine Massenkopierprogramm-Ausgabe aller Tabellen im Zeichenmodus. Zur Unterstützung von erforderlich [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] und nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten.|  
  
 [  **@allow_push =** ] **"***Allow_push***"**  
 Gibt an, ob für die angegebene Veröffentlichung Pushabonnements erstellt werden können. *Allow_push* ist **nvarchar(5)**, hat den Standardwert "true", womit Pushabonnements für die Veröffentlichung zulässig.  
  
 [  **@allow_pull =** ] **"***Allow_pull***"**  
 Gibt an, ob für die angegebene Veröffentlichung Pullabonnements erstellt werden können. *Allow_pull* ist **nvarchar(5)**, hat den Standardwert "true", womit Pullabonnements für die Veröffentlichung zulässig. Geben Sie "true" Unterstützung [!INCLUDE[ssEW](../../includes/ssew-md.md)] Abonnenten.  
  
 [  **@allow_anonymous =** ] **"***Allow_anonymous***"**  
 Gibt an, ob für die angegebene Veröffentlichung anonyme Abonnements erstellt werden können. *Allow_anonymous* ist **nvarchar(5)**, Standardwert ist "true", womit anonyme Abonnements für die Veröffentlichung. Zur Unterstützung [!INCLUDE[ssEW](../../includes/ssew-md.md)] -Abonnenten, die Sie angeben müssen **"true"**.  
  
 [  **@enabled_for_internet =** ] **"***Enabled_for_internet***"**  
 Gibt an, ob die Veröffentlichung für das Internet aktiviert ist, und bestimmt, ob die Momentaufnahmedateien per FTP (File Transfer Protocol) an einen Abonnenten übertragen werden können. *Enabled_for_internet* ist **nvarchar(5)**, hat den Standardwert "false". Wenn **"true"**, die Synchronisierungsdateien für die Veröffentlichung werden im Verzeichnis C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp ablegen. Der Benutzer muss das FTP-Verzeichnis erstellen. Wenn **"false"**, die Veröffentlichung ist nicht für den Internetzugriff aktiviert.  
  
 [  **@centralized_conflicts =**] **"***Centralized_conflicts***"**  
 Dieser Parameter wurde als veraltet markiert und wird nur zum Sicherstellen der Abwärtskompatibilität von Skripts unterstützt. Verwendung *Conflict_logging* um den Speicherort anzugeben, wo Konfliktdatensätze gespeichert werden.  
  
 [  **@dynamic_filters =**] **"***Dynamic_filters***"**  
 Aktiviert die Mergeveröffentlichung, um parametrisierte Zeilenfilter zu verwenden. *Dynamic_filters* ist **nvarchar(5)**, hat den Standardwert "false".  
  
> [!NOTE]  
>  Sie sollten diesen Parameter nicht angeben, sondern stattdessen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zulassen, damit automatisch festgestellt wird, ob parametrisierte Zeilenfilter verwendet werden. Wenn Sie einen Wert angeben **"true"** für *Dynamic_filters*, müssen Sie für den Artikel einen parametrisierten Zeilenfilter definieren. Weitere Informationen finden Sie unter [Definieren und Ändern eines parametrisierten Zeilenfilters für einen Mergeartikel](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
 [  **@snapshot_in_defaultfolder =** ] **"***Snapshot_in_default_folder***"**  
 Legt fest, ob die Momentaufnahmedateien im Standardordner gespeichert werden. *Snapshot_in_default_folder* ist **nvarchar(5)**, Standardwert ist "true". Wenn **"true"**, momentaufnahmedateien im Standardordner gefunden werden können. Wenn **"false"**, momentaufnahmedateien im alternativen vom angegebenen Speicherort gespeichert *Alternate_snapshot_folder*. Alternative Speicherorte können sich auf einem anderen Server, auf einem Netzlaufwerk oder auf einem Wechselmedium (z. B. CD-ROM oder Wechseldatenträger) befinden. Momentaufnahmedateien lassen sich auch auf einer FTP-Site (File Transfer Protocol) speichern, um zu einem späteren Zeitpunkt vom Abonnenten abgerufen zu werden. Beachten Sie, dass dieser Parameter kann "true" sein und dennoch fehlgeschlagene vom angegebenen Speicherort *Alt_snapshot_folder*. Diese Kombination gibt an, dass die Momentaufnahmedateien sowohl im Standardpfad als auch im alternativen Pfad gespeichert werden.  
  
 [  **@alt_snapshot_folder =** ] **"***Alternate_snapshot_folder***"**  
 Gibt den Speicherort des anderen Ordners für die Momentaufnahme an. *Alternate_snapshot_folder* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
 [  **@pre_snapshot_script =** ] **"***Pre_snapshot_script***"**  
 Gibt einen Zeiger auf eine **.sql** Dateispeicherort. *Pre_snapshot_script* ist **nvarchar(255)**, hat den Standardwert NULL. Der Merge-Agent führt pre_snapshot_script vor allen Skripts für replizierte Objekte aus, wenn die Momentaufnahme auf einem Abonnenten angewendet wird. Das Skript wird in dem Sicherheitskontext ausgeführt, der vom Merge-Agent beim Herstellen einer Verbindung mit der Abonnementdatenbank verwendet wird. Vor der Momentaufnahme-Skripts werden nicht ausgeführt, auf [!INCLUDE[ssEW](../../includes/ssew-md.md)] Abonnenten.  
  
 [  **@post_snapshot_script =** ] **"***Post_snapshot_script***"**  
 Gibt einen Zeiger auf eine **.sql** Dateispeicherort. *Post_snapshot_script* ist **nvarchar(255)**, hat den Standardwert NULL. Der Merge-Agent führt das nach der Momentaufnahme ausgeführte Skript aus, nachdem alle anderen Skripts und Daten für replizierte Objekte während einer Erstsynchronisierung angewendet wurden. Das Skript wird in dem Sicherheitskontext ausgeführt, der vom Merge-Agent beim Herstellen einer Verbindung mit der Abonnementdatenbank verwendet wird. Nach der Momentaufnahme-Skripts werden nicht ausgeführt, auf [!INCLUDE[ssEW](../../includes/ssew-md.md)] Abonnenten.  
  
 [  **@compress_snapshot =** ] **"***Compress_snapshot***"**  
 Gibt an, dass die Momentaufnahme, die geschrieben werden, um die **@alt_snapshot_folder** Speicherort ist in komprimiert werden soll die [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB-Format. *Compress_snapshot* ist **nvarchar(5)**, hat den Standardwert "false". **"false"** gibt an, dass die Momentaufnahme nicht komprimiert wird. **"true"** gibt an, dass die Momentaufnahme komprimiert werden. Momentaufnahmedateien, die größer als 2 GB sind, können nicht komprimiert werden. Komprimierte Momentaufnahmedateien werden an der Stelle dekomprimiert, an der der Merge-Agent ausgeführt wird. Pullabonnements werden in der Regel mit komprimierten Momentaufnahmen verwendet, sodass die Dateien auf dem Abonnenten dekomprimiert werden. Die Momentaufnahme im Standardordner kann nicht komprimiert werden. Zur Unterstützung [!INCLUDE[ssEW](../../includes/ssew-md.md)] -Abonnenten, die Sie angeben müssen **"false"**.  
  
 [  **@ftp_address =** ] **"***Ftp_address***"**  
 Die Netzwerkadresse des FTP-Diensts für den Verteiler. *Ftp_address* ist **Sysname**, hat den Standardwert NULL. Gibt an, wo die veröffentlichungsmomentaufnahmedateien der Merge-Agent eines Abonnenten zum Abholen gespeichert sind. Da diese Eigenschaft für jede Veröffentlichung gespeichert wird, kann jede Veröffentlichung einen anderen haben *Ftp_address*. Die Veröffentlichung muss die Weitergabe von Momentaufnahmen über FTP unterstützen.  
  
 [  **@ftp_port=** ] *Ftp_port*  
 Die Anschlussnummer des FTP-Diensts für den Verteiler. *Ftp_port* ist **Int**, hat den Standardwert 21. Gibt an, wo die Veröffentlichungsmomentaufnahmedateien zum Abholen durch den Merge-Agent eines Abonnenten abgelegt werden. Da diese Eigenschaft für jede Veröffentlichung gespeichert wird, jede Veröffentlichung kann einen eigenen besitzen *Ftp_port*.  
  
 [  **@ftp_subdirectory =** ] **"***Ftp_subdirectory***"**  
 Gibt an, wo die Momentaufnahmedateien für den Merge-Agent des Abonnenten zum Abholen verfügbar sind, wenn die Veröffentlichung das Weitergeben von Momentaufnahmen mithilfe von FTP unterstützt. *Ftp_subdirectory* ist **nvarchar(255)**, hat den Standardwert NULL. Da diese Eigenschaft für jede Veröffentlichung gespeichert wird, jede Veröffentlichung kann einen eigenen besitzen *ftp_subdirectory* oder festlegen, dass keine Unterverzeichnisse mit einem Nullwert.  
  
 Wenn Momentaufnahmen für Veröffentlichungen vorab mit parametrisierten Filtern erstellt werden, dann muss die Datenmomentaufnahme für jede Abonnentenpartition jeweils in einem eigenen Ordner abgelegt sein. Die Verzeichnisstruktur für vorab über FTP generierte Momentaufnahmen muss der folgenden Struktur entsprechen:  
  
 *Alternate_snapshot_folder*\ftp\\*Publisher_publicationDB_publication*\\*PartitionID*.  
  
> [!NOTE]  
>  Die oben kursiv dargestellten Werte sind von den Festlegungen für die Veröffentlichung und Abonnentenpartition abhängig.  
  
 [  **@ftp_login =** ] **"***Ftp_login***"**  
 Der Benutzername, der für die Verbindung mit dem FTP-Dienst verwendet wird. *Ftp_login* ist **Sysname**, hat den Standardwert "anonymous".  
  
 [  **@ftp_password =** ] **"***Ftp_password***"**  
 Das Benutzerkennwort, mit dem eine Verbindung zum FTP-Dienst hergestellt wird. *Ftp_password* ist **Sysname**, hat den Standardwert NULL.  
  
> [!IMPORTANT]  
>  Verwenden Sie kein leeres Kennwort. Verwenden Sie ein sicheres Kennwort.  
  
 [  **@conflict_retention =** ] *Conflict_retention*  
 Gibt die Aufbewahrungsdauer in Tagen an, für die Konflikte beibehalten werden. *Conflict_retention* ist **Int**, hat den Standardwert von 14 Tagen vor dem den Konflikt Konfliktzeile aus der Konflikttabelle.  
  
 [  **@keep_partition_changes =** ] **"***Keep_partition_changes***"**  
 Gibt an, ob Partitionsänderungsoptimierungen zu aktivieren sind, wenn vorausberechnete Partitionen nicht verwendet werden können. *Keep_partition_changes* ist **nvarchar(5)**, Standardwert ist "true". **"false"** bedeutet, die Änderungen partitionieren nicht optimiert werden, und wenn Vorausberechnete Partitionen nicht verwendet werden, die an alle Abonnenten gesendeten Partitionen werden überprüft, wenn Daten in einer Partition ändern. **"true"** bedeutet, die Änderungen partitionieren optimiert werden, und nur Abonnenten, die über Zeilen in den geänderten Partitionen betroffen sind. Legen Sie bei Verwendung vorausberechneter Partitionen *Use_partition_groups* auf **"true"** und legen Sie *Keep_partition_changes* auf **"false"**. Weitere Informationen finden Sie unter [parametrisierte Filter-Leistung mit Vorausberechneten Partitionen optimieren](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
> [!NOTE]  
>  Wenn Sie einen Wert angeben **"true"** für *Keep_partition_changes*, geben Sie den Wert **1** für den Momentaufnahme-Agent-Parameter **- MaxNetworkOptimization** . Weitere Informationen zu diesem Parameter finden Sie unter [Replikationsmomentaufnahme-Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md). Informationen über das Angeben von Agentparametern finden Sie unter [Replikations-Agent-Verwaltung](../../relational-databases/replication/agents/replication-agent-administration.md).  
  
 Mit [!INCLUDE[ssEW](../../includes/ssew-md.md)] Abonnenten *Keep_partition_changes* muss festgelegt werden, auf "true", um sicherzustellen, dass Löschvorgänge ordnungsgemäß weitergegeben werden. Wenn die Einstellung auf "false" festgelegt ist, erhält der Abonnent möglicherweise mehr Zeilen als erwartet.  
  
 [  **@allow_subscription_copy=** ] **"***Allow_subscription_copy***"**  
 Aktiviert oder deaktiviert die Option zum Kopieren der Abonnementdatenbanken, die diese Veröffentlichung abonniert haben. *Allow_subscription_copy* ist **nvarchar(5)**, hat den Standardwert "false". Die Größe der kopierten Abonnementdatenbank muss weniger als 2 Gigabyte (GB) betragen.  
  
 [  **@allow_synctoalternate =** ] **"***Allow_synctoalternate***"**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@validate_subscriber_info =** ] **"***Validate_subscriber_info***"**  
 Listet die Funktionen auf, mit denen eine Abonnentenpartition der veröffentlichten Daten definiert wird, wenn parametrisierte Zeilenfilter verwendet werden. *Validate_subscriber_info* ist **nvarchar(500)**, hat den Standardwert NULL. Diese Informationen werden vom Merge-Agent verwendet, um die Abonnentenpartition zu überprüfen. Z. B. wenn [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) dient der Parameter muss in den parametrisierten Zeilenfilter `@validate_subscriber_info=N'SUSER_SNAME()'`.  
  
> [!NOTE]  
>  Sie sollten diesen Parameter nicht angeben, sondern stattdessen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zulassen, damit das Filterkriterium automatisch ermittelt wird.  
  
 [  **@add_to_active_directory =** ] **"***Add_to_active_directory***"**  
 Dieser Parameter wurde als veraltet markiert und wird nur zum Sicherstellen der Abwärtskompatibilität von Skripts unterstützt. Für [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory ist das Hinzufügen von Veröffentlichungsinformationen nicht länger möglich.  
  
 [  **@max_concurrent_merge =** ] *Maximum_concurrent_merge*  
 Die maximale Anzahl an gleichzeitigen Mergeprozessen. *Maximum_concurrent_merge* ist **Int** hat den Standardwert 0. Der Wert **0** für diese Eigenschaft bedeutet, dass es keine Beschränkung der Anzahl gleichzeitiger Mergeprozesse, die einem bestimmten Zeitpunkt ausgeführt. Diese Eigenschaft legt eine Grenze für die Anzahl von gleichzeitigen Mergeprozessen fest, die zu einem Zeitpunkt für eine Mergeveröffentlichung ausgeführt werden können. Wenn für einen Zeitpunkt eine größere Anzahl von Mergeprozessen geplant ist, als der Wert für eine Ausführung zulässt, werden die überzähligen Aufträge in eine Warteschlange gestellt, in der sie warten, bis ein aktuell ausgeführter Mergeprozess beendet wird.  
  
 [  **@max_concurrent_dynamic_snapshots =**] *Max_concurrent_dynamic_snapshots*  
 Die maximale Anzahl an Momentaufnahme-Agent-Sitzungen, die gleichzeitig ausgeführt werden können, um gefilterte Datenmomentaufnahmen für Abonnentenpartitionen zu generieren. *Maximum_concurrent_dynamic_snapshots* ist **Int** hat den Standardwert 0. Wenn **0**, besteht keine Einschränkung für die Anzahl von momentaufnahmesitzungen. Wenn zum gleichen Zeitpunkt mehr Momentaufnahmeprozesse geplant sind, als der Wert für eine Ausführung zulässt, werden die überschüssigen Aufträge in eine Warteschlange eingereiht, in der sie darauf warten, dass ein aktuell ausgeführter Momentaufnahmeprozess abgeschlossen wird.  
  
 [  **@use_partition_groups =** ] **"***Use_partition_groups***"**  
 Gibt an, dass vorausberechnete Partitionen verwendet werden sollen, um den Synchronisierungsprozess zu optimieren. *Use_partition_groups* ist **nvarchar(5)**, und kann einen der folgenden Werte:  
  
|Wert|Description|  
|-----------|-----------------|  
|**true**|Die Veröffentlichung verwendet vorausberechnete Partitionen.|  
|**false**|Die Veröffentlichung verwendet keine vorausberechneten Partitionen.|  
|Null(Default)|Die Partitionierungsstrategie wird vom System festgelegt.|  
  
 Standardmäßig werden vorausberechnete Partitionen verwendet. Um zu vermeiden, verwenden Vorausberechnete Partitionen *Use_partition_groups* muss festgelegt werden, um **"false"**. Wird NULL festgelegt, entscheidet das System, ob vorausberechnete Partitionen verwendet werden können. Wenn Vorausberechnete Partitionen nicht verwendet werden, und klicken Sie dann diesen Wert wird wirksam, **"false"** keine Fehler generiert. In solchen Fällen *Keep_partition_changes* kann festgelegt werden, um **"true"** auf eine Optimierung zu erreichen. Weitere Informationen finden Sie unter [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md) und [parametrisierte Filter Leistung mit Vorausberechnete Partitionen optimieren](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
 [  **@publication_compatibility_level =** ] *Backward_comp_level*  
 Gibt die Abwärtskompatibilität der Veröffentlichung an. *Backward_comp_level* ist **nvarchar(6)**, und kann einen der folgenden Werte:  
  
|Wert|Version|  
|-----------|-------------|  
|**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
  
 [  **@replicate_ddl =** ] *Replicate_ddl*  
 Gibt an, ob für die Veröffentlichung die Schemareplikation unterstützt wird. *Replicate_ddl* ist **Int**, hat den Standardwert 1. **1** gibt an, dass die Anweisungen des Data Definition Language (DDL) wird auf dem Verleger ausgeführte repliziert werden, und **0** gibt an, dass die DDL-Anweisungen nicht repliziert werden. Weitere Informationen finden Sie unter [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 Die *@replicate_ddl* Parameter wird berücksichtigt, wenn eine DDL-Anweisung eine Spalte hinzugefügt. Die *@replicate_ddl* Parameter wird ignoriert, wenn eine DDL-Anweisung ändert oder eine Spalte aus den folgenden Gründen löscht.  
  
-   Wenn eine Spalte gelöscht wird, muss die Sysarticlecolumns aktualisiert werden, um zu verhindern, dass neue DML-Anweisungen die gelöschte Spalte, die der Verteilungs-Agent fehlschlagen würde aufnehmen. Die *@replicate_ddl* Parameter wird ignoriert, da die Replikation immer die schemaänderung replizieren muss.  
  
-   Wenn eine Spalte geändert wird, hat sich möglicherweise der Quelldatentyp oder die NULL-Zulässigkeit geändert. Dies hat zur Folge, dass DML-Anweisungen einen Wert enthalten, der möglicherweise nicht mit der Tabelle beim Abonnenten kompatibel ist. Solche DML-Anweisungen können bewirken, dass der Verteilungs-Agent fehlschlägt. Die *@replicate_ddl* Parameter wird ignoriert, da die Replikation immer die schemaänderung replizieren muss.  
  
-   Wenn eine DDL-Anweisung eine neue Spalte hinzufügt, schließt Sysarticlecolumns nicht die neue Spalte. DML-Anweisungen versuchen nicht, Daten für die neue Spalte zu replizieren. Der Parameter wird berücksichtigt, da sowohl das Replizieren als auch das Nicht-Replizieren der DDL akzeptabel ist.  
  
 [  **@allow_subscriber_initiated_snapshot =** ] **"***Allow_subscriber_initiated_snapshot***"**  
 Gibt an, ob Abonnenten für diese Veröffentlichung den Momentaufnahmeprozess initiieren können, um die gefilterte Momentaufnahme für ihre Datenpartition zu generieren. *Allow_subscriber_initiated_snapshot* ist **nvarchar(5)**, hat den Standardwert "false". **"true"** gibt an, dass Abonnenten den momentaufnahmeprozess initiieren können.  
  
 [  **@allow_web_synchronization =** ] **"***Allow_web_synchronization***"**  
 Gibt an, ob die Veröffentlichung für die Websynchronisierung aktiviert ist. *Allow_web_synchronization* ist **nvarchar(5)**, hat den Standardwert "false". **"true"** gibt an, dass Abonnements dieser Veröffentlichung über HTTPS synchronisiert werden können. Weitere Informationen finden Sie unter [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md). Zur Unterstützung [!INCLUDE[ssEW](../../includes/ssew-md.md)] -Abonnenten, die Sie angeben müssen **"true"**.  
  
 [  **@web_synchronization_url=** ] **"***Web_synchronization_url***"**  
 Gibt den Standardwert für die Internet-URL an, die für die Websynchronisierung verwendet wird. *Web_synchronization_url ich*s **nvarchar(500)**, hat den Standardwert NULL. Definiert die Standard-Internet-URL, wenn eine nicht explizit angegeben ist [Sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) ausgeführt wird.  
  
 [  **@allow_partition_realignment =** ] **"***Allow_partition_realignment***"**  
 Bestimmt, ob Löschungen an den Abonnenten gesendet werden, wenn durch eine Änderung der Zeile auf Verlegerebene eine Änderung der zugehörigen Partition ausgelöst wird. *Allow_partition_realignment* ist **nvarchar(5)**, Standardwert ist "true". **"true"** sendet löschungen an den Abonnenten auf die Ergebnisse einer partitionsänderung widerzuspiegeln, durch das Entfernen von Daten, die nicht mehr zur Partition des Abonnenten gehört. **"false"** behält die Daten aus einer alten Partition auf dem Abonnenten, auf die Daten auf dem Verleger vorgenommene Änderungen nicht an diesen Abonnenten repliziert werden, wobei ein auf dem Abonnenten vorgenommene Änderungen an den Verleger repliziert werden. Festlegen von *Allow_partition_realignment* auf **"false"** wird verwendet, um Daten in einem Abonnement aus einer alten Partition beibehalten, wenn die Daten zu historischen Zwecken zugegriffen werden müssen.  
  
> [!NOTE]  
>  Daten, die auf dem Abonnenten verbleiben *Allow_partition_realignment* auf **"false"** behandelt werden soll, als wäre er schreibgeschützt; Dies wird jedoch vom Replikationssystem nicht erzwungen.  
  
 [  **@retention_period_unit =** ] **"***Retention_period_unit***"**  
 Gibt die Einheiten für die Aufbewahrungsdauer von *Aufbewahrung*. *Retention_period_unit* ist **nvarchar(10)**, und kann einen der folgenden Werte.  
  
|Wert|Version|  
|-----------|-------------|  
|**Tag** (Standard)|Die Beibehaltungsdauer wird in Tagen angegeben.|  
|**week**|Die Beibehaltungsdauer wird in Wochen angegeben.|  
|**month**|Die Beibehaltungsdauer wird in Monaten angegeben.|  
|**year**|Die Beibehaltungsdauer wird in Jahren angegeben.|  
  
 [  **@generation_leveling_threshold=** ] *Generation_leveling_threshold*  
 Gibt die Anzahl der Änderungen, die in einer Generierung enthalten sind. Eine Generierung ist eine Auflistung von Änderungen, die an einen Verleger oder Abonnenten übermittelt werden. *Generation_leveling_threshold* ist **Int**, Standardwert ist 1000.  
  
 [  **@automatic_reinitialization_policy =** ] *Automatic_reinitialization_policy*  
 Gibt an, ob Änderungen vom Abonnenten vor einer automatischen neuinitialisierung, die durch eine Änderung an der Veröffentlichung erforderlich, wobei der Wert hochgeladen werden **1** Zielsätzen für **@force_reinit_subscription**. *Automatic_reinitialization_policy* bit und hat den Standardwert 0. **1** bedeutet, dass Änderungen vom Abonnenten vor einer automatischen erneuten Initialisierung hochgeladen werden.  
  
> [!IMPORTANT]  
>  Wenn Sie einen parametrisierten Filter hinzufügen, löschen oder ändern, können ausstehende Änderungen auf dem Abonnenten während der erneuten Initialisierung nicht auf den Verleger hochgeladen werden. Wenn Sie ausstehende Änderungen hochladen möchten, sollten Sie vor dem Ändern des Filters alle Abonnements synchronisieren.  
  
 [  **@conflict_logging =** ] **"***Conflict_logging***"**  
 Gibt an, wo Konfliktdatensätze gespeichert werden. *Conflict_logging* ist **nvarchar(15)**, und kann einen der folgenden Werte:  
  
|Wert|Description|  
|-----------|-----------------|  
|**publisher**|Die Konfliktdatensätze werden auf dem Verleger gespeichert.|  
|**subscriber**|Die Konfliktdatensätze werden auf dem Abonnenten gespeichert, der den Konflikt verursacht hat. Nicht unterstützt für [!INCLUDE[ssEW](../../includes/ssew-md.md)] Abonnenten.|  
|**both**|Die Konfliktdatensätze werden auf dem Verleger und auf dem Abonnenten gespeichert.|  
|NULL (Standard)|Die Replikation automatisch aktiviert *Conflict_logging* auf **beide** Wenn der Wert *Backward_comp_level* ist **90RTM** und **Publisher** in allen anderen Fällen.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_addmergepublication** wird bei der Mergereplikation verwendet.  
  
 Zum Auflisten von veröffentlichungsobjekten zu Active Directory unter Verwendung der **@add_to_active_directory** Parameter, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekt muss bereits in Active Directory erstellt werden.  
  
 Wenn mehrere Veröffentlichungen vorhanden sind, die veröffentlichen, der dasselbe Datenbankobjekt nur Veröffentlichungen mit einer *Replicate_ddl* Wert **1** repliziert, ALTER TABLE, ALTER VIEW, ALTER PROCEDURE, ALTER FUNCTION und ALTER TRIGGER-DDL-Anweisungen. Eine ALTER TABLE DROP COLUMN DDL-Anweisung wird hingegen von allen Veröffentlichungen repliziert, die die gelöschte Spalte veröffentlichen.  
  
 Für [!INCLUDE[ssEW](../../includes/ssew-md.md)] -Abonnenten wird der Wert der *Alternate_snapshot_folder* wird nur verwendet, wenn der Wert der *Snapshot_in_default_folder* ist **"false"**.  
  
 Mit aktivierter DDL-Replikation (* Replicate_ddl ***= 1**) nicht replizierende-DDL für eine Veröffentlichung ändert, für die Veröffentlichung [Sp_changemergepublication &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)muss zuerst ausgeführt werden, zum Festlegen von *Replicate_ddl* auf **0**. Nachdem die nicht replizierenden DDL-Anweisungen ausgestellt wurden, **Sp_changemergepublication** erneut ausgeführt werden können, um die DDL-Replikation wieder aktivieren.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_AddMergePub](../../relational-databases/replication/codesnippet/tsql/sp-addmergepublication-t_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_addmergepublication**.  
  
## <a name="see-also"></a>Siehe auch  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [Sp_dropmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
