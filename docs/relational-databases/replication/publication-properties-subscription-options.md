---
title: "Ver&#246;ffentlichungseigenschaften, Abonnementoptionen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.subscriptionoptions.f1"
ms.assetid: 31abd605-b273-419d-86df-d0ecf539a507
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Ver&#246;ffentlichungseigenschaften, Abonnementoptionen
  Auf der Seite **Abonnementoptionen** des Dialogfelds **Veröffentlichungseigenschaften** können Sie die mit den Abonnements verknüpften Veröffentlichungsebeneneigenschaften anzeigen und festlegen. Die Eigenschaften sind in folgenden Kategorien angeordnet:  
  
-   Eigenschaften, die für alle Veröffentlichungen gelten.  
  
-   Eigenschaften, die für Momentaufnahme- und Transaktionsveröffentlichungen gelten (einschließlich Veröffentlichungen, für die Updateabonnements zulässig sind).  
  
-   Eigenschaften, die für Mergeveröffentlichungen gelten.  
  
> [!NOTE]  
>  Einige Eigenschaften sind schreibgeschützt. Die Gründe dafür werden im Rahmen der Eigenschaftenbeschreibungen in diesem Thema behandelt. Bei einigen Eigenschaftenänderungen ist eine neue Momentaufnahme für die Veröffentlichung erforderlich, und bei einigen müssen sogar alle Abonnements erneut initialisiert werden. Weitere Informationen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
## Optionen für alle Veröffentlichungen  
  
### Erstellung und Synchronisierung  
 **Anonyme Abonnements zulassen**  
 Bestimmt, ob anonyme Pullabonnements zulässig sind. Anonyme Abonnements werden für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEWEd2005](../../includes/ssewed2005-md.md)], [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssMobileEd2005](../../includes/ssmobileed2005-md.md)]und [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für Windows CE unterstützt. Um diese Option für Momentaufnahme- und Transaktionsveröffentlichungen zu verwenden, muss für die Option **Momentaufnahme immer verfügbar** der Wert **True**festgelegt sein.  
  
 **Anfügbare Abonnementdatenbank**  
 Bestimmt, ob Abonnements durch Anfügen einer Kopie einer Abonnementdatenbank erstellt werden können (erfordert, dass die Option **Momentaufnahme immer verfügbar** Wert **True** für Momentaufnahme- und transaktionsveröffentlichungen).  
  
> [!IMPORTANT]  
>  Anfügbare Abonnements wird es in künftigen Versionen nicht geben. Die Funktion ist als veraltet markiert.  
  
 **Pullabonnements zulassen**  
 Bestimmt, ob Abonnenten Pullabonnements dieser Veröffentlichung erstellen dürfen. Weitere Informationen finden Sie unter [abonnieren Publikationen](../../relational-databases/replication/subscribe-to-publications.md).  
  
### Schemareplikation  
 **Schemaänderungen replizieren**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen. Bestimmt, ob Schemaänderungen auf veröffentlichte Objekte repliziert werden. (Dazu gehört z. B. das Hinzufügen einer Spalte zu einer Tabelle oder das Ändern des Datentyps einer Spalte.) Weitere Informationen finden Sie unter [vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## Optionen für Momentaufnahme- und Transaktionsveröffentlichungen  
  
### Erstellung und Synchronisierung  
 **Unabhängiger Verteilungs-Agent**  
 Bestimmt, ob ein Agent verwendet wird, der von anderen Veröffentlichungen dieser Datenbank unabhängig ist. Diese Option ist schreibgeschützt. Dieses Attribut ist **True** für Veröffentlichungen mit dem Assistenten für neue Veröffentlichung erstellt und nicht werden, nachdem geändert können die Veröffentlichung wird standardmäßig erstellt. Weitere Informationen finden Sie unter [Replikations-Agent-Verwaltung](../../relational-databases/replication/agents/replication-agent-administration.md).  
  
 **Momentaufnahme immer verfügbar**  
 Bestimmt, ob die Snapshotdateien erstellt werden, jedes Mal, wenn der Snapshot-Agent ausgeführt wird (erfordert **unabhängiger Verteilungs-Agent**). Diese Option ist schreibgeschützt. ist **True** bei Auswahl von **Snapshot sofort erstellen und zum Initialisieren von Abonnements verfügbar halten** auf die **Snapshot-Agent** Seite des Assistenten für neue Veröffentlichung (Standard). Weitere Informationen finden Sie unter [Erstellen und Anwenden der Momentaufnahme](../../relational-databases/replication/create-and-apply-the-snapshot.md).  
  
 **Initialisierung aus Sicherungsdateien zulassen**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen. Bestimmt, ob Sicherungsdateien für die Initialisierung von Abonnements verwendet werden dürfen. Weitere Informationen finden Sie unter [eine Transaktionsabonnements ohne Momentaufnahme initialisieren](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 **Nicht-SQL Server-Abonnenten zulassen**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen. Bestimmt, ob Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten von der Veröffentlichung unterstützt werden. Wenn diese Option auf **True** legt andere Veröffentlichungseigenschaften unterstützen nicht -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten. Diese Option ist schreibgeschützt, wenn Abonnements vorhanden sind. Es kann nicht festgelegt werden, um **True** Wenn **sofort aktualisierbare Abonnements zulassen**, **Zulassen Abonnements mit verzögerter Aktualisierung**, oder **Peer-zu-Peer-Abonnements zulassen** auf festgelegt ist **True**. Weitere Informationen finden Sie unter [nicht-SQL Server-Abonnenten](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
### Datentransformation  
 **Datentransformationen zulassen**  
 Bestimmt, ob vor der Verteilung der Daten an einen Abonnenten Data Transformation Services (DTS) verwendet werden soll, um Daten zu transformieren. Diese Option ist schreibgeschützt. Datentransformationen können nur aktiviert werden, wenn mithilfe gespeicherter Prozeduren eine Veröffentlichung erstellt wird.  
  
> [!IMPORTANT]  
>  Transformierbare Abonnements wird es in künftigen Versionen nicht geben. Die Funktion ist als veraltet markiert.  
  
### Peer-zu-Peer-Replikation  
 **Peer-zu-Peer-Abonnements zulassen**  
 Gilt nur für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höhere Versionen. Bestimmt, ob von der Veröffentlichung Peer-zu-Peer-Replikation unterstützt wird. Wenn diese Option auf **True** legt andere Veröffentlichungseigenschaften um Peer-to-Peer-Replikation zu unterstützen. Diese Option ist schreibgeschützt, wenn Abonnements vorhanden sind. Diese Option kann nicht festgelegt werden, um **True** Wenn **sofort aktualisierbare Abonnements zulassen** oder **Zulassen Abonnements mit verzögerter Aktualisierung**, oder **nicht - SQL Server-Abonnenten zulassen** Wert **True**. Weitere Informationen finden Sie unter [Peer-zu-Peer-Transaktionsreplikation](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 **Peer-zu-Peer-Konflikterkennung zulassen**  
 Gilt nur für [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höhere Versionen. Gibt an, ob die Konflikterkennung für diese Veröffentlichung aktiviert ist. Zur Verwendung der Konflikterkennung muss auf allen Knoten [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oder eine höhere Version ausgeführt werden, und die Erkennung muss für alle Knoten aktiviert sein. Zusätzlich müssen Sie zum Verwenden der Konflikterkennung einen Wert für **Absender-ID des Peers**angeben. Weitere Informationen finden Sie unter [Konflikterkennung bei der Peer-to-Peer-Replikation](../../relational-databases/replication/transactional/conflict-detection-in-peer-to-peer-replication.md).  
  
 **Absender-ID des Peers**  
 Gilt nur für [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höhere Versionen. Gibt eine ID für einen Knoten in einer Peer-zu-Peer-Topologie an. Diese ID wird für die konflikterkennung verwendet, wenn **Peer-zu-Peer-konflikterkennung zulassen** Wert **True**. Geben Sie eine positive ID ungleich 0 an, die in der Topologie noch nicht verwendet wurde. Abfragen für eine Liste der IDs, die bereits verwendet wurden, die [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) -Systemtabelle.  
  
### Aktualisierbare Abonnements  
 **Abonnements mit sofortigem Update zulassen**  
 Bestimmt, ob Abonnentendatenänderungen sofort an den Verleger repliziert werden können. Diese Option ist schreibgeschützt. Updateabonnements können nur aktiviert werden, wenn eine Veröffentlichung erstellt wird. Weitere Informationen finden Sie unter [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 **Abonnements mit verzögertem Update über eine Warteschlange zulassen**  
 Bestimmt, ob Abonnentendatenänderungen in eine Warteschlange gestellt und zu einem späteren Zeitpunkt an den Verleger repliziert werden können. Diese Option ist schreibgeschützt. Updateabonnements können nur aktiviert werden, wenn eine Veröffentlichung erstellt wird. Weitere Informationen finden Sie unter [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 **Konflikte zentral berichten**  
 Bestimmt, ob in Konflikt stehende datenänderungen nur auf dem Verleger oder auf dem Verleger und dem Abonnenten gemeldet (muss die Option **Zulassen Abonnements mit verzögerter Aktualisierung**). Diese Option ist schreibgeschützt. Dieses Attribut ist **True** für Veröffentlichungen mit dem Assistenten für neue Veröffentlichung erstellt und nicht werden, nachdem geändert können die Veröffentlichung wird standardmäßig erstellt. Durch den Wert **True** wird festgelegt, dass die Konflikte nur auf dem Verleger gemeldet werden. Die Konflikte können nur angezeigt werden, wo sie gemeldet werden.  
  
 **Richtlinie zur Konfliktlösung**  
 Gibt die Aktion an, wenn eine Änderung auf dem Abonnenten mit einer verlegeränderung in Konflikt steht (muss die Option **Zulassen Abonnements mit verzögerter Aktualisierung**). Weitere Informationen finden Sie unter [Queued Updating Conflict Detection and Resolution](../../relational-databases/replication/transactional/queued-updating-conflict-detection-and-resolution.md).  
  
 **Warteschlangentyp**  
 Bestimmt, ob ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Warteschlange oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (MSMQ) auf Warteschlange Änderungen auf dem Abonnenten, bis sie auf den Verleger angewendet werden können (erfordert die Option **Zulassen Abonnements mit verzögerter Aktualisierung**). Diese Option ist nur für [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]relevant, da in höheren Versionen grundsätzlich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabellen als Warteschlange verwendet werden.  
  
## Optionen für Mergeveröffentlichungen  
  
### Konfliktberichterstellung  
 **Konflikte zentral berichten**  
 Bestimmt, ob konfligierende Datenänderungen nur auf dem Verleger oder sowohl auf dem Verleger als auch auf dem Abonnenten gemeldet werden. Diese Option ist schreibgeschützt. Dieses Attribut ist **True** für Veröffentlichungen mit dem Assistenten für neue Veröffentlichung erstellt und nicht werden, nachdem geändert können die Veröffentlichung wird standardmäßig erstellt. Durch den Wert **True** wird festgelegt, dass die Konflikte nur auf dem Verleger gemeldet werden. Die Konflikte können nur angezeigt werden, wo sie gemeldet werden. Weitere Informationen finden Sie im Abschnitt zum Anzeigen von Konflikten unter [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
### Filterung  
 **Parametrisierte Filter zulassen**  
 Wählen Sie die Option aus, um zuzulassen, dass parametrisierte Filter durch eine Veröffentlichung verwendet werden. Diese Option ist immer schreibgeschützt. Weitere Informationen finden Sie unter [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 **Abonnenten überprüfen**  
 Bestimmt, welche Funktionen verwendet werden sollen, um zu überprüfen, ob ein Abonnent über die richtige Partition der Daten verfügt. Bei mehreren Werten werden Kommas als Trennzeichen verwendet. Weitere Informationen finden Sie unter [Überprüfen von Partitionsinformationen für einen Abonnenten Merge](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md).  
  
 **Partitionen im Voraus berechnen**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen. Bestimmt, ob die Synchronisierung optimiert werden soll, indem im Voraus berechnet wird, welche Datenzeilen in welche Partitionen gehören. Der Standardwert für diese Option lautet **True** , wenn die Veröffentlichung die Kriterien für im Voraus berechnete Partitionen erfüllt. Weitere Informationen finden Sie unter [parametrisierte Filter Leistung mit Vorausberechnete Partitionen optimieren](../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md).  
  
 **Synchronisierung optimieren**  
 Bestimmt, ob die Mergeverarbeitung optimiert werden soll, indem zusätzliche Metadaten auf den einzelnen Abonnenten gespeichert werden. An die Stelle dieser Optimierung sind die im Voraus berechneten Partitionen getreten, d. h., die Option **Synchronisierung optimieren** ist nur relevant, wenn für **Partitionen im Voraus berechnen** der Wert **False**festgelegt ist. Weitere Informationen finden Sie unter [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
### Mergeprozesse  
 **Gleichzeitige Prozesse beschränken**  
 Bestimmt, ob die Anzahl der gleichzeitig ausführbaren Merge-Agents beschränkt werden soll. Diese Option wird normalerweise verwendet, wenn eine Veröffentlichung eine große Anzahl von Pushabonnements aufweist, für die die Synchronisierung möglicherweise gleichzeitig erfolgt.  
  
 **Maximale Anzahl von gleichzeitigen Prozessen**  
 Die maximale Anzahl der Merge-Agents, die gleichzeitig ausgeführt werden können (erfordert **gleichzeitige Prozesse beschränken**). Wenn die Anzahl der Agents, für die die Synchronisierung erfolgt, den Maximalwert überschreitet, werden die Agents in eine Warteschlange gestellt, bis die Anzahl unter das Maximum abfällt.  
  
## Siehe auch  
 [Erstellen einer Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  