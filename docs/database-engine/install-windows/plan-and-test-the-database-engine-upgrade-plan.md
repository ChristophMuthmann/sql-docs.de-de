---
title: "Planen und Testen des Upgradeplans für das Datenbankmodul | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/20/2016
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 19c5b725-7400-4881-af8f-fd232ca28234
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cbe7bceca06dd5eef19b56433a8054c20d2e88d2
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="plan-and-test-the-database-engine-upgrade-plan"></a>Planen und Testen des Upgradeplans für das Datenbankmodul
  Für eine erfolgreiches Upgrade von [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] ist unabhängig von der Herangehensweise eine angemessene Planung erforderlich.  
  
## <a name="release-notes-and-known-upgrade-issues"></a>Anmerkungen zu dieser Version und bekannte Upgradeprobleme  
 Bevor Sie auf [!INCLUDE[ssDE](../../includes/ssde-md.md)] aktualisieren, sollten Sie sich folgende Artikel anschauen:

- [Versionsanmerkungen zu SQL Server 2017](../../sql-server/sql-server-2017-release-notes.md) 
- [Versionsanmerkungen zu SQL Server 2016](../../sql-server/sql-server-2016-release-notes.md) 
- Thema [Abwärtskompatibilität des SQL Server-Datenbankmoduls](../../database-engine/sql-server-database-engine-backward-compatibility.md)  
  
## <a name="pre-upgrade-planning-checklist"></a>Planungsprüfliste zur Vorbereitung des Upgrades  
 Lesen Sie vor dem Upgrade von [!INCLUDE[ssDE](../../includes/ssde-md.md)]die folgende Prüfliste und die dazugehörigen Themen. Diese Themen gelten für alle Upgrades, unabhängig von der Upgrademethode, und werden Ihnen helfen, die am besten geeignete Upgrademethode zu ermitteln: entweder ein paralleles oder direktes Upgrade oder die Neuinstallation der aktuellen Programmversion auf neuer Hardware. So kann es beispielsweise geschehen, dass Sie kein direktes oder paralleles Upgrade durchführen können, wenn Sie das Betriebssystem, SQL Server 2005 oder eine 32-Bit-Version von SQL Server upgraden. Eine Entscheidungsstruktur finden Sie unter [Choose a Database Engine Upgrade Method](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
  
-   **Hardware- und Softwareanforderungen:** Lesen Sie das Thema zu den Hardware- und Softwareanforderungen für die Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Diese Anforderungen finden Sie unter [Hardware- und Softwareanforderungen für die Installation von SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md). Es gehört zu jedem Upgradeplanungszyklus, ein Upgrade des Betriebssystems und der Hardware in Betracht zu ziehen, da neuere Hardware schneller ist und den Lizenzbedarf aufgrund der geringeren Anzahl von Prozessoren oder aufgrund der Datenbank- und Serverkonsolidierung reduzieren kann. Diese Art von Hardware- und Softwareänderungen wirken sich darauf aus, welche Upgrademethode Sie wählen.  
  
-   **Aktuelle Umgebung:** Überprüfen Sie die aktuelle Umgebung, um die verwendeten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten und die mit Ihrer Umgebung verbundenen Clients zu verstehen.  
  
    -   **Client-Anbieter:** Obwohl ein Upgrade kein gleichzeitiges Update aller Ihrer Clients erfordert, steht es Ihnen frei, dies zu tun. Wenn Sie ein Upgrade von [!INCLUDE[sql14](../../includes/sssql14-md.md)] oder höher durchführen, setzen die folgenden [!INCLUDE[sql15](../../includes/sssql15-md.md)]-Funktionen eine Anbieteraktualisierung generell voraus oder benötigen diese, um Ihnen zusätzliche Funktionen zur Verfügung stellen zu können.  
  
       -   [Always Encrypted &#40;Datenbankmodul&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
       -   [Stretch-Datenbank](../../sql-server/stretch-database/stretch-database.md)  
  
       -   [Verfügbarkeitsgruppenlistener, Clientkonnektivität und Anwendungsfailover &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
       -   SSL-Sicherheitsupdate  

   >[!NOTE]
   >Die vorherige Liste gilt auch für [!INCLUDE[sscurrent](../../includes/sscurrent-md.md)].
  
-   **Komponenten von Drittanbietern:** Ermitteln Sie die Kompatibilität von Drittanbieterkomponenten, z.B. dem integrierten Backup.  
  
-   **Zielumgebung:** Stellen Sie sicher, dass Ihre Zielumgebung die Hardware- und Softwareanforderungen erfüllt und die Anforderungen des ursprünglichen Systems unterstützen kann. Ihr Upgrade kann z.B. die Konsolidierung mehrerer SQL Server-Instanzen in eine einzelne, neue [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] -Instanz bedeuten oder die Virtualisierung Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Umgebung zu einer privaten oder öffentlichen Cloud.  
  
-   **Edition:** Ermitteln Sie die entsprechende Version von [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] für das Upgrade, und bestimmen Sie die gültigen Upgradepfade für das Upgrade. Ausführliche Informationen finden Sie unter [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md). Bevor Sie eine Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf eine andere Edition aktualisieren, sollten Sie überprüfen, ob die derzeit verwendete Funktionalität in der Edition, die Ziel des Upgrades ist, unterstützt wird.  
  
    > [!NOTE]  
    >  Wenn Sie [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] von einer früheren Version der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise-Edition aktualisieren, wählen Sie zwischen „Enterprise Edition: Core-basierte Lizenzierung“ und „Enterprise Edition“ aus. Diese Enterprise Editionen unterscheiden sich nur im Hinblick auf den Lizenzierungsmodus. Weitere Informationen finden Sie unter [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
-   **Abwärtskompatibilität:** Lesen Sie das Thema zur Abwärtskompatibilität des [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] -Datenbankmoduls, um sich über Änderungen im Verhalten zwischen [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version zu informieren, von der Sie upgraden. Siehe [SQL Server Database Engine Backward Compatibility](../../database-engine/sql-server-database-engine-backward-compatibility.md).  
  
-   **Aktualisierungsratgeber:**  Führen Sie den Aktualisierungsratgeber für [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] aus, um Hilfestellung bei Problemen zu erhalten, die den Upgradeprozess blockieren oder auf Grund besonders wichtiger Änderungen Modifikationen an Skripten oder Anwendungen erfordern. [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] enthält eine neue Version des Aktualisierungsratgebers, um Kunden beim Vorbereiten des Upgrades eines vorhandenen Systems zu unterstützen.  Mit diesem Tool können Sie außerdem prüfen, ob Ihre vorhandenen Datenbanken nach dem Upgrade neue Funktionen wie Stretch-Tabellen nutzen können.   
    Sie können den [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]Aktualisierungsratgeber  [hier](https://www.microsoft.com/en-us/download/details.aspx?id=48119)herunterladen.  
  
-   **Systemkonfigurationsprüfung:**  Führen Sie die [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] -Systemkonfigurationsprüfung (System Configuration Checker; SCC) aus, um festzustellen, ob das SQL Server-Setupprogramm Blockierungsprobleme erkennt, bevor Sie das Upgrade tatsächlich planen. Weitere Informationen finden Sie unter [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md).  
  
-   **Upgraden von speicheroptimierten Tabellen:** Wenn Sie eine SQL Server 2014-Datenbankinstanz mit speicheroptimierten Tabellen auf SQL Server 2016 aktualisieren, benötigt der Vorgang zusätzliche Zeit, um die speicheroptimierten Tabellen in das neue Format auf dem Datenträger zu konvertieren (die Datenbank ist währenddessen offline).   Die Zeitspanne hängt von der Größe der speicheroptimierten Tabellen und der Geschwindigkeit des E/A-Subsystems ab. Das Upgrade erfordert für direkte und neue Installationsupgrades drei Vorgänge hinsichtlich der Datengröße (Schritt 1 ist für parallele Upgrades nicht notwendig, die Schritte 2 und 3 indes schon):  
  
    1.  Führen Sie die Datenbankwiederherstellung mithilfe des alten Datenträgerformats aus (dies bedeutet, dass alle speicheroptimierten Tabellen vom Datenträger in den Speicher geladen werden).  
  
    2.  Serialisieren Sie die Daten auf dem Datenträger im neuen Format auf dem Datenträger  
  
    3.  Führen Sie die Datenbankwiederherstellung mithilfe des neuen Formats aus (dies bedeutet, dass alle speicheroptimierten Tabellen vom Datenträger in den Speicher geladen werden).  
  
     Wenn während dieses Vorgangs nicht genügend Speicherplatz auf dem Datenträger verfügbar ist, kann die Wiederherstellung nicht erfolgreich durchgeführt werden. Wenn Sie ein direktes Upgrade ausführen oder eine SQL Server 2014-Datenbank an eine SQL Server 2016-Instanz anfügen möchten, sollten Sie sicherstellen, dass genügend Speicherplatz auf dem Datenträger verfügbar ist, um die vorhandene Datenbank und den zusätzlichen Speicher zu speichern. Der zusätzliche Speicher entspricht hierbei der aktuellen Größe der Container in der MEMORY_OPTIMIZED_DATA-Dateigruppe in der Datenbank. Mithilfe der folgenden Abfrage können Sie den Speicherplatz ermitteln, den derzeit die MEMORY_OPTIMIZED_DATA-Dateigruppe und folglich auch die Menge des für eine erfolgreiches Upgrade erforderlichen Speicherplatzes erfordert:  
  
    ```  
    select cast(sum(size) as float)*8/1024/1024 'size in GB'   
    from sys.database_files  
    where data_space_id in (select data_space_id from sys.filegroups where type=N'FX')  
    ```  
  
## <a name="develop-and-test-the-upgrade-plan"></a>Entwickeln und Testen des Upgradeplans  
 Die beste Herangehensweise ist, das Upgrade wie jedes andere IT-Projekt zu behandeln. Sie sollten ein Upgrade-Team ernennen, das die für das Upgrade maßgeblichen Qualifikationen für die Datenbankverwaltung, das Netzwerk sowie das Extrahieren, Transformieren und Laden (ETL) besitzt. Das Team muss:  
  
-   **Informationen zum Auswählen einer Upgrademethode** finden Sie unter [Wählen einer Upgrademethode für das Datenbankmodul](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
  
-   **Entwickeln eines Wiederherstellungsplans:**. Mit diesem Plan können Sie Ihre ursprüngliche Umgebung wiederherstellen, wenn Sie sie zurücksetzen müssen.  
  
-   **Akzeptanzkriterien bestimmen:** Sie müssen wissen, ob das Upgrade erfolgreich war, bevor Sie Benutzer auf die upgegradete Umgebung umstellen.  
  
-   **Den Upgradeplan testen:** Verwenden Sie Microsoft SQL Server Distributed Replay Utility, um die Leistung mit der tatsächlichen Arbeitsauslastung zu testen. Dieses Hilfsprogramm kann Ablaufverfolgungsdaten mithilfe mehrerer Computer wiedergeben, indem es eine für die Unternehmung maßgebliche Arbeitsauslastung simuliert. Durch Ausführen einer Wiedergabe auf einem Testserver vor und nach einem SQL Server-Upgrade können Sie Leistungsunterschiede messen und nach Inkompatibilitäten der Anwendung suchen, die möglicherweise durch das Upgrade verursacht werden. Weitere Informationen finden Sie unter [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md) und [Befehlszeilenoptionen für das Verwaltungstool &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md).  
  
## <a name="next-steps"></a>Nächste Schritte  
 [Aktualisieren des Datenbankmoduls](../../database-engine/install-windows/upgrade-database-engine.md)  
  
  

