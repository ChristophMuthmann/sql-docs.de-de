---
title: "&#220;bermitteln einer Momentaufnahme &#252;ber FTP | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Momentaufnahmen [SQL Server-Replikation], FTP-Momentaufnahmen"
  - "FTP-Momentaufnahmen [SQL Server-Replikation]"
  - "Momentaufnahmereplikation [SQL Server], FTP"
ms.assetid: 99872c4f-40ce-4405-8fd4-44052d3bd827
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# &#220;bermitteln einer Momentaufnahme &#252;ber FTP
  In diesem Thema wird beschrieben, wie in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]eine Momentaufnahme über FTP bereitgestellt wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Sicherheit](#Security)  
  
-   **So übermitteln Sie eine Momentaufnahme über FTP mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Der Momentaufnahme-Agent muss Schreibberechtigungen für das angegebene Verzeichnis und der Verteilungs-Agent oder Merge-Agent muss Leseberechtigungen besitzen. Wenn Pullabonnements verwendet werden, geben Sie ein freigegebenes Verzeichnis als ein Pfad universal naming Convention (UNC), wie z. B. \\\ftpserver\home\snapshots. Weitere Informationen finden Sie unter [Sichern des Momentaufnahmeordners](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Zum Übertragen von Momentaufnahmedateien über FTP (File Transfer Protocol) müssen Sie zuerst einen FTP-Server konfigurieren. Weitere Informationen finden Sie in der Dokumentation zu den [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internetinformationsdiensten (IIS).  
  
###  <a name="Security"></a> Sicherheit  
 Implementieren Sie ein virtuelles privates Netzwerk (VPN), wenn Sie FTP-Momentaufnahmeübermittlung über das Internet verwenden, um die Sicherheit zu verbessern. Weitere Informationen finden Sie unter [Veröffentlichen von Daten über das Internet mithilfe von VPN](../../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md).  
  
 Lassen Sie als bewährte Sicherheitsmethode keine anonymen Anmeldungen am FTP-Server zu. Der Momentaufnahme-Agent muss Schreibberechtigungen für das angegebene Verzeichnis und der Verteilungs-Agent oder Merge-Agent muss Leseberechtigungen besitzen. Wenn Pullabonnements verwendet werden, geben Sie ein freigegebenes Verzeichnis als ein Pfad universal naming Convention (UNC), wie z. B. \\\ftpserver\home\snapshots. Weitere Informationen finden Sie unter [Sichern des Momentaufnahmeordners](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
 Die Benutzer sollten nach Möglichkeit während der Laufzeit zur Eingabe von Anmeldeinformationen aufgefordert werden. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden, müssen Sie sicherstellen, dass die Datei geschützt ist.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Nach der FTP-Server konfiguriert ist, geben Sie die Verzeichnis- und Sicherheitsdienste Informationen für diesen Server in der **Veröffentlichungseigenschaften \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So geben Sie FTP-Informationen an  
  
1.  In der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Wählen Sie im Dialogfeld **ermöglichen Abonnenten das Herunterladen von momentaufnahmedateien über FTP von** aus den folgenden Seiten:  
  
    -   Der Seite **FTP-Momentaufnahme** , für Momentaufnahme- und Transaktionsveröffentlichungen und für Mergeveröffentlichungen bei Verlegern, auf denen niedrigere Versionen als [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]ausgeführt werden.  
  
    -   Der Seite **FTP-Momentaufnahme und Internet** , für Mergeveröffentlichungen von Verlegern, auf denen [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder höher ausgeführt wird.  
  
2.  Geben Sie Werte für **FTP-Servername**, **Portnummer**, **Pfad des FTP-Stammordners**, **Anmeldename**und **Kennwort**an.  
  
     Wenn der FTP-Stammordner ist z. B. \\\ftpserver\home, und Sie möchten Sie Snapshots an gespeichert werden \\\ftpserver\home\snapshots, geben Sie \snapshots\ftp für die Eigenschaft **Pfad des FTP-Stammordners** (Replikation Anhängen 'ftp' an den Pfad für den Snapshotordner beim Erstellen von Snapshot-Dateien).  
  
3.  Geben Sie an, dass der Momentaufnahme-Agent die Momentaufnahmedateien in das in Schritt 2 angegebene Verzeichnis schreiben soll. Beispielsweise schreiben Agent haben Sie die Momentaufnahme die Snapshotdateien \\\ftpserver\home\snapshots\ftp, geben Sie den Pfad \\\ftpserver\home\snapshots an zwei Stellen:  
  
    -   Dem Standardspeicherort für Momentaufnahmen für den Verteiler, dem diese Veröffentlichung zugeordnet ist.  
  
         Weitere Informationen zum Angeben des Standardspeicherorts für Momentaufnahmen finden Sie unter [Geben Sie den Standard-Snapshotspeicherort & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md).  
  
    -   Einem alternativen Speicherort für den Momentaufnahmeordner für diese Veröffentlichung. Ein alternativer Speicherort ist erforderlich, wenn die Momentaufnahme komprimiert wird.  
  
         Geben Sie den Pfad in die **Kopieren Sie die Dateien im folgenden Ordner** Textfeld auf der Seite Momentaufnahme der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zu alternativen Speicherorten für Momentaufnahmeordner finden Sie unter [Alternate Snapshot Folder Locations](../../../relational-databases/replication/alternate-snapshot-folder-locations.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Die Option, Momentaufnahmedateien auf einem FTP-Server verfügbar zu machen, und die entsprechenden FTP-Einstellungen können mithilfe gespeicherter Replikationsprozeduren programmgesteuert festgelegt und geändert werden. Welche Prozedur verwendet wird, hängt vom Typ der Veröffentlichung ab. FTP-Momentaufnahmeübermittlung wird nur bei Pullabonnements verwendet.  
  
#### So aktivieren Sie die FTP-Momentaufnahmeübermittlung für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md). Geben Sie **@publication**, ein Wert von **true** für **@enabled_for_internet**, und die entsprechenden Werte für die folgenden Parameter:  
  
    -   **@ftp_address** -die Adresse des FTP-Server verwendet, um die Übermittlung der Momentaufnahme.  
  
    -   (Optional) **@ftp_port** -der vom FTP-Server verwendete Port.  
  
    -   (Optional) **@ftp_subdirectory** -Unterverzeichnis des einer FTP-Anmeldung zugewiesenen Standard-FTP-Verzeichnisses. Beispielsweise, wenn der FTP-Stammordner ist \\\ftpserver\home, und Sie möchten Sie Snapshots an gespeichert werden \\\ftpserver\home\snapshots, geben Sie **\snapshots\ftp** für **@ftp_subdirectory** (Replikation Anhängen 'ftp' an den Pfad für den Snapshotordner beim Erstellen von Snapshot-Dateien).  
  
    -   (Optional) **@ftp_login** -Anmeldekonto, das beim Verbinden mit dem FTP-Server verwendet.  
  
    -   (Optional) **@ftp_password** -das Kennwort für die FTP-Anmeldung.  
  
     Dadurch wird eine Veröffentlichung erstellt, die FTP verwendet. Weitere Informationen finden Sie unter [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### So aktivieren Sie die FTP-Momentaufnahmeübermittlung für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Geben Sie **@publication**, ein Wert von **true** für **@enabled_for_internet** und die entsprechenden Werte für die folgenden Parameter:  
  
    -   **@ftp_address** -die Adresse des FTP-Server verwendet, um die Übermittlung der Momentaufnahme.  
  
    -   (Optional) **@ftp_port** -der vom FTP-Server verwendete Port.  
  
    -   (Optional) **@ftp_subdirectory** -Unterverzeichnis des einer FTP-Anmeldung zugewiesenen Standard-FTP-Verzeichnisses. Beispielsweise, wenn der FTP-Stammordner ist \\\ftpserver\home, und Sie möchten Sie Snapshots an gespeichert werden \\\ftpserver\home\snapshots, geben Sie **\snapshots\ftp** für **@ftp_subdirectory** (Replikation Anhängen 'ftp' an den Pfad für den Snapshotordner beim Erstellen von Snapshot-Dateien).  
  
    -   (Optional) **@ftp_login** -Anmeldekonto, das beim Verbinden mit dem FTP-Server verwendet.  
  
    -   (Optional) **@ftp_password** -das Kennwort für die FTP-Anmeldung.  
  
     Dadurch wird eine Veröffentlichung erstellt, die FTP verwendet. Weitere Informationen finden Sie unter [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### So erstellen Sie ein Pullabonnement für eine Momentaufnahme- oder Transaktionsveröffentlichung, die FTP-Snapshotübermittlung verwendet  
  
1.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Geben Sie **@publisher** und **@publication**an.  
  
    -   Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Geben Sie **@publisher**, **@publisher_db**, **@publication**, der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Anmeldeinformationen, unter dem der Verteilungsagent auf dem Abonnenten ausgeführt, für wird **@job_login** und **@job_password**, und der Wert **true** für **@use_ftp**.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) das Pullabonnement zu registrieren. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
#### So erstellen Sie ein Pullabonnement für eine Mergeveröffentlichung, die FTP-Momentaufnahmeübermittlung verwendet  
  
1.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Geben Sie **@publisher** und **@publication**an.  
  
2.  Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md). Geben Sie **@publisher**, **@publisher_db**, **@publication**, unter dem der Verteilungsagent auf dem Abonnenten ausgeführt, für wird, die Windows-Anmeldeinformationen **@job_login** und **@job_password**, und der Wert **true** für **@use_ftp**.  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) das Pullabonnement zu registrieren. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
#### So ändern Sie eine oder mehrere Einstellungen der FTP-Momentaufnahmeübermittlung für eine Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md). Geben Sie einen der folgenden Werte für **@property** und einen neuen Wert für diese Einstellung für **@value**an:  
  
    -   **Ftp_address** -die Adresse des FTP-Server verwendet, um die Übermittlung der Momentaufnahme.  
  
    -   **Ftp_port** -der vom FTP-Server verwendete Port.  
  
    -   **Ftp_subdirectory** -Unterverzeichnis des Standard-FTP-Verzeichnisses für FTP-Momentaufnahme.  
  
    -   **Ftp_login** -eine Anmeldung zum Verbinden mit dem FTP-Server verwendet.  
  
    -   **Ftp_password** -das Kennwort für die FTP-Anmeldung.  
  
2.  (Optional) Wiederholen Sie Schritt 1 für jede zu ändernde FTP-Einstellung.  
  
3.  (Optional) Um die FTP-momentaufnahmeübermittlung zu deaktivieren, führen Sie [Sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Geben Sie den Wert **Enabled_for_internet** für **@property** und einem Wert von **false** für **@value**.  
  
#### So ändern Sie die Einstellungen der FTP-Momentaufnahmeübermittlung für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Geben Sie einen der folgenden Werte für **@property** und einen neuen Wert für diese Einstellung für **@value**an:  
  
    -   **Ftp_address** -die Adresse des FTP-Server verwendet, um die Übermittlung der Momentaufnahme.  
  
    -   **Ftp_port** -der vom FTP-Server verwendete Port.  
  
    -   **Ftp_subdirectory** -Unterverzeichnis des Standard-FTP-Verzeichnisses für FTP-Momentaufnahme.  
  
    -   **Ftp_login** -eine Anmeldung zum Verbinden mit dem FTP-Server verwendet.  
  
    -   **Ftp_password** -das Kennwort für die FTP-Anmeldung.  
  
2.  (Optional) Wiederholen Sie Schritt 1 für jede zu ändernde FTP-Einstellung.  
  
3.  (Optional) Um die FTP-momentaufnahmeübermittlung zu deaktivieren, führen Sie [Sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Geben Sie den Wert **Enabled_for_internet** für **@property** und einem Wert von **false** für **@value**.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 Im folgenden Beispiel wird eine Mergeveröffentlichung erstellt, die Abonnenten ermöglicht, über FTP auf die Momentaufnahmedaten zuzugreifen. Beim Zugreifen auf die FTP-Freigabe sollte der Abonnent eine sichere VPN-Verbindung verwenden. **sqlcmd** -Skriptvariablen werden verwendet, um Anmelde- und Kennwortwerte anzugeben. Weitere Informationen finden Sie unter [Verwenden von Sqlcmd mit Skriptvariablen](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md).  
  
 [!code-sql[HowTo#sp_createmergepub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_1.sql)]  
  
 Im folgenden Beispiel wird ein Abonnement für eine Mergeveröffentlichung erstellt, bei dem der Abonnent die Momentaufnahme über FTP abruft. Beim Zugreifen auf die FTP-Freigabe sollte der Abonnent eine sichere VPN-Verbindung verwenden. **sqlcmd** -Skriptvariablen werden verwendet, um Anmelde- und Kennwortwerte anzugeben. Weitere Informationen finden Sie unter [Verwenden von Sqlcmd mit Skriptvariablen](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md).  
  
 [!code-sql[HowTo#sp_createmergepullsub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_2.sql)]  
  
 [!code-sql[HowTo#sp_createmergepullsubagent_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_3.sql)]  
  
## Siehe auch  
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Übertragen von Momentaufnahmen über FTP](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  