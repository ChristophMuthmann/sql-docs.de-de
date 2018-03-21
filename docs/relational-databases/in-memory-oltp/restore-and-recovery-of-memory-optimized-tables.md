---
title: Wiederherstellen von speicheroptimierten Tabellen | Microsoft-Dokumentation
ms.custom: 
ms.date: 12/31/2017
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
ms.assetid: 294975b7-e7d1-491b-b66a-fdb1100d2acc
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dc4980acc94353003205668ef81653d6b9c55f75
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/19/2018
---
# <a name="restore-and-recovery-of-memory-optimized-tables"></a>Wiederherstellen von speicheroptimierten Tabellen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Der grundlegende Mechanismus zum Wiederherstellen einer Datenbank mit speicheroptimierten Tabellen ist ähnlich wie der Mechanismus bei Datenbanken, die nur datenträgerbasierte Tabellen enthalten. Anders als datenträgerbasierte Tabellen müssen speicheroptimierte Tabellen jedoch in den Arbeitsspeicher geladen werden, bevor die Benutzer auf die Datenbank zugreifen können. Durch diese Anforderung wird ein neuer Schritt bei der Datenbankwiederherstellung hinzugefügt.  
  
Wenn ein Server nicht über genügend Arbeitsspeicher verfügt, schlägt die Datenbankwiederherstellung fehl, und die Datenbank wird als fehlerverdächtig markiert. Weitere Informationen zur Behebung dieses Problems finden Sie unter [Beheben von OOM-Problemen (nicht genügend Arbeitsspeicher)](resolve-out-of-memory-issues.md). 
  
## <a name="factors-that-affect-load-time"></a>Aspekte, die sich auf die Ladezeit auswirken
Während der Wiederherstellung liest das In-Memory OLTP-Modul Daten- und Änderungsdateien zum Laden in den physischen Speicher. Die Ladezeit wird bestimmt durch:  
  
-   Die zu ladende Datenmenge.  
  
-   Sequenzielle E/A-Bandbreite.  
  
-   Der Grad der Parallelität, bestimmt durch die Anzahl der Dateicontainer und Prozessorkerne.  
  
-   Die Anzahl von Protokolldatensätzen im aktiven Teil des Protokolls, die wiederholt werden müssen.  

## <a name="phases-of-recovery"></a>Wiederherstellungsphasen
Beim Neustart von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durchläuft jede Datenbank einen Wiederherstellungsprozess, der aus drei Phasen besteht:  
  
1.  **Analysephase**. Während dieser Phase werden die aktiven Transaktionsprotokolle durchsucht, um Transaktionen mit ausgeführtem Commit und Transaktionen ohne Commit zu erkennen. Das In-Memory OLTP-Modul identifiziert den zu ladenden Prüfpunkt und lädt die Protokolleinträge der Systemtabelle vorab. Außerdem werden einige Protokolldatensätze für die Dateizuordnung verarbeitet.  
  
2.  **Rollforwardphase**. Diese Phase wird für datenträgerbasierte und speicheroptimierte Tabellen gleichzeitig ausgeführt.  
  
    - Bei datenträgerbasierten Tabellen wird die Datenbank auf den aktuellen Stand verschoben, und es werden Sperren abgerufen, die von Transaktionen ohne Commit aktiviert wurden.  
  
    - Daten aus den Daten- und Änderungsdateipaaren werden für speicheroptimierte Tabellen in den Arbeitsspeicher geladen. Im Anschluss werden die Daten mit dem aktiven Transaktionsprotokoll auf Grundlage des letzten dauerhaften Prüfpunkts aktualisiert.  
  
    Wenn die oben genannten Vorgänge für datenträgerbasierte und speicheroptimierte Tabellen abgeschlossen wurden, kann auf die Datenbank zugegriffen werden.  
  
3.  **Rollbackphase**. In dieser Phase wird für die Transaktionen ohne Commit ein Rollback ausgeführt.  
  
## <a name="process-for-improving-load-time"></a>Verbesserung der Ladezeit
Das Laden von speicheroptimierten Tabellen in den Arbeitsspeicher kann die Leistung des Wiederherstellungszeitziels (Recovery Time Objective, RTO) beeinträchtigen. Um die Ladezeit von speicheroptimierten Daten aus Daten- und Änderungsdateien zu verbessern, lädt das In-Memory OLTP-Modul die Daten-/Änderungsdateien wie folgt parallel:  
  
-   **Erstellen eines Änderungszuordnungsfilters.** In Änderungsdateien werden Verweise auf die gelöschten Zeilen gespeichert. Ein Thread pro Container liest die Änderungsdateien und erstellt einen Änderungszuordnungsfilter. (Eine speicheroptimierte Datendateigruppe kann mehrere Container enthalten.)  
  
-   **Streaming der Datendateien.** Nachdem der Änderungszuordnungsfilter erstellt wurde, werden Datendateien von so vielen Threads gelesen wie logische CPUs vorhanden sind. Jeder Thread liest die Datenzeilen, überprüft die zugeordnete Änderungszuordnung und fügt die Zeile nur dann in der Tabelle ein, wenn diese Zeile nicht gelöscht wurde. Dieser Teil der Wiederherstellung kann in einigen Fällen CPU-gebunden sein, wie im unten stehenden Diagramm aufgeführt:  
  
    ![Datenstrom in speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/media/memory-optimized-tables.gif "Data streaming to memory-optimized tables")  
  
## <a name="specific-cases-of-slow-load-times"></a>Fälle langsamer Ladezeiten
Speicheroptimierte Tabellen können generell mit der Geschwindigkeit des E/A-Vorgangs in den Arbeitsspeicher geladen werden. Es kann jedoch vorkommen, dass das Laden von Datenzeilen in den Arbeitsspeicher längere Zeit in Anspruch nimmt. Dies ist insbesondere in folgenden Situationen der Fall:  
  
-   Eine niedrige Bucketanzahl für einen Hashindex kann zu übermäßigen Konflikten führen, wodurch das Einfügen von Datenzeilen langsamer erfolgt. Dies führt normalerweise zu einer hohen allgemeinen CPU-Auslastung, insbesondere gegen Ende der Wiederherstellung. Wenn Sie den Hashindex ordnungsgemäß konfiguriert haben, sollte die Wiederherstellungszeit nicht beeinträchtigt werden.  
  
-   Große speicheroptimierte Tabellen mit mindestens einem nicht gruppierten Index können zu einer hohen CPU-Auslastung führen. Im Gegensatz zu einem Hashindex, dessen Bucketanzahl beim Erstellen festgelegt wird, wachsen nicht gruppierte Indizes dynamisch.  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern und Wiederherstellen speicheroptimierter Tabellen](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  
  
