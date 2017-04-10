---
title: "F&#252;hren Sie ein Upgrade von SQL Server 2005 aus? | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad40e66f-71fe-4ee6-9ce3-17127e7b1d7a
caps.latest.revision: 21
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 21
---
# F&#252;hren Sie ein Upgrade von SQL Server 2005 aus?
  Das Ende des erweiterten Support für SQL Server 2005 ist ein guter Grund für das Upgrade auf eine neuere Version von SQL Server und der Azure SQL-Datenbank. Ein Upgrade ermöglicht es Ihnen, Sicherheit und Compliance beizubehalten, eine bahnbrechende Leistung zu erzielen, und die Infrastruktur Ihrer Datenplattform zu optimieren.  
  
 Weitere Informationen, Anleitungen und Tools zum Planen und Automatisieren Ihres Upgrades oder Ihrer Migration finden Sie unter [SQL Server 2005-Supportende](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
## Warum jetzt für ein Upgrade entscheiden?  
  
> [!IMPORTANT]  
>  Der erweiterte Support für SQL Server 2005 wird am 12. April 2016 eingestellt. Wenn Sie SQL Server 2005 nach dem 12. April 2016 noch einsetzen, erhalten Sie keine Sicherheitsupdates mehr.  
  
 Um ein Datenblatt im PDF-Format abzurufen, in dem die Vorteile des Upgrades von SQL Server 2005 erläutert werden, [klicken Sie hier](https://info.microsoft.com/rs/157-GQE-382/images/EN-CNTNT-Infographic-UpgradeSQL2005Datasheet.pdf) (nicht auf das Miniaturbild unten).  
  
 ![Data sheet about upgrading from SQL Server 2005](../../database-engine/install-windows/media/sqlserver2005eos.png "Data sheet about upgrading from SQL Server 2005")  
  
## Wählen Sie Ihre Upgradeoption  
 Wenn Sie ein Upgrade für relationale Datenbanken von SQL Server 2005 ausführen, finden Sie hier die Optionen für die relationale Speicherung auf der Microsoft-Plattform.  
  
 Um eine umfassendere Analyse dieser Optionen anzuzeigen, [klicken Sie hier](http://sql05upgrade.azurewebsites.net/).  
  
|Relationale Speicheroption|Vorteile|Weitere zu berücksichtigende Faktoren|  
|-------------------------------|--------------|-------------------------------|  
|**Lokale SQL Server-Infrastruktur**<br /><br /> Diese Option bietet sich für Datenbankanwendungen jeder Art an, von Transaktionssystemen bis hin zu Data Warehouses.|Sie haben die bestmögliche Kontrolle über Features und Skalierbarkeit, da Sie sowohl Hardware als auch Software selbst verwalten.<br /><br /> Wenn Sie ein Upgrade von SQL Server 2005 ausführen, ist dies die ähnlichste Umgebung.|Sie müssen vorab die größte Investition leisten und haben im laufenden Betrieb den höchsten Verwaltungsaufwand, da Sie Ihre eigene Hardware und Software kaufen, warten und verwalten müssen.<br /><br /> Weitere Informationen finden Sie unter [SQL Server 2016](https://www.microsoft.com/EN-US/server-cloud/products/sql-server-2016/).|  
|**SQL Server auf virtuellen Azure-Computern gehostet**<br /><br /> Ziehen Sie diese Option in Erwägung, wenn Ihnen die folgenden Punkte wichtig sind:<br /><br /> Vorzüge der Migration zu einer gehosteten Umgebung.<br /><br /> Kontrolle über die Betriebsumgebung.<br /><br /> Vertrauter Funktionsumfang von SQL Server.|Die Bereitstellung kann schnell aus einer Bibliothek mit Images virtueller Computer erfolgen.<br /><br /> Sie erhalten den vollständigen Funktionsumfang von SQL Server.<br /><br /> Sie sparen die Kosten für Hardware und Serversoftware. Sie zahlen nur für die Nutzungsstunden.|Sie müssen sowohl die SQL Server- als auch die Betriebssystemsoftware konfigurieren und verwalten.<br /><br /> <br /><br /> Weitere Informationen finden Sie unter [Übersicht zu SQL Server auf virtuellen Azure-Computern](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/).<br /><br /> Informationen zur Migration finden Sie unter [Migrieren einer Datenbank zu SQL Server auf einem virtuellen Azure-Computer](https://azure.microsoft.com/documentation/articles/virtual-machines-migrate-onpremises-database/).|  
|**Gehosteter Azure SQL-Datenbankdienst**<br /><br /> Ziehen Sie diese Option in Betracht, wenn Sie eine kostengünstigere Lösung mit weniger Wartung wünschen.<br /><br /> Diese Option eignet sich besonders für Apps, die nicht zu allen Zeiten die gleiche Kapazität erfordern oder externen Zugriff bereitstellen müssen.|Sie können schnell bereitstellen und einfach zentral hochskalieren.<br /><br /> Sie zahlen nur für die Nutzungsstunden.<br /><br /> Die Kosten für den Dienst beinhalten nicht nur die Speicherung, sondern darüber hinaus auch hohe Verfügbarkeit und automatische Sicherungen.|Azure SQL-Datenbank bringt den Verzicht auf einige Features von SQL Server mit sich, die in einer gehosteten Cloudumgebung nicht anwendbar sind. Weitere Informationen finden Sie unter [Azure SQL-Datenbank – Transact-SQL-Informationen.](https://azure.microsoft.com/documentation/articles/sql-database-transact-sql-information/).<br /><br /> Außerdem beträgt die maximale Datenbankgröße für Azure SQL-Datenbank 500 GB, im Vergleich dazu beträgt sie 524 PB für SQL Server.<br /><br /> Weitere Informationen finden Sie unter [SQL-Datenbank](https://azure.microsoft.com/services/sql-database/).<br /><br /> Informationen zur Migration finden Sie unter [Migrieren einer SQL Server-Datenbank zu Azure SQL-Datenbank](https://azure.microsoft.com/documentation/articles/sql-database-cloud-migrate/).|  
  
 Für bestimmte Daten und Anwendungen kann außerdem eine nicht relationale oder NoSQL-Lösung sinnvoll sein.  
  
|Nicht-relationale Lösung|Vorteile|  
|------------------------------|--------------|  
|**Azure DocumentDB**<br /><br /> Erwägen Sie diese Option für moderne skalierbare Web- und mobile Anwendungen, die JSON-Daten verwenden und eine Kombination aus stabiler Abfrage- und Transaktionsdatenverarbeitung benötigen.<br /><br /> Weitere Informationen finden Sie unter [DocumentDB](https://azure.microsoft.com/en-us/services/documentdb/).<br /><br /> Informationen zum Importieren von Daten finden Sie unter [Importieren von Daten in DocumentDB](https://azure.microsoft.com/documentation/articles/documentdb-import-data/).|Ihre Dokumente werden indiziert, und Sie können die vertraute SQL-Syntax für Abfragen darauf verwenden.<br /><br /> Die Datenbank besitzt kein Schema.<br /><br /> Sie können Dokumenten Eigenschaften hinzufügen, ohne die Indizes neu erstellen zu müssen.<br /><br /> Sie erhalten JSON- und JavaScript-Unterstützung direkt innerhalb des Datenbankmoduls.<br /><br /> Sie erhalten systemeigene Unterstützung für räumliche Daten und Integration mit anderen Azure-Services, einschließlich Azure Search, HDInsight, und Data Factory.<br /><br /> Sie erhalten Speicherung mit geringer Latenz und hoher Leistung bei reservierten Durchsatzniveaus.|  
|**Azure-Tabellenspeicher**<br /><br /> Erwägen Sie diese Option, um Petabytes teilweise strukturierter Daten in einer kostengünstigen Lösung zu speichern.<br /><br /> Weitere Informationen finden Sie unter [Tabellenspeicher](https://azure.microsoft.com/services/storage/tables/).|Sie können Ihre Apps und Ihr Tabellenschema weiterentwickeln, ohne die Daten offline nehmen zu müssen.<br /><br /> Sie können zentral hochskalieren, ohne Ihr Dataset horizontal partitionieren zu müssen.<br /><br /> Sie erhalten geografisch redundanten Speicher, der Daten über mehrere Regionen repliziert.|  
  
 Um den Bericht „Migrieren von SQL Server 2005“ von Directions on Microsoft herunterzuladen, der weitere Details zu den Upgradeoptionen enthält, [klicken Sie hier](https://info.microsoft.com/CO-SQL-CNTNT-FY16-09Sep-14-ModernizationDirOnMFST-Register.html) (nicht auf das Miniaturbild unten).  
  
 ![Report about migrating from SQL Server 2005](../../database-engine/install-windows/media/sqlserver2005migratingdoc.png "Report about migrating from SQL Server 2005")  
  
## Planen des Upgrades  
  
-   Lesen Sie die Informationen zur Planung Ihres Upgrades in den folgenden Blogbeiträgen des SQL Server-Teams.  
  
    -   [Planen eines effizienten Upgrades von SQL Server 2005: Schritt 1 von 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/10/planning-an-efficient-upgrade-from-sql-server-2005-step-1-of-3.aspx)  
  
    -   [Planen eines effizienten Upgrades von SQL Server 2005: Schritt 2 von 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/15/planning-an-efficient-upgrade-from-sql-server-2005-step-2-of-3.aspx)  
  
    -   [Planen eines effizienten Upgrades von SQL Server 2005: Schritt 3 von 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/17/planning-an-efficient-upgrade-from-sql-server-2005-step-3-of-3.aspx)  
  
-   Überprüfen Sie die Voraussetzungen und Überlegungen unter [Planen einer SQL Server-Installation](../../sql-server/install/planning-a-sql-server-installation.md), einschließlich der [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md).  
  
-   Lesen Sie, wie Sie das Upgrade durchführen können   
  
    -   Gehen Sie die verfügbaren Upgrademethoden durch, und erfahren Sie im Thema [Aktualisieren des Datenbankmoduls](../../database-engine/install-windows/upgrade-database-engine.md), wie Sie sie planen und testen können.  
  
        > [!IMPORTANT]  
        >  Sie können ein Upgrade eines SQL Server 2005-Servers auf einen SQL Server 2016-Server nicht an Ort und Stelle ausführen. Sie müssen zuerst SQL Server 2016 installieren und dann Ihre SQL Server 2005-Datenbanken zur neuen Installation migrieren. Weitere Informationen finden Sie im Abschnitt zum Upgrade von Neuinstallationen im Thema [Wählen einer Upgrademethode für das Datenbankmodul](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
  
    -   Um den ausführlicheren technischen Upgradeleitfaden im PDF-Format herunterzuladen, [klicken Sie hier](http://download.microsoft.com/download/7/1/5/715BDFA7-51B6-4D7B-AF17-61E78C7E538F/SQL_Server_2014_Upgrade_technical_guide.pdf).  
  
        > [!NOTE]  
        >  Dies ist derzeit die SQL Server 2014-Version des "Technischen Upgradeleitfadens". Die SQL Server 2016-Version des Leitfadens ist noch nicht verfügbar.  
  
-   Weitere Informationen, Anleitungen und Tools zum Planen und Automatisieren Ihres Upgrades oder Ihrer Migration finden Sie unter [SQL Server 2005-Supportende](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
## Herunterladen von SQL Server 2016  
 Um eine Evaluierungsversion von SQL Server 2016 herunterzuladen, [klicken Sie hier](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016/?wt.mc_id=upgrade2005).  
  
## Siehe auch  
 [SQL Server 2016](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2016/default.aspx)   
 [SQL Server 2005-Supportende](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)   
 [Upgrade von SQL Server 2005 auf SQL Server 2014](https://msdn.microsoft.com/en-us/library/mt170591\(v=sql.120\).aspx)  
  
  