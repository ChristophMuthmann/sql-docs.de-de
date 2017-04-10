---
title: "Sichern einer Datenbank mit speicheroptimierten Tabellen | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 83d47694-e56d-4dae-b54e-14945bf8ba31
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# Sichern einer Datenbank mit speicheroptimierten Tabellen
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Speicheroptimierte Tabellen werden im Rahmen regelmäßiger Datenbanksicherungen gesichert. Wie bei datenträgerbasierten Tabellen wird die CHECKSUM von Daten-/Änderungsdateipaaren als Teil der Datenbanksicherung überprüft, um Speicherbeschädigungen zu erkennen.  
  
> [!NOTE]  
>  Wenn während einer Sicherung in einer oder mehreren Dateien einer speicheroptimierten Dateigruppe ein CHECKSUM-Fehler auftritt, kann der Sicherungsvorgang nicht durchgeführt werden. In diesem Fall müssen Sie die Datenbank von der letzten als fehlerfrei bekannten Sicherung wiederherstellen.  
>   
>  Wenn keine Sicherung verfügbar ist, können Sie die Daten aus den speicheroptimierten und datenträgerbasierten Tabellen exportieren und erneut laden, nachdem Sie die Datenbank gelöscht und neu erstellt haben.  
  
 Eine vollständige Sicherung einer Datenbank mit mindestens einer speicheroptimierten Tabelle besteht aus dem zugeordneten Speicher für datenträgerbasierte Tabellen (falls vorhanden), dem aktiven Transaktionsprotokoll und den Daten-/Änderungsdateipaaren (auch als Prüfpunktdateipaare bezeichnet) für speicheroptimierte Tabellen. Allerdings kann der unter [Dauerhaftigkeit für speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md) beschriebene, von speicheroptimierten Tabellen genutzte Speicher wesentlich größer als die belegte Arbeitsspeicherkapazität sein, was sich auf die Größe der Datenbanksicherung auswirkt.  
  
## Vollständige Datenbanksicherung  
 Diese Erläuterung bezieht sich auf Datenbanksicherungen für Datenbanken, die ausschließlich über dauerhafte speicheroptimierte Tabellen verfügen, da die Sicherung für datenträgerbasierte Tabellen identisch ist. Die Prüfpunktdateipaare in der speicheroptimierten Dateigruppe können unterschiedliche Statusphasen aufweisen. In der folgenden Tabelle wird beschrieben, welcher Teil der Dateien gesichert wird.  
  
|Status des Prüfpunktdateipaars|Sicherung|  
|--------------------------------|------------|  
|PRECREATED|Nur Dateimetadaten|  
|UNDER CONSTRUCTION|Nur Dateimetadaten|  
|ACTIVE|Dateimetadaten plus verwendete Bytes|  
|MERGE TARGET|Nur Dateimetadaten|  
|WAITING FOR LOG TRUNCATION|Dateimetadaten plus verwendete Bytes|  
  
 Beschreibungen der Statusphasen für Prüfpunktdateipaare finden Sie unter [sys.dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) und in der Spalte „state_desc“.  
  
 Die Größe von Datenbanksicherungen mit einer oder mehreren speicheroptimierten Tabellen liegt in der Regel über deren Größe im Arbeitsspeicher jedoch unter dem auf dem Datenträger belegten Speicherplatz. Die zusätzliche Größe hängt neben anderen Faktoren von der Anzahl der gelöschten Zeilen ab.  
  
### Schätzen der Größe einer vollständigen Datenbanksicherung  
  
> [!IMPORTANT]  
>  Es wird empfohlen, den BackupSizeInBytes-Wert nicht zu verwenden, um die Sicherungsgröße für In-Memory OLTP zu schätzen.  
  
 Das erste Arbeitsauslastungsszenario bezieht sich (hauptsächlich) auf Einfügevorgänge. In diesem Szenario weisen die meisten Datendateien den Status ACTIVE und einige wenige gelöschte Zeilen auf und wurden vollständig geladen. Die Größe der Datenbanksicherung entspricht in etwa der Größe der Daten im Arbeitsspeicher.  
  
 Das zweite Arbeitsauslastungsszenario bezieht sich auf häufige Einfüge-, Lösch- und Updatevorgänge: Im ungünstigsten Fall wurde jedes Prüfpunktdateipaar nach Berücksichtigung der gelöschten Zeilen zu 50 % geladen. Die Datenbanksicherung ist mindestens doppelt so groß wie die Daten im Arbeitsspeicher.  
  
## Differenzielle Sicherungen von Datenbanken mit speicheroptimierten Tabellen  
 Der Speicher für speicheroptimierte Tabellen setzt sich zusammen aus Daten- und Änderungsdateien, wie in [Dauerhaftigkeit für speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md) beschrieben. Eine differenzielle Sicherung einer Datenbank mit speicheroptimierten Tabellen enthält die folgenden Daten:  
  
-   Die differenzielle Sicherung für Dateigruppen, in denen datenträgerbasierte Tabellen gespeichert sind, wird durch das Vorhandensein von speicheroptimierten Tabellen nicht beeinflusst.  
  
-   Das aktive Transaktionsprotokoll ist dasselbe wie bei einer vollständigen Datenbanksicherung.  
  
-   Für eine speicheroptimierte Datendateigruppe verwendet die differenzielle Sicherung den gleichen Algorithmus wie bei einer vollständigen Datenbanksicherung, um die Daten- und Änderungsdateien für die Sicherung identifizieren. Anschließend wird wie folgt eine Teilmenge dieser Dateien herausgefiltert:  
  
    -   Eine Datendatei, die neu eingefügte Zeilen enthält und voll ist, wird geschlossen und als schreibgeschützt gekennzeichnet. Eine Datendatei wird nur gesichert, wenn sie nach der letzten vollständigen Datenbanksicherung geschlossen wurde. Bei der differenziellen Sicherung werden nur Datendateien gesichert, welche die seit der letzten vollständigen Sicherung eingefügten Zeilen enthalten. Eine Ausnahme ist ein Aktualisierungs- und Löschszenario. Hier können einige der eingefügten Zeilen bereits entweder für die Speicherbereinigung markiert oder bereits sein.  
  
    -   Eine Änderungsdatei speichert Verweise auf die gelöschten Datenzeilen. Da jede zukünftige Transaktion eine Zeile löschen kann, kann eine Änderungsdatei zu jedem Zeitpunkt innerhalb ihrer Lebensdauer geändert werden. Sie wird daher nie geschlossen. Eine Änderungsdatei wird immer gesichert. Änderungsdateien belegen normalerweise weniger als 10 % des Speichers, sodass Änderungsdateien nur eine minimale Auswirkung auf der Größe der differenziellen Sicherung haben.  
  
 Wenn speicheroptimierte Tabellen einen großen Teil der Datenbank ausmachen, kann die Größe der Datenbanksicherung durch die differenzielle Sicherung erheblich reduziert werden. Bei typischen OLTP-Arbeitsauslastungen fallen differenzielle Sicherungen wesentlich kleiner als vollständige Datenbanksicherungen aus.  
  
## Siehe auch  
 [Sichern und Wiederherstellen speicheroptimierter Tabellen](../Topic/Backup,%20Restore,%20and%20Recovery%20of%20Memory-Optimized%20Tables.md)  
  
  