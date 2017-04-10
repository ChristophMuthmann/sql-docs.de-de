---
title: "Erstellen und Verwalten von Volltextindizes | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Volltextindizes [SQL Server], Informationen zu"
ms.assetid: f8a98486-5438-44a8-b454-9e6ecbc74f83
caps.latest.revision: 23
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 20
---
# Erstellen und Verwalten von Volltextindizes
  Die Informationen in Volltextindizes werden vom Volltextmodul verwendet, um Volltextabfragen zu kompilieren, die eine Tabelle schnell nach bestimmten Wörtern oder Wortkombination durchsuchen können. In einem Volltextindex werden Informationen zu signifikanten Wörtern und ihre Position innerhalb einer oder mehreren Spalte einer Datenbanktabelle gespeichert. Ein Volltextindex ist besonderer Typ eines tokenbasierten funktionellen Index, der durch das Volltextmodul für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt und verwaltet wird. Der Vorgang der Erstellung eines Volltextindexes unterscheidet sich vom Erstellen anderer Indextypen. Statt eine B-Struktur basierend auf einem Wert in einer bestimmten Zeile aufzubauen, erstellt das Volltextsuchmodul eine invertierte, gestapelte, komprimierte Indexstruktur basierend auf einzelnen Token aus dem zu indizierenden Text.  Die Größe des Volltextindexes wird nur durch den verfügbaren Speicherplatz des Computers eingeschränkt, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird.  
  
 Beginnend mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] sind Volltextindizes in das Datenbankmodul integriert und befinden sich nicht mehr im Dateisystem, wie dies in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] der Fall war. Bei einer neuen Datenbank ist ein Volltextkatalog jetzt ein virtuelles Objekt, das keiner Dateigruppe angehört. Es ist lediglich ein logisches Konzept, das für eine Gruppe von Volltextindizes steht. Beachten Sie jedoch, dass während des Upgrades einer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Datenbank für alle Volltextkataloge, die Datendateien enthalten, eine neue Dateigruppe erstellt wird. Weitere Information finden Sie unter [Upgrade der Volltextsuche](../../relational-databases/search/upgrade-full-text-search.md).  
  
> [!NOTE]  
>  In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höheren Versionen befindet sich das Volltextmodul im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozess, anstatt in einem separaten Dienst. Durch die Integration des Volltextmoduls in das Datenbankmodul konnte die Verwaltbarkeit verbessert und die Leistung bei gemischten Abfragen sowie die Leistung insgesamt optimiert werden.  
  
 Nur ein Volltextindex pro Tabelle ist zulässig. Damit ein Volltextindex für eine Tabelle erstellt werden kann, muss die Tabelle eine einzelne eindeutige Spalte aufweisen, die keine NULL-Werte enthält. Sie können einen Volltextindex für die Volltextsuche für alle Spalten vom Typ **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** und **varbinary(max)** erstellen. Beim Erstellen eines Volltextindex für eine Spalte, dessen Datentyp **varbinary**, **varbinary(max)**, **image** oder **xml** lautet, müssen Sie eine Typspalte angeben. Eine *Typspalte* ist eine Tabellenspalte, in der die Dateierweiterung (DOC, PDF, XLS usw.) für das Dokument in der betreffenden Zeile gespeichert wird.  
  
 Der Vorgang, bei dem ein Volltextindex erstellt und verwaltet wird, wird als *Auffüllung* (oder *Durchforstung*) bezeichnet. Es gibt drei Auffüllungstypen für Volltextindizes: vollständige Auffüllungen, Auffüllungen mithilfe der Änderungsnachverfolgung sowie inkrementelle, auf Timestamps basierende Auffüllungen. Weitere Informationen finden Sie unter [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md).  
  
##  <a name="tasks"></a> Allgemeine Aufgaben  
 **So erstellen Sie einen Volltextindex**  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
 **So ändern Sie einen Volltextindex**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
 **So löschen Sie einen Volltextindex**  
  
-   [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)  
  
 [In diesem Thema](#top)  
  
##  <a name="structure"></a> Struktur der Volltextindizes  
 Die Kenntnis der Struktur eines Volltextindex hilft Ihnen dabei, die Funktionsweise des Volltextsuchmoduls zu verstehen. In diesem Thema wird der folgende Auszug der Tabelle **Dokument** in [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] als Beispieltabelle verwendet. Der Auszug enthält nur zwei Spalten, **DocumentID** und **Title** , und drei Zeilen der Tabelle.  
  
 Für dieses Beispiel wird davon ausgegangen, dass ein Volltextindex für die **Title**-Spalte erstellt wurde.  
  
|DocumentID|Titel|  
|----------------|-----------|  
|1|Crank Arm and Tire Maintenance|  
|2|Front Reflector Bracket and Reflector Assembly 3|  
|3|Front Reflector Bracket Installation|  
  
 Die folgende Tabelle, in der Fragment 1 enthalten ist, zeigt den Inhalt des Volltextindex, der für die **Title**-Spalte der **Document**-Tabelle erstellt wurde. Volltextindizes enthalten mehr Informationen als die in dieser Tabelle dargestellten. Die Tabelle ist eine logische Darstellung eines Volltextindex und wird nur zu Demonstrationszwecken bereitgestellt. Die Zeilen werden in einem komprimierten Format gespeichert, um die Datenträgernutzung zu optimieren.  
  
 Beachten Sie, dass die Daten gegenüber den Originaldokumenten umgekehrt wurden. Die Umkehrung tritt auf, da die Schlüsselwörter den Dokument-IDs zugeordnet sind. Aus diesem Grund wird ein Volltextindex häufig als invertierter Index bezeichnet.  
  
 Beachten Sie auch, dass das Schlüsselwort "and" aus dem Volltextindex entfernt wurde. Dies ist der Fall, weil "and" ein Stoppwort ist und das Entfernen von Stoppwörtern aus einem Volltextindex zu beträchtlichen Einsparungen beim Datenträgerspeicher führen kann, wodurch die Abfrageleistung verbessert wird. Weitere Informationen finden sie unter [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
 **Fragment 1**  
  
|Schlüsselwort|ColId|DocId|Vorkommen|  
|-------------|-----------|-----------|----------------|  
|Crank|1|1|1|  
|Arm|1|1|2|  
|Tire|1|1|4|  
|Verwaltung|1|1|5|  
|Front|1|2|1|  
|Front|1|3|1|  
|Reflector|1|2|2|  
|Reflector|1|2|5|  
|Reflector|1|3|2|  
|Bracket|1|2|3|  
|Bracket|1|3|3|  
|Assembly|1|2|6|  
|3|1|2|7|  
|Installation|1|3|4|  
  
 Die **Keyword** -Spalte enthält eine Darstellung eines einzelnen Tokens, das zum Zeitpunkt der Indizierung extrahiert wurde. Woraus ein Token besteht, wird durch die Wörtertrennung bestimmt.  
  
 Die **ColId**-Spalte enthält einen Wert, der einer bestimmten volltextindizierten Spalte entspricht.  
  
 Die **DocId**-Spalte enthält Werte für eine aus acht Bytes bestehende ganze Zahl, die einem bestimmten Volltextschlüsselwert in einer volltextindizierten Tabelle zugeordnet ist. Diese Zuordnung ist notwendig, wenn der Volltextschlüssel kein ganzzahliger Datentyp ist. In diesen Fällen werden Zuordnungen zwischen Volltextschlüsselwerten und **DocId**-Werten in einer separaten Tabelle mit der Bezeichnung DocId-Zuordnungstabelle verwaltet. Um diese Zuordnungen abzufragen, verwenden Sie die gespeicherte Systemprozedur [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md). Um eine Suchbedingung zu erfüllen, müssen DocId-Werte aus der obigen Tabelle mit der DocId-Zuordnungstabelle verknüpft werden, um Zeilen aus der abgefragten Basistabelle abzurufen. Wenn der Volltextschlüsselwert der Basistabelle ein ganzzahliger Typ ist, wird der Wert direkt als DocID verwendet, und es ist keine Zuordnung erforderlich. Die Verwendung von ganzzahligen Volltextschlüsselwerten kann also zur Optimierung von Volltextabfragen beitragen.  
  
 Die Spalte **Vorkommen** enthält einen ganzzahligen Wert. Für jeden DocId-Wert ist eine Liste von Vorkommenwerten vorhanden, die den relativen Wortoffsets des betreffenden Schlüsselworts innerhalb dieser DocId entsprechen. Die Vorkommenwerte sind zum Ermitteln von Ausdrucks- oder NEAR-Übereinstimmungen hilfreich, da z. B. Ausdrücke numerisch aufeinander folgende Vorkommenwerte besitzen. Zum Berechnen von Relevanzbewertungen erfüllen sie ebenfalls eine hilfreiche Funktion. So kann z. B. die Anzahl der Vorkommen eines Schlüsselworts in einer DocId zur Rangfolgenberechnung verwendet werden.  
  
 [In diesem Thema](#top)  
  
##  <a name="fragments"></a> Volltextindexfragmente  
 Der logische Volltextindex wird normalerweise auf mehrere interne Tabellen aufgeteilt. Jede interne Tabelle wird als Volltextindexfragment bezeichnet. Einige dieser Fragmente enthalten ggf. aktuellere Daten als andere. Wenn Benutzer z. B. die folgende Zeile aktualisieren, deren DocId den Wert 3 hat, und für die Tabelle die automatische Änderungsnachverfolgung verwendet wird, wird ein neues Fragment erstellt.  
  
|DocumentID|Titel|  
|----------------|-----------|  
|3|Rear Reflector|  
  
 Im folgenden Beispiel, das Fragment 2 zeigt, enthält das Fragment im Vergleich zu Fragment 1 für DocId 3 aktuellere Daten. Wenn Benutzer eine Abfrage für "Rear Reflector" ausführen, werden daher für DocId 3 die Daten aus Fragment 2 verwendet. Jedes Fragment ist mit einem Erstellungszeitstempel gekennzeichnet, der abgefragt werden kann, indem die Katalogsicht [sys.fulltext_index_fragments](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md) verwendet wird.  
  
 **Fragment 2**  
  
|Schlüsselwort|ColId|DocId|Occ|  
|-------------|-----------|-----------|---------|  
|Rear|1|3|1|  
|Reflector|1|3|2|  
  
 Wie Sie in Fragment 2 sehen, müssen Volltextabfragen jedes Fragment intern abfragen und ältere Einträge verwerfen. Daher können zu viele Volltextindexfragmente im Volltextindex zu einer beträchtlichen Verringerung der Abfrageleistung führen. Um die Anzahl der Fragmente zu reduzieren, organisieren Sie den Volltextkatalog neu, indem Sie die REORGANIZE-Option der [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung verwenden. Diese Anweisung führt eine *Hauptzusammenführung* aus, sodass die Fragmente zu einem einzigen größeren Fragment zusammengeführt werden, und entfernt alle veralteten Einträge aus dem Volltextindex.  
  
 Nach dem erneuten Organisieren würde der Beispielindex die folgenden Zeilen enthalten:  
  
|Schlüsselwort|ColId|DocId|Occ|  
|-------------|-----------|-----------|---------|  
|Crank|1|1|1|  
|Arm|1|1|2|  
|Tire|1|1|4|  
|Verwaltung|1|1|5|  
|Front|1|2|1|  
|Rear|1|3|1|  
|Reflector|1|2|2|  
|Reflector|1|2|5|  
|Reflector|1|3|2|  
|Bracket|1|2|3|  
|Assembly|1|2|6|  
|3|1|2|7|  
  
 [In diesem Thema](#top)  
  
  