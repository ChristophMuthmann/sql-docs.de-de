---
title: Artikeleigenschaften – &lt;Artikel&gt; | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.rep.newpubwizard.articleproperties.f1
helpviewer_keywords:
- Article Properties dialog box
ms.assetid: 6dd601a4-1233-43d9-a9f0-bc8d84e5d188
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: acee0f4698c9a1c6d26bd042f1413257df528828
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="article-properties---ltarticlegt"></a>Artikeleigenschaften – &lt;Artikel&gt;
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Das Dialogfeld **Artikeleigenschaften** steht über den Assistenten für neue Veröffentlichung und das Dialogfeld **Veröffentlichungseigenschaften** zur Verfügung. Es ermöglicht Ihnen, die Eigenschaften für alle Typen von Artikeln anzuzeigen und festzulegen. Bestimmte Eigenschaften können nur beim Erstellen der Veröffentlichung festgelegt werden, andere nur, wenn für die Veröffentlichung keine aktiven Abonnements vorhanden sind. Eigenschaften, die nicht festgelegt werden können, werden als schreibgeschützt angezeigt.  
  
> [!NOTE]  
>  Nachdem eine Veröffentlichung erstellt wurde, ist für bestimmte Eigenschaftsänderungen eine neue Momentaufnahme erforderlich. Wenn für eine Veröffentlichung Abonnements erstellt wurden, müssen bei bestimmten Änderungen alle Abonnements erneut initialisiert werden. Weitere Informationen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
 Zu jeder der im Dialogfeld **Artikeleigenschaften** verfügbaren Eigenschaften wird auch eine Beschreibung angezeigt. Klicken Sie auf eine Eigenschaft, um die dazugehörige Beschreibung am unteren Rand des Dialogfelds anzuzeigen. Dieses Thema enthält zusätzliche Informationen zu verschiedenen Eigenschaften. Die Eigenschaften sind in folgenden Kategorien angeordnet:  
  
-   Eigenschaften, die für alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Veröffentlichungen gelten.  
  
-   Eigenschaften, die für Transaktionsveröffentlichungen aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gelten.  
  
-   Eigenschaften, die für Mergeveröffentlichungen gelten.  
  
-   Eigenschaften, die für Transaktions- und Momentaufnahmeveröffentlichungen aus Oracle-Verlegern gelten.  
  
## <a name="options-for-all-publications"></a>Optionen für alle Veröffentlichungen  
 **Tabellenpartitionierungsschemas kopieren** und **Indexpartitionierungsschemas kopieren**  
 In[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] wurde die Tabellen- und Indexpartitionierung eingeführt, die in keinem Zusammenhang zu der Partitionierung stehen, die die Replikation über Zeilen- und Spaltenfilter anbietet. Die Optionen **Tabellenpartitionierungsschemas kopieren** und **Indexpartitionierungsschemas kopieren** geben an, ob Partitionierungsschemas auf den Abonnenten kopiert werden sollen. Weitere Informationen zur Partitionierung finden Sie unter [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 **Datentypen konvertieren**  
 Bestimmt, ob beim Erstellen von Objekten auf dem Abonnenten benutzerdefinierte Datentypen in Basisdatentypen konvertiert werden. Zu den benutzerdefinierten Datentypen gehören die benutzerdefinierten CLR-Typen, die in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]eingeführt wurden. Geben Sie den Wert **True** an, wenn Sie diese Datentypen auf frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]replizieren. Auf diese Weise stellen Sie sicher, dass sie auf dem Abonnenten fehlerfrei verarbeitet werden können.  
  
 **Schemas auf dem Abonnenten erstellen**  
 In[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] wurden Schemas eingeführt, die mithilfe der CREATE SCHEMA-Anweisung definiert werden. Ein Schema ist der Eigentümer eines Objekts. Es wird in einem mehrteiligen Namen verwendet, z.B. \<Database>.\<Schema>.\<Object>. Wenn Sie in der Datenbank Objekte haben, deren Besitzer nicht DBO ist, kann die Replikation diese Schemas auf dem Abonnenten erstellen, sodass veröffentlichte Objekte erstellt werden können.  
  
 Gehen Sie folgendermaßen vor, wenn Sie Daten auf Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]replizieren:  
  
-   Legen Sie für diese Option **False**fest, da frühere Versionen CREATE SCHEMA nicht unterstützen.  
  
-   Fügen Sie für jedes Schema einen Benutzer mit demselben Namen wie das Schema zur Abonnementdatenbank hinzu.  
  
 **XML in NTEXT konvertieren**, **MAX-Datentypen in NTEXT und IMAGE konvertieren**, **Neue datetime-Typen in NVARCHAR konvertieren**, **Filestream- in MAX-Datentypen konvertieren**, **Große CLR- in MAX-Datentypen konvertieren**, **HierarchyId- in MAX-Datentypen konvertieren**und **Räumliche in MAX-Datentypen konvertieren**.  
 Bestimmt, ob die Datentypen und Attribute wie beschrieben konvertiert werden. Geben Sie den Wert **True** an, wenn diese Datentypen für frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]repliziert werden sollen. So kann sichergestellt werden, dass sie auf dem Abonnenenten fehlerfrei verarbeitet werden können.  
  
 **Zielobjektname**  
 Der Name des in der Abonnementdatenbank erstellten Objekts. Diese Option kann für Artikel in Veröffentlichungen, die für die Peer-zu-Peer-Transaktionsreplikation aktiviert sind, nicht geändert werden.  
  
 **Zielobjektbesitzer**  
 Das Schema, unter dem das Objekt in der Abonnementdatenbank erstellt wird. Standardmäßig ist dies das Schema, zu dem das Objekt in der Veröffentlichungsdatenbank gehört. Es gelten folgende Ausnahmen:  
  
-   Für Artikel in Mergeveröffentlichungen mit einem Kompatibilitätsgrad von unter 90: Standardmäßig wird der Besitzer leer gelassen und während der Erstellung des Objekts auf dem Abonnenten mit **dbo** angeben.  
  
-   Für Artikel in Oracle-Veröffentlichungen: Standardmäßig wird der Besitzer mit **dbo**angegeben.  
  
-   Für Artikel in Veröffentlichungen, die Zeichenmodus-Momentaufnahmen verwenden (werden für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten und [!INCLUDE[ssEW](../../includes/ssew-md.md)] -Abonnenten verwendet): Standardmäßig wird der Besitzer leer gelassen. Als Besitzer wird standardmäßig der Besitzer verwendet, der mit dem vom Verteilungs- oder Merge-Agent zum Herstellen einer Verbindung mit dem Abonnenten verwendeten Konto verknüpft ist.  
  
 Diese Option kann für Artikel in Veröffentlichungen, die für die Peer-zu-Peer-Transaktionsreplikation aktiviert sind, nicht geändert werden.  
  
 **Identitätsbereiche automatisch verwalten**  
 Die Replikation verwaltet standardmäßig alle Identitätsspalten auf dem Verleger und jedem Abonnenten. Jeder Replikationsknoten ist einem Bereich von Identitätswerten zugewiesen (angegeben mit den Optionen **Bereichsgröße auf dem Verleger** und **Bereichsgröße auf dem Abonnenten** ), um sicherzustellen, dass ein angegebener Wert nur auf einem Knoten verwendet wird. Weitere Informationen finden Sie unter [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
## <a name="options-for-transactional-publications"></a>Optionen für Transaktionsveröffentlichungen  
 **Die gespeicherten Prozeduren INSERT, UPDATE und DELETE kopieren**  
 Wenn Sie im Abschnitt **Anweisungsübermittlung** dieses Dialogfelds gespeicherte Prozeduren zum Weitergeben von Änderungen an Abonnenten auswählen (Standardeinstellung), wählen Sie mithilfe dieser Option aus, ob die Prozeduren auf jeden Abonnenten kopiert werden. Wenn Sie **False**auswählen, müssen Sie die Prozeduren manuell kopieren. Andernfalls schlägt der Verteilungs-Agent beim Versuch, Änderungen zu übermitteln, fehl.  
  
 **Statement delivery**  
 Die Optionen in diesem Abschnitt gelten für alle Tabellen, einschließlich indizierter Sichten, die als Tabellen repliziert werden. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt die Verwendung der Standardoptionen, sofern die Anwendung keine andere Funktionalität erfordert. Standardmäßig gibt die Transaktionsreplikation Änderungen an Abonnenten mithilfe einer Reihe gespeicherter Prozeduren weiter, die auf jedem Abonnenten gespeichert sind. Wenn für eine Tabelle auf dem Verleger ein Einfüge-, Update- oder Löschvorgang ansteht, wird der Vorgang in einen Aufruf einer gespeicherten Prozedur auf den Abonnenten übersetzt.  
  
 Mit den Optionen unter **Anweisungsübermittlung** wird angegeben, ob eine gespeicherte Prozedur verwendet wird und wenn ja, welches Format für an die Prozedur übergebene Parameter verwendet werden soll. Die Optionen für **gespeicherte Prozeduren** ermöglichen es Ihnen, die Prozeduren zu verwenden, die die Replikation automatisch erstellt, oder diese durch von Ihnen erstellte benutzerdefinierte Prozeduren zu ersetzen.  
  
 Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)  
  
 **Replizieren**  
 Diese Option gilt nur für gespeicherte Prozeduren. Sie bestimmt, ob die Definition der gespeicherten Prozedur (die CREATE PROCEDURE-Anweisung) oder deren Ausführung repliziert wird. Wenn Sie die Ausführung der Prozedur replizieren, wird die Prozedurdefinition auf den Abonnenten repliziert, nachdem das Abonnement initialisiert wurde. Wenn die Prozedur auf dem Verleger ausgeführt wird, führt die Replikation die zugehörige Prozedur auf dem Abonnenten aus. Dies kann in Fällen, in denen große Batchvorgänge ausgeführt werden, zu einer deutlich verbesserten Leistung führen. Weitere Informationen finden Sie unter [Publishing Stored Procedure Execution in Transactional Replication](../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
## <a name="options-for-merge-publications"></a>Optionen für Mergeveröffentlichungen  
 Das Dialogfeld **Artikeleigenschaften** für Mergeveröffentlichungen verfügt über zwei Registerkarten: **Eigenschaften** und **Konfliktlöser**.  
  
### <a name="properties-tab"></a>Eigenschaften (Registerkarte)  
 **Synchronisierungsrichtung**  
 Bestimmt, ob Änderungen von Abonnenten hochgeladen werden können, die den folgenden Clientabonnementtyp verwenden:  
  
-   **Bidirektional** (Standardeinstellung): Änderungen können auf den Abonnenten heruntergeladen und auf den Verleger hochgeladen werden.  
  
-   **Nur herunterladbar auf Abonnenten, Abonnentenänderungen nicht zulassen**: Änderungen können auf den Abonnenten heruntergeladen, jedoch nicht auf den Verleger hochgeladen werden. Trigger verhindern, dass auf dem Abonnenten Änderungen vorgenommen werden.  
  
-   **Nur herunterladbar auf Abonnenten, Abonnentenänderungen zulassen**: Änderungen können auf den Abonnenten heruntergeladen, jedoch nicht auf den Verleger hochgeladen werden.  
  
 Weitere Informationen finden Sie unter [Optimieren der Leistung der Mergereplikation durch nur herunterladbare Artikel](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **Partitionsoptionen**  
 Geben Sie den Typ von Partitionen an, den ein parametrisierter Filter erstellt. Weitere Informationen finden Sie im Abschnitt zum Festlegen von Partitionsoptionen unter [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Nachverfolgungsebene**  
 Bestimmt, ob Änderungen an derselben Zeile oder Spalte als Konflikt behandelt werden.  
  
 **INSERT-Berechtigung überprüfen**, **UPDATE-Berechtigung überprüfen**und **DELETE-Berechtigung überprüfen**  
 Bestimmt, ob während der Synchronisierung überprüft wird, ob die Abonnentenanmeldung für die veröffentlichten Tabellen in der Veröffentlichungsdatenbank INSERT-, UPDATE- oder DELETE-Berechtigungen besitzt. Die Standardeinstellung ist **False** , da die Mergereplikation diese Berechtigungen nicht benötigt. Der Zugriff auf die veröffentlichten Tabellen wird über die Veröffentlichungszugriffsliste (Publication Access List, PAL) gesteuert. Weitere Informationen zur PAL finden Sie unter [Sichern des Verlegers](../../relational-databases/replication/security/secure-the-publisher.md).  
  
 Sie können die Überprüfung der Berechtigungen anfordern, wenn Sie einem oder mehreren Abonnenten gestatten möchten, nur bestimmte Änderungen an den veröffentlichten Daten hochzuladen. Sie können beispielsweise einen Abonnenten zur PAL hinzufügen, ihm jedoch keine Berechtigungen für die Tabellen in der Veröffentlichungsdatenbank erteilen. Anschließend legen Sie die Option DELETE-Berechtigung überprüfen auf **True**fest: Der Abonnent kann jetzt Einfüge- und Updatevorgänge hochladen, aber keine Löschvorgänge.  
  
 **UPDATE-Anweisung für mehrere Spalten**  
 Wenn die Mergereplikation ein Update ausführt, aktualisiert sie alle geänderten Spalten in einer UPDATE-Anweisung und setzt nicht geänderte Spalten auf ihre ursprünglichen Werte zurück. Die Alternative in diesen Fällen besteht darin, mehrere UPDATE-Anweisungen auszugeben, mit einer UPDATE-Anweisung für jede Spalte, die sich geändert hat. Die UPDATE-Anweisung für mehrere Spalten ist in der Regel effizienter. Sie sollten aber in Betracht ziehen, die Option auf **False** festzulegen, wenn Trigger für die Tabelle so festgelegt sind, dass sie auf Updates bestimmter Spalten reagieren, und sie falsch reagieren, weil diese Spalten bei Updates zurückgesetzt werden.  
  
> [!IMPORTANT]  
>  Diese Option ist als veraltet markiert und wird in einer zukünftigen Version entfernt.  
  
### <a name="resolver-tab"></a>Konfliktlöser (Registerkarte)  
 **Standardkonfliktlöser verwenden**  
 Wenn Sie den Standardkonfliktlöser auswählen, werden Konflikte in Abhängigkeit vom verwendeten Abonnementtyp basierend auf der jedem Abonnenten zugewiesenen Priorität oder der ersten auf dem Verleger geschriebenen Änderung gelöst. Weitere Informationen finden Sie unter [Erkennen und Beseitigen von Konflikten bei der Mergereplikation](../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md).  
  
 **Benutzerdefinierten Konfliktlöser verwenden (registriert auf dem Verteiler)**  
 Wenn Sie einen Artikelkonfliktlöser verwenden möchten (entweder einen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] bereitgestellten oder einen von Ihnen geschriebenen), müssen Sie einen Konfliktlöser aus dem Listenfeld auswählen. Weitere Informationen finden Sie unter [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
 Wenn der Konfliktlöser eine Eingabe erfordert, geben Sie diese im Textfeld **Geben Sie die vom Konfliktlöser benötigten Informationen ein** an. Weitere Informationen zu den für benutzerdefinierte [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Konfliktlöser erforderlichen Eingaben finden Sie unter [Microsoft COM-Based Resolvers](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
 **Zulassen, dass der Abonnent Konflikte während bedarfsgesteuerter Synchronisierungen interaktiv löst**  
 Wählen Sie diese Option aus, wenn Abonnenten die bedarfsgesteuerte Synchronisierung verwenden (Standardeinstellung für die Mergereplikation), und Sie Konflikte interaktiv lösen möchten. Geben Sie die bedarfsgesteuerte Synchronisierung auf der Seite **Synchronisierungszeitplan** des Assistenten für neue Abonnements an. Verwenden Sie zum interaktiven Lösen von Konflikten die Benutzeroberfläche des interaktiven Konfliktlösers. Weitere Informationen finden Sie unter [Interactive Conflict Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
 **Vor dem Zusammenführen die Überprüfung einer digitalen Signatur verlangen**  
 Alle von [!INCLUDE[msCoName](../../includes/msconame-md.md)] bereitgestellten COM-basierten Konfliktlöser sind signiert. Wählen Sie diese Option aus, um bei der Synchronisierung die Gültigkeit des Konfliktlösers zu überprüfen.  
  
## <a name="options-for-oracle-publications"></a>Optionen für Oracle-Veröffentlichungen  
 Das Dialogfeld **Artikeleigenschaften** für Oracle-Veröffentlichungen verfügt über zwei Registerkarten: **Eigenschaften** und **Datenzuordnung**. Oracle-Veröffentlichungen unterstützen nicht alle von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Veröffentlichungen unterstützten Eigenschaften. Weitere Informationen finden Sie unter [Design Considerations and Limitations for Oracle Publishers](../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
### <a name="properties-tab"></a>Eigenschaften (Registerkarte)  
 **Die gespeicherten Prozeduren INSERT, UPDATE und DELETE kopieren**  
 Wenn der Artikel Teil einer Transaktionsveröffentlichung ist und Sie im Abschnitt **Anweisungsübermittlung** dieses Dialogfelds gespeicherte Prozeduren zum Weitergeben von Änderungen an Abonnenten auswählen (Standardeinstellung), wählen Sie mithilfe dieser Option aus, ob die Prozeduren auf jeden Abonnenten kopiert werden. Wenn Sie **False**auswählen, müssen Sie die Prozeduren manuell kopieren. Andernfalls schlägt der Verteilungs-Agent beim Versuch, Änderungen zu übermitteln, fehl.  
  
 **Zielobjektbesitzer**  
 Beachten Sie folgende Punkte, wenn Sie einen anderen Wert als **dbo**eingeben:  
  
-   Bei Abonnenten mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder später müssen Sie sicherstellen, dass auf den Abonnenten ein Schema mit demselben Namen wie dem von Ihnen eingegebenen Wert erstellt wird. Weitere Informationen finden Sie unter [CREATE SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/create-schema-transact-sql.md).  
  
-   Fügen Sie bei Abonnenten mit Versionen vor [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]für jedes Schema einen Benutzer mit demselben Namen wie das Schema zur Abonnementdatenbank hinzu.  
  
 **Tabellenbereichsname**  
 Der Tabellenbereich, in dem die Nachverfolgungstabellen für Replikationsänderungen auf der Oracle-Serverinstanz erstellt werden. Weitere Informationen finden Sie unter [Verwalten von Oracle-Tabellenbereichen](../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md).  
  
 **Statement delivery**  
 Die Optionen in diesem Abschnitt gelten für alle Tabellen in Transaktionsveröffentlichungen. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt die Verwendung der Standardoptionen, sofern die Anwendung keine andere Funktionalität erfordert. Standardmäßig gibt die Transaktionsreplikation Änderungen an Abonnenten mithilfe einer Reihe gespeicherter Prozeduren weiter, die auf jedem Abonnenten gespeichert sind. Wenn für eine Tabelle auf dem Verleger ein Einfüge-, Update- oder Löschvorgang ansteht, wird der Vorgang in einen Aufruf einer gespeicherten Prozedur auf den Abonnenten übersetzt.  
  
 Mit den Optionen unter **Anweisungsübermittlung** wird angegeben, ob eine gespeicherte Prozedur verwendet wird und wenn ja, welches Format für an die Prozedur übergebene Parameter verwendet werden soll. Die Optionen für **gespeicherte Prozeduren** ermöglichen es Ihnen, die Prozeduren zu verwenden, die die Replikation automatisch erstellt, oder diese durch von Ihnen erstellte benutzerdefinierte Prozeduren zu ersetzen.  
  
 Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
### <a name="data-mapping-tab"></a>Datenzuordnung (Registerkarte)  
 **Spaltenname**  
 Der Name der Spalte auf dem Verleger (schreibgeschützt).  
  
 **Verlegerdatentyp**  
 Der Oracle-Datentyp der Spalte auf dem Verleger (schreibgeschützt). Der Datentyp kann nur direkt in der Oracle-Datenbank geändert werden. Weitere Informationen finden Sie in der Oracle-Dokumentation.  
  
 **Abonnentendatentyp**  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp, dem der Oracle-Datentyp bei der Replikation von Daten zugeordnet ist:  
  
-   Bei bestimmten Datentypen gibt es nur eine mögliche Zuordnung. In diesem Fall ist die Spalte im Eigenschaftenraster schreibgeschützt.  
  
-   Für einige Typen sind mehrere Typen zur Auswahl vorhanden. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt die Verwendung der Standardzuordnung, sofern die Anwendung keine andere Zuordnung erfordert. Weitere Informationen finden Sie unter [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Erstellen und Anwenden der Anfangsmomentaufnahme](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Erneutes Initialisieren eines Abonnements](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
