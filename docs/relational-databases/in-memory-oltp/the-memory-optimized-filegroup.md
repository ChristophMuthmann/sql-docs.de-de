---
title: Die speicheroptimierte Dateigruppe | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 14106cc9-816b-493a-bcb9-fe66a1cd4630
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ff868be847d703d4ce4b8b291a725abc255a5788
ms.sourcegitcommit: b09bccd6dfdba55b022355e892c29cb50aadd795
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/23/2018
---
# <a name="the-memory-optimized-filegroup"></a>Die speicheroptimierte Dateigruppe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Um speicheroptimierte Tabellen zu erstellen, müssen Sie zuerst eine speicheroptimierte Dateigruppe erstellen. Die speicheroptimierte Dateigruppe enthält mindestens einen Container. Jeder Container enthält Datendateien oder Änderungsdateien oder sowohl als auch.  
  
 Obwohl Datenzeilen aus SCHEMA_ONLY-Tabellen nicht beibehalten werden und die Metadaten für speicheroptimierte Tabellen und systemintern kompilierte gespeicherte Prozeduren in herkömmlichen Katalogen gespeichert werden, ist für das [!INCLUDE[hek_2](../../includes/hek-2-md.md)] -Modul weiterhin eine speicheroptimierte Dateigruppe erforderlich, damit die Behandlung speicheroptimierter SCHEMA_ONLY-Tabellen für Datenbanken mit speicheroptimierten Tabellen konsistent ist.  
  
 Die speicheroptimierte Dateigruppe basiert auf Filestream-Dateigruppen, von denen sie sich in folgenden Punkten unterscheidet:  
  
-   Sie können nur eine speicheroptimierte Dateigruppe pro Datenbank erstellen. Sie müssen die Dateigruppe explizit als Container für aus memory_optimized_data markieren. Sie können die Dateigruppe erstellen, wenn Sie die Datenbank erstellen, oder Sie können sie später hinzufügen:  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA  
    ```  
  
-   Sie müssen mindestens einen Container der Dateigruppe `MEMORY_OPTIMIZED_DATA` hinzufügen. Zum Beispiel:  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod  
    ```  
  
-   Es ist nicht erforderlich, Filestream zu aktivieren ([Aktivieren und Konfigurieren von FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)), um eine speicheroptimierte Dateigruppe zu erstellen. Die Zuordnung zu Filestream wird über das [!INCLUDE[hek_2](../../includes/hek-2-md.md)] -Modul ausgeführt.  
  
-   Sie können einer speicheroptimierten Dateigruppe neue Container hinzufügen. Möglicherweise benötigen Sie einen neuen Container, um den Speicher zu erweitern, der für die dauerhafte speicheroptimierte Tabelle und die Weitergabe von E/A über mehrere Container hinweg benötigt wird.  
  
-   Die Datenverschiebung mit einer speicheroptimierten Dateigruppe ist in einer Konfiguration von Always On-Verfügbarkeitsgruppen optimiert. Im Gegensatz zu Filestream-Dateien, die an sekundäre Replikate gesendet werden, werden die Prüfpunktdateien (Daten und Änderungen) in der speicheroptimierten Dateigruppe nicht an die sekundären Replikate gesendet. Die Daten- und Änderungsdateien werden mithilfe des Transaktionsprotokolls für das sekundäre Replikat erstellt.  
  
Die folgenden Einschränkungen gelten für speicheroptimierte Dateigruppen:  
  
-   Sobald Sie eine speicheroptimierte Dateigruppe erstellt haben, können Sie sie nur entfernen, indem Sie die Datenbank löschen. In einer Produktionsumgebung müssen Sie die speicheroptimierte Dateigruppe wahrscheinlich nicht entfernen.  
  
-   Sie können einen nicht leeren Container nicht löschen und Daten- und Änderungsdateipaare nicht in einen anderen Container in der speicheroptimierten Dateigruppe verschieben.  
  
-   Sie können für den Container nicht `MAXSIZE` angeben.  
  
## <a name="configuring-a-memory-optimized-filegroup"></a>Konfigurieren einer speicheroptimierten Dateigruppe  
 Sie sollten mehrere Container in der speicheroptimierten Dateigruppe erstellen und auf unterschiedliche Laufwerke verteilen, um beim Streamen der Daten in den Arbeitsspeicher eine höhere Bandbreite zu erzielen.  
  
 Wenn Sie den Speicher konfigurieren, müssen Sie freien Speicherplatz bereitstellen, der viermal so groß wie die dauerhaften speicheroptimierten Tabellen ist. Stellen Sie auch sicher, dass Ihr E/A-Subsystem die benötigten IOPS für Ihre Workload unterstützt. Wenn Daten- und Änderungsdateipaare bei bestimmten IOPS aufgefüllt werden, benötigen Sie dreimal so viel IOPS, um Speicher- und Zusammenführungsvorgänge zu berücksichtigen. Sie können Speicherkapazität und IOPS hinzufügen, indem Sie einen oder mehrere Container zur speicheroptimierten Dateigruppe hinzufügen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen und Verwalten von Speicher für speicheroptimierte Objekte](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
 [Datenbankdateien und Dateigruppen](../../relational-databases/databases/database-files-and-filegroups.md) 
  
