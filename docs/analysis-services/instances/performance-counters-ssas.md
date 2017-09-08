---
title: Leistungsindikatoren (SSAS) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 05d7d5ab-a96c-4f82-94b1-48a657d7c580
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0e2d625f6c9060f32fb2a2dc676c84c673f55c8f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="performance-counters-ssas"></a>Leistungsindikatoren (SSAS)
  Mit dem Systemmonitor können Sie die Leistung einer Microsoft SQL Server Analysis Services (SSAS)-Instanz mithilfe von Leistungsindikatoren überwachen.  
  
 Der Systemmonitor ist ein MMC-Snap-In ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Control), das die Verwendung von Ressourcen nachverfolgt. Sie können dieses MMC-Snap-In starten, indem Sie an der Eingabeaufforderung **PerfMon** eingeben oder in der Systemsteuerung auf **Verwaltung**und anschließend auf **Systemmonitor**klicken. Mithilfe des Systemmonitors können Sie die Leistung und Aktivität von Server und Prozessen mithilfe vordefinierter Objekte und Leistungsindikatoren nachverfolgen sowie Ereignisse mithilfe benutzerdefinierter Leistungsindikatoren überwachen. Der Systemmonitor erfasst Anzahlwerte anstelle von Daten zu den Ereignissen, z. B. die Speicherauslastung, die Anzahl der aktiven Transaktionen oder die CPU-Aktivität. Für bestimmte Leistungsindikatoren können auch Schwellenwerte festgelegt werden, um Warnungen zu generieren, durch die Operatoren benachrichtigt werden.  
  
 Der Systemmonitor ist in der Lage, Remoteinstanzen und lokale Instanzen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu überwachen. Weitere Informationen finden Sie unter [Verwenden des Systemmonitors](http://technet.microsoft.com/library/cc749115.aspx).  
  
 Wenn Sie die Beschreibung eines Leistungsindikators anzeigen möchten, der mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]verwendet werden kann, öffnen Sie im Systemmonitor das Dialogfeld **Leistungsindikatoren hinzufügen** , wählen Sie ein Leistungsobjekt aus, und klicken Sie dann auf **Beschreibung anzeigen**. Die wichtigsten Leistungsindikatoren sind die CPU-Nutzung, die Speicherauslastung und die Datenträger-E/A-Geschwindigkeit. Es wird empfohlen, dass Sie mit diesen wichtigen Leistungsindikatoren beginnen und mit detaillierteren Indikatoren fortfahren, wenn Sie genauere Vorstellungen über die Verbesserungsmöglichkeiten durch eine Überwachung haben. Weitere Informationen zu den relevanten Leistungsindikatoren finden Sie im [SQL Server 2008 R2-Vorgangshandbuch](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
 Leistungsindikatoren werden so gruppiert, dass verwandte Leistungsindikatoren leichter auffindbar sind.  
  
## <a name="counters-by-groups"></a>Leistungsindikatoren nach Gruppen  
  
|Gruppieren|Description|  
|-----------|-----------------|  
|[Cache](#bkmk_Cache)|Statistik zum Analysis Services-Aggregationscache.|  
|[Verbindung](#bkmk_Connection)|Statistik zu Microsoft Analysis Services-Verbindungen.|  
|[Data Mining-Vorhersage](#bkmk_DataMiningPrediction)|Statistik zur Verarbeitung von Data Mining-Modellen.|  
|[Data Mining-Modellverarbeitung](#bkmk_DataMiningModelProcessing)|Statistik zur Erstellung von Vorhersagen aus Data Mining-Modellen.|  
|[Locks](#bkmk_Locks)|Statistik zu internen Microsoft Analysis Services-Serversperren.|  
|[MDX](#bkmk_MDX)|Statistik zu Microsoft Analysis Services-MDX-Berechnungen.|  
|[Speicher](#bkmk_Memory)|Statistik zu internem Microsoft Analysis Services-Serverspeicher.|  
|[Proaktives Zwischenspeichern](#bkmk_ProactiveCaching)|Statistik zur proaktiven Microsoft Analysis Services-Zwischenspeicherung.|  
|[Verarbeiten von Aggregationen](#bkmk_ProcAggregations)|Statistik zur Verarbeitung der Aggregationen in MOLAP-Datendateien.|  
|[Verarbeiten von Indizes](#bkmk_ProcIndexes)|Statistik zur Verarbeitung von Indizes für MOLAP-Datendateien.|  
|[Verarbeitung](#bkmk_Processing)|Statistik zur Verarbeitung von Daten.|  
|[Speichermodulabfrage](#bkmk_StorageEngineQuery)|Statistik zu Microsoft Analysis Services-Speichermodulabfragen.|  
|[Threads](#bkmk_Threads)|Statistik zu Microsoft Analysis Services-Threads.|  
  
###  <a name="bkmk_Cache"></a> Cache  
 Statistik zum Microsoft Analysis Services-Aggregationscache.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|KB aktuell|Aktueller vom Aggregationscache verwendeter Arbeitsspeicher (in KB).|  
|Pro Sekunde hinzugefügte KB|Menge des Arbeitsspeichers, die dem Cache hinzugefügt wird (in KB/s).|  
|Aktuelle Einträge|Aktuelle Anzahl von Cacheeinträgen.|  
|Einfügungen/s|Rate der Einfügungen in den Cache.  Die Rate wird pro Partition, Cube und Datenbank nachverfolgt.|  
|Entfernungen/s|Rate der Entfernungen vom Cache.  Wird pro Partition, Cube und Datenbank angegeben.  Entfernungen sind in der Regel auf Hintergrundbereinigungsprozesse zurückzuführen.|  
|Gesamte Einfügungen|Einfügungen in den Cache.  Die Rate wird pro Partition, Cube und Datenbank nachverfolgt.|  
|Gesamte Entfernungen|Entfernungen aus dem Cache.  Entfernungen werden pro Partition, Cube und Datenbank nachverfolgt.  Entfernungen sind in der Regel auf Hintergrundbereinigungsprozesse zurückzuführen.|  
|Direkte Treffer/s|Rate der direkten Cachetreffer. Ein Cachetreffer gibt an, dass Abfragen von einem vorhandenen Cacheeintrag beantwortet wurden.|  
|Fehlversuche/s|Rate der fehlgeschlagenen Zugriffe auf den Cache.|  
|Suchvorgänge/s|Rate der Cachesuchvorgänge.|  
|Gesamte direkte Treffer|Gesamtanzahl an direkten Cachetreffern.  Ein direkter Cachetreffer gibt an, dass Abfragen von vorhandenen Cacheeinträgen beantwortet wurden.|  
|Gesamte Fehlversuche|Gesamtanzahl an fehlgeschlagenen Zugriffe auf den Cache.|  
|Gesamte Suchvorgänge|Gesamtzahl der Suchvorgänge im Cache.|  
|Direkte Trefferquote|Verhältnis der direkten Cachetreffer zur Zwischenspeicherung von Suchvorgängen für den Zeitraum zwischen Indikatorwerten.|  
|Gesamte gefilterte Iteratorcachetreffer|Gesamtzahl der Cachetreffer in den gefilterten Ergebnissen, bei denen ein indizierter Iterator zurückgegeben wurde.|  
|Gesamtanzahl der gefilterten fehlgeschlagenen Zugriffe auf den Iteratorcache|Gesamtzahl der Cachetreffer, mit denen anhand der gefilterten Ergebnisse kein indizierter Iterator erstellt werden konnte. Stattdessen musste mit den gefilterten Ergebnissen ein neuer Cache erstellt werden.|  
  
###  <a name="bkmk_Connection"></a> Verbindung  
 Statistik zu Microsoft Analysis Services-Verbindungen.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|Aktuelle Verbindungen|Aktuelle Anzahl von eingerichteten Clientverbindungen.|  
|Anforderungen/s|Rate der Verbindungsanforderungen.  Dabei handelt es sich um erhaltene Anforderungen.|  
|Gesamte Anforderungen|Gesamte Verbindungsanforderungen.  Dabei handelt es sich um erhaltene Anforderungen.|  
|Erfolgreiche Vorgänge/s|Rate der erfolgreichen Verbindungsabschlüsse.|  
|Gesamte erfolgreiche Vorgänge|Gesamte erfolgreiche Verbindungen.|  
|Fehler/s|Rate der Verbindungsfehler.|  
|Gesamte Fehler|Gesamte fehlerhafte Verbindungsversuche.|  
|Aktuelle Benutzersitzungen|Aktuelle Anzahl der eingerichteten Benutzersitzungen.|  
  
###  <a name="bkmk_DataMiningModelProcessing"></a> Data Mining-Modellverarbeitung  
 Statistiken zur Microsoft Analysis Services Data Mining-Modellverarbeitung.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|Fälle/s|Rate, mit der Fälle verarbeitet werden.|  
|Verarbeitung aktueller Modelle|Aktuelle Anzahl der Modelle, die verarbeitet werden.|  
  
###  <a name="bkmk_DataMiningPrediction"></a> Data Mining-Vorhersage  
 Statistiken zu Microsoft Analysis Services Data Mining-Vorhersagen.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|Gleichzeitige Data Mining-Abfragen|Aktuelle Anzahl der Data Mining-Abfragen, an denen aktiv gearbeitet wird.|  
|Vorhersagen/s|Anzahl der Vorhersagen, die in Data Mining-Abfragen generiert werden|  
|Zeilen/s|Anzahl der Zeilen, die während einer Data Mining-Vorhersageabfrage behandelt wurden.|  
|Abfragen/s|Anzahl der Data Mining-Abfragen, die behandelt wurden.|  
|Abfragen gesamt|Gesamte vom Server empfangene Data Mining-Abfragen.|  
|Ergebniszeilen|Gesamtanzahl der Zeilen, die von Data Mining-Abfragen zurückgegeben wurden.|  
|Gesamte Vorhersagen|Gesamte vom Server empfangene Vorhersageabfragen.|  
  
###  <a name="bkmk_Locks"></a> Locks  
 Statistik zu internen Microsoft Analysis Services-Serversperren.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|Aktuelle Latchwartevorgänge|Aktuelle Anzahl von Threads, die auf einen Latch warten.  Dies sind Latchanforderungen, die nicht unmittelbar genehmigt werden konnten und sich im Wartezustand befinden.|  
|Latchwartevorgänge/s|Rate der Latchwartevorgänge, die nicht umgehend genehmigt werden konnten und vor der Genehmigung in einen Wartezustand versetzt wurden.|  
|Aktuelle Sperren|Aktuelle Anzahl der gesperrten Objekte.|  
|Aktuelle Sperrwartevorgänge|Aktuelle Anzahl der Clients, die auf eine Sperre warten.|  
|Sperranforderungen/s|Anzahl der Sperrungsanforderungen pro Sekunde.|  
|Erteilte Sperren/s|Anzahl der erteilten Sperren pro Sekunde.|  
|Sperrwartevorgänge/s|Anzahl der Sperrwartevorgänge pro Sekunde.  Dies sind Sperrungsanforderungen, die nicht unmittelbar genehmigt werden konnten und in einen Wartezustand versetzt wurden.|  
|Verweigerte Sperren/s|Rate der verweigerten Sperren.|  
|Sperraufhebungsanforderungen/s|Anzahl der Sperraufhebungsanforderungen pro Sekunde.|  
|Gesamte erkannte Deadlocks|Gesamtzahl der erkannten Deadlocks.|  
  
###  <a name="bkmk_MDX"></a> MDX  
 Statistik zu Microsoft Analysis Services-MDX-Berechnungen.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|Anzahl der abdeckenden Berechnungen|Gesamtzahl von Auswertungsknoten, die von MDX-Ausführungsplänen erstellt wurden, einschließlich aktiver und zwischengespeicherter Knoten.|  
|Aktuelle Anzahl der Auswertungsknoten|Aktuelle (ungefähre) Anzahl der Auswertungsknoten, die von MDX-Ausführungsplänen erstellt wurden, einschließlich aktiver und zwischengespeicherter Knoten.|  
|Anzahl der Speichermodul-Auswertungsknoten|Gesamtzahl der Speichermodul-Auswertungsknoten, die von MDX-Ausführungsplänen erstellt wurden.|  
|Anzahl der Knoten für die Auswertung nach Zellen|Gesamtzahl der Knoten für die Auswertung nach Zellen, die von MDX-Ausführungsplänen erstellt wurden.|  
|Anzahl der Massenmodus-Auswertungsknoten|Gesamtzahl der Massenmodus-Auswertungsknoten, die von MDX-Ausführungsplänen erstellt wurden.|  
|Anzahl der Auswertungsknoten, die eine einzelne Zelle abdeckten|Gesamtzahl der Auswertungsknoten, die von MDX-Ausführungsplänen erstellt wird, die nur eine Zelle abdeckten.|  
|Anzahl der Auswertungsknoten, die Berechnungen mit der gleichen Granularität beinhalten|Gesamtzahl der Auswertungsknoten, die von MDX-Ausführungsplänen erstellt wurden, für die die Berechnungen mit der gleichen Granularität wie beim Auswertungsknoten ausgeführt wurden.|  
|Aktuelle Anzahl der zwischengespeicherten Auswertungsknoten|Aktuelle (ungefähre) Anzahl der zwischengespeicherter Auswertungsknoten, die von MDX-Ausführungsplänen erstellt wurden.|  
|Anzahl der zwischengespeicherten Speichermodul-Auswertungsknoten|Gesamtzahl der zwischengespeicherten Speichermodul-Auswertungsknoten, die von MDX-Ausführungsplänen erstellt wurden.|  
|Anzahl der zwischengespeicherten Massenmodus-Auswertungsknoten|Gesamtzahl der zwischengespeicherten Massenmodus-Auswertungsknoten, die von MDX-Ausführungsplänen erstellt wurden.|  
|Anzahl zwischengespeicherter "anderer" Auswertungsknoten|Gesamtzahl der zwischengespeicherten Auswertungsknoten, die von MDX-Ausführungsplänen erstellt wurden, bei denen es sich weder um Speichermodule noch um Massenmodus handelt.|  
|Anzahl der Entfernungen von Auswertungsknoten|Gesamtzahl der Cacheentfernungen von Auswertungsknoten aufgrund von Konflikten.|  
|Anzahl der Hashsindextreffer im Cache der Auswertungsknoten|Gesamtzahl der Treffer im Cache von Auswertungsknoten, denen vom Hashindex entsprochen wurde.|  
|Anzahl der Treffer nach Zellen im Cache von Auswertungsknoten|Gesamte Anzahl der Treffer nach Zellen im Cache von Auswertungsknoten.|  
|Anzahl der Fehlversuche nach Zellen im Cache von Auswertungsknoten|Gesamte Anzahl der Fehlversuche nach Zellen im Cache von Auswertungsknoten.|  
|Anzahl der Teilcubetreffer im Cache von Auswertungsknoten|Gesamte Anzahl der Teilcubetreffer im Cache von Auswertungsknoten.|  
|Anzahl der Teilcubefehlversuche im Cache von Auswertungsknoten|Gesamte Anzahl der Teilcubefehlversuche im Cache von Auswertungsknoten.|  
|Gesamtzahl der Sonar-Teilcubes|Gesamte Anzahl von Teilcubes, die vom Abfrageoptimierer generiert wurden.|  
|Gesamte berechnete Zellen|Gesamtzahl der berechneten Zelleigenschaften.|  
|Gesamte Neuberechnungen|Gesamtzahl der Zellen, die aufgrund von Fehlern neu berechnet wurden.|  
|Gesamte Flatcacheeinfügungen|Gesamtzahl der Zellwerte, die in den Flatberechnungscache eingefügt wurden.|  
|Gesamter registrierter Berechnungscache|Gesamtzahl der registrierten Berechnungscaches.|  
|NON EMPTY gesamt|Häufigkeit, mit der ein NON EMPTY-Algorithmus verwendet wurde.|  
|Nicht optimierter NON EMPTY-Algorithmus gesamt|Häufigkeit, mit der ein nicht optimierter NON EMPTY-Algorithmus verwendet wurde.|  
|NON EMPTY für berechnete Elemente gesamt|Häufigkeit, mit der von einem NON EMPTY-Algorithmus eine Schleife über berechnete Elemente ausgeführt wurde.|  
|Autoexist gesamt|Häufigkeit, mit der Autoexist ausgeführt wurde.|  
|EXISTING gesamt|Häufigkeit, mit der EXISTING-Satz ausgeführt wurde.|  
  
###  <a name="bkmk_Memory"></a> Speicher  
 Statistik zu internem Microsoft Analysis Services-Serverspeicher.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|Seitenpool 64 KB zugeordnet|Von System geliehener Arbeitsspeicher in KB.  Dieser Speicher wird anderen Teilen des Servers zugewiesen.|  
|Seitenpool 64 KB Lookaside|Aktueller Speicher in 64 KB-Lookaside-Liste (in KB).  (Zur Verwendung bereite Speicherseiten.)|  
|Seitenpool 8 KB zugeordnet|Von 64 KB-Seitenpool geliehener Arbeitsspeicher (in KB).  Dieser Speicher wird anderen Teilen des Servers zugewiesen.|  
|Seitenpool 8 KB Lookaside|Aktueller Speicher in 8 KB-Lookaside-Liste (in KB).  (Zur Verwendung bereite Speicherseiten.)|  
|Seitenpool 1 KB zugeordnet|Von 64 KB-Seitenpool geliehener Arbeitsspeicher (in KB).  Dieser Speicher wird anderen Teilen des Servers zugewiesen.|  
|Seitenpool 1 KB Lookaside|Aktueller Speicher in 8 KB-Lookaside-Liste (in KB).  (Zur Verwendung bereite Speicherseiten.)|  
|Bereinigung – aktueller Preis|Aktueller Preis des Speichers, €/Byte/Zeit (normalisiert auf 1000).|  
|Bereinigungsausgleich/s|Rate der Ausgleichs- und Verkleinerungsvorgänge.|  
|Bereinigung - Arbeitsspeicherverkleinerung in KB/Sekunde|Verkleinerungsrate in KB/s|  
|Bereinigung - verkleinerbarer Arbeitsspeicher in KB|Umfang des Arbeitsspeichers in KB, der mit dem Hintergrundbereinigungsprozess bereinigt wird.|  
|Bereinigung - nicht verkleinerbarer Arbeitsspeicher in KB|Umfang des Arbeitsspeichers in KB, der nicht mit dem Hintergrundbereinigungsprozess bereinigt wird.|  
|Bereinigung - Arbeitsspeicher in KB|Umfang des Arbeitsspeichers in KB, der mit dem Hintergrundbereinigungsprozess bereinigt wird.  (Verkleinerbarer Arbeitsspeicher für Bereinigungsprozess + Nicht verkleinerbarer Arbeitsspeicher für Bereinigungsprozess.)|  
|Speicherauslastung in KB|Speicherauslastung des Serverprozesses, wie bei der Berechnung bereinigter Speicherkosten verwendet.  Entspricht dem Indikator "Process\PrivateBytes" zuzüglich der Größe der im Speicher abgebildeten Daten. Vom xVelocity-Modul für Datenanalyse im Arbeitsspeicher (VertiPaq) abgebildeter oder belegter Arbeitsspeicher, der über die xVelocity-Arbeitsspeichergrenze hinausgeht, wird dabei ignoriert.|  
|Untere Arbeitsspeichergrenze in KB|Niedriges Speicherlimit von der Konfigurationsdatei.|  
|Obere Arbeitsspeichergrenze in KB|Hohes Speicherlimit von der Konfigurationsdatei.|  
|AggCacheKB|Vom Aggregationscache aktuell belegter Arbeitsspeicher in KB.|  
|Kontingent in KB|Aktuelles Arbeitsspeicherkontingent in KB.  Auch als Speicherzuweisung oder reservierter Speicher bezeichnet.|  
|Kontingent blockiert|Aktuelle Anzahl der Kontingentanforderungen, die blockiert sind, bis andere Arbeitsspeicherkontingente freigegeben werden.|  
|Dateispeicher in KB|Vom Dateispeicher (Dateicache) aktuell belegter Arbeitsspeicher in KB.|  
|Dateispeicher-Seitenfehler/s|Seitenfehlerrate des Dateispeichers.|  
|Dateispeicher-Lesevorgänge/s|Dateispeicher-Seitenlesevorgänge/s|  
|Dateispeicher-Lesevorgänge in KB/s|Dateispeicher-Lesevorgänge in KB/s|  
|Dateispeicher-Schreibvorgänge/s|Im Dateispeicher geschriebene Seiten pro Sekunde.  Die Schreibvorgänge sind asynchron.|  
|Dateispeicher-Schreibvorgänge in KB/s|Dateispeicher in KB/s.  Die Schreibvorgänge sind asynchron.|  
|Dateispeicher-E/A-Fehler/s|Rate der Dateispeicher-E/A-Fehler.|  
|Dateispeicher-E/A-Fehler|Dateispeicher-E/A-Fehler gesamt.|  
|Dateispeicher-Clockpages überprüft/s|Rate, mit der der Hintergrundbereinigungsprozess Seiten daraufhin überprüft, ob sie entfernt werden können.|  
|Dateispeicher-Clockpages mit Verweis/s|Rate, mit der der Hintergrundbereinigungsprozess Seiten daraufhin überprüft, ob sie eine aktuelle Verweisanzahl besitzen (ob sie aktuell in Verwendung sind).|  
|Dateispeicher-Clockpages gültig/s|Rate, mit der der Hintergrundbereinigungsprozess Seiten daraufhin überprüft, ob sie entfernt werden können.|  
|Festgesetzter Dateispeicher in KB|Aktuell festgesetzter Dateispeicher in KB.|  
|Dimensionseigenschaftendatei im Arbeitsspeicher in KB|Aktuelle Dimensionseigenschaftendatei im Arbeitsspeicher in KB.|  
|Dimensionseigenschaftendatei im Arbeitsspeicher in KB pro Sekunde|Rate der Schreibvorgänge in Dimensionseigenschaftendatei im Arbeitsspeicher in KB.|  
|Potenzielle Größe der Dimensionseigenschaftendatei im Arbeitsspeicher in KB|Potenzielle Dimensionseigenschaftendatei im Arbeitsspeicher in KB.|  
|Dimensionseigenschaftendateien|Anzahl der Dimensionseigenschaftendateien.|  
|Dimensionsindexdatei (Hashdatei) im Arbeitsspeicher in KB|Größe der aktuellen Dimensionsindexdatei (Hashdatei) im Arbeitsspeicher in KB.|  
|Dimensionsindexdatei (Hashdatei) im Arbeitsspeicher in KB pro Sekunde|Rate der Schreibvorgänge in Dimensionsindexdatei (Hashdatei) im Arbeitsspeicher in KB.|  
|Potenzielle Dimensionsindexdatei (Hashdatei) im Arbeitsspeicher in KB|Potenzielle Größe der Dimensionsindexdatei (Hashdatei) im Arbeitsspeicher in KB.|  
|Dimensionsindexdateien (Hashdateien)|Anzahl der Dimensionsindexdateien (Hashdateien).|  
|Dimensionszeichenfolgendatei im Arbeitsspeicher in KB|Aktuelle Dimensionszeichenfolgendatei im Arbeitsspeicher in KB.|  
|Dimensionszeichenfolgendatei im Arbeitsspeicher in KB pro Sekunde|Rate der Schreibvorgänge in Dimensionszeichenfolgendatei im Arbeitsspeicher in KB.|  
|Potenzielle Dimensionszeichenfolgendatei im Arbeitsspeicher in KB|Potenzielle Dimensionszeichenfolgendatei im Arbeitsspeicher in KB.|  
|Dimensionszeichenfolgendateien|Anzahl der Dimensionszeichenfolgendateien.|  
|Zuordnungsdatei im Arbeitsspeicher in KB|Aktuelle Größe der Zuordnungsdatei im Arbeitsspeicher in KB.|  
|Zuordnungsdatei im Arbeitsspeicher in KB/s|Rate der Schreibvorgänge in Zuordnungsdatei im Arbeitsspeicher in KB.|  
|Potenzielle Zuordnungsdatei im Arbeitsspeicher in KB|Potenzielle Größe der Zuordnungsdatei im Arbeitsspeicher in KB.|  
|Zuordnungsdateien|Anzahl der Zuordnungsdateien.|  
|Aggregationszuordnungsdatei im Arbeitsspeicher in KB|Aktuelle Größe der Aggregationszuordnungsdatei im Arbeitsspeicher in KB.|  
|Aggregationszuordnungsdatei im Arbeitsspeicher in KB pro Sekunde|Rate der Schreibvorgänge in Aggregationszuordnungsdatei im Arbeitsspeicher in KB.|  
|Potenzielle Aggregationszuordnungsdatei im Arbeitsspeicher in KB|Größe der potenziellen Aggregationszuordnungsdatei im Arbeitsspeicher in KB.|  
|Aggregationszuordnungsdateien|Anzahl der Aggregationszuordnungsdateien.|  
|Faktendatendatei im Arbeitsspeicher in KB|Größe der aktuellen Faktendatendatei im Arbeitsspeicher in KB.|  
|Faktendatendatei im Arbeitsspeicher in KB pro Sekunde|Raten der Schreibvorgänge in Faktendatendatei im Arbeitsspeicher in KB.|  
|Potenzielle Faktendatendatei im Arbeitsspeicher in KB|Größe der potenziellen Faktendatendatei im Arbeitsspeicher in KB.|  
|Faktendatendateien|Anzahl der Faktendatendateien.|  
|Faktenzeichenfolgendatei im Arbeitsspeicher in KB|Größe der aktuellen Faktenzeichenfolgendatei im Arbeitsspeicher in KB.|  
|Faktenzeichenfolgendatei im Arbeitsspeicher in KB pro Sekunde|Rate der Schreibvorgänge in Faktenzeichenfolgendatei im Arbeitsspeicher in KB.|  
|Potenzielle Faktenzeichenfolgendatei im Arbeitsspeicher in KB|Größe der potenziellen Faktenzeichenfolgendatei im Arbeitsspeicher in KB.|  
|Faktenzeichenfolgendateien|Anzahl der Faktenzeichenfolgendateien.|  
|Faktenaggregationsdatei im Arbeitsspeicher in KB|Aktuelle Größe der Faktenaggregationsdatei im Arbeitsspeicher in KB.|  
|Faktenaggregationsdatei im Arbeitsspeicher in KB pro Sekunde|Rate der Schreibvorgänge in Faktenaggregationsdatei im Arbeitsspeicher in KB.|  
|Potenzielle Faktenaggregationsdatei im Arbeitsspeicher in KB|Größe der potenziellen Faktenaggregationsdatei im Arbeitsspeicher in KB.|  
|Faktenaggregationsdateien|Anzahl der Faktenaggregationsdateien.|  
|Andere Datei im Arbeitsspeicher in KB|Größe der aktuellen anderen Datei im Arbeitsspeicher in KB.|  
|Andere Datei im Arbeitsspeicher in KB/s|Rate der Schreibvorgänge in andere Datei im Arbeitsspeicher in KB.|  
|Potenzielle andere Datei im Arbeitsspeicher in KB|Größe der potenziellen anderen Datei im Arbeitsspeicher in KB.|  
|Andere Dateien|Anzahl anderer Dateien.|  
|Ausgelagerte VertiPaq-Daten (KB)|Der ausgelagerte Arbeitsspeicher (in KB), der für speicherinterne Daten verwendet wird.|  
|Nicht ausgelagerte VertiPaq-Daten (KB)|Der Arbeitsspeicher (in KB), der im Workingset für die Verwendung durch das speicherinterne Modul gesperrt ist.|  
|Im Speicher abgebildete VertiPaq-Daten (KB)|Der auslagerbare Arbeitsspeicher (in KB), der für speicherinterne Daten verwendet wird.|  
|Grenzwert für den festen Speicher (KB)|Der Grenzwert für den festen Speicher aus der Konfigurationsdatei.|  
|VertiPaq-Arbeitsspeichergrenze (KB)|Speicherinterner Grenzwert aus der Konfigurationsdatei.|  
  
###  <a name="bkmk_ProactiveCaching"></a> Proaktives Zwischenspeichern  
 Statistik zur proaktiven Microsoft Analysis Services-Zwischenspeicherung.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|Benachrichtigungen/s|Rate der Benachrichtigungen von der relationalen Datenbank.|  
|Verarbeitungsabbrüche/s|Rate der Verarbeitungsabbrüche, die durch Benachrichtigungen verursacht werden.|  
|Start des proaktiven Zwischenspeicherns/s|Rate der Starts des proaktiven Zwischenspeicherns.|  
|Abschluss für proaktives Zwischenspeichern/s|Abschlussrate für proaktives Zwischenspeichern.|  
  
###  <a name="bkmk_ProcAggregations"></a> Verarbeiten von Aggregationen  
 Statistik zur Verarbeitung von Aggregationen in MOLAP-Datendateien in Microsoft Analysis Services.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|Aktuelle Partitionen|Aktuelle Anzahl der Partitionen, die verarbeitet werden.|  
|Gesamte Partitionen|Gesamtanzahl der verarbeiteten Partitionen (unabhängig vom Erfolg).|  
|Arbeitsspeichergröße in Zeilen|Größe der aktuellen Aggregationen im Arbeitsspeicher.  Diese Zahl ist eine Schätzung.|  
|Arbeitsspeichergröße in Bytes|Größe der aktuellen Aggregationen im Arbeitsspeicher.  Diese Zahl ist eine Schätzung.|  
|Zusammengeführte Zeilen/s|Rate der in einer Aggregation zusammengeführten oder in eine Aggregation eingefügten Zeilen.|  
|Erstellte Zeilen/s|Rate der erstellten Aggregationszeilen.|  
|In temporäre Datei geschriebene Zeilen/s|Rate des Schreibens von Zeilen in eine temporäre Datei.  Temporäre Dateien werden geschrieben, wenn Aggregationen das Arbeitsspeichergrenze überschreiten.|  
|In temporäre Datei geschriebene Bytes/s|Rate des Schreibens von Bytes in eine temporäre Datei.  Temporäre Dateien werden geschrieben, wenn Aggregationen das Arbeitsspeichergrenze überschreiten.|  
  
###  <a name="bkmk_ProcIndexes"></a> Verarbeiten von Indizes  
 Statistik zur Verarbeitung von Indizes für MOLAP-Datendateien in Microsoft Analysis Services.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|Aktuelle Partitionen|Aktuelle Anzahl der Partitionen, die verarbeitet werden.|  
|Gesamte Partitionen|Gesamtanzahl der verarbeiteten Partitionen (unabhängig vom Erfolg).|  
|Zeilen/s|Rate der Zeilen aus MOLAP-Dateien, die zum Erstellen von Indizes verwendet wurden.|  
|Ergebniszeilen|Gesamte Zeilen aus MOLAP-Dateien, die zum Erstellen von Indizes verwendet wurden.|  
  
###  <a name="bkmk_Processing"></a> Verarbeitung  
 Statistiken zur Microsoft Analysis Services-Datenverarbeitung.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|Zeilen lasen/s|Rate der aus allen relationalen Datenbanken gelesenen Zeilen.|  
|Gelesene Zeilen gesamt|Anzahl der aus allen relationalen Datenbanken gelesenen Zeilen.|  
|Konvertierte Zeilen/s|Rate der bei der Verarbeitung konvertierten Zeilen.|  
|Konvertierte Zeilen gesamt|Anzahl der bei der Verarbeitung konvertierten Zeilen.|  
|Geschriebene Zeilen/s|Rate der bei der Verarbeitung geschriebenen Zeilen.|  
|Geschriebene Zeilen gesamt|Anzahl der bei der Verarbeitung geschriebenen Zeilen.|  
  
###  <a name="bkmk_StorageEngineQuery"></a> Speichermodulabfrage  
 Statistik zu Microsoft Analysis Services-Speichermodulabfragen.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|Aktuelle Measuregruppenabfragen|Aktuelle Anzahl der Measuregruppenabfragen, die aktiv bearbeitet werden.|  
|Measuregruppenabfragen/s|Rate der Measuregruppenabfragen|  
|Measuregruppenabfragen gesamt|Gesamtanzahl der Abfragen der Measuregruppe.|  
|Aktuelle Dimensionsabfragen|Aktuelle Anzahl der Dimensionsabfragen, die aktiv bearbeitet werden.|  
|Dimensionsabfragen/s|Rate der Dimensionsabfragen|  
|Gesamte Dimensionsabfragen.|Gesamtzahl der Dimensionabfragen.|  
|Beantwortete Abfragen/s|Rate der beantworteten Abfragen.|  
|Gesamte beantwortete Abfragen|Gesamtzahl der beantworteten Abfragen.|  
|Gesendete Bytes/s|Rate der vom Server an Clients als Antwort auf Abfragen gesendeten Bytes.|  
|Gesendete Bytes gesamt|Gesamtanzahl der vom Server an Clients als Antwort auf Abfragen gesendeten Bytes.|  
|Gesendete Zeilen/s|Rate der vom Server an Clients gesendeten Zeilen.|  
|Gesendete Zeilen gesamt|Gesamtanzahl der vom Server an Clients gesendeten Zeilen.|  
|Abfragen aus Cache direkt/s|Rate der direkt aus dem Cache beantworteten Abfragen.|  
|Abfragen aus Cache gefiltert/s|Rate der durch Filtern vorhandener Cacheeinträge beantworteten Abfragen.|  
|Abfragen aus Datei/s|Rate der aus Dateien beantworteten Abfragen.|  
|Abfragen aus Cache direkt (gesamt)|Gesamtanzahl der direkt aus dem Cache abgeleiteten Abfragen.  Dies gilt pro Partition.|  
|Abfragen aus Cache gefiltert gesamt)|Gesamtanzahl der durch Filtern vorhandener Cacheeinträge beantworteten Abfragen.|  
|Abfragen aus Datei gesamt|Gesamtanzahl der aus Dateien beantworteten Abfragen.|  
|Zuordnungslesevorgänge/s|Anzahl der logischen Lesevorgänge für die Zuordnungsdatei.|  
|Zuordnungsbytes/s|Aus der Zuordnungsdatei gelesene Bytes.|  
|Datenlesevorgänge/s|Anzahl der logischen Lesevorgänge für die Datendatei.|  
|Datenbytes/s|Aus der Datendatei gelesene Bytes.|  
|Durchschnittl. Zeit/Abfrage|Durchschnittliche Zeit pro Abfrage in Millisekunden.  Die Antwortzeit basiert auf den Abfragen, die seit der letzten Messung des Leistungsindikators beantwortet wurden.|  
|Netzwerkroundtrips/s|Rate der Netzwerkroundtrips.  Dies schließt die gesamte Client/Server-Kommunikation ein.|  
|Netzwerkroundtrips gesamt|Netzwerkroundtrips gesamt.  Dies schließt die gesamte Client/Server-Kommunikation ein.|  
|Flatcache-Suchvorgänge/s|Rate der Flatcache-Suchvorgänge.  Hierzu gehören globale Flatcaches sowie Sitzungs- und Abfragebereichs-Flatcaches.|  
|Flatcachetreffer/s|Rate der Flatcachetreffer.  Hierzu gehören globale Flatcaches sowie Sitzungs- und Abfragebereichs-Flatcaches.|  
|Berechnungscache-Suchvorgänge/s|Rate der Berechnungscache-Suchvorgänge.  Hierzu gehören globale Caches, Sitzungs- und Abfragebereichs-Berechnungscaches.|  
|Berechnungscachetreffer/s|Rate der Berechnungscachetreffer.  Hierzu gehören globale Caches, Sitzungs- und Abfragebereichs-Berechnungscaches.|  
|Suchvorgänge im permanenten Cache/s|Rate der Suchvorgänge im permanenten Cache.  Permanente Caches werden durch die CACHE-Anweisung des MDX-Skripts erstellt.|  
|Treffer im permanenten Cache/s|Rate der Treffer im permanenten Cache.  Permanente Caches werden durch die CACHE-Anweisung des MDX-Skripts erstellt.|  
|Dimensionscache-Suchvorgänge/s|Rate der Dimensionscache-Suchvorgänge.|  
|Dimensionscachetreffer/s|Rate der Dimensionscachetreffer.|  
|Measuregruppencache-Suchvorgänge/s|Rate der Measuregruppencache-Suchvorgänge.|  
|Measuregruppencache-Treffer/s|Rate der Measuregruppencache-Treffer.|  
|Aggregationssuchvorgänge/s|Rate der Aggregationssuchvorgänge.|  
|Aggregationstreffer/s|Rate der Aggregationstreffer.|  
  
###  <a name="bkmk_Threads"></a> Threads  
 Statistik zu Microsoft Analysis Services-Threads.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|Kurze Analysethreads im Leerlauf|Anzahl der Leerlaufthreads im Pool für kurze Analysethreads.|  
|Ausgelastete kurze Analysethreads|Anzahl der ausgelasteten Threads im Pool für kurze Analysethreads.|  
|Warteschlangenlänge für kurze Analyseaufträge|Anzahl der Aufträge in der Warteschlange des Pools für kurze Analysethreads.|  
|Rate kurzer Analyseaufträge|Rate der Aufträge über den Pool für kurze Analysethreads.|  
|Lange Analysethreads im Leerlauf|Anzahl der Leerlaufthreads im Pool für lange Analysethreads.|  
|Ausgelastete lange Analysethreads|Anzahl der ausgelasteten Threads im Pool für lange Analysethreads.|  
|Warteschlangenlänge für lange Analyseaufträge|Anzahl der Aufträge in der Warteschlange des Pools für lange Analysethreads.|  
|Rate langer Analyseaufträge|Rate der Aufträge über den Pool für lange Analysethreads.|  
|Abfragepoolthreads im Leerlauf|Anzahl der Leerlaufthreads im Abfragethreadpool.|  
|Ausgelastete Abfragepoolthreads|Anzahl der ausgelasteten Threads im Abfragethreadpool.|  
|Warteschlangenlänge für Abfragepoolaufträge|Anzahl der Aufträge in der Warteschlange des Abfragethreadpools.|  
|Auftragsrate des Abfragepools|Rate der Aufträge über den Abfragethreadpool.|  
|Nicht-E/A-Threads für Verarbeitungspool im Leerlauf|Anzahl der im Leerlauf befindlichen Threads im Verarbeitungsthreadpool, der für Nicht-E/A-Aufträge vorgesehen ist.|  
|Nicht-E/A-Threads für ausgelasteten Verarbeitungspool|Anzahl der Threads, die Nicht-E/A-Aufträge im Verarbeitungsthreadpool ausführen.|  
|Warteschlangenlänge für Verarbeitungspoolaufträge|Anzahl der Nicht-E/A-Aufträge in der Warteschlange des Verarbeitungsthreadpools.|  
|Auftragsrate des Verarbeitungspools|Rate der Nicht-E/A-Aufträge im Verarbeitungsthreadpool.|  
|E/A-Auftragsthreads für Verarbeitungspool im Leerlauf|Anzahl der Threads im Leerlauf für E/A-Aufträge im Verarbeitungsthreadpool.|  
|E/A-Auftragsthreads für ausgelastete Verarbeitungspool|Anzahl der Threads, die E/A-Aufträge im Verarbeitungsthreadpool ausführen.|  
|Warteschlangenlänge für Verarbeitungspool-E/A-Aufträge|Anzahl der E/A-Aufträge in der Warteschlange des Verarbeitungsthreadpools.|  
|E/A-Auftragsabschlussrate in Verarbeitungspool|Rate der E/A-Aufträge im Verarbeitungsthreadpool.|  
  
  
