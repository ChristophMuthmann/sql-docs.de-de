---
title: Berichtsserver-Datenbank (einheitlicher SSRS-Modus) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [Reporting Services]
- report servers [Reporting Services], databases
- temporary databases [Reporting Services]
- report server database
- reportservertempdb
- reportserver database
ms.assetid: 0fc5c033-3fe1-4cea-86c7-66ea5e424d65
caps.latest.revision: "48"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 477c4bfb55742102aa08da46a1fa08bf2686b4cf
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="report-server-database-ssrs-native-mode"></a>Berichtsserver-Datenbank (einheitlicher SSRS-Modus)
  Ein Berichtsserver ist ein Server ohne Status, der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] zum Speichern von Metadaten und Objektdefinitionen verwendet. Eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Installation im einheitlichen Modus verwendet zwei Datenbanken, um den persistenten Datenspeicher von temporären Speicheranforderungen zu trennen. Die Datenbanken werden zusammen erstellt und sind namentlich aneinander gebunden. Die Namen der Datenbanken lauten standardmäßig **reportserver** bzw. **reportservertempdb**.  
  
 Eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Installation im SharePoint-Modus erstellt auch eine Datenbank für die Datenwarnungsfunktion. Die drei Datenbanken im SharePoint-Modus sind [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendungen zugeordnet. Weitere Informationen finden Sie unter [Verwalten einer Reporting Services-SharePoint-Dienstanwendung](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  
  
 Die Datenbanken können in einer lokalen Instanz oder in einer Remoteinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] ausgeführt werden. Die Auswahl einer lokalen Instanz ist hilfreich, wenn Sie über genügend Systemressourcen verfügen oder die Verwendung von Softwarelizenzen einschränken möchten. Durch das Ausführen von Datenbanken auf einem Remotecomputer kann jedoch die Leistung verbessert werden.  
  
 Sie können eine bereits vorhandene Berichtsserver-Datenbank aus einer früheren Installation oder einer anderen Instanz mit einer anderen Berichtsserverinstanz verbinden oder wiederverwenden. Das Schema der Berichtsserver-Datenbank muss mit der Berichtsserverinstanz kompatibel sein. Falls die Datenbank in einem älteren Format vorliegt, werden Sie zum Aktualisieren auf das aktuelle Format aufgefordert. Neuere Versionen können nicht auf eine frühere Version herabgestuft werden. Falls Sie mit einer aktuelleren Berichtsserver-Datenbank arbeiten, können Sie diese nicht mit einer früheren Version einer Berichtsserverinstanz verwenden. Weitere Informationen über das Aktualisieren der Berichtsserver-Datenbanken auf neuere Formate finden Sie unter [Upgraden der Berichtsserver-Datenbank](../../reporting-services/install-windows/upgrade-a-report-server-database.md).  
  
> [!IMPORTANT]  
>  Die Tabellenstruktur für die Datenbanken wird für Servervorgänge optimiert und sollte nicht geändert oder weiter optimiert werden. [!INCLUDE[msCoName](../../includes/msconame-md.md)] kann die Tabellenstruktur eventuell von einer Version zur nächsten ändern. Durch eigene Änderungen oder Erweiterungen der Datenbank beschränken oder verhindern Sie u. U. die Möglichkeit, zukünftige Upgrades auszuführen oder Service Packs anzuwenden. Möglicherweise werden durch Ihre Änderungen auch Berichtsservervorgänge beeinträchtigt. Wenn Sie z. B. in der ReportServer-Datenbank READ_COMMITTED_SNAPSHOT aktivieren, deaktivieren Sie die interaktive Sortierfunktion.  
  
 Alle Zugriffe auf eine Berichtsserver-Datenbank müssen durch den Berichtsserver behandelt werden. Für den Zugriff auf Inhalte in einer Berichtsserver-Datenbank können Sie Berichtsserver-Verwaltungstools, wie z.B. den Berichts-Manager oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], oder Programmierschnittstellen verwenden, wie z.B. den URL-Zugriff, den Report Server-Webdienst oder den WMI-Anbieter (Windows Management Instrumentation, Windows-Verwaltungsinstrumentation).  
  
 Die Verbindung mit der Berichtsserver-Datenbank wird normalerweise über den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager definiert. Die Verbindung kann jedoch auch während des Setupvorgangs definiert werden, wenn Sie die Standardkonfiguration installieren. Weitere Informationen zur Berichtsserververbindung mit der Datenbank finden Sie unter [Konfigurieren einer Verbindung mit der Berichtsserver-Datenbank (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="report-server-database"></a>Berichtsserver-Datenbank  
 Die Berichtsserver-Datenbank ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank, in der folgende Inhalte gespeichert werden:  
  
-   Von einem Berichtsserver verwaltete Elemente (Berichte und verknüpfte Berichte, freigegebene Datenquellen, Berichtsmodelle, Ordner, Ressourcen) sowie alle Eigenschaften und Sicherheitseinstellungen, die diesen Elementen zugeordnet sind.  
  
-   Abonnements und Zeitplandefinitionen.  
  
-   Berichtsmomentaufnahmen (einschließlich Abfrageergebnisse) und den Berichtsverlauf.  
  
-   Systemeigenschaften und Sicherheitseinstellungen auf Systemebene.  
  
-   Protokolldaten zur Berichtsausführung.  
  
-   Symmetrische Schlüssel, die verschlüsselte Verbindung und Anmeldeinformationen für externe Datenquellen.  
  
 Da in der Berichtsserver-Datenbank der Anwendungsstatus und persistente Daten gespeichert werden, empfiehlt es sich, einen Sicherungszeitplan für diese Datenbank zu erstellen, um Datenverlust zu vermeiden. Empfehlungen und Anweisungen zum Sichern der Datenbank finden Sie unter [Verschieben von Berichtsserver-Datenbanken auf einen anderen Computer (einheitlicher SSRS-Modus)](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
## <a name="report-server-temporary-database"></a>Temporäre Berichtsserver-Datenbank  
 Jede Berichtsserver-Datenbank speichert mithilfe einer zugehörigen temporären Datenbank Sitzungs- und Ausführungsdaten, zwischengespeicherte Berichte und Arbeitstabellen, die vom Berichtsserver generiert werden. Hintergrundserverprozesse entfernen regelmäßig ältere und nicht verwendete Elemente aus den Tabellen in der temporären Datenbank.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] erstellt die temporäre Datenbank nicht neu, wenn diese fehlt, und repariert auch keine fehlenden oder geänderten Tabellen. Obwohl die temporäre Datenbank keine persistenten Daten enthält, sollten Sie sie trotzdem sichern, sodass Sie sie nach einem Notfall nicht wiederherstellen müssen.  
  
 Wenn Sie die temporäre Datenbank sichern und anschließend wiederherstellen, sollten Sie die Inhalte löschen. Im Allgemeinen können die Inhalte der temporären Datenbank jederzeit bedenkenlos gelöscht werden. Nach dem Löschen der Inhalte müssen Sie jedoch den Report Server-Windows-Dienst neu starten.  
  
## <a name="see-also"></a>Siehe auch  
 [Hosten einer Berichtsserver-Datenbank in einem SQL Server-Failovercluster](../../reporting-services/install-windows/host-a-report-server-database-in-a-sql-server-failover-cluster.md)   
 [Speichern verschlüsselter Berichtsserverdaten (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services-Berichtsserver](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)   
 [Verwalten einer Berichtsserver-Datenbank (einheitlicher SSRS-Modus)](../../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)   
 [Erstellen einer Berichtsserver-Datenbank &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
 [Backup and Restore Operations for Reporting Services (Sicherungs- und Wiederherstellungsvorgänge für Reporting Services)](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md)  
  
  
