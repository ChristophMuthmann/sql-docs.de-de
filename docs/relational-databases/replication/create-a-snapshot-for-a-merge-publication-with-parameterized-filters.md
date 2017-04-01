---
title: "Erstellen einer Momentaufnahme f&#252;r eine Mergever&#246;ffentlichung mit parametrisierten Filtern | Microsoft Docs"
ms.custom: ""
ms.date: "05/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Parametrisierte Filter [SQL Server-Replikation], Momentaufnahmen"
  - "Momentaufnahmen [SQL Server-Replikation], parametrisierte Filter und"
  - "Filter [SQL Server-Replikation], parametrisierte"
ms.assetid: 00dfb229-f1de-4d33-90b0-d7c99ab52dcb
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Erstellen einer Momentaufnahme f&#252;r eine Mergever&#246;ffentlichung mit parametrisierten Filtern
  In diesem Thema wird beschrieben, wie eine Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] oder Replikationsverwaltungsobjekten (RMO) erstellt wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
-   **So erstellen Sie eine Momentaufnahme für eine Mergeveröffentlichung unter Verwendung von parametrisierten Filtern mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replikationsverwaltungsobjekte (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Zur Erstellung einer Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern müssen Sie zunächst eine Standardmomentaufnahme (Schemamomentaufnahme) erstellen, die alle veröffentlichten Daten und die Abonnentenmetadaten für das Abonnement enthält. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md). Nachdem Sie die Schemamomentaufnahme erstellt haben, können Sie den Teil der Momentaufnahme generieren, der die abonnentenspezifische Partition der veröffentlichten Daten enthält.  
  
-   Wenn das Filtern nach einem oder mehreren Artikeln in der Veröffentlichung nicht überlappende Partitionen ergibt, die für jedes Abonnement eindeutig sind, wird für Metadaten bei jedem Ausführen des Merge-Agents einen Cleanup ausgeführt. Das bedeutet, dass die partitionierte Momentaufnahme schneller abläuft. Bei dieser Methode sollten Sie zulassen, dass Abonnenten das Generieren und Übermitteln von Momentaufnahmen einleiten. Weitere Informationen zu Filteroptionen finden Sie im Abschnitt "Festlegen von 'partition Options'" von [Momentaufnahmen für Mergeveröffentlichungen mit parametrisierten Filtern](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Generieren von Momentaufnahmen für Partitionen auf der **Datenpartitionen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md). Sie können zulassen, dass Abonnenten die Momentaufnahmegenerierung und -übermittlung starten bzw. Momentaufnahmen generieren.  
  
 Vor der Generierung von Momentaufnahmen für eine oder mehrere Partitionen müssen Sie folgende Aktionen ausführen:  
  
1.  Erstellen Sie eine Mergeveröffentlichung mit dem Assistenten für neue Veröffentlichung, und geben Sie einen oder mehrere Zeilenfilter auf der Seite **Filter hinzufügen** an. Weitere Informationen finden Sie unter [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
2.  Generieren Sie eine Schemamomentaufnahme für die Veröffentlichung. Es wird standardmäßig eine Schemamomentaufnahme generiert, sobald Sie den Assistenten für neue Veröffentlichung abschließen. Sie können auch eine Schemamomentaufnahme aus [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]generieren.  
  
#### So generieren Sie eine Schemamomentaufnahme  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Veröffentlichungen** .  
  
3.  Mit der rechten Maustaste in der Veröffentlichung für die Sie eine Momentaufnahme erstellen, und klicken Sie dann auf möchten **Snapshot-Agent-Anzeigestatus**.  
  
4.  In der **Snapshot-Agent-Status anzeigen - \< Veröffentlichung>** im Dialogfeld klicken Sie auf **Start**.  
  
     Nachdem der Momentaufnahme-Agent die Momentaufnahme generiert hat, wird eine Meldung angezeigt, die beispielsweise wie folgt lautet: "[100%] Es wurde eine Momentaufnahme mit 17 Artikel(n) generiert".  
  
#### So lassen Sie zu, dass Abonnenten die Momentaufnahmegenerierung und -übermittlung starten  
  
1.  Auf der **Datenpartitionen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Wählen Sie im Dialogfeld **automatisch eine Partition definieren und eine Momentaufnahme generieren, falls erforderlich, wenn ein neuer Abonnent zu synchronisieren versucht**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### So generieren und aktualisieren Sie Momentaufnahmen  
  
1.  Auf der **Datenpartitionen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** im Dialogfeld klicken Sie auf **Hinzufügen**.  
  
2.  Geben Sie einen Wert für die **HOST_NAME()** und/oder **SUSER_SNAME()** Integerwert für die Partition eine Momentaufnahme erstellt werden soll.  
  
3.  Optional können Sie einen Zeitplan für das Aktualisieren von Momentaufnahmen angeben:  
  
    1.  Wählen Sie **Planen der Snapshot-Agent für diese Partition zu folgenden Zeitpunkten ausführen**  
  
    2.  Akzeptieren Sie den Standardzeitplan für die Aktualisierung von Momentaufnahmen, oder klicken Sie auf **Ändern** , um einen anderen Zeitplan anzugeben.  
  
4.  Klicken Sie auf **OK**, womit Sie die **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld).  
  
5.  Wählen Sie die Partition im Eigenschaftsraster aus, und klicken Sie anschließend auf **Die ausgewählten Momentaufnahmen jetzt generieren**.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Mithilfe von gespeicherten Prozeduren und dem Momentaufnahme-Agent können Sie folgende Aktionen durchführen:  
  
-   Abonnenten das Anfordern der Momentaufnahmegenerierung und -anwendung beim erstmaligen Synchronisieren ermöglichen.  
  
-   Vorabgenerieren von Momentaufnahmen für jede Partition.  
  
-   Manuell eine Momentaufnahme für jeden Abonnenten generieren.  
  
    > [!IMPORTANT]  
    >  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
#### So erstellen Sie eine Veröffentlichung, die es Abonnenten ermöglicht, die Generierung und Übermittlung von Momentaufnahmen zu initiieren  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Geben Sie die folgenden Parameter an:  
  
    -   Den Namen der Veröffentlichung für **@publication**.  
  
    -   Der Wert **true** für **@allow_subscriber_initiated_snapshot**, die Abonnenten den momentaufnahmeprozess initiieren können.  
  
    -   (Optional) Die Anzahl der dynamischen Snapshot gleichzeitig ausgeführten Prozessen für können **@max_concurrent_dynamic_snapshots**. Wird die maximale Anzahl von Prozessen ausgeführt, wenn ein Abonnent versucht, eine Momentaufnahme zu generieren, wird der Prozess in eine Warteschlange eingefügt. Standardmäßig gibt es für die Anzahl gleichzeitig ausgeführter Prozesse keine Beschränkung.  
  
2.  Führen Sie auf dem Verleger [Sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Geben Sie den in Schritt 1 verwendeten Veröffentlichungsnamen **@publication** und die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen, unter denen der [Replikationsmomentaufnahme-Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md) ausgeführt wird, für **@job_login** und **@password**. Wenn der Agent [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung, wenn eine Verbindung mit dem Verleger herstellen, müssen Sie auch den Wert angeben **0** für **@publisher_security_mode** und [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt. Weitere Informationen darüber, wie eine Anfangsmomentaufnahme generiert und ein benutzerdefinierter Zeitplan für den Momentaufnahme-Agent definiert wird, finden Sie unter [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die angegebenen Werte für alle Parameter einschließlich *Job_login* und *Job_password*, werden als nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul & #40; SQL Server-Konfigurations-Manager & #41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
3.  Führen Sie [Sp_addmergearticle & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) zum Hinzufügen von Artikeln für die Veröffentlichung. Diese gespeicherte Prozedur muss einmal für jeden Artikel in der Veröffentlichung ausgeführt werden. Wenn Sie parametrisierte Filter verwenden, geben Sie einen parametrisierten Filter für einen oder mehrere Artikel, die mit der **@subset_filterclause** Parameter. Weitere Informationen finden Sie unter [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
4.  Wenn Sie andere Artikel basierend auf den parametrisierten Zeilenfilter gefiltert werden, führen Sie [Sp_addmergefilter & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) um den Join oder logische datensatzbeziehungen zwischen Artikeln zu definieren. Diese gespeicherte Prozedur muss einmal für jede zu definierende Beziehung ausgeführt werden. Weitere Informationen finden Sie unter [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
5.  Wenn der Merge-Agent die Momentaufnahme zur Initialisierung des Abonnenten anfordert, wird die Momentaufnahme für die anfordernde Partition des Abonnements automatisch generiert.  
  
#### So erstellen Sie eine Veröffentlichung, und generieren vorab Momentaufnahmen oder aktualisieren sie automatisch  
  
1.  Führen Sie [Sp_addmergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) um die Veröffentlichung zu erstellen. Weitere Informationen finden Sie unter [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Führen Sie auf dem Verleger [Sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Geben Sie den in Schritt 1 verwendeten Veröffentlichungsnamen **@publication** und die Windows-Anmeldeinformationen, unter denen der Snapshot-Agent ausgeführt, für die wird **@job_login** und **@password**. Wenn der Agent [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung, wenn eine Verbindung mit dem Verleger herstellen, müssen Sie auch den Wert angeben **0** für **@publisher_security_mode** und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt. Weitere Informationen darüber, wie eine Anfangsmomentaufnahme generiert und ein benutzerdefinierter Zeitplan für den Momentaufnahme-Agent definiert wird, finden Sie unter [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die angegebenen Werte für alle Parameter einschließlich *Job_login* und *Job_password*, werden als nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul & #40; SQL Server-Konfigurations-Manager & #41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
3.  Führen Sie [Sp_addmergearticle & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) zum Hinzufügen von Artikeln für die Veröffentlichung. Diese gespeicherte Prozedur muss einmal für jeden Artikel in der Veröffentlichung ausgeführt werden. Wenn Sie parametrisierte Filter verwenden, geben Sie einen parametrisierten Filter für einen Artikel mit der **@subset_filterclause** Parameter. Weitere Informationen finden Sie unter [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
4.  Wenn Sie andere Artikel basierend auf den parametrisierten Zeilenfilter gefiltert werden, führen Sie [Sp_addmergefilter & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) um den Join oder logische datensatzbeziehungen zwischen Artikeln zu definieren. Diese gespeicherte Prozedur muss einmal für jede zu definierende Beziehung ausgeführt werden. Weitere Informationen finden Sie unter [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
5.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helpmergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), der Wert für **@publication** aus Schritt 1. Beachten Sie den Wert der **Snapshot_jobid** im Ergebnis festlegen.  
  
6.  Konvertiert den Wert der **Snapshot_jobid** die in Schritt 5 **Uniqueidentifier**.  
  
7.  Auf dem Verleger für die **Msdb** Datenbank, führen Sie [Sp_start_job & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md), den konvertierten Wert in Schritt 6 für die Angabe **@job_id**.  
  
8.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergepartition & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md). Geben Sie den Namen der Veröffentlichung aus Schritt 1 für **@publication** und der Wert, der zur Definition der Partition **@suser_sname** Wenn [SUSER_SNAME & #40; Transact-SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md) wird verwendet, in der Filterklausel oder für **@host_name** Wenn [HOST_NAME & #40; Transact-SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) wird in der Filterklausel verwendet werden.  
  
9. Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_adddynamicsnapshot_job & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md). Geben Sie den Namen der Veröffentlichung aus Schritt 1 für **@publication**, den Wert der **@suser_sname** oder **@host_name** aus Schritt 8 und einen Zeitplan für den Auftrag. Dadurch wird der Auftrag erstellt, der die parametrisierte Momentaufnahme für die angegebene Partition generiert. Weitere Informationen finden Sie unter [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > [!NOTE]  
    >  Dieser Auftrag wird mit dem gleichen Windows-Konto ausgeführt wie der in Schritt 2 definierte Anfangs-Momentaufnahmeauftrag. Um den parametrisierten momentaufnahmeauftrag und seine zugehörige Datenpartition zu entfernen, führen [Sp_dropdynamicsnapshot_job & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md).  
  
10. Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helpmergepartition & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md), der Wert für **@publication** aus Schritt 1 und der Wert der **@suser_sname** oder **@host_name** aus Schritt 8. Beachten Sie den Wert der **Dynamic_snapshot_jobid** im Ergebnis festlegen.  
  
11. Auf dem Verteiler für die **Msdb** Datenbank, führen Sie [Sp_start_job & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md), der Wert abgerufen in Schritt 9 für **@job_id**. Dadurch wird der parametrisierte Momentaufnahmeauftrag für die Partition gestartet.  
  
12. Wiederholen Sie die Schritte 8 bis 11, um für jedes Abonnement eine partitionierte Momentaufnahme zu generieren.  
  
#### So erstellen Sie eine Veröffentlichung und für jede Partition manuell Momentaufnahmen  
  
1.  Führen Sie [Sp_addmergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) um die Veröffentlichung zu erstellen. Weitere Informationen finden Sie unter [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Führen Sie auf dem Verleger [Sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Geben Sie den in Schritt 1 verwendeten Veröffentlichungsnamen **@publication** und die Windows-Anmeldeinformationen, unter denen der Snapshot-Agent ausgeführt, für die wird **@job_login** und **@password**. Wenn der Agent [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung, wenn eine Verbindung mit dem Verleger herstellen, müssen Sie auch den Wert angeben **0** für **@publisher_security_mode** und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldeinformationen für **@publisher_login** und **@publisher_password**. Dadurch wird ein Auftrag des Momentaufnahme-Agents für die Veröffentlichung erstellt. Weitere Informationen darüber, wie eine Anfangsmomentaufnahme generiert und ein benutzerdefinierter Zeitplan für den Momentaufnahme-Agent definiert wird, finden Sie unter [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die angegebenen Werte für alle Parameter einschließlich *Job_login* und *Job_password*, werden als nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul & #40; SQL Server-Konfigurations-Manager & #41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
3.  Führen Sie [Sp_addmergearticle & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) zum Hinzufügen von Artikeln für die Veröffentlichung. Diese gespeicherte Prozedur muss einmal für jeden Artikel in der Veröffentlichung ausgeführt werden. Wenn Sie parametrisierte Filter verwenden, geben Sie einen parametrisierten Filter für mindestens einen Artikel mit der **@subset_filterclause** Parameter. Weitere Informationen finden Sie unter [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
4.  Wenn Sie andere Artikel basierend auf den parametrisierten Zeilenfilter gefiltert werden, führen Sie [Sp_addmergefilter & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) um den Join oder logische datensatzbeziehungen zwischen Artikeln zu definieren. Diese gespeicherte Prozedur muss einmal für jede zu definierende Beziehung ausgeführt werden. Weitere Informationen finden Sie unter [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
5.  Starten Sie den Momentaufnahmeauftrag oder führen Sie den Replikationsmomentaufnahme-Agent von der Eingabeaufforderung aus, um das Standard-Momentaufnahmeschema und andere Dateien zu erzeugen. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
6.  Führen den Replikationsmomentaufnahme-Agent erneut aus, über die Befehlszeile zum Generieren von Dateien, Angeben des Speicherorts für die partitionierte Momentaufnahme für (Massenkopierdateien) **- DynamicSnapshotLocation** und eine oder beide der folgenden Eigenschaften, die die Partition definiert:  
  
    -   **-DynamicFilterHostName** -Wert Wenn [HOST_NAME & #40; Transact-SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) wird verwendet.  
  
    -   **-DynamicFilterLogin** -Wert Wenn [SUSER_SNAME & #40; Transact-SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md) wird verwendet.  
  
7.  Wiederholen Sie Schritt 8, um für jedes Abonnement eine partitionierte Momentaufnahme zu generieren.  
  
8.  Führen Sie den Merge-Agent für jedes Abonnement aus, um die partitionierte Anfangsmomentaufnahme auf die Abonnenten anzuwenden, wobei Sie die folgenden Eigenschaften angeben:  
  
    -   **-Hostname** -der Wert verwendet, um die Partition zu definieren, wenn der tatsächliche Wert von HOST_NAME überschrieben wurde.  
  
    -   **-DynamicSnapshotLocation** – der Speicherort der dynamischen Momentaufnahme für diese Partition.  
  
> [!NOTE]  
>  Weitere Informationen über die Programmierung von Replikations-Agents finden Sie unter [Replikations-Agent ausführbare Konzepte](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
 In diesem Beispiel wird eine Mergeveröffentlichung mit parametrisierten Filtern erstellt, bei der die Abonnenten den Momentaufnahmegenerierungsprozess initiieren. Werte für **@job_login** und **@job_password** werden mithilfe von Skriptvariablen übergeben.  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_1.sql)]  
  
 Dieses Beispiel erstellt eine Veröffentlichung mit parametrisierten Filtern, in dem die Partition definiert, die durch Ausführen von verfügt jeder Abonnent [Sp_addmergepartition](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md) und der gefilterte momentaufnahmeauftrag durch Ausführung erstellt [Sp_adddynamicsnapshot_job](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md) der Partitionierungsinformationen. Werte für **@job_login** und **@job_password** werden mithilfe von Skriptvariablen übergeben.  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_2.sql)]  
  
 In diesem Beispiel wird eine Mergeveröffentlichung mit parametrisierten Filtern erstellt, bei der die Partition und der gefilterte Momentaufnahmeauftrag jedes Abonnenten durch Angabe der Partitionierungsinformationen erstellt wird. Ein Abonnent gibt die Partitionierungsinformationen mithilfe von Befehlszeilenparametern an, wenn die Replikations-Agents manuell ausgeführt werden. In diesem Beispiel wird davon ausgegangen, dass auch ein Abonnement für die Veröffentlichung erstellt wurde.  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPartitionManual](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_3.sql)]  
  
```  
  
REM Line breaks are added to improve readability.   
REM In a batch file, commands must be made in a single line.  
REM Run the Snapshot agent from the command line to generate the standard snapshot   
REM schema and other files.   
SET DistPub=%computername%  
SET PubDB=AdventureWorks2012   
SET PubName=AdvWorksSalesPersonMerge  
  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %PubName%    
-Publisher %DistPub% -Distributor  %DistPub%  -PublisherDB %PubDB%  -ReplicationType 2    
-OutputVerboseLevel 1  -DistributorSecurityMode 1  
  
PAUSE  
  
```  
  
```  
  
REM Run the Snapshot agent from the command line, this time to generate   
REM the bulk copy (.bcp) data for each Subscriber partition.    
SET DistPub=%computername%  
SET PubDB=AdventureWorks2012   
SET PubName=AdvWorksSalesPersonMerge  
SET SnapshotDir=\\%DistPub%\repldata\unc\fernando  
  
MD %SnapshotDir%  
  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %PubName%    
-Publisher %DistPub%  -Distributor  %DistPub%  -PublisherDB %PubDB%  -ReplicationType 2    
-OutputVerboseLevel 1  -DistributorSecurityMode 1  -DynamicFilterHostName "adventure-works\Fernando"    
-DynamicSnapshotLocation %SnapshotDir%  
  
PAUSE  
  
```  
  
```  
  
REM Run the Merge Agent for each subscription to apply the partitioned   
REM snapshot for each Subscriber.    
SET Publisher = %computername%  
SET Subscriber = %computername%  
SET PubDB = AdventureWorks2012   
SET SubDB = AdventureWorks2012Replica   
SET PubName = AdvWorksSalesPersonMerge   
SET SnapshotDir=\\%DistPub%\repldata\unc\fernando  
  
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE" -Publisher  %Publisher%    
-Subscriber  %Subscriber%  -Distributor %Publisher%  -PublisherDB %PubDB%    
-SubscriberDB %SubDB% -Publication %PubName%  -PublisherSecurityMode 1  -OutputVerboseLevel 3    
-Output -SubscriberSecurityMode 1  -SubscriptionType 3 -DistributorSecurityMode 1    
-Hostname "adventure-works\Fernando"  -DynamicSnapshotLocation %SnapshotDir%  
  
PAUSE  
  
```  
  
##  <a name="RMOProcedure"></a> Verwenden von Replikationsverwaltungsobjekten (RMO)  
 Sie können Replikationsverwaltungsobjekte (RMO) verwenden, um partitionierte Momentaufnahmen mit einem der folgenden Verfahren programmgesteuert zu generieren:  
  
-   Abonnenten das Anfordern der Momentaufnahmegenerierung und -anwendung beim erstmaligen Synchronisieren ermöglichen.  
  
-   Vorabgenerieren von Momentaufnahmen für jede Partition.  
  
-   Manuelles Generieren einer Momentaufnahme für jeden Abonnenten durch Ausführen des Momentaufnahme-Agent  
  
> [!NOTE]  
>  Bei der Filterung für ein Artikel nicht überlappende Partitionen, die für jedes Abonnement eindeutig sind ergibt (durch Angabe der Wert F:Microsoft.SqlServer.Replication.PartitionOptions.NonOverlappingSingleSubscription für P:Microsoft.SqlServer.Replication.MergeArticle.PartitionOption, beim Erstellen eines Mergeartikels), Metadaten bereinigt wird, wenn der Merge-Agent ausgeführt wird. Das bedeutet, dass die partitionierte Momentaufnahme schneller abläuft. Bei dieser Methode sollten Sie zulassen, dass Abonnenten das Generieren von Momentaufnahmen anfordern. Weitere Informationen finden Sie unter "Verwenden der richtigen Filteroptionen" im Thema [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
> [!IMPORTANT]  
>  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen speichern müssen, verwenden Sie die [Kryptografiedienste](http://go.microsoft.com/fwlink/?LinkId=34733) von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows .NET Framework.  
  
#### So erstellen Sie eine Veröffentlichung, die es Abonnenten ermöglicht, die Generierung und Übermittlung von Momentaufnahmen zu initiieren  
  
1.  Erstellen Sie eine Verbindung mit dem Verleger mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
2.  Erstellen Sie eine Instanz von der <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> Klasse für die Veröffentlichungsdatenbank, legen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft, um die Instanz von <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1, und rufen die <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> Methode. Wenn <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> gibt **false**, bestätigen Sie, dass die Datenbank vorhanden ist.  
  
3.  Wenn <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> Eigenschaft **false**, legen Sie es auf **true** und rufen Sie <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>.  
  
4.  Erstellen Sie eine Instanz von der <xref:Microsoft.SqlServer.Replication.MergePublication> Klasse, und legen Sie für dieses Objekt die folgenden Eigenschaften:  
  
    -   Die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus Schritt 1 für <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Der Name der veröffentlichten Datenbank für <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>.  
  
    -   Einen Namen für die Veröffentlichung für <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>.  
  
    -   Die maximale Anzahl von Aufträgen für dynamische Momentaufnahmen ausgeführt <xref:Microsoft.SqlServer.Replication.MergePublication.MaxConcurrentDynamicSnapshots%2A>. Da von Abonnenten initiierte Momentaufnahmeanforderungen jederzeit erfolgen können, begrenzt diese Eigenschaft die Anzahl der Momentaufnahme-Agentaufträge, die gleichzeitig ausgeführt werden können, wenn mehrere Abonnenten ihre partitionierte Momentaufnahme gleichzeitig anfordern. Wenn die maximale Anzahl an Aufträgen ausgeführt wird, werden weitere Anforderungen für partitionierte Momentaufnahmen in die Warteschlange eingefügt, bis einer der Aufträge abgeschlossen ist.  
  
    -   Verwenden Sie den bitweisen logischen OR (**|** in Visual c# und **oder** in Visual Basic) Operator den Wert hinzufügen <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowSubscriberInitiatedSnapshot> auf <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>.  
  
    -   Die <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> und <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> Felder <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> für die Anmeldeinformationen für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, unter dem der Snapshot-Agent-Auftrag ausgeführt wird.  
  
        > [!NOTE]  
        >  Festlegen von <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> wird empfohlen, beim Erstellen der Veröffentlichung von einem Mitglied der **Sysadmin** festen Serverrolle. Weitere Informationen finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
5.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> Methode, um die Veröffentlichung zu erstellen.  
  
    > [!IMPORTANT]  
    >  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die angegebenen Werte für alle Eigenschaften, einschließlich <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, werden als nur-Text an den Verteiler gesendet. Verschlüsseln Sie die Verbindung zwischen dem Verleger und die zugehörigen Remoteverteiler vor dem Aufruf der <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> Methode. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul & #40; SQL Server-Konfigurations-Manager & #41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
6.  Verwenden der <xref:Microsoft.SqlServer.Replication.MergeArticle> Eigenschaft, um die Veröffentlichung Artikel hinzuzufügen. Geben Sie die <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> -Eigenschaft für mindestens einen Artikel, der den parametrisierten Filter definiert. (Optional) Erstellen Sie <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> -Objekten, definieren die joinfilter zwischen Artikeln. Weitere Informationen finden Sie unter [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
7.  Wenn der Wert der <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> ist **false**, rufen Sie <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> den anfängliche Snapshot-Agent-Auftrag für diese Veröffentlichung zu erstellen.  
  
8.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> Methode der <xref:Microsoft.SqlServer.Replication.MergePublication> in Schritt 4 erstellte Objekt. Dadurch wird der Agentauftrag gestartet, der die Anfangsmomentaufnahme generiert. Weitere Informationen darüber, wie eine Anfangsmomentaufnahme generiert und ein benutzerdefinierter Zeitplan für den Momentaufnahme-Agent definiert wird, finden Sie unter [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
9. (Optional) Überprüfen Sie den Wert **true** für die <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> -Eigenschaft können Sie bestimmen, wann die anfangsmomentaufnahme zur Verfügung steht.  
  
10. Wenn der Merge-Agent eines Abonnenten die Verbindung erstmalig herstellt, wird automatisch eine partitionierte Momentaufnahme generiert.  
  
#### So erstellen Sie eine Veröffentlichung und generieren Momentaufnahmen vorab oder aktualisieren sie automatisch  
  
1.  Verwenden Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePublication> Klasse, um eine Mergeveröffentlichung zu definieren. Weitere Informationen finden Sie unter [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Verwenden der <xref:Microsoft.SqlServer.Replication.MergeArticle> Eigenschaft, um die Veröffentlichung Artikel hinzuzufügen. Geben Sie die <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> -Eigenschaft für mindestens einen Artikel, der den parametrisierten Filter definiert, und erstellen Sie beliebige <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> -Objekten, definieren die joinfilter zwischen Artikeln. Weitere Informationen finden Sie unter [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
3.  Wenn der Wert der <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> ist **false**, rufen Sie <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> der Momentaufnahme-Agentauftrag für diese Veröffentlichung zu erstellen.  
  
4.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> Methode der <xref:Microsoft.SqlServer.Replication.MergePublication> in Schritt 1 erstellte Objekt. Durch diese Methode wird der Agentauftrag gestartet, der die Anfangsmomentaufnahme generiert. Weitere Informationen darüber, wie eine Anfangsmomentaufnahme generiert und ein benutzerdefinierter Zeitplan für den Momentaufnahme-Agent definiert wird, finden Sie unter [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
5.  Überprüfen Sie den Wert **true** für die <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> -Eigenschaft können Sie bestimmen, wann die anfangsmomentaufnahme zur Verfügung steht.  
  
6.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePartition> Klasse, und legen Sie die parametrisierten Filterkriterien für den Abonnenten mit einem oder beiden der folgenden Eigenschaften:  
  
    -   Wenn die Partition des Abonnenten, durch das Ergebnis des definiert ist [SUSER_SNAME & #40; Transact-SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md), verwenden <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A>.  
  
    -   Wenn die Partition des Abonnenten, durch das Ergebnis des definiert ist [HOST_NAME & #40; Transact-SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) oder eine Überladung dieser Funktion, verwenden Sie <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A>.  
  
7.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> Klasse, und legen Sie dieselbe Eigenschaft wie in Schritt 6.  
  
8.  Verwenden der <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> Klasse, um einen Zeitplan für die Generierung der gefilterten Momentaufnahme für die Abonnentenpartition zu definieren.  
  
9. Mit der Instanz von <xref:Microsoft.SqlServer.Replication.MergePublication> Aufrufen aus Schritt 1 <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergePartition%2A>. Übergeben Sie die <xref:Microsoft.SqlServer.Replication.MergePartition> -Objekt aus Schritt 6.  
  
10. Mit der Instanz von <xref:Microsoft.SqlServer.Replication.MergePublication> aus Schritt 1, rufen Sie die <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergeDynamicSnapshotJob%2A> Methode. Übergeben Sie die <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> -Objekt aus Schritt 7 und die <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> -Objekt aus Schritt 8.  
  
11. Rufen Sie <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergeDynamicSnapshotJobs%2A>, und suchen Sie die <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> Objekt für den Auftrag neu hinzugefügten partitionierte Momentaufnahme in das zurückgegebene Array.  
  
12. Abrufen der <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob.Name%2A> Eigenschaft für den Auftrag.  
  
13. Erstellen Sie eine Verbindung mit dem Verteiler mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Klasse.  
  
14. Erstellen Sie eine Instanz von SQL Server Management Objects (SMO) <xref:Microsoft.SqlServer.Management.Smo.Server> -Klasse, die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> -Objekt aus Schritt 13.  
  
15. Erstellen Sie eine Instanz von der <xref:Microsoft.SqlServer.Management.Smo.Agent.Job> -Klasse, die <xref:Microsoft.SqlServer.Management.Smo.Server.JobServer%2A> Eigenschaft der <xref:Microsoft.SqlServer.Management.Smo.Server> -Objekt aus Schritt 14 und den auftragnamen aus Schritt 12.  
  
16. Rufen Sie die <xref:Microsoft.SqlServer.Management.Smo.Agent.Job.Start%2A> Methode, um den Auftrag für die partitionierte Momentaufnahme zu starten.  
  
17. Wiederholen Sie die Schritte 6 bis 16 für jeden Abonnenten.  
  
#### So erstellen Sie eine Veröffentlichung und für jede Partition manuell Momentaufnahmen  
  
1.  Verwenden Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.MergePublication> Klasse, um eine Mergeveröffentlichung zu definieren. Weitere Informationen finden Sie unter [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Verwenden der <xref:Microsoft.SqlServer.Replication.MergeArticle> Eigenschaft zum Hinzufügen von Artikeln für die Veröffentlichung angeben der <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> -Eigenschaft für mindestens einen Artikel, der den parametrisierten Filter definiert, und erstellen Sie beliebige <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> -Objekten, definieren die joinfilter zwischen Artikeln. Weitere Informationen finden Sie unter [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
3.  Generieren Sie die Anfangsmomentaufnahme. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
4.  Erstellen Sie eine Instanz der <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> -Klasse, und legen Sie die folgenden erforderlichen Eigenschaften fest:  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - Name des Verlegers  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - Name der Veröffentlichungsdatenbank  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - Name der Veröffentlichung  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - Name des Verteilers  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> -Wert <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> verwendet integrierte Windows-Authentifizierung oder der Wert <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> SQL Server-Authentifizierung verwenden.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> -Wert <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> verwendet integrierte Windows-Authentifizierung oder der Wert <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> SQL Server-Authentifizierung verwenden.  
  
5.  Legen Sie den Wert <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> für <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>.  
  
6.  Legen Sie eine oder mehrere der folgenden Eigenschaften fest, um die Partitionierungsparameter zu definieren:  
  
    -   Wenn die Partition des Abonnenten, durch das Ergebnis des definiert ist [SUSER_SNAME & #40; Transact-SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md), verwenden Sie <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterLogin%2A>.  
  
    -   Wenn die Partition des Abonnenten, durch das Ergebnis des definiert ist [HOST_NAME & #40; Transact-SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) oder eine Überladung dieser Funktion, verwenden Sie <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterHostName%2A>.  
  
7.  Rufen Sie die <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> -Methode auf.  
  
8.  Wiederholen Sie die Schritte 4 - 7 für jeden Abonnenten.  
  
###  <a name="PShellExample"></a> Beispiele (RMO)  
 In diesem Beispiel wird eine Mergeveröffentlichung erstellt, die es Abonnenten ermöglicht, die Momentaufnahmegenerierung anzufordern.  
  
 [!code-csharp[HowTo#rmo_CreateMergePub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
 In diesem Beispiel werden die Abonnentenpartition und die gefilterte Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Zeilenfiltern manuell erstellt.  
  
 [!code-csharp[HowTo#rmo_CreateMergePartition](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepartition)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePartition](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepartition)]  
  
 In diesem Beispiel wird der Momentaufnahme-Agent manuell gestartet, um die gefilterten Momentaufnahmedaten für den Abonnenten einer Mergeveröffentlichung mit parametrisierten Zeilenfiltern zu generieren.  
  
 [!code-csharp[HowTo#rmo_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatefilteredsnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatefilteredsnapshot)]  
  
## Siehe auch  
 [Parametrisierte Zeilenfilter](../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Momentaufnahmen für Mergeveröffentlichungen mit parametrisierten Filtern](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  