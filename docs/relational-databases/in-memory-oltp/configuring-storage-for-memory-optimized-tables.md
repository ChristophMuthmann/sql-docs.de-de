---
title: "Konfigurieren von Speicher f&#252;r speicheroptimierte Tabellen | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
caps.latest.revision: 7
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 7
---
# Konfigurieren von Speicher f&#252;r speicheroptimierte Tabellen
  Sie müssen die Speicherkapazität und die E/A-Vorgänge pro Sekunde (IOPS) konfigurieren.  
  
## Speicherkapazität  
 Verwenden Sie die Informationen unter [Schätzen der Arbeitsspeicheranforderungen speicheroptimierter Tabellen](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md), um für die dauerhaften speicheroptimierten Tabellen der Datenbank deren Größe im Arbeitsspeicher zu schätzen. Da die Indizes der speicheroptimierten Tabellen nicht beibehalten werden, muss die Größe der Indizes nicht berücksichtigt werden. Wenn Sie die Größe ermittelt haben, müssen Sie Speicherplatz bereitstellen, der vier Mal der Größe der dauerhaften Tabellen im Arbeitsspeicher entspricht.  
  
## Speicher-IOPS  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] kann den Arbeitsauslastungsdurchsatz erheblich erhöhen. Daher ist es wichtig sicherzustellen, dass die E/A-Vorgänge keinen Engpass darstellen.  
  
-   Wenn Sie datenträgerbasierte Tabellen zu speicheroptimierten Tabellen migrieren, stellen Sie sicher, dass sich das Transaktionsprotokoll auf einem Speichermedium befindet, das die erhöhte Transaktionsprotokollaktivität verarbeiten kann. Wenn das Speichermedium z. B. Transaktionsprotokollvorgänge bei 100 MB/s unterstützt und durch speicheroptimierte Tabellen eine fünfmal höhere Leistung erzielt wird, muss das Speichermedium des Transaktionsprotokolls in der Lage sein, die fünfmal höhere Leistung auch zu unterstützen, damit die Transaktionsprotokollaktivitäten nicht zu einem Leistungsengpass führen.  
  
-   Speicheroptimierte Tabellen werden in Dateien beibehalten, die über einen oder mehrere Container verteilt sind. Jeder Container sollte in der Regel einer eigenen Spindel zugeordnet sein. Er wird sowohl für eine höhere Speicherkapazität als auch für einen höheren IOPS-Wert verwendet. Sie müssen sicherstellen, dass bei sequenziellen IOPS auf dem Speichermedium der dreifache Wert des Transaktionsprotokolldurchsatzes unterstützt wird.  
  
     Wenn durch speicheroptimierte Tabellen z. B. Aktivitäten mit 500 MB/s im Transaktionsprotokoll generiert werden, muss der Speicher für speicheroptimierte Tabellen einen IOPS-Wert von 1,5 GB/s unterstützen. Die Notwendigkeit zur Unterstützung des dreifachen Transaktionsprotokolldurchsatzes ergibt sich daraus, dass zuerst die Daten-/Änderungsdateipaare mit den anfänglichen Daten geschrieben und diese anschließend als Teil eines Zusammenführungsvorgangs gelesen und erneut geschrieben werden müssen.  
  
     Ein weiterer Faktor bei der Schätzung des IOPS-Werts für den Speicher ist die Wiederherstellungszeit für speicheroptimierte Tabellen. Daten aus dauerhaften Tabellen müssen in den Speicher gelesen werden, bevor die Datenbank für Anwendungen zur Verfügung steht. Normalerweise können Daten mit dem maximalen IOPS-Wert in speicheroptimierte Tabellen geladen werden. Wenn der gesamte Speicherplatz für dauerhafte speicheroptimierte Tabellen 60 GB beträgt und Sie diese Daten innerhalb von 1 Minute laden möchten, muss der Speicher IOPS mit 1 GB/s unterstützen.  
  
-   Wenn Sie über eine gerade Anzahl an Spindeln verfügen, werden die Prüfpunktdateien anders als in SQL Server 2014 gleichmäßig auf alle Spindeln verteilt.  
  
## Verschlüsselung  
 In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] wird der Speicher für speicheroptimierte Tabellen im Rahmen der Aktivierung von TDE für die Datenbank verschlüsselt. Weitere Informationen finden Sie unter [Transparente Datenverschlüsselung &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption-tde.md).  
  
## Siehe auch  
 [Erstellen und Verwalten von Speicher für speicheroptimierte Objekte](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  