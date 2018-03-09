---
title: SQL Server, Puffer-Manager-Objekt | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Buffer Manager object
- SQLServer:Buffer Manager
ms.assetid: 9775ebde-111d-476c-9188-b77805f90e98
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 492c60be544246d0f94e5a8eba4198bca2815e95
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-buffer-manager-object"></a>SQL Server, Puffer-Manager-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Das **Puffer-Manager**-Objekt stellt Leistungsindikatoren bereit, mit denen die Verwendung folgender Ressourcen durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] überwacht werden kann:  
  
-   Arbeitsspeicher zum Speichern von Datenseiten.  
  
-   Leistungsindikatoren zur Überwachung der physischen E/A, während [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbankseiten liest und schreibt.  
  
-   Pufferpoolerweiterung zur Erweiterung des Puffercaches mithilfe von schnellem, nicht flüchtigem Speicher wie Festkörperlaufwerken (SSD).  
  
 Durch Überwachen des Arbeitsspeichers und der Leistungsindikatoren, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden, können Sie Folgendes ermitteln:  
  
-   Ob es zu Engpässen wegen nicht ausreichendem physischem Arbeitsspeicher kommt. Wenn häufig verwendete Daten nicht im Cache gespeichert werden können, muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Daten vom Datenträger abrufen.   
  
-   Ob die Abfrageleistung durch Hinzufügen von Arbeitsspeicher oder durch Zuordnen von zusätzlichem Arbeitsspeicher für den Datencache bzw. für interne Strukturen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbessert werden kann.  
  
-   Wie oft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten vom Datenträger lesen muss. Verglichen mit anderen Vorgängen, wie z. B. dem Arbeitsspeicherzugriff, beansprucht die physische E/A viel Zeit. Durch Minimieren der physischen E/A kann die Abfrageleistung verbessert werden.  
  
## <a name="buffer-manager-performance-objects"></a>Leistungsobjekte für den Puffer-Manager  
 In dieser Tabelle werden die Leistungsobjekte für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Puffer-Manager** beschrieben.  
  
|Puffer-Manager-Leistungsindikatoren von SQL Server|Description|  
|----------------------------------------|-----------------|  
|**Hintergrund-Writer-Seiten/Sekunde**|Die Anzahl der Seiten, die zum Durchsetzen der Einstellungen für das Wiederherstellungsintervall geleert wurden.| 
|**Puffercache-Trefferquote**|Gibt den Prozentsatz der Seiten an, die im Puffercache gefunden wurden, ohne dass ein Lesevorgang vom Datenträger erforderlich war. Die Quote ist die Gesamtzahl von Cachetreffern dividiert durch die Gesamtzahl der Cachesuchvorgänge für die letzten paar Tausend Seitenzugriffe. Nach längerer Zeit verschiebt sich die Quote geringfügig. Da das Lesen vom Cache weniger aufwendig als das Lesen vom Datenträger ist, ist es in Ihrem Interesse, dass diese Quote hoch ist. Im Allgemeinen können Sie die Trefferquote des Puffercaches erhöhen, indem Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mehr Arbeitsspeicher zur Verfügung stellen oder die Pufferpoolerweiterungsfunktion verwenden.|  
|**Basis für Puffercache-Trefferquote**|Nur zur internen Verwendung.|
|**Prüfpunktseiten/Sekunde**|Gibt die Anzahl der Seiten an, die pro Sekunde durch einen Prüfpunkt oder eine andere Operation, die das Leeren aller modifizierten Seiten erfordert, auf den Datenträger geleert wurden.|  
|**Datenbankseiten**|Gibt die Anzahl der Seiten im Pufferpool mit Datenbankinhalt an.|  
|**Extension allocated pages**|Gesamtzahl nicht freier Cacheseiten in der Pufferpoolerweiterungsdatei.|  
|**Extension free pages**|Gesamtzahl freier Cacheseiten in der Pufferpoolerweiterungsdatei.|  
|**Extension in use as percentage**|Prozentsatz der Pufferpoolerweiterungs-Auslagerungsdatei, der durch Puffer-Manager-Seiten belegt ist.|  
|**Extension outstanding IO counter**|E/A-Warteschlangenlänge für die Pufferpoolerweiterungsdatei.|  
|**Extension page evictions/sec**|Anzahl der Seiten, die aus der Pufferpoolerweiterungsdatei pro Sekunde entfernt wurden.|  
|**Erweiterungsseiten-Lesevorgänge/Sekunde**|Anzahl der Seiten, die aus der Pufferpoolerweiterungsdatei pro Sekunde gelesen wurden.|  
|**Extension page unreferenced time**|Durchschnittliche Sekunden, die eine Seite in der Pufferpoolerweiterung ohne Verweise darauf verbleibt.|  
|**Erweiterungsseiten-Schreibvorgänge/Sekunde**|Anzahl der Seiten, die in die Pufferpoolerweiterungsdatei pro Sekunde geschrieben wurden.|  
|**Anhalten der Freiliste/Sekunde**|Gibt die Anzahl der Anforderungen pro Sekunde an, die auf eine freie Seite warten mussten.|  
|**Steigung des integralen Controllers**|Der vom integralen Controller für den Pufferpool zuletzt verwendete Steigungswert multipliziert mit -10 Milliarden.| 
|**Verzögerte Schreibvorgänge/Sekunde**|Gibt die Anzahl der Puffer pro Sekunde an, die vom Puffer-Manager verzögert geschrieben wurden. Beim *LAZY WRITER* -Prozess (verzögertes Schreiben) handelt es sich um einen Systemprozess, der Batches mit alten, modifizierten Puffern (die auf den Datenträger zurückgeschrieben werden müssen, bevor der Puffer für eine andere Seite erneut verwendet werden kann) auf den Datenträger schreibt und Benutzerprozessen zur Verfügung stellt. Durch den LAZY WRITER-Prozess ist es nicht mehr nötig, häufig Prüfpunkte auszuführen, um verfügbare Puffer zu erhalten.|  
|**Lebenserwartung von Seiten**|Gibt die Anzahl der Sekunden an, für die eine Seite ohne Verweise im Pufferpool verbleibt.|  
|**Suchvorgänge in Seiten/Sekunde**|Gibt die Anzahl der Anforderungen pro Sekunde zum Suchen einer Seite im Pufferpool an.|  
|**Seitenlesevorgänge/Sekunde**|Gibt die Anzahl der pro Sekunde ausgegebenen Lesevorgänge für physische Datenbankseiten an. Diese Statistik zeigt die Gesamtanzahl der physischen Seitenlesevorgänge aller Datenbanken an. Da die physische E/A aufwendig ist, sind Sie eventuell in der Lage, die Kosten durch einen größeren Datencache, intelligente Indizes oder effizientere Abfragen oder durch Ändern des Datenbankentwurfs zu minimieren.|  
|**Seitenschreibvorgänge/Sekunde**|Gibt die Anzahl der pro Sekunde ausgegebenen Schreibvorgänge für physische Datenbankseiten an.|  
|**Read-Ahead-Seiten/Sekunde**|Gibt die Anzahl der Seiten pro Sekunde an, die vor dem Verwenden gelesen werden.|  
|**Read-Ahead-Dauer/s**|Die Dauer (Mikrosekunden) für die Read-Ahead-Ausgabe.|
|**Zielseiten**|Die ideale Anzahl von Seiten im Pufferpool.|

  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQLServer: Buffer Node](../../relational-databases/performance-monitor/sql-server-buffer-node.md)   
 [Serverkonfigurationsoptionen für den Serverarbeitsspeicher](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [SQL Server, Plancache-Objekt](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)   
 [Pufferpoolerweiterung](../../database-engine/configure-windows/buffer-pool-extension.md)  
  
  
