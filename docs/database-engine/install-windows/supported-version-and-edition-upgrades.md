---
title: "Unterst&#252;tzte Versions- und Editionsupgrades | Microsoft Docs"
ms.custom: ""
ms.date: "08/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Komponenten [SQL Server], hinzufügen zu vorhandenen Installationen"
  - "Versionen [SQL Server], aktualisieren"
  - "Aktualisieren von SQL Server, unterstützte Upgrades"
  - "Sprachübergreifende Unterstützung"
ms.assetid: 702359c4-6ca9-42a8-860c-a95a802898a1
caps.latest.revision: 148
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 147
---
# Unterst&#252;tzte Versions- und Editionsupgrades
  Sie können ein Upgrade von [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]und [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]ausführen. In diesem Thema werden die unterstützten Upgradepfade von diesen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen sowie die unterstützten Editionsupgrades für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]aufgeführt.  
  
## Prüfliste vor dem Upgrade  
  
-   Bevor eine Edition von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] auf eine andere Edition aktualisiert wird, sollten Sie überprüfen, ob die derzeit verwendete Funktionalität in der Edition, die Ziel des Upgrades ist, unterstützt wird.  
  
-   Aktivieren Sie vor dem Upgrade auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]die Windows-Authentifizierung für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent, und überprüfen Sie die erforderliche Standardkonfiguration. Dabei muss das Konto des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Diensts Mitglied der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Gruppe der Systemadministratoren sein.  
  
-   Um auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] aktualisieren zu können, müssen Sie ein unterstütztes Betriebssystem ausführen. Weitere Informationen finden Sie unter [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md).  
  
-   Das Upgrade wird blockiert, wenn noch ein Neustart aussteht.  
  
-   Das Upgrade wird blockiert, wenn der Windows Installer-Dienst nicht ausgeführt wird.  
  
## Nicht unterstützte Szenarien  
  
-   Versionsübergreifende Instanzen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] werden nicht unterstützt. Die Versionsnummern der [!INCLUDE[ssDE](../../includes/ssde-md.md)]-, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]- und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Komponenten innerhalb einer Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] müssen identisch sein.  
  
-   SQL Server 2016 ist nur für 64-Bit-Plattformen verfügbar. Ein plattformübergreifendes Upgrade wird nicht unterstützt. Sie können keine 32-Bit-Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup auf systemeigenes 64-Bit aktualisieren. Sie können jedoch Datenbanken von einer 32-Bit-Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sichern oder trennen und sie in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (64-Bit) wiederherstellen oder anfügen, wenn die Datenbanken nicht in der Replikation veröffentlicht sind. Sie müssen alle Anmeldenamen und anderen Benutzerobjekte in den Systemdatenbanken „master“, „msdb“ und „model“ wiederherstellen.  
  
-   Sie können während des Upgrades der vorhandenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keine neuen Funktionen hinzufügen. Nachdem Sie eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] aktualisiert haben, können Sie Funktionen mit dem [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Setup hinzufügen. Weitere Informationen finden Sie unter [Hinzufügen von Funktionen zu einer Instanz von SQL Server 2016 &#40;Setup&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md).  
 
-   Failovercluster werden im WOW-Modus nicht unterstützt.  
  
-   Upgrades von einer Evaluation Edition einer früheren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version werden nicht unterstützt.  
  
## Upgrades von früheren Versionen auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 
SQL Server 2016 unterstützt ein Upgrade von folgenden Versionen von SQL Server:
 
- SQL Server 2008 SP3 oder höher
- SQL Server 2008 R2 SP2 oder höher
- SQL Server 2012 SP2 oder höher
- SQL Server 2014 oder höher 
 

  
> [!NOTE]  
>  Informationen zum Aktualisieren von Datenbanken aus [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] finden Sie unter [SQL Server 2016-Unterstützung für SQL Server 2005](#SupportFor2005).  
  
 In der nachfolgenden Tabelle sind die unterstützten Szenarien für das Upgrade von früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] aufgeführt.  
  
|Upgrade von|Unterstützter Upgradepfad|  
|------------------|----------------------------|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Enterprise|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Developer|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Entwickler|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Standard|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Small Business|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Web|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Workgroup|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Datacenter|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Enterprise|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Developer|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Entwickler|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Small Business|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Standard|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Web|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Workgroup|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Enterprise|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Developer|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Entwickler <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Standard|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Express |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Express <br/> <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Business Intelligence|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Evaluation|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Evaluation <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Entwickler|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Entwickler|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Developer <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Express <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Entwickler|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Evaluation|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Evaluation <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Entwickler|  
|[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] Release Candidate* |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise |  
|[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] Entwickler |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise | 

 \* Microsoft-Unterstützung zum Aktualisieren von Release Candidate-Software ist speziell für Kunden vorgesehen, die am Technology Adoption Program (TAP) teilgenommen haben. 

   
###  <a name="SupportFor2005"></a> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Unterstützung für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
 In diesem Abschnitt wird die [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Unterstützung für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]erläutert. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] können Sie die folgenden Schritte ausführen:  
  
-   Anfügen einer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Datenbank (MDF-/LDF-Dateien) an eine [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Instanz des Datenbankmoduls.  
  
-   Wiederherstellen einer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Datenbank auf einer [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Instanz des Datenbankmoduls mithilfe einer Sicherung.  
  
-   Sichern eines [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] -Cubes und Wiederherstellen für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Wenn für eine [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Datenbank ein Upgrade auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ausgeführt wird, ändern sich der Datenbank-Kompatibilitätsgrad von 90 in 100. (In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] sind 100, 110, 120 und 130 gültige Werte für den Datenbank-Kompatibilitätsgrad.) In [ALTER DATABASE Kompatibilitätsgrad &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20Compatibility%20Level%20\(Transact-SQL\).md) wird erläutert, wie sich eine Änderung des Datenbank-Kompatibilitätsgrads auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anwendungen auswirken kann.  
  
 Szenarien, die in der Liste nicht aufgeführt sind, werden nicht unterstützt. Das gilt z. B. für:  
  
-   Installieren von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] auf demselben Computer (parallel).  
  
-   Verwenden einer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Instanz als Mitglied der Replikationstopologie, die eine [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Instanz umfasst.  
  
-   Konfigurieren der Datenbankspiegelung zwischen [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] - und [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Instanzen.  
  
-   Sichern des Transaktionsprotokolls mit Protokollversand zwischen [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] - und [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Instanzen.  
  
-   Konfigurieren von Verbindungsservern zwischen [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] - und [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Instanzen.  
  
-   Verwalten einer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Management Studio aus.  
  
-   Anfügen eines [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] -Cubes in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Management Studio.  
  
-   Herstellen einer Verbindung mit [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Management Studio aus.  
  
-   Verwalten eines [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] -Diensts von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Management Studio aus.  
  
-   Unterstützung von benutzerdefinierten Integration Services-Drittanbieterkomponenten für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] sowie Ausführen und Upgrade der Komponenten.  
  
## [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Editionsupgrade  
 In der folgenden Tabelle sind die unterstützten Szenarien für das Editionsupgrade in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] aufgeführt.  
  
 Schrittweise Anweisungen zum Ausführen eines Editionsupgrades finden Sie unter [Aktualisieren auf eine andere Edition von SQL Server 2016 &#40;Setup&#41;](../../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-2016-setup.md).  
  
|Upgrade von|Upgrade auf|  
|------------------|----------------|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (Server+CAL und Core)**|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise |  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise Evaluation**|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (Server+CAL- oder Core-Lizenz) <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Entwickler <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web <br/> <br/> Upgrades von Evaluation (kostenlose Edition) auf eine kostenpflichtige Edition werden für eigenständige Installationen, für gruppierte Installationen jedoch nicht unterstützt.|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard**|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (Server+CAL- oder Core-Lizenz)|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Developer**|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (Server+CAL- oder Core-Lizenz) <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (Server+CAL- oder Core-Lizenz) <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Express*|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (Server+CAL- oder Core-Lizenz) <br/><br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Entwickler <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard <br/> <br/> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Web|  
  
 Außerdem können Sie ein Editionsupgrade zwischen [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (Server+CAL-Lizenz) und [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (Core-Lizenz) ausführen:  
  
|Editionsupgrade von|Editionsupgrade auf|  
|--------------------------|------------------------|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (Server+CAL-Lizenz)**|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (Core-Lizenz)|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (Core-Lizenz)|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (Server+CAL-Lizenz)|  
  
 \* Gilt auch für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Express with Tools und [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Express with Advanced Services.  
  
 ** Das Ändern der Edition eines [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Failoverclusters ist nur beschränkt möglich. Die folgenden Szenarien werden bei [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Failoverclustern nicht unterstützt:  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Developer, Standard oder Evaluation.  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Developer in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard oder Evaluation.  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Evaluation.  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Evaluation in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard.  
  
## Siehe auch  
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)   
 [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)   
 [Aktualisieren auf SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)  
  
  