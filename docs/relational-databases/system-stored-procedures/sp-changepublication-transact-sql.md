---
title: Sp_changepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
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
- sp_changepublication
- sp_changepublication_TSQL
helpviewer_keywords:
- sp_changepublication
ms.assetid: c36e5865-25d5-42b7-b045-dc5036225081
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6b7f1c4b8c6075c322944a57f81a04a8a1763fa9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spchangepublication-transact-sql"></a>sp_changepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Eigenschaften einer Veröffentlichung. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_changepublication [ [ @publication = ] 'publication' ]  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication =** ] **'***publication***'**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@property =** ] **"***Eigenschaft***"**  
 Der Name der zu ändernden Veröffentlichungseigenschaft. *Eigenschaft* ist **nvarchar(255)**.  
  
 [  **@value =** ] **"***Wert***"**  
 Der neue Eigenschaftswert. *Wert* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
 Diese Tabelle beschreibt die änderbaren Eigenschaften der Veröffentlichung sowie die Einschränkungen für die Werte dieser Eigenschaften.  
  
|Eigenschaft|Wert|Description|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|Für die angegebene Veröffentlichung anonyme Abonnements erstellt werden und *Immediate_sync* zudem muss **"true"**. Kann für Peer-zu-Peer-Veröffentlichungen nicht geändert werden.|  
||**false**|Anonyme Abonnements können für die Veröffentlichung nicht erstellt werden. Kann für Peer-zu-Peer-Veröffentlichungen nicht geändert werden.|  
|**allow_initialize_from_backup**|**true**|Abonnenten können ein Abonnement für diese Veröffentlichung aus einer Sicherung statt aus einer Anfangsmomentaufnahme initialisieren. Diese Eigenschaft kann nicht geändert werden, für nicht -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Veröffentlichungen.|  
||**false**|Abonnenten müssen die Anfangsmomentaufnahme verwenden. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
|**allow_partition_switch**|**true**|ALTER TABLE…SWITCH-Anweisungen können für die veröffentlichte Datenbank ausgeführt werden. Weitere Informationen finden Sie unter [Replicate Partitioned Tables and Indexes](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
||**false**|ALTER TABLE…SWITCH-Anweisungen können nicht für die veröffentlichte Datenbank ausgeführt werden.|  
|**allow_pull**|**true**|Pullabonnements sind für die angegebene Veröffentlichung zulässig. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
||**false**|Pullabonnements sind für die angegebene Veröffentlichung nicht zulässig. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
|**allow_push**|**true**|Pushabonnements sind für die angegebene Veröffentlichung zulässig.|  
||**false**|Pushabonnements sind für die angegebene Veröffentlichung nicht zulässig.|  
|**allow_subscription_copy**|**true**|Aktiviert die Möglichkeit zum Kopieren von Datenbanken, die diese Veröffentlichung abonnieren. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
||**false**|Deaktiviert die Möglichkeit zum Kopieren von Datenbanken, die diese Veröffentlichung abonnieren. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
|**alt_snapshot_folder**||Der Speicherort des alternativen Ordners für die Momentaufnahme.|  
|**centralized_conflicts**|**true**|Die Konfliktdatensätze werden auf dem Verleger gespeichert. Kann nur geändert werden, wenn keine aktiven Abonnements vorhanden sind. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
||**false**|Die Konfliktdatensätze werden auf dem Verleger und auf dem Abonnenten gespeichert, der den Konflikt verursacht hat. Kann nur geändert werden, wenn keine aktiven Abonnements vorhanden sind. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
|**compress_snapshot**|**true**|Die Momentaufnahme in einem alternativen Momentaufnahmeordner wird in das CAB-Dateiformat komprimiert. Die Momentaufnahme im Standard-Momentaufnahmeordner kann nicht komprimiert werden.|  
||**false**|Die Momentaufnahme wird nicht komprimiert. Dies ist das Standardverhalten für die Replikation.|  
|**conflict_policy**|**Pub wins**|Richtlinie zur Konfliktlösung für Updateabonnenten, bei der der Verleger den Konflikt gewinnt. Diese Eigenschaft kann nur geändert werden, wenn keine aktiven Abonnements vorhanden sind. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
||**Sub reinit**|Wenn für Updateabonnenten ein Konflikt auftritt, muss das Abonnement erneut initialisiert werden. Diese Eigenschaft kann nur geändert werden, wenn keine aktiven Abonnements vorhanden sind. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
||**Sub wins**|Richtlinie zur Konfliktlösung für Updateabonnenten, bei der der Abonnent den Konflikt gewinnt. Diese Eigenschaft kann nur geändert werden, wenn keine aktiven Abonnements vorhanden sind. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|**conflict_retention**||**Int** , der die Konfliktaufbewahrungsdauer in Tagen angibt. Die Standardaufbewahrungsdauer beträgt 14 Tage. **0** bedeutet, dass kein konfliktcleanup notwendig ist. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|**description**||Eine optionale Beschreibung der Veröffentlichung.|  
|**enabled_for_het_sub**|**true**|Aktiviert die Unterstützung von Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten durch die Veröffentlichung. **Enabled_for_het_sub** kann nicht geändert werden, wenn Abonnements für die Veröffentlichung vorhanden sind. Müssen Sie möglicherweise ausführen [gespeicherte Replikationsprozeduren (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) zur Einhaltung der folgenden Anforderungen vor der Einstellung **Enabled_for_het_sub** auf "true":<br /> - **Allow_queued_tran** muss **"false"**.<br /> - **Allow_sync_tran** muss **"false"**.<br /> Ändern von **Enabled_for_het_sub** auf **"true"** möglicherweise vorhandene veröffentlichungseinstellungen geändert. Weitere Informationen finden Sie unter [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md). Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
||**false**|Die Veröffentlichung unterstützt Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten nicht. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
|**enabled_for_internet**|**true**|Die Veröffentlichung ist für das Internet aktiviert. FTP (File Transfer Protocol) kann dazu verwendet werden, die Momentaufnahmedateien an einen Abonnenten zu übermitteln. Die Synchronisierungsdateien für die Veröffentlichung werden im folgenden Verzeichnis abgelegt: C:\Programme\Microsoft SQL Server\MSSQL\Repldata\ftp. *Ftp_address* darf nicht NULL sein. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
||**false**|Die Veröffentlichung ist nicht für das Internet aktiviert. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
|**enabled_for_p2p**|**true**|Die Veröffentlichung unterstützt die Peer-zu-Peer-Replikation. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.<br /> Festzulegende **enabled_for_p2p** auf **"true"**, gelten die folgenden Einschränkungen:<br /> - **Allow_anonymous** muss **"false"**<br /> - **allow_dts nicht** muss **"false"**.<br /> - **Allow_initialize_from_backup** muss **"true"**<br /> - **Allow_queued_tran** muss **"false"**.<br /> - **Allow_sync_tran** muss **"false"**.<br /> - **Enabled_for_het_sub** muss **"false"**.<br /> - **Independent_agent** muss **"true"**.<br /> - **Repl_freq** muss **fortlaufende**.<br /> - **Replicate_ddl** muss **1**.|  
||**false**|Die Veröffentlichung unterstützt die Peer-zu-Peer-Replikation nicht. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
|**ftp_address**||Der Speicherort der Veröffentlichungsmomentaufnahmedateien, auf den über FTP zugegriffen werden kann. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
|**ftp_login**||Der Benutzername, mit dem eine Verbindung mit dem FTP-Dienst hergestellt wird. Der Wert ANONYMOUS ist zulässig. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
|**ftp_password**||Das Kennwort für den Benutzernamen, mit dem eine Verbindung mit dem FTP-Dienst hergestellt wird. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
|**ftp_port**||Die Nummer des Anschlusses für den FTP-Dienst des Verteilers. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
|**ftp_subdirectory**||Gibt an, in dem die momentaufnahmedateien erstellt werden, wenn die Veröffentlichung die Weitergabe von Momentaufnahmen über FTP unterstützt. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
|**immediate_sync**|**true**|Die Synchronisierungsdateien für die Veröffentlichung werden bei jeder Ausführung des Momentaufnahme-Agents erstellt oder neu erstellt. Abonnenten können die Synchronisierungsdateien unmittelbar nach der Abonnierung erhalten, wenn der Momentaufnahme-Agent vor der Abonnierung abgeschlossen wurde. Neue Abonnements rufen die neuesten Synchronisierungsdateien ab, die von der letzten Ausführung des Momentaufnahmeagents generiert wurden. *Independent_agent* zudem muss **"true"**. Finden Sie unter "Hinweise" unten für Weitere Informationen zu **Immediate_sync**.|  
||**false**|Synchronisierungsdateien werden nur erstellt, wenn neue Abonnements vorhanden sind. Abonnenten können nicht die Synchronisierungsdateien nach der Abonnierung erhalten, bis der Momentaufnahme-Agent gestartet wird und abgeschlossen wurde.|  
|**independent_agent**|**true**|Die Veröffentlichung verfügt über ihren eigenen dedizierten Verteilungs-Agent.|  
||**false**|Die Veröffentlichung verwendet einen freigegebenen Verteilungs-Agent, und jedes Paar aus Veröffentlichungsdatenbank und Abonnementdatenbank verfügt über einen freigegebenen Agent.|  
|**p2p_continue_onconflict**|**true**|Der Verteilungs-Agent setzt bei Erkennung eines Konflikts die Verarbeitung von Änderungen fort.<br /> **Vorsicht:** es wird empfohlen, dass Sie den Standardwert verwenden `FALSE`. Wenn diese Option festgelegt wird, um `TRUE`, den Verteilungs-Agent versucht, die Datenkonvergenz in der Topologie herbeizuführen, indem die konfliktverursachende Zeile von dem Knoten mit der höchsten Absender-ID angewendet Bei dieser Methode ist keine Konvergenz garantiert. Sie sollten sicherstellen, dass die Topologie nach der Erkennung eines Konflikts konsistent ist. Weitere Informationen finden Sie im Abschnitt "Konfliktbehandlung" unter [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
||**false**|Der Verteilungs-Agent beendet bei Erkennung eines Konflikts die Verarbeitung von Änderungen.|  
|**post_snapshot_script**||Gibt den Speicherort einer Skriptdatei von [!INCLUDE[tsql](../../includes/tsql-md.md)] an, die der Verteilungs-Agent ausführt, nachdem alle anderen Skripts für replizierte Objekte und Daten während der Anfangssynchronisierung angewendet wurden.|  
|**pre_snapshot_script**||Gibt den Speicherort einer Skriptdatei von [!INCLUDE[tsql](../../includes/tsql-md.md)] an, die der Verteilungs-Agent ausführt, bevor alle anderen Skripts für replizierte Objekte und Daten während der Anfangssynchronisierung angewendet wurden.|  
|**publish_to_ActiveDirectory**|**true**|Dieser Parameter wurde als veraltet markiert und wird nur zum Sicherstellen der Abwärtskompatibilität von Skripts unterstützt. Für [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory ist das Hinzufügen von Veröffentlichungsinformationen nicht länger möglich.|  
||**false**|Entfernt die Veröffentlichungsinformationen aus Active Directory.|  
|**queue_type**|**sql**|Verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Speichern von Transaktionen. Diese Eigenschaft kann nur geändert werden, wenn keine aktiven Abonnements vorhanden sind.<br /><br /> Hinweis: Unterstützung für die Verwendung von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing wurde eingestellt. Angeben des Werts **Msmq** für *Wert* führt zu einem Fehler.|  
|**repl_freq**|**Fortlaufende**|Veröffentlicht die Ausgabe aller protokollbasierten Transaktionen.|  
||**Momentaufnahme**|Veröffentlicht nur geplante Synchronisierungsereignisse.|  
|**replicate_ddl**|**1**|Auf dem Verleger ausgeführte Anweisungen der Datendefinitionssprache (DDL, Data Definition Language) werden repliziert. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden.|  
||**0**|DDL-Anweisungen werden nicht repliziert. Diese Eigenschaft kann für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Veröffentlichungen nicht geändert werden. Die Replikation von Schemaänderungen kann nicht deaktiviert werden, wenn Peer-zu-Peer-Replikation verwendet wird.|  
|**replicate_partition_switch**|**true**|ALTER TABLE…SWITCH-Anweisungen, die für die veröffentlichte Datenbank ausgeführt werden, sollten auf Abonnenten repliziert werden. Diese Option gilt nur, wenn *Allow_partition_switch* auf "true" festgelegt ist. Weitere Informationen finden Sie unter [Replicate Partitioned Tables and Indexes](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
||**false**|ALTER TABLE…SWITCH-Anweisungen sollten nicht auf Abonnenten repliziert werden.|  
|**Beibehaltungsdauer**||**Int** , die Beibehaltungsdauer in Stunden für Abonnementaktivitäten darstellt. Wenn ein Abonnement innerhalb der Beibehaltungsdauer nicht aktiv ist, wird es entfernt.|  
|**snapshot_in_defaultfolder**|**true**|Momentaufnahmedateien werden im Standardmomentaufnahmeordner gespeichert. Wenn *Alt_snapshot_folder*ebenfalls angegeben wird, werden momentaufnahmedateien in der Standardeinstellung und der alternativen Speicherorten gespeichert.|  
||**false**|Momentaufnahmedateien am alternativen Speicherort vom angegebenen gespeichert sind *Alt_snapshot_folder*.|  
|**status**|**Aktive**|Veröffentlichungsdaten sind für Abonnenten sofort beim Erstellen der Veröffentlichung verfügbar. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
||**Inaktive**|Veröffentlichungsdaten sind für Abonnenten nicht beim Erstellen der Veröffentlichung verfügbar. Diese Option wird für Oracle-Verleger nicht unterstützt.|  
|**sync_method**|**native**|Verwendet beim Synchronisieren von Abonnements eine Massenkopierausgabe aller Tabellen im einheitlichen Modus.|  
||**character**|Verwendet beim Synchronisieren von Abonnements eine Massenkopierausgabe aller Tabellen im Zeichenmodus.|  
||**gleichzeitige**|Verwendet eine Massenkopierprogramm-Ausgabe aller Tabellen im einheitlichen Modus, sperrt jedoch die Tabellen beim Generieren der Momentaufnahme nicht. Nicht für die Momentaufnahmereplikation gültig.|  
||**' concurrent_c '**|Verwendet eine Massenkopierprogramm-Ausgabe aller Tabellen im Zeichenmodus, sperrt jedoch die Tabellen beim Generieren der Momentaufnahme nicht. Nicht für die Momentaufnahmereplikation gültig.|  
|**Aufgaben-ID**||Diese Eigenschaft wurde als veraltet markiert und wird nicht mehr unterstützt.|  
|**allow_drop**|**true**|Ermöglicht `DROP TABLE` DLL-Unterstützung für Artikel, die Teil einer Transaktionsreplikation sind. Unterstützte Mindestversion: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2 oder höher und [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Service Pack 1 oder höher. Zusätzliche Referenz: [3170123 KB](https://support.microsoft.com/en-us/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactional-replication-in-sql-server-2014-or-in-sql-server-2016-sp1)|
||**false**|Deaktiviert die `DROP TABLE` DLL-Unterstützung für Artikel, die Teil der Transaktionsreplikation sind. Dies ist die **Standardwert** Wert für diese Eigenschaft.|
|**NULL** (Standard)||Gibt die Liste der unterstützten Werte für *Eigenschaft*.|  
  
[  **@force_invalidate_snapshot =** ] *Force_invalidate_snapshot*  
 Bestätigt, dass durch die von dieser gespeicherten Prozedur ausgeführte Aktion möglicherweise eine vorhandene Momentaufnahme ungültig wird. *Force_invalidate_snapshot* ist ein **Bit**, hat den Standardwert **0**.  
  - **0** gibt an, dass Änderungen am Artikel bewirken nicht, die Momentaufnahme ungültig wird. Wenn die gespeicherte Prozedur erkennt, dass die Änderungen eine neue Momentaufnahme erfordern, tritt ein Fehler auf und es werden keine Änderungen vorgenommen.  
  - **1** gibt an, dass Änderungen am Artikel bewirken, dass die Momentaufnahme ungültig werden können. Wenn Abonnements vorhanden sind, die eine neue Momentaufnahme erfordern würden, wird mit diesem Wert die Berechtigung erteilt, die vorhandene Momentaufnahme als veraltet zu markieren und eine neue Momentaufnahme zu generieren.   
Weitere Informationen zu den Eigenschaften, bei deren Änderung die Generierung einer neuen Momentaufnahme erforderlich ist, finden Sie im Abschnitt "Hinweise".  
  
[ **@force_reinit_subscription =** ] *Force_reinit_subscription*  
 Bestätigt, dass die von dieser gespeicherten Prozedur ausgeführte Aktion die erneute Initialisierung vorhandener Abonnements erfordern kann. *Force_reinit_subscription* ist ein **Bit** hat den Standardwert **0**.  
  - **0** gibt an, dass Änderungen am Artikel nicht das Abonnement erneut initialisiert werden können. Wenn die gespeicherte Prozedur erkennt, dass die Änderung die Neuinitialisierung vorhandener Abonnements erfordert, tritt ein Fehler auf, und es werden keine Änderungen durchgeführt.  
  - **1** gibt an, dass Änderungen am Artikel bewirken, das vorhandene Abonnement erneut initialisiert werden dass, und die Berechtigung für den erneuten Initialisierung der Abonnements erteilt.  
  
[ **@publisher** = ] **'***publisher***'**  
 Gibt einen Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger an. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
  > [!NOTE]  
  >  *Publisher* sollte nicht verwendet werden, beim Ändern von Artikeleigenschaften auf einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_changepublication** wird bei Momentaufnahme- und Transaktionsreplikation verwendet.  
  
 Nach dem Ändern der folgenden Eigenschaften, müssen Sie eine neue Momentaufnahme generieren, und geben Sie einen Wert von **1** für die *Force_invalidate_snapshot* Parameter.  
-   **alt_snapshot_folder**  
-   **compress_snapshot**  
-   **enabled_for_het_sub**  
-   **ftp_address**  
-   **ftp_login**  
-   **ftp_password**  
-   **ftp_port**  
-   **ftp_subdirectory**  
-   **post_snapshot_script**  
-   **pre_snapshot_script**  
-   **snapshot_in_defaultfolder**  
-   **sync_mode**  
  
Zum Auflisten von veröffentlichungsobjekten in Active Directory mit den **Publish_to_active_directory** Parameter, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekt muss bereits in Active Directory erstellt werden.  
  
## <a name="impact-of-immediate-sync"></a>Auswirkungen von "immediate_sync"  
 Wenn immediate_sync aktiviert ist, werden alle Änderungen im Protokoll nachverfolgt, unmittelbar nachdem die anfangsmomentaufnahme generiert wird, auch wenn keine Abonnements vorhanden sind. Protokollierte Änderungen werden verwendet, wenn ein Kunde Sicherung verwendet wird, um einen neuen Peerknoten hinzufügen. Nach der Sicherung wiederhergestellt wird, wird der Peer synchronisiert, mit anderen Änderungen, die auftritt, nachdem die Sicherung erstellt wurde. Da die Befehle in der Verteilungsdatenbank nachverfolgt werden, kann die synchronisierungslogik sehen Sie sich die letzte gesicherte LSN und verwenden Sie diese als Ausgangspunkt zu wissen, dass der Befehl ist verfügbar, wenn innerhalb der maximalen Beibehaltungsdauer der Sicherung befunden hat. (Der Standardwert für die minimale Beibehaltungsdauer beträgt 0 Std. und der maximale Aufbewahrungszeitraum ist ist 24 Stunden.)  
  
 Wenn immediate_sync deaktiviert ist, werden die Änderungen beibehalten mindestens die minimale Beibehaltungsdauer und sofort für alle Transaktionen, die bereits repliziert werden bereinigt. Wenn immediate_sync deaktiviert und mit der Standardbeibehaltungsdauer konfiguriert ist, ist es wahrscheinlich, dass die erforderlichen Änderungen nach der Sicherung bereinigt wurden und dass der neue Peerknoten nicht ordnungsgemäß initialisiert wird. Die einzige Option besteht darin, die Topologie in einen inaktiven Zustand zu versetzen. Wenn Sie immediate_synch aktivieren, erhöht sich die Flexibilität. Darüber hinaus ist dies die empfohlene Einstellung für P2P-Replikationen.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_changepublication](../../relational-databases/replication/codesnippet/tsql/sp-changepublication-tra_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_changepublication**.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [Sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
