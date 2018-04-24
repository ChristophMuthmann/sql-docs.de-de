---
title: Konfigurieren von Speicher für speicheroptimierte Tabellen | Microsoft Dokumentation
ms.custom: ''
ms.date: 10/25/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
caps.latest.revision: 7
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c33ef5aa3bfa5598ed306af4836d7d8f36f53233
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>Konfigurieren von Speicher für speicheroptimierte Tabellen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Sie müssen die Speicherkapazität und die E/A-Vorgänge pro Sekunde (IOPS) konfigurieren.  
  
## <a name="storage-capacity"></a>Speicherkapazität  
 Verwenden Sie die Informationen unter [Schätzen der Arbeitsspeicheranforderungen speicheroptimierter Tabellen](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) , um für die dauerhaften speicheroptimierten Tabellen der Datenbank deren Größe im Arbeitsspeicher zu schätzen. Da die Indizes der speicheroptimierten Tabellen nicht beibehalten werden, muss die Größe der Indizes nicht berücksichtigt werden. Wenn Sie die Größe ermittelt haben, müssen Sie Speicherplatz bereitstellen, der vier Mal der Größe der dauerhaften Tabellen im Arbeitsspeicher entspricht.  
  
## <a name="storage-iops"></a>Speicher-IOPS  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] kann den Arbeitsauslastungsdurchsatz erheblich erhöhen. Daher ist es wichtig sicherzustellen, dass die E/A-Vorgänge keinen Engpass darstellen.  
  
-   Wenn Sie datenträgerbasierte Tabellen zu speicheroptimierten Tabellen migrieren, stellen Sie sicher, dass sich das Transaktionsprotokoll auf einem Speichermedium befindet, das die erhöhte Transaktionsprotokollaktivität verarbeiten kann. Wenn das Speichermedium z. B. Transaktionsprotokollvorgänge bei 100 MB/s unterstützt und durch speicheroptimierte Tabellen eine fünfmal höhere Leistung erzielt wird, muss das Speichermedium des Transaktionsprotokolls in der Lage sein, die fünfmal höhere Leistung auch zu unterstützen, damit die Transaktionsprotokollaktivitäten nicht zu einem Leistungsengpass führen.  
  
-   Speicheroptimierte Tabellen werden in Prüfpunktdateien beibehalten, die über einen oder mehrere Container verteilt sind. Jeder Container sollte in der Regel einem eigenen Speichergerät zugeordnet sein. Er wird sowohl für eine höhere Speicherkapazität als auch für einen höheren IOPS-Wert verwendet. Sie müssen sicherstellen, dass durch sequenziellen IOPS des Speichermediums der dreifache Wert des Transaktionsprotokolldurchsatzes unterstützt werden kann. Schreibvorgänge in Prüfpunktdateien entsprechen 256 KB für Datendateien und 4 KB für Änderungsdateien.
  
     - Wenn durch speicheroptimierte Tabellen z.B. dauerhafte Aktivitäten mit 500 MB/s im Transaktionsprotokoll generiert werden, muss der Speicher für speicheroptimierte Tabellen einen IOPS-Wert von 1,5 GB/s unterstützen. Die Notwendigkeit zur Unterstützung des dreifachen dauerhaften Transaktionsprotokolldurchsatzes ergibt sich daraus, dass zuerst die Daten-/Änderungsdateipaare mit den anfänglichen Daten geschrieben und diese anschließend als Teil eines Zusammenführungsvorgangs gelesen und erneut geschrieben werden müssen.  
  
- Ein weiterer Faktor bei der Schätzung des IOPS-Werts für den Speicher ist die Wiederherstellungszeit für speicheroptimierte Tabellen. Daten aus dauerhaften Tabellen müssen in den Speicher gelesen werden, bevor die Datenbank für Anwendungen zur Verfügung steht. Normalerweise können Daten mit dem maximalen IOPS-Wert in speicheroptimierte Tabellen geladen werden. Wenn der gesamte Speicherplatz für dauerhafte speicheroptimierte Tabellen 60 GB beträgt und Sie diese Daten innerhalb von 1 Minute laden möchten, muss der Speicher IOPS mit 1 GB/s unterstützen.  
  
-   Prüfpunktdateien werden in der Regel gleichmäßig in allen Containern verteilt, wenn genügend Speicherplatz vorhanden ist. Bei SQL Server 2014 müssen Sie eine ungerade Anzahl von Containern bereitstellen, um eine gleichmäßige Verteilung zu erzielen. Ab 2016 kann eine gleichmäßige Verteilung durch eine ungerade oder gerade Anzahl von Containern erzielt werden.
  
## <a name="encryption"></a>Verschlüsselung  
 In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] wird der Speicher für speicheroptimierte Tabellen im Rahmen der Aktivierung von TDE für die Datenbank verschlüsselt. Weitere Informationen finden Sie unter [Transparente Datenverschlüsselung &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md). In [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] werden Prüfpunktdateien nicht verschlüsselt, auch wenn TDE für die Datenbank aktiviert ist.
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen und Verwalten von Speicher für speicheroptimierte Objekte](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
