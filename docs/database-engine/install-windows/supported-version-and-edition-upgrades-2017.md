---
title: "Unterstützte Versions- und Editionsupgrades in SQL Server 2017 | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- components [SQL Server], adding to existing installations
- versions [SQL Server], upgrading
- upgrading SQL Server, upgrades supported
- cross-language support
ms.assetid: 702359c4-6ca9-42a8-860c-a95a802898a1
caps.latest.revision: 148
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4fdcc353e4dc1d29a2411b5ec846f2d8e415a849
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="supported-version-and-edition-upgrades-for-sql-server-2017"></a>Unterstützte Versions- und Editionsupgrades in SQL Server 2017
  Sie können ein Upgrade von [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] und [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] ausführen. In diesem Thema werden die unterstützten Upgradepfade von diesen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen sowie die unterstützten Editionsupgrades für [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]aufgeführt.  
  
## <a name="pre-upgrade-checklist"></a>Prüfliste vor dem Upgrade  
  
-   Bevor eine Edition von [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] auf eine andere Edition aktualisiert wird, sollten Sie überprüfen, ob die derzeit verwendete Funktionalität in der Edition, die Ziel des Upgrades ist, unterstützt wird.  
  
-   Aktivieren Sie vor dem Upgrade auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]die Windows-Authentifizierung für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent, und überprüfen Sie die erforderliche Standardkonfiguration. Dabei muss das Konto des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Diensts Mitglied der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Gruppe der Systemadministratoren sein.  
  
-   Um auf [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] aktualisieren zu können, müssen Sie ein unterstütztes Betriebssystem ausführen. Weitere Informationen finden Sie unter [Hardware- und Softwareanforderungen für die Installation von SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Das Upgrade wird blockiert, wenn noch ein Neustart aussteht.  
  
-   Das Upgrade wird blockiert, wenn der Windows Installer-Dienst nicht ausgeführt wird.  
  
## <a name="unsupported-scenarios"></a>Nicht unterstützte Szenarien  
  
-   Versionsübergreifende Instanzen von [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] werden nicht unterstützt. Die Versionsnummern der [!INCLUDE[ssDE](../../includes/ssde-md.md)]-, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]- und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Komponenten innerhalb einer Instanz von [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]müssen identisch sein.  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] ist nur für 64-Bit-Plattformen verfügbar. Ein plattformübergreifendes Upgrade wird nicht unterstützt. Sie können keine 32-Bit-Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup auf systemeigenes 64-Bit aktualisieren. Sie können jedoch Datenbanken von einer 32-Bit-Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sichern oder trennen und sie in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (64-Bit) wiederherstellen oder anfügen, wenn die Datenbanken nicht in der Replikation veröffentlicht sind. Sie müssen alle Anmeldenamen und anderen Benutzerobjekte in den Systemdatenbanken „master“, „msdb“ und „model“ wiederherstellen.  
  
-   Sie können während des Upgrades der vorhandenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]keine neuen Funktionen hinzufügen. Nachdem Sie eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] aktualisiert haben, können Sie Funktionen mit dem [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]-Setup hinzufügen. Weitere Informationen finden Sie unter [Hinzufügen von Funktionen zu einer Instanz von SQL Server 40 (Setup)](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md).  
 
-   Failovercluster werden im WOW-Modus nicht unterstützt.  
  
-   Upgrades von einer Evaluation Edition einer früheren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version werden nicht unterstützt.
  
## <a name="upgrades-from-earlier-versions-to-includesssqlv14-mdincludessssqlv14-mdmd"></a>Upgrades von früheren Versionen auf [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]  
 
[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] unterstützt ein Upgrade von folgenden Versionen von SQL Server:
 
- SQL Server 2008 SP4 oder höher
- SQL Server 2008 R2 SP3 oder höher
- SQL Server 2012 SP2 oder höher
- SQL Server 2014 oder höher 
- SQL Server 2016 oder höher
 

  
> [!NOTE]  
>  Informationen zum Aktualisieren von Datenbanken aus [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] finden Sie unter [SQL Server 2016-Unterstützung für SQL Server 2005](#SupportFor2005).  
  
 In der nachfolgenden Tabelle sind die unterstützten Szenarien für das Upgrade von früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] aufgeführt.  
  
|Upgrade von|Unterstützter Upgradepfad|  
|:------|:------|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Small Business|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Workgroup|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Datacenter|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Small Business|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Workgroup|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express <br/> <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Business Intelligence|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Evaluation|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Entwickler|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Evaluation|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Business Intelligence|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Evaluation|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Release Candidate* |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise |  
|[!INCLUDE[sssqlv14_md](../../includes/sssqlv14-md.md)] Developer |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise | 

 \* Microsoft-Unterstützung zum Aktualisieren von Release Candidate-Software ist speziell für Kunden vorgesehen, die am Technology Adoption Program (TAP) teilgenommen haben. 

   
###  <a name="SupportFor2005"></a> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Unterstützung für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
 In diesem Abschnitt wird die [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] -Unterstützung für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]erläutert. In [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] können Sie die folgenden Schritte ausführen:  
  
-   Anfügen einer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Datenbank (MDF-/LDF-Dateien) an eine [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]-Instanz des Datenbankmoduls.  
  
-   Wiederherstellen einer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Datenbank auf einer [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]-Instanz des Datenbankmoduls mithilfe einer Sicherung.  
  
-   Sichern eines [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)]-Cubes und Wiederherstellen in [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  
  
Wenn für eine [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Datenbank ein Upgrade auf [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] ausgeführt wird, ändern sich der Datenbank-Kompatibilitätsgrad von 90 in 100. (In [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] sind 100, 110, 120, 130 und 140 gültige Werte für den Datenbank-Kompatibilitätsgrad.) In [ALTER DATABASE Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) wird erläutert, wie sich eine Änderung des Datenbank-Kompatibilitätsgrads auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anwendungen auswirken kann.  
  
Szenarien, die in der Liste nicht aufgeführt sind, werden nicht unterstützt. Das gilt z. B. für:  
  
- Installieren von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] auf demselben Computer (parallel).  
  
- Verwenden einer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Instanz als Mitglied der Replikationstopologie, die eine [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]-Instanz umfasst.  
  
- Konfigurieren der Datenbankspiegelung zwischen [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] - und [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Instanzen.  
  
- Sichern des Transaktionsprotokolls mit Protokollversand zwischen [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] - und [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Instanzen.  
  
- Konfigurieren von Verbindungsservern zwischen [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] - und [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Instanzen.  
  
- Verwalten einer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Instanz von [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Management Studio aus.  
  
- Anfügen eines [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] -Cubes in [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Management Studio.  
  
- Herstellen einer Verbindung mit [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] von [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Management Studio aus.  
  
- Verwalten eines [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] -Diensts von [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Management Studio aus.  
  
- Unterstützung von benutzerdefinierten Integration Services-Drittanbieterkomponenten für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] sowie Ausführen und Upgrade der Komponenten.  
  
## <a name="includesssqlv14-mdincludessssqlv14-mdmd-edition-upgrade"></a>[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Editionsupgrade  
In der folgenden Tabelle sind die unterstützten Szenarien für das Editionsupgrade in [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] aufgeführt.  
  
Ausführliche Anweisungen zum Ausführen eines Editionsupgrades finden Sie unter [Aktualisieren auf eine andere Edition von SQL Server (Setup)](../../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md).  
  
|Upgrade von|Upgrade auf|  
|------------------|----------------|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL und Core)**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise |  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise Evaluation**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL- oder Core-Lizenz) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> Upgrades von Evaluation (kostenlose Edition) auf eine kostenpflichtige Edition werden für eigenständige Installationen, für gruppierte Installationen jedoch nicht unterstützt.|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL- oder Core-Lizenz)|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL- oder Core-Lizenz) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL- oder Core-Lizenz) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express*|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL- oder Core-Lizenz) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
  
 Außerdem können Sie ein Editionsupgrade zwischen [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL-Lizenz) und [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Core-Lizenz) ausführen:  
  
|Editionsupgrade von|Editionsupgrade auf|  
|--------------------------|------------------------|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL-Lizenz)**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Core-Lizenz)|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Core-Lizenz)|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL-Lizenz)|  
  
 \* Gilt auch für [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express mit Tools und [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express mit Advanced Services.  
  
 ** Das Ändern der Edition eines [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]-Failoverclusters ist nur beschränkt möglich. Die folgenden Szenarien werden bei [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]-Failoverclustern nicht unterstützt:  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise in [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer, Standard oder Evaluation.  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer in [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard oder Evaluation.  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard auf [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation.  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation auf [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard.  
  
## <a name="see-also"></a>Siehe auch  

 [Editionen und unterstützten Funktionen von SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)
 
 [Hardware- und Softwareanforderungen für die Installation von SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 
 [Aktualisieren von SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
  
  

