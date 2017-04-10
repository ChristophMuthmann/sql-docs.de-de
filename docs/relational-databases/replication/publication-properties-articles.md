---
title: "Ver&#246;ffentlichungseigenschaften (Registerkarte Artikel) | Microsoft Docs"
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
  - "sql13.rep.newpubwizard.pubproperties.articles.f1"
ms.assetid: bdeea318-a153-44b8-9e51-9155f3bad18b
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Ver&#246;ffentlichungseigenschaften (Registerkarte Artikel)
  Die Seite **Artikel** des Dialogfelds **Veröffentlichungseigenschaften** enthält Informationen zu den in einer Veröffentlichung enthaltenen Artikeln. Auf dieser Seite können Sie Artikel per Drag und Drop aus vorhandenen Veröffentlichungen hinzufügen sowie Artikeleigenschaften und Filtereinstellungen für Spalten ändern.  
  
> [!NOTE]  
>  Nachdem eine Veröffentlichung erstellt wurde, ist für bestimmte Eigenschaftsänderungen eine neue Momentaufnahme erforderlich. Wenn für eine Veröffentlichung Abonnements erstellt wurden, müssen bei bestimmten Änderungen alle Abonnements erneut initialisiert werden. Weitere Informationen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../relational-databases/replication/publish/change-publication-and-article-properties.md) und [Hinzufügen und löschen Artikeln aus vorhandenen Veröffentlichungen](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 Wenn Sie ein Datenbankobjekt veröffentlichen, das von mindestens einem weiteren Datenbankobjekt abhängt, müssen Sie alle Objekte veröffentlichen, auf die verwiesen wird. Wenn Sie beispielsweise eine Sicht veröffentlichen, die von einer Tabelle abhängt, muss auch die Tabelle veröffentlicht werden.  
  
 Objekte, die nicht veröffentlicht werden können, sind neben dem Objekt durch ein rotes Symbol gekennzeichnet. Zusätzlich wird im Informationsbereich am unteren Rand der Assistentenseite eine Erläuterung angezeigt. Folgende Objekte können nicht veröffentlicht werden:  
  
-   Verschlüsselte Objekte.  
  
-   Indizierte Sichten mit Spalten, in denen NULL-Werte zulässig sind.  
  
-   Tabellen ohne Primärschlüssel können nicht in Transaktionsveröffentlichungen veröffentlicht werden.  
  
-   Tabellen können nicht gleichzeitig in einer Mergeveröffentlichung und in einer Transaktionsveröffentlichung veröffentlicht werden, für die Abonnements mit verzögertem Update über eine Warteschlange zulässig sind. Weitere Informationen zum Veröffentlichen eines Artikels in mehreren Veröffentlichungen finden Sie im Abschnitt "Veröffentlichen von Tabellen in mehreren Veröffentlichungen" im [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
## Oracle-Verleger  
 Für Oracle-Verleger gelten zusätzliche Festlegungen:  
  
-   Eine Liste der Objekte, die aus Oracle veröffentlicht werden können, finden Sie unter [Design Considerations and Limitations for Oracle Publishers](../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md). Objekte, die nicht veröffentlicht werden können, werden nicht angezeigt.  
  
-   Eine Liste der Datentypen, die veröffentlicht werden können, finden Sie unter [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md). Spalten mit Datentypen, die nicht veröffentlicht werden können, werden nicht angezeigt.  
  
## Spaltenfilter  
 Filtern von Spalten auf dieser Seite erweitern Sie eine Tabelle in der **zu veröffentlichende Objekte** Bereich auswählen und dann nur die erforderlichen Spalten (Zeilen gefiltert werden können, der **Tabellenzeilen filtern** Seite dieses Assistenten). Das Filtern von Spalten kann aus verschiedenen Gründen nützlich sein, darunter aus Sicherheitsgründen (um zu vermeiden, dass vertrauliche Daten ungewollt repliziert werden) oder aus Leistungsgründen (um beispielsweise die Replikation großer BLOB-Spalten zu vermeiden). Weitere Informationen zum Filtern von Spalten, einschließlich einer Liste von Spaltentypen, die gefiltert werden können, finden Sie unter [veröffentlichten Filterdaten](../../relational-databases/replication/publish/filter-published-data.md).  
  
## Optionen  
 Im Bereich **Zu veröffentlichende Objekte** können Sie folgende Schritte ausführen:  
  
-   Anzeigen aller für die Replikation verfügbaren Objekte.  
  
-   Hinzufügen eines Artikels zu einer Veröffentlichung durch Aktivieren des Kontrollkästchens neben dem Objekt.  
  
-   Löschen eines Artikels aus einer Veröffentlichung durch Deaktivieren des Kontrollkästchens neben dem Objekt. Informationen dazu, wann Artikel gelöscht werden können, finden Sie unter [Hinzufügen und löschen Artikeln aus vorhandenen Veröffentlichungen](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
-   Einschließen aller Objekte eines bestimmten Typs (z. B. eine Tabelle) in die Veröffentlichung durch Aktivieren des Kontrollkästchens neben, der Objekttyp (z. B. **Tabellen**).  
  
-   Erweitern von Tabellenknoten zum Anzeigen der Spalten in der Tabelle.  
  
-   Filtern von Tabellenspalten in einer Veröffentlichung durch Deaktivieren des Kontrollkästchens neben der Spalte bzw. Einbeziehen unveröffentlichter Spalten durch Aktivieren des Kontrollkästchens.  
  
-   Aufrufen eines Kontextmenüs durch Klicken mit der rechten Maustaste auf ein Objekt.  
  
 **Artikeleigenschaften**  
 Klicken Sie auf **Artikeleigenschaften** , und klicken Sie dann auf eine der folgenden:  
  
-   Klicken Sie auf **Eigenschaften des hervorgehobenen \< ObjectType> Artikel** zum Starten der **Artikeleigenschaften - \< ObjectName>** das Dialogfeld in diesem Dialogfeld vorgenommene Änderungen gelten nur für das Objekt, das im Objektbereich hervorgehoben ist die **Artikel** Seite.  
  
-   Klicken Sie auf **Eigenschaften aller \< ObjectType> Artikel**, um die **Eigenschaften für alle \< ObjectType> Artikel** das Dialogfeld in diesem Dialogfeld vorgenommene Änderungen gelten für alle Objekte dieses Typs im Objektbereich auf der **Artikel** Seite, einschließlich Objekten, die noch nicht für die Veröffentlichung ausgewählt.  
  
    > [!NOTE]  
    >  Eigenschaftenänderungen in der **Eigenschaften für alle \< ObjectType> Artikel** Überschreiben Sie alle zuvor im Dialogfeld die **Artikeleigenschaften - \< ObjectName>** (Dialogfeld). Wenn Sie beispielsweise sowohl mehrere Standardwerte für alle Artikel eines Objekttyps als auch bestimmte Eigenschaften für einzelne Objekte festlegen möchten, legen Sie zuerst die Standardwerte für alle Artikel fest. Legen Sie anschließend die Eigenschaften für die einzelnen Objekte fest.  
  
 **Die durch Hervorhebung markierte Tabelle ist nur herunterladbar**  
 Nur für Mergereplikationen zulässig. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen. Durch Auswahl dieser Option geben Sie an, dass bei Verwendung eines Clientabonnements keine Änderungen auf dem Abonnenten zulässig sind. Da nur herunterladbare Artikel nicht auf dem Abonnenten aktualisiert werden können, wird das Nachverfolgen von Metadaten nicht an die Abonnenten gesendet. Das kann den Speicher auf den Abonnenten entlasten und zu einer höheren Leistung führen, besonders bei einer langsamen Netzwerkverbindung. Diese Option entspricht der Wert **nur herunterladbar auf Abonnenten, abonnentenänderungen** für die Option **synchronisierungsrichtung** in den **Artikeleigenschaften** Dialogfeld. Weitere Informationen finden Sie unter [Merge Replikationsleistung mit Download-Only Artikeln optimieren](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **Nur in der Liste aktivierte Objekte anzeigen**  
 Aktivieren Sie dieses Kontrollkästchen, um nur die im Objektbereich ausgewählten Artikel anzuzeigen.  
  
## Siehe auch  
 [Erstellen einer Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Erstellen und Anwenden der Anfangsmomentaufnahme](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Erneutes Initialisieren eines Abonnements](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  