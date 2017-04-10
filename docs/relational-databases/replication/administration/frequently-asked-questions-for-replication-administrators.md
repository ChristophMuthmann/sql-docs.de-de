---
title: "H&#228;ufig gestellte Fragen f&#252;r Replikationsadministratoren | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Verwalten der Replikation, häufig gestellte Fragen"
  - "Replikation [SQL Server], verwalten"
ms.assetid: 5a9e4ddf-3cb1-4baf-94d6-b80acca24f64
caps.latest.revision: 59
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 59
---
# H&#228;ufig gestellte Fragen f&#252;r Replikationsadministratoren
  Die folgenden Fragen und Antworten bieten einen Leitfaden für zahlreiche Aufgaben, die Administratoren von replizierten Datenbanken ausführen müssen.  
  
## Konfigurieren der Replikation  
  
### Muss die Aktivität einer Datenbank beim Veröffentlichen angehalten werden?  
 Nein. Die Aktivität einer Datenbank kann während der Erstellung der Veröffentlichung fortgesetzt werden. Sie sollten jedoch berücksichtigen, dass das Erstellen einer Momentaufnahme zu einer hohe Auslastung der Ressourcen führen kann. Es empfiehlt sich also, Momentaufnahmen in Zeiten geringerer Aktivität in der Datenbank zu erstellen (eine Momentaufnahme wird standardmäßig beim Abschließen des Assistenten für neue Veröffentlichung generiert).  
  
### Werden Tabellen während der Momentaufnahmeerstellung gesperrt?  
 Die Dauer der vorgenommenen Sperren ist vom Typ der verwendeten Replikation abhängig:  
  
-   Bei Mergeveröffentlichungen richtet der Momentaufnahme-Agent keine Sperren ein.  
  
-   Bei Transaktionsveröffentlichungen nimmt der Momentaufnahme-Agent standardmäßig nur in der Anfangsphase der Momentaufnahmeerstellung eine Sperre vor.  
  
-   Bei Momentaufnahmeveröffentlichungen nimmt der Momentaufnahme-Agent während des gesamten Momentaufnahmeerstellungsvorgangs eine Sperre vor.  
  
 Da andere Benutzer die Tabellen bei Sperren nicht aktualisieren können, sollte die Ausführung des Momentaufnahme-Agents für Zeiträume geringerer Aktivität in der Datenbank geplant werden. Dies gilt insbesondere für Momentaufnahmeveröffentlichungen.  
  
### Wenn ein Abonnement verfügbar ist, wann kann dann die Abonnementdatenbank verwendet werden?  
 Ein Abonnement ist verfügbar, nachdem die Momentaufnahme auf die Abonnementdatenbank angewendet wurde. Obgleich auch vorher auf die Abonnementdatenbank zugegriffen werden kann, sollte die Datenbank erst verwendet werden, nachdem die Momentaufnahme angewendet wurde. Überprüfen Sie den Status der Momentaufnahmeerstellung mithilfe des Replikationsmonitors:  
  
-   Die Momentaufnahme wird durch den Momentaufnahme-Agent erstellt. Im Replikationsmonitor können Sie den Status der Momentaufnahmeerstellung auf der Registerkarte **Agents** anzeigen. Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents verknüpft sind mit einer Publikation & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
-   Die Momentaufnahme wird vom Verteilungs-Agent oder vom Merge-Agent angewendet. Im Replikationsmonitor können Sie den Status der Momentaufnahmeanwendung auf der Seite **Verteilungs-Agent** oder **Merge-Agent** anzeigen. Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents einem Abonnement zugeordneten & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
### Was geschieht, wenn beim Start des Verteilungs- oder des Merge-Agents der Momentaufnahme-Agent noch nicht abgeschlossen ist?  
 Wenn der Verteilungs-Agent oder der Merge-Agent gleichzeitig mit dem Momentaufnahme-Agent ausgeführt wird, tritt kein Fehler auf. Es ist jedoch Folgendes zu beachten:  
  
-   Wenn der Verteilungs-Agent oder der Merge-Agent für die kontinuierliche Ausführung konfiguriert ist, wendet der Agent die Momentaufnahme automatisch nach dem Abschluss des Momentaufnahme-Agents an.  
  
-   Wenn der Verteilungs-Agent oder der Merge-Agent so konfiguriert ist, dass er nach einem Zeitplan oder bei Bedarf ausgeführt wird und beim Ausführen des Agents keine Momentaufnahme verfügbar ist, wird der Agent mit einer Meldung heruntergefahren, die besagt, dass noch keine Momentaufnahme verfügbar ist. Sie müssen den Agent erneut ausführen, um die Momentaufnahme nach Abschluss des Momentaufnahme-Agents erneut anzuwenden. Weitere Informationen zum Ausführen von Agents finden Sie unter [Synchronisieren eines Abonnements Push](../../../relational-databases/replication/synchronize-a-push-subscription.md), [synchronisieren Sie ein Pullabonnement](../../../relational-databases/replication/synchronize-a-pull-subscription.md), und [Replikations-Agent ausführbare Konzepte](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
### Sollte ich ein Skript für meine Replikationskonfiguration erstellen?  
 Ja. Die Erstellung eines Skripts für die Replikationskonfiguration ist ein wesentlicher Bestandteil des Plans für die Notfallwiederherstellung in einer Replikationstopologie. Weitere Informationen zur Skripterstellung finden Sie unter [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
### Welches Wiederherstellungsmodell ist für eine replizierte Datenbank erforderlich?  
 Die Replikation ist mit allen Wiederherstellungsmodellen ordnungsgemäß funktionsfähig: einfach, massenprotokolliert oder vollständig. Bei der Mergereplikation werden Änderungen durch Speichern von Informationen in Metadatentabellen verfolgt. Bei der Transaktionsreplikation werden Änderungen durch Markierungen im Transaktionsprotokoll verfolgt. Das Wiederherstellungsmodell hat jedoch keinen Einfluss auf diesen Markierungsvorgang.  
  
### Warum wird durch die Replikation in replizierten Tabellen eine Spalte hinzugefügt, und wird sie wieder entfernt, wenn die Tabelle nicht veröffentlicht wird?  
 Damit Änderungen nachverfolgt werden können, müssen Mergereplikationen und Transaktionsreplikationen mit Abonnements mit verzögertem Update über eine Warteschlange jede Zeile in jeder veröffentlichten Tabelle eindeutig identifizieren können. Dies erreichen Sie folgendermaßen:  
  
-   Mergereplikation fügt die Spalte **Rowguid** zu jeder Tabelle, wenn die Tabelle bereits eine Spalte vom Datentyp wurde **Uniqueidentifier** mit der **ROWGUIDCOL** -Eigenschaft (in diesem Fall wird diese Spalte verwendet). Beim Löschen der Tabelle aus der Veröffentlichung wird auch die **rowguid** -Spalte entfernt. Wurde eine vorhandene Spalte zur Nachverfolgung verwendet, wird die Spalte nicht entfernt.  
  
-   Wenn eine transaktionsveröffentlichung Abonnements mit verzögerter Aktualisierung unterstützt, bei der Replikation die Spalte hinzugefügt **Msrepl_tran_version** zu jeder Tabelle. Wenn die Tabelle, aus der Veröffentlichung gelöscht wird der **Msrepl_tran_version** Spalte nicht entfernt.  
  
-   Ein Filter muss die von der Replikation verwendete **rowguidcol** nicht einschließen, um Zeilen zu identifizieren. Standardmäßig ist dies die Spalte, die zum Zeitpunkt hinzugefügt wurde, als Sie die Mergereplikation eingerichtet haben, und sie heißt **rowguid**.  
  
### Wie verwalte ich Einschränkungen in veröffentlichten Tabellen?  
 Hinsichtlich der Einschränkungen für veröffentlichte Tabellen sind mehrere Probleme zu berücksichtigen:  
  
-   Für die Transaktionsreplikation ist für jede veröffentlichte Tabelle eine PRIMARY KEY-Einschränkung erforderlich. Für die Mergereplikation ist kein Primärschlüssel erforderlich, sollte jedoch einer vorhanden sein, so muss er repliziert werden. Bei der Momentaufnahmereplikation ist kein Primärschlüssel erforderlich.  
  
-   PRIMARY KEY-Einschränkungen, Indizes und CHECK-Einschränkungen werden standardmäßig auf den Abonnenten repliziert.  
  
-   Die NOT FOR REPLICATION-Option ist standardmäßig für FOREIGN KEY-Einschränkungen und CHECK-Einschränkungen angegeben, die bei Benutzeroperationen, nicht jedoch bei Agent-Operationen erzwungen werden.  
  
 Informationen zum Festlegen der Schemaoptionen, mit denen die Replikation von Einschränkungen gesteuert wird, finden Sie unter [Specify Schema Options](../../../relational-databases/replication/publish/specify-schema-options.md).  
  
### Wie verwalte ich Identitätsspalten?  
 Bei der Replikation wird eine automatische Identitätsbereichsverwaltung für Replikationstopologien durchgeführt, die Updates auf dem Abonnenten beinhalten. Weitere Informationen finden Sie unter [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
### Können dieselben Objekte in unterschiedlichen Veröffentlichungen veröffentlicht werden?  
 Ja, allerdings gelten hier einige Einschränkungen. Weitere Informationen finden Sie im Abschnitt "Veröffentlichen von Tabellen in mehreren Veröffentlichungen" im Thema [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
### Kann für mehrere Veröffentlichungen dieselbe Verteilungsdatenbank verwendet werden?  
 Ja. Hinsichtlich der Anzahl oder der Arten der Veröffentlichungen, die dieselbe Verteilungsdatenbank verwenden können, gelten keine Einschränkungen. Alle Veröffentlichungen von einem bestimmten Verleger müssen denselben Verteiler und dieselbe Verteilungsdatenbank verwenden.  
  
 Wenn Sie über mehrere Veröffentlichungen verfügen, können Sie mehrere Verteilungsdatenbanken auf dem Verteiler konfigurieren, um sicherzustellen, dass der Datenfluss über jede Verteilungsdatenbank von einer einzigen Veröffentlichung stammt. Verwenden der **Verteilereigenschaften** Dialogfeld oder [Sp_adddistributiondb & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) zum Hinzufügen einer Verteilungsdatenbank. Weitere Informationen zum Zugreifen auf das Dialogfeld finden Sie unter [anzeigen und ändern, Verteiler und Verlegereigenschaften](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### Wie erhalte ich Informationen zu dem Verteiler und dem Verleger, wenn ich beispielsweise wissen möchte, welche Objekte in einer Datenbank veröffentlicht sind?  
 Diese Informationen sind über [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]und mehrere gespeicherte Replikationsprozeduren verfügbar. Weitere Informationen finden Sie unter [Distributor and Publisher Information Script](../../../relational-databases/replication/administration/distributor-and-publisher-information-script.md).  
  
### Werden bei der Replikation Daten verschlüsselt?  
 Nein. Bei der Replikation werden keine Daten verschlüsselt, die in der Datenbank gespeichert oder über das Netzwerk übertragen werden. Weitere Informationen finden Sie im Abschnitt "Verschlüsselung" des Themas [Sicherheitsübersicht & #40; Replikation und #41;](../../../relational-databases/replication/security/security-overview-replication.md).  
  
### Wie repliziere ich Daten über das Internet?  
 Verwenden Sie Folgendes, um Daten über das Internet zu replizieren:  
  
-   Ein Virtuelles Privates Netzwerk (VPN). Weitere Informationen finden Sie unter [Veröffentlichen von Daten über das Internet mithilfe von VPN](../../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md).  
  
-   Die Websynchronisierungsoption für die Mergereplikation. Weitere Informationen finden Sie unter [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 Bei allen Typen der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Replikation können Daten über ein VPN repliziert werden. Sie sollten jedoch die Websynchronisierung in Betracht ziehen, falls Sie die Mergereplikation verwenden.  
  
### Wird die Replikation fortgesetzt, wenn eine Verbindung getrennt wird?  
 Ja. Die Replikationsverarbeitung wird an der Stelle fortgesetzt, an der sie beim Trennen der Verbindung unterbrochen wurde. Wenn Sie eine Mergereplikation über ein unzuverlässiges Netzwerk ausführen, sollten Sie die Verwendung logischer Datensätze in Betracht ziehen, mit denen sichergestellt wird, dass aufeinander bezogene Änderungen als Einheit verarbeitet werden. Weitere Informationen finden Sie unter [Gruppieren Sie Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
### Ist die Replikation über Verbindungen mit geringer Bandbreite funktionsfähig? Wird hierbei eine Komprimierung angewendet?  
 Ja, die Replikation ist über Verbindungen mit geringer Bandbreite funktionsfähig. Für Verbindungen über TCP/IP wird die vom Protokoll bereitgestellte Komprimierung verwendet. Eine zusätzliche Komprimierung findet jedoch nicht statt. Für Websynchronisierungsverbindungen über HTTPS wird neben der vom Protokoll bereitgestellten Komprimierung eine zusätzliche Komprimierung der XML-Dateien angewendet, um Änderungen zu replizieren.  
  
## Benutzernamen und Objektbesitz  
  
### Werden Benutzernamen und Kennwörter repliziert?  
 Nein. Für die Übertragung von Benutzernamen und Kennwörtern von einem Verleger an einen oder mehrere Abonnenten können Sie ein DTS-Paket erstellen.  
  
### Was sind Schemas, und wie werden sie repliziert?  
 Ab [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], *Schema* zwei Bedeutungen:  
  
-   Die Definition eines Objekts, beispielsweise als CREATE TABLE-Anweisung. Bei der Replikation werden standardmäßig die Definitionen aller replizierten Objekte auf den Abonnenten kopiert.  
  
-   Der Namespace, in dem ein Objekt erstellt wird: \< Datenbank>. \< Schema>. \< Objekt>. Schemas werden mit der CREATE SCHEMA-Anweisung definiert.  
  
-   Im Assistenten für neue Veröffentlichung weist die Replikation in Bezug auf Schemas und den Objektbesitz das folgende Standardverhalten auf:  
  
-   Für Artikel in Mergeveröffentlichungen mit einem Kompatibilitätsgrad von mindestens 90, Momentaufnahmeveröffentlichungen und Transaktionsveröffentlichungen gilt: Standardmäßig entspricht der Objektbesitzer auf dem Abonnenten dem Besitzer des entsprechenden Objekts auf dem Verleger. Wenn die Schemas, die Besitzer von Objekten sind, auf dem Abonnenten nicht vorhanden sind, werden sie automatisch erstellt.  
  
-   Für Artikel in Mergeveröffentlichungen mit einem Kompatibilitätsgrad von unter 90: Standardmäßig wird der Besitzer leer gelassen und während der Erstellung des Objekts auf dem Abonnenten mit **dbo** angeben.  
  
-   Für Artikel in Oracle-Veröffentlichungen: Standardmäßig wird der Besitzer mit **dbo**angegeben.  
  
-   Für Artikel in Veröffentlichungen, die Zeichenmodus-Momentaufnahmen verwenden (werden für Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Abonnenten und [!INCLUDE[ssEW](../../../includes/ssew-md.md)]-Abonnenten verwendet): Standardmäßig wird der Besitzer leer gelassen. Als Besitzer wird standardmäßig der Besitzer verwendet, der mit dem vom Verteilungs- oder Merge-Agent zum Herstellen einer Verbindung mit dem Abonnenten verwendeten Konto verknüpft ist.  
  
 Der Besitzer des Objekts geändert werden kann, über die **Artikeleigenschaften - \<***Artikel***>** Dialogfeld und über die folgenden gespeicherten Prozeduren: **Sp_addarticle**, **Sp_addmergearticle**, **Sp_changearticle**, und **Sp_changemergearticle**. Weitere Informationen finden Sie unter [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md), [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md), und [anzeigen und Ändern von Artikeleigenschaften](../../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
### Wie können Erteilungen in der Abonnementdatenbank so konfiguriert werden, dass sie mit den Erteilungen in der Veröffentlichungsdatenbank übereinstimmen?  
 Bei der Replikation werden GRANT-Anweisungen standardmäßig nicht für die Abonnementdatenbank ausgeführt. Wenn die Berechtigungen für die Abonnementdatenbank mit denen für die Veröffentlichungsdatenbank übereinstimmen sollen, verwenden Sie eine der folgenden Methoden:  
  
-   Führen Sie GRANT-Anweisungen direkt in der Abonnementdatenbank aus.  
  
-   Verwenden Sie zum Ausführen der Anweisungen ein Nach-Momentaufnahme-Skript. Weitere Informationen finden Sie unter [Ausführen von Skripts vor und nach der Momentaufnahme angewendet wird](../../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).  
  
-   Verwenden Sie die gespeicherte Prozedur [Sp_addscriptexec](../../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md) zum Ausführen der Anweisungen.  
  
### Was geschieht mit den in einer Abonnementdatenbank erteilten Berechtigungen, wenn ein Abonnement erneut initialisiert wird?  
 Die Objekte auf dem Abonnenten werden standardmäßig gelöscht und bei der erneuten Initialisierung eines Abonnements erneut erstellt. Dadurch werden alle erteilten Berechtigungen für diese Objekte gelöscht. Dieses Problem lässt sich auf zwei Arten lösen:  
  
-   Wenden Sie die Erteilungen nach der erneuten Initialisierung unter Anwendung der im vorigen Abschnitt beschriebenen Techniken erneut an.  
  
-   Geben Sie an, dass Objekte bei einer erneuten Initialisierung des Abonnements nicht gelöscht werden sollen. Führen Sie vor der erneuten Initialisierung einen der folgenden Vorgänge aus:  
  
    -   Führen Sie [Sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) oder [Sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Geben Sie den Wert 'Pre_creation_cmd' (**Sp_changearticle**) oder 'Pre_creation_command' (**Sp_changemergearticle**) für den Parameter **@property** und der Wert 'none', 'delete' oder 'truncate' für den Parameter **@value**.  
  
    -   In der **Artikeleigenschaften - \< Artikel>** im Dialogfeld die **Zielobjekt** Abschnitt, wählen Sie einen Wert von **Vorhandenes Objekt unverändert beibehalten**, **Daten löschen. Wenn ein Artikel einen Zeilenfilter aufweist, löschen Sie nur Daten, die mit dem Filter übereinstimmt.** oder **alle Daten im vorhandenen Objekt abschneiden** für die Option **Aktion, wenn der Name wird**. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
## Datenbankwartung  
  
### Warum kann ich TRUNCATE TABLE für eine veröffentlichte Tabelle nicht ausführen?  
 Bei TRUNCATE TABLE handelt es sich um eine nicht protokollierte Operation, bei der keine Trigger ausgelöst werden. Dieser Vorgang ist nicht zulässig, da die von der Operation verursachten Änderungen bei der Replikation nicht nachverfolgt werden können: Bei der Transaktionsreplikation werden Änderungen über das Transaktionsprotokoll verfolgt; bei der Mergereplikation werden Änderungen über Trigger in veröffentlichten Tabellen verfolgt.  
  
### Welche Auswirkungen hat die Ausführung eines Masseneinfügungsbefehls für eine replizierte Datenbank?  
 Bei Transaktionsreplikationen werden Masseneinfügungen wie andere Einfügungen verfolgt und repliziert. Bei Mergereplikationen muss sichergestellt werden, dass die Metadaten zur Änderungsnachverfolgung ordnungsgemäß aktualisiert werden.  
  
### Sind hinsichtlich der Sicherung und Wiederherstellung bestimmte Überlegungen zu berücksichtigen?  
 Ja. Für an einer Replikation beteiligte Datenbanken sind mehrere besondere Punkte zu berücksichtigen. Weitere Informationen finden Sie unter [Sichern und Wiederherstellen von replizierten Datenbanken](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).  
  
### Hat die Replikation Auswirkungen auf die Größe des Transaktionsprotokolls?  
 Die Mergereplikation und die Momentaufnahmereplikation haben im Gegensatz zur Transaktionsreplikation keine Auswirkungen auf die Transaktionsprotokollgröße. Wenn eine Datenbank eine oder mehrere Transaktionsveröffentlichungen enthält, wird das Protokoll erst dann abgeschnitten, wenn alle für die Veröffentlichungen relevanten Transaktionen an die Verteilungsdatenbank übermittelt wurden. Wenn das Transaktionsprotokoll zu umfangreich wird und der Protokolllese-Agent basierend auf einem Zeitplan ausgeführt wird, sollten Sie eine Verkürzung des Intervalls zwischen den Ausführungen in Betracht ziehen. Sie können auch festlegen, dass die Ausführung im kontinuierlichen Modus erfolgt. Wenn der Agent so festgelegt ist, dass er im kontinuierlichen Modus ausgeführt wird (Standardeinstellung), stellen Sie sicher, dass er läuft. Weitere Informationen zum Prüfen des Protokolllese-Agent-Status finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents verknüpft sind mit einer Publikation & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
 Zudem wird das Transaktionsprotokoll nicht abgeschnitten, bis alle Transaktionen gesichert wurden, wenn Sie für die Veröffentlichungsdatenbank oder für die Verteilungsdatenbank die Option 'sync with backup' festgelegt haben. Wenn das Transaktionsprotokoll zu umfangreich wird und Sie diese Option festgelegt haben, sollten Sie eine Verkürzung des Intervalls zwischen den Transaktionsprotokollsicherungen in Betracht ziehen. Weitere Informationen zum Sichern und Wiederherstellen der Transaktionsreplikation beteiligten Datenbanken finden Sie unter [Strategien zum Sichern und Wiederherstellen einer Momentaufnahme- und Transaktionsreplikation](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
### Wie kann ich Indizes oder Tabellen in replizierten Datenbanken neu erstellen?  
 Es gibt unterschiedliche Mechanismen für die Neuerstellung von Indizes. Sie können alle ohne besondere Berücksichtigung der Replikation mit folgender Ausnahme verwendet werden: Für Tabellen in Transaktionsveröffentlichungen sind Primärschlüssel erforderlich, sodass Primärschlüssel in diesen Tabellen nicht gelöscht und neu erstellt werden können.  
  
### Wie kann ich in Veröffentlichungs- und Abonnementdatenbanken Indizes hinzufügen bzw. ändern?  
 Auf dem Verleger oder auf Abonnenten können Indizes ohne besondere Berücksichtigung der Replikation hinzugefügt werden (beachten Sie jedoch, dass Indizes die Leistung beeinträchtigen können). CREATE INDEX und ALTER INDEX werden nicht repliziert. Wenn Sie also beispielsweise auf dem Verleger einen Index hinzufügen oder ändern, müssen Sie denselben Hinzufüge- oder Änderungsvorgang auf dem Abonnenten vornehmen, wenn er dort reflektiert werden soll.  
  
### Wie kann ich Dateien für an einer Replikation beteiligte Datenbanken verschieben bzw. umbenennen?  
 In Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]war zum Verschieben oder zum Umbenennen von Datenbankdateien ein Trennen und erneutes Anfügen der Datenbank erforderlich. Da das Trennen einer replizierten Datenbank nicht möglich ist, musste die Replikation zuerst von diesen Datenbanken entfernt werden. Ab [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] können Sie Dateien ohne Trennen und erneutes Anfügen der Datenbank verschieben und umbenennen. Dies hat keine Auswirkungen auf die Replikation. Weitere Informationen zum Verschieben und Umbenennen von Dateien finden Sie unter [ALTER DATABASE & #40; Transact-SQL & #41;](../../../t-sql/statements/alter-database-transact-sql.md).  
  
### Wie lösche ich eine Tabelle, die repliziert wird?  
 Löschen Sie zuerst den Artikel über die Veröffentlichung mit [Sp_droparticle](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md), [Sp_dropmergearticle](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md), oder die **Veröffentlichungseigenschaften - \< Veröffentlichung>** Dialogfeld ein, und legen Sie es dann aus der Datenbank `DROP <Object>`. Artikel in Momentaufnahme- oder Transaktionsveröffentlichungen können nach dem Hinzufügen von Abonnements nicht mehr gelöscht werden; zuerst müssen die Abonnements gelöscht werden. Weitere Informationen finden Sie unter [Hinzufügen und löschen Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### Wie kann ich in einer veröffentlichten Tabelle Spalten hinzufügen bzw. löschen?  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt zahlreiche Schemaänderungen für veröffentliche Objekte einschließlich des Hinzufügens und Löschens von Spalten. Führen Sie beispielsweise ALTER TABLE … DROP COLUMN auf dem Verleger aus, damit die Anweisung auf die Abonnenten repliziert und dann zum Löschen der Spalte ausgeführt wird. Abonnenten, auf denen Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Hinzufügen und Löschen von Spalten über die gespeicherten Prozeduren unterstützt [Sp_repladdcolumn](../../../relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql.md) und [Sp_repldropcolumn](../../../relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql.md). Weitere Informationen finden Sie unter [vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## Replikationswartung  
  
### Wie kann ich feststellen, ob die Daten auf den Abonnenten mit denen auf dem Verleger synchronisiert sind?  
 Führen Sie eine Überprüfung aus. Bei der Überprüfung wird angegeben, ob ein bestimmter Abonnent mit dem Verleger synchronisiert ist. Weitere Informationen finden Sie unter [Überprüfen von replizierten Daten](../../../relational-databases/replication/validate-replicated-data.md). Bei der Überprüfung wird nicht angegeben, in welchen Zeilen die Synchronisierung möglicherweise nicht richtig ausgeführt wurde. Im [Hilfsprogramm "tablediff"](../../../tools/tablediff-utility.md) werden die entsprechenden Informationen hingegen angezeigt.  
  
### Wie füge ich einer vorhandenen Veröffentlichung eine Tabelle hinzu?  
 Wenn eine Tabelle (oder ein anderes Objekt) hinzugefügt werden soll, ist das Anhalten der Aktivität in der Veröffentlichungs- oder in der Abonnementdatenbank nicht erforderlich. Hinzufügen einer Tabelle zu einer Veröffentlichung über die **Veröffentlichungseigenschaften - \< Veröffentlichung>** Dialogfeld oder die gespeicherten Prozeduren [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) und [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Weitere Informationen finden Sie unter [Hinzufügen und löschen Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### Wie entferne ich eine Tabelle in einer Veröffentlichung?  
 Entfernen einer Tabelle aus der Veröffentlichung mit [Sp_droparticle](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md), [Sp_dropmergearticle](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md), oder die **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Artikel in Momentaufnahme- oder Transaktionsveröffentlichungen können nach dem Hinzufügen von Abonnements nicht mehr gelöscht werden; zuerst müssen die Abonnements gelöscht werden. Weitere Informationen finden Sie unter [Hinzufügen und löschen Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### Für welche Aktionen müssen Abonnements erneut initialisiert werden?  
 Für einige Artikel- und Veröffentlichungsänderungen ist eine erneute Initialisierung der Abonnements erforderlich. Weitere Informationen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
### Durch welche Aktionen werden Momentaufnahmen für ungültig erklärt?  
 Bei einigen Artikel- und Veröffentlichungsänderungen werden Momentaufnahmen für ungültig erklärt, sodass eine neue Momentaufnahme generiert werden muss. Weitere Informationen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
### Wie entferne ich eine Replikation?  
 Die zum Entfernen einer Replikation aus einer Datenbank erforderlichen Aktionen sind davon abhängig, ob die Datenbank als Veröffentlichungsdatenbank, als Abonnementdatenbank oder beides dient.  
  
### Wie stelle ich fest, ob Transaktionen oder Zeilen repliziert werden müssen?  
 Verwenden Sie für die Transaktionsreplikation gespeicherte Prozeduren oder die Registerkarte **Nicht verteilte Befehle** im Replikationsmonitor. Weitere Informationen finden Sie unter [Ansicht replizierte Befehle und andere Informationen in der Verteilungsdatenbank & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) und [Informationen anzeigen und Ausführen von Aufgaben für ein Abonnement & #40; zugeordneten Agents Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
 Verwenden Sie für die Mergereplikation die gespeicherte Prozedur **Sp_showpendingchanges**. Weitere Informationen finden Sie unter [Sp_showpendingchanges & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md).  
  
### Wie weit ist der Verteilungs-Agent in Verzug? Sollte ich eine erneute Initialisierung ausführen?  
 Verwenden der **Sp_replmonitorsubscriptionpendingcmds** gespeicherte Prozedur oder die **nicht verteilte Befehle** Registerkarte im Replikationsmonitor. In der gespeicherten Prozedur und auf der Registerkarte wird Folgendes angezeigt:  
  
-   Die Anzahl von Befehlen in der Verteilungsdatenbank, die nicht an den ausgewählten Abonnenten übermittelt wurden. Ein Befehl besteht aus einer Transact-SQL-DML-Anweisung (Data Manipulation Language, Datenbearbeitungssprache) oder einer DDL-Anweisung (Data Definition Language, Datendefinitionssprache).  
  
-   Die geschätzte Zeitdauer für die Übermittlung von Befehlen an den Abonnenten. Wenn dieser Wert größer ist, als die zum Generieren und Anwenden einer Momentaufnahme auf den Abonnenten erforderliche Zeit, sollten Sie eine erneute Initialisierung des Abonnenten in Betracht ziehen. Weitere Informationen finden Sie unter [Abonnements erneut initialisieren](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
 Weitere Informationen finden Sie unter [Sp_replmonitorsubscriptionpendingcmds & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md) und [Informationen anzeigen und Ausführen von Aufgaben für ein Abonnement & #40; zugeordneten Agents Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
## Replikationen und sonstige Datenbankfunktionen  
  
### Ist die Replikation in Verbindung mit dem Protokollversand und der Datenbankspiegelung funktionsfähig?  
 Ja. Weitere Informationen finden Sie unter [Protokollversand und Replikation & #40; SQL Server & #41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md) und [Datenbankspiegelung und Replikation & #40; SQL Server & #41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
### Ist die Replikation in Verbindung mit dem Cluster funktionsfähig?  
 Ja. Da alle Daten auf einem Datenträgersatz im Cluster gespeichert sind, sind keine besonderen Überlegungen erforderlich.  
  
## Siehe auch  
 [Verwaltung & #40; Replikation & #41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [Bewährte Methoden für die Replikationsverwaltung](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  