---
title: "Führen Sie ein Upgrade von SQL Server 2005 aus? | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ad40e66f-71fe-4ee6-9ce3-17127e7b1d7a
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d582d7d9ca0bc90ca40ee34e946d49bf545024bd
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="are-you-upgrading-from-sql-server-2005"></a>Führen Sie ein Upgrade von SQL Server 2005 aus?

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 Das Ende des erweiterten Support für SQL Server 2005 ist ein guter Grund für das Upgrade auf eine neuere Version von SQL Server und der Azure SQL-Datenbank. Ein Upgrade ermöglicht es Ihnen, Sicherheit und Compliance beizubehalten, eine bahnbrechende Leistung zu erzielen, und die Infrastruktur Ihrer Datenplattform zu optimieren.  
  
 Weitere Informationen, Anleitungen und Tools zum Planen und Automatisieren Ihres Upgrades oder Ihrer Migration finden Sie unter [SQL Server 2005-Supportende](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
## <a name="why-upgrade"></a>Warum jetzt für ein Upgrade entscheiden?  
  
> [!IMPORTANT]  
>  Der erweiterte Support für SQL Server 2005 wurde am 12. April 2016 eingestellt. Wenn Sie SQL Server 2005 nach dem 12. April 2016 noch einsetzen, erhalten Sie keine Sicherheitsupdates mehr.  
  
## <a name="choose-your-upgrade-option"></a>Wählen Sie Ihre Upgradeoption  
Wenn Sie ein Upgrade für relationale Datenbanken von SQL Server 2005 ausführen, finden Sie hier die Optionen für die relationale Speicherung auf der Microsoft-Plattform.  
  
Um eine umfassendere Analyse dieser Optionen anzuzeigen, [klicken Sie hier](http://sql05upgrade.azurewebsites.net/).  
  
|Relationale Speicheroption|Vorteile|Weitere zu berücksichtigende Faktoren|  
|-------------------------------|--------------|-------------------------------|  
|**Lokale SQL Server-Infrastruktur**<br /><br /> Diese Option bietet sich für Datenbankanwendungen jeder Art an, von Transaktionssystemen bis hin zu Data Warehouses.|Sie haben die bestmögliche Kontrolle über Features und Skalierbarkeit, da Sie sowohl Hardware als auch Software selbst verwalten.<br /><br /> Wenn Sie ein Upgrade von SQL Server 2005 ausführen, ist dies die ähnlichste Umgebung.|Sie müssen vorab die größte Investition leisten und haben im laufenden Betrieb den höchsten Verwaltungsaufwand, da Sie Ihre eigene Hardware und Software kaufen, warten und verwalten müssen.<br /><br /> Weitere Informationen finden Sie unter [SQL Server](https://www.microsoft.com/EN-US/server-cloud/products/sql-server-2017/).|  
|**SQL Server auf virtuellen Azure-Computern gehostet**<br /><br /> Ziehen Sie diese Option in Erwägung, wenn Ihnen die folgenden Punkte wichtig sind:<br /><br /> Vorzüge der Migration zu einer gehosteten Umgebung.<br /><br /> Kontrolle über die Betriebsumgebung.<br /><br /> Vertrauter Funktionsumfang von SQL Server.|Die Bereitstellung kann schnell aus einer Bibliothek mit Images virtueller Computer erfolgen.<br /><br /> Sie erhalten den vollständigen Funktionsumfang von SQL Server.<br /><br /> Sie sparen die Kosten für Hardware und Serversoftware. Sie zahlen nur für die Nutzungsstunden.|Sie müssen sowohl die SQL Server- als auch die Betriebssystemsoftware konfigurieren und verwalten.<br /><br /> <br /><br /> Weitere Informationen finden Sie unter [Übersicht zu SQL Server auf virtuellen Azure-Computern](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/).<br /><br /> Informationen zur Migration finden Sie unter [Migrieren einer Datenbank zu SQL Server auf einem virtuellen Azure-Computer](https://azure.microsoft.com/documentation/articles/virtual-machines-migrate-onpremises-database/).|  
|**Gehosteter Azure SQL-Datenbankdienst**<br /><br /> Ziehen Sie diese Option in Betracht, wenn Sie eine kostengünstigere Lösung mit weniger Wartung wünschen.<br /><br /> Diese Option eignet sich besonders für Apps, die nicht zu allen Zeiten die gleiche Kapazität erfordern oder externen Zugriff bereitstellen müssen.|Sie können schnell bereitstellen und einfach zentral hochskalieren.<br /><br /> Sie zahlen nur für die Nutzungsstunden.<br /><br /> Die Kosten für den Dienst beinhalten nicht nur die Speicherung, sondern darüber hinaus auch Hochverfügbarkeit und automatische Sicherungen.|Azure SQL-Datenbank bringt den Verzicht auf einige Features von SQL Server mit sich, die in einer gehosteten Cloudumgebung nicht anwendbar sind. Weitere Informationen finden Sie unter [Azure SQL-Datenbank – Transact-SQL-Informationen](https://azure.microsoft.com/documentation/articles/sql-database-transact-sql-information/).<br /><br /> Außerdem beträgt die maximale Datenbankgröße für Azure SQL-Datenbank 500 GB, im Vergleich dazu beträgt sie 524 PB für SQL Server.<br /><br /> Weitere Informationen finden Sie unter [SQL-Datenbank](https://azure.microsoft.com/services/sql-database/).<br /><br /> Informationen zur Migration finden Sie unter [Migrieren einer SQL Server-Datenbank zu Azure SQL-Datenbank](https://azure.microsoft.com/documentation/articles/sql-database-cloud-migrate/).|  
  
 Für bestimmte Daten und Anwendungen kann außerdem eine nicht relationale oder NoSQL-Lösung sinnvoll sein.  
  
|Nicht-relationale Lösung|Vorteile|  
|------------------------------|--------------|  
|**Azure Cosmos DB**<br /><br /> Erwägen Sie diese Option für moderne skalierbare Web- und mobile Anwendungen, die JSON-Daten verwenden und eine Kombination aus stabiler Abfrage- und Transaktionsdatenverarbeitung benötigen.<br /><br /> Weitere Informationen finden Sie unter [Cosmos DB](http://azure.microsoft.com/services/cosmos-db/).<br /><br /> Informationen zum Importieren von Daten finden Sie unter [Import data to Cosmos DB (Importieren von Daten in Cosmos DB)](http://docs.microsoft.com/azure/cosmos-db/import-data/).|Ihre Dokumente werden indiziert, und Sie können die vertraute SQL-Syntax für Abfragen darauf verwenden.<br /><br /> Die Datenbank besitzt kein Schema.<br /><br /> Sie können Dokumenten Eigenschaften hinzufügen, ohne die Indizes neu erstellen zu müssen.<br /><br /> Sie erhalten JSON- und JavaScript-Unterstützung direkt innerhalb des Datenbankmoduls.<br /><br /> Sie erhalten systemeigene Unterstützung für räumliche Daten und Integration mit anderen Azure-Services, einschließlich Azure Search, HDInsight, und Data Factory.<br /><br /> Sie erhalten Speicherung mit geringer Latenz und hoher Leistung bei reservierten Durchsatzniveaus.|  
|**Azure-Tabellenspeicher**<br /><br /> Erwägen Sie diese Option, um Petabytes teilweise strukturierter Daten in einer kostengünstigen Lösung zu speichern.<br /><br /> Weitere Informationen finden Sie unter [Tabellenspeicher](https://azure.microsoft.com/services/storage/tables/).|Sie können Ihre Apps und Ihr Tabellenschema weiterentwickeln, ohne die Daten offline nehmen zu müssen.<br /><br /> Sie können zentral hochskalieren, ohne Ihr Dataset horizontal partitionieren zu müssen.<br /><br /> Sie erhalten geografisch redundanten Speicher, der Daten über mehrere Regionen repliziert.|  
  
## <a name="plan-your-upgrade"></a>Planen des Upgrades  
  
-   Lesen Sie die Informationen zur Planung Ihres Upgrades in den folgenden Blogbeiträgen des SQL Server-Teams.  
  
    -   [Planen eines effizienten Upgrades von SQL Server 2005: Schritt 1 von 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/10/planning-an-efficient-upgrade-from-sql-server-2005-step-1-of-3.aspx)  
  
    -   [Planen eines effizienten Upgrades von SQL Server 2005: Schritt 2 von 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/15/planning-an-efficient-upgrade-from-sql-server-2005-step-2-of-3.aspx)  
  
    -   [Planen eines effizienten Upgrades von SQL Server 2005: Schritt 3 von 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/17/planning-an-efficient-upgrade-from-sql-server-2005-step-3-of-3.aspx)  
  
-   Überprüfen Sie die Voraussetzungen und Überlegungen unter [Planning a SQL Server Installation (Planen einer SQL Server-Installation)](../../sql-server/install/planning-a-sql-server-installation.md), einschließlich der [Hardware and Software Requirements for Installing SQL Server (Hardware- und Softwareanforderungen für die Installation von SQL Server)](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Lesen Sie, wie Sie das Upgrade durchführen können  
  
    -   Gehen Sie die verfügbaren Upgrademethoden durch, und erfahren Sie im Artikel [Aktualisieren der Datenbank-Engine](../../database-engine/install-windows/upgrade-database-engine.md), wie Sie die Methoden planen und testen können.  
  
        > [!IMPORTANT]  
        >  Sie können ein Upgrade einer SQL Server 2005-Instanz auf einen SQL Server 2017-Server nicht an Ort und Stelle ausführen. Sie müssen zuerst eine Instanz von SQL Server 2017 installieren und dann Ihre SQL Server 2005-Datenbanken zur neuen Installation migrieren. Weitere Informationen finden Sie im Abschnitt zum Upgrade von Neuinstallationen im Thema [Wählen einer Upgrademethode für die Datenbank-Engine](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
   
  
-   Weitere Informationen, Anleitungen und Tools zum Planen und Automatisieren Ihres Upgrades oder Ihrer Migration finden Sie unter [SQL Server 2005-Supportende](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
## <a name="get-sql-server"></a>SQL Server erwerben  
 Um eine Evaluierungsversion von SQL Server herunterzuladen, [click here (klicken Sie hier)](http://www.microsoft.com/evalcenter/evaluate-sql-server-2016).  
  
## <a name="next-steps"></a>Next Steps  
 [SQL Server (2017)](http://www.microsoft.com/sql-server/sql-server-2017)   
 [SQL Server 2005: Supportende](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)   
  
  
