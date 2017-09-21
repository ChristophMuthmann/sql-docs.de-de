---
title: Aktualisieren von Analysis Services | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/12/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
caps.latest.revision: 79
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 1df54edd5857ac2816fa4b164d268835d9713638
ms.openlocfilehash: 7e6b4f4e6c984e8d3e6f88939e88d73dfc2d3909
ms.contentlocale: de-de
ms.lasthandoff: 09/12/2017

---
# <a name="upgrade-analysis-services"></a>Aktualisieren von Analysis Services
  Analysis Services-Instanzen können auf eine SQL Server-Version mit demselben Servermodus aktualisiert werden, um von den Funktionen zu profitieren, die in der aktuellen Version eingeführt wurden. Informationen zu diesen Funktionen finden Sie unter [What's New in Analysis Services (Neuigkeiten in Analysis Services)](../../analysis-services/what-s-new-in-analysis-services.md).  
  
 Sie können jede Instanz unabhängig von anderen Instanzen, die auf derselben Hardware ausgeführt werden, direkt aktualisieren. Die meisten Administratoren entscheiden sich für die Installation einer neuen Instanz der neuen Version zum Testen der Anwendung, ehe Produktionsarbeitsauslastungen auf den neuen Server übertragen werden. Doch für Entwicklungs- oder Testserver kann ein direktes Upgrade möglicherweise empfehlenswert sein.  
  
## <a name="server-upgrade"></a>Upgrade von Servern  
 Es gibt zwei grundlegende Ansätze für Upgrades von Servern und Datenbanken:  
  
> [!NOTE]
> Die Kompatibilitätsgrade von Datenbanken, die einem bestimmten Server zugeordnet sind, bleiben unverändert, bis Sie sie manuell ändern.
   
  
### <a name="in-place-upgrade"></a>Direktes Upgrade  
 Der Upgradeprozess migriert automatisch bestehende Datenbanken von der alten Instanz zur neuen Instanz. Da die Metadaten und die binären Daten zwischen den beiden Versionen kompatibel sind, behalten Sie die Daten nach dem Upgrade bei, und es ist nicht nötig, eine manuelle Datenmigration durchzuführen.  
  
 Um eine vorhandene Instanz zu aktualisieren, führen Sie das Setup aus, und geben Sie den Namen der vorhandenen Instanz als Namen für die neue Instanz an.  
  
### <a name="side-by-side-upgrade"></a>Paralleles Upgrade  
  
-   Sichern Sie alle Datenbanken, und stellen Sie sicher, dass jede wiederhergestellt werden kann. Weitere Informationen finden Sie unter [Sichern und Wiederherstellen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md).  
  
-   Bestimmen Sie eine Teilmenge der Berichte, Kalkulationstabellen oder Momentaufnahmen von Dashboards, die Sie später als Grundlage für das Überprüfen der Servervorgänge im Anschluss an das Upgrade nutzen möchten. Erfassen Sie nach Möglichkeit Leistungsmesswerte, damit Sie Vergleiche mit denselben Arbeitsauslastungen auf einem aktualisierten Server ausführen können.  
  
-   Installieren Sie eine neue Instanz von Analysis Services, und wählen Sie den gleichen Servermodus (tabellarisch oder mehrdimensional) wie auf dem Server, den Sie ersetzen möchten. 
  
     Nach der Installation müssen Sie Ports konfigurieren und Serveradministratoren hinzufügen. Weitere Informationen finden Sie unter [Konfiguration nach der Installation &#40;Analysis Services&#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md).  
  
-   Sie können dann die einzelnen Datenbanken anfügen oder wiederherstellen.  
  
-   Führen Sie DBCC aus, um die Datenbankintegrität zu überprüfen. Tabellarische Modelle werden einer gründlicheren Überprüfung mit Tests auf verwaiste Objekte in der gesamten Modellhierarchie unterzogen. Bei mehrdimensionalen Modellen werden nur die Partitionsindizes überprüft. Weitere Informationen finden Sie unter [Datenbankkonsistenzprüfung &#40;DBCC&#41; für tabellarische und mehrdimensionale Analysis Services-Datenbanken](../../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md).  
  
-   Testen Sie Berichte, Kalkulationstabellen und Dashboards, um zu bestätigen, dass sich Verhalten oder Berechnungen nicht negativ verändert haben. Für mehrdimensionale und tabellarische Arbeitslasten sollte eine bessere Leistung spürbar werden.  
  
-   Testen Sie Verarbeitungsvorgänge, und korrigieren Sie Anmeldungs- oder Berechtigungsprobleme. Bei Verwendung des Standarddienstkontos für Verbindungen wird der neue Dienst unter einem anderen Konto ausgeführt. Weitere Informationen finden Sie unter [Konfigurieren von Dienstkonten &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md).  
  
-   Testen Sie Sicherungs- und Wiederherstellungsvorgänge auf dem aktualisierten Server, und passen Sie Skripts so an, dass der neue Servername verwendet wird.  
  
## <a name="database-upgrade"></a>Upgrade von Datenbanken  
 Datenbanken, die in früheren Versionen erstellt wurden, werden auf dem aktualisierten Server mit dem ursprünglichen Kompatibilitätsgrad ausgeführt. Im Allgemeinen können Sie für eine Datenbank oder ein Modell ein Upgrade zum Betrieb mit einem höheren Kompatibilitätsgrad vornehmen, um Zugriff auf neue Features zu erhalten. Beachten Sie dabei allerdings, dass Sie sich an eine bestimmte Serverversion binden.  
  
 Für ein Upgrade einer Datenbank aktualisieren Sie in der Regel das Modell in SQL Server Data Tools (SSDT) und stellen die Lösung anschließend in einer aktualisierten Serverinstanz bereit.
  
 Tabellarische und mehrdimensionale Datenbanken haben unterschiedliche Versionspfade. Es ist Zufall, dass mehrdimensionale und tabellarische Modelle über ähnlich nummerierte Kompatibilitätsgrade verfügen.  Die Modi werden sich mit unterschiedlichem Tempo entwickeln, sobald Änderungen an Features sich nur auf ein Modell auswirken.  
  
 Die folgende Tabelle enthält Hintergrundinformationen zu den Kompatibilitätsgraden, doch Sie sollten die Detailthemen lesen, um zu erfahren, was die einzelnen Grade zu bieten haben.  
  
||||  
|-|-|-|  
|Tabellarisch|1400|SQL Server 2017|
|Tabellarisch|1200|SQL Server 2016|  
|Tabellarisch|1103|SQL Server 2014|  
|Tabellarisch|1100|SQL Server 2012|  
|Multidimensional|1100|SQL Server 2012 und höher|  
|Multidimensional|1050|SQL Server 2005, 2008, 2008 R2|  
  
 Weitere Informationen finden Sie unter [Kompatibilitätsgrad einer mehrdimensionalen Datenbank &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md) und [Kompatibilitätsgrad für tabellarische Modelle von Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Planen einer SQL Server-Installation](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Aktualisieren von PowerPivot für SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
  
  

