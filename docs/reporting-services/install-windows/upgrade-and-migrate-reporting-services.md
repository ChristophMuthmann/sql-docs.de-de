---
title: Aktualisieren und Migrieren von Reporting Services | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSRS, upgrading
- Reporting Services, upgrades
- SQL Server Reporting Services, upgrading
- upgrading Reporting Services
ms.assetid: 851a19a8-07ab-4d42-992f-1986c4c8df55
caps.latest.revision: "92"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: af94ddd1515281c0e6efefce3d3e6e329c8292c1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="upgrade-and-migrate-reporting-services"></a>Aktualisieren und Migrieren von Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  Dieser Artikel dient zur Übersicht über die Upgrade- und Migrationsoptionen für SQL Server Reporting Services. Es gibt zwei allgemeine Vorgehensweisen beim Upgrade einer SQL Server Reporting Services-Bereitstellung:  
  
-   **Upgrade:** Sie aktualisieren die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Komponenten auf den Servern und Instanzen, auf denen sie derzeit installiert sind. Dies wird im Allgemeinen als "direktes" Upgrade bezeichnet. Direkte Upgrades zwischen verschiedenen Modi des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Servers werden nicht unterstützt. Beispielsweise können Sie keinen Berichtsserver im einheitlichen Modus auf einen Berichtsserver im SharePoint-Modus aktualisieren. Berichtselemente können allerdings zwischen verschiedenen Modi migriert werden. Weitere Informationen finden Sie weiter unten in diesem Dokument im Abschnitt "Migration vom einheitlichen Modus zum SharePoint-Modus".  
  
-   **Migrieren:**Sie installieren und konfigurieren eine neue SharePoint-Umgebung, kopieren Ihre Berichtselemente und Ressourcen in die neue Umgebung und konfigurieren die neue Umgebung für die Verwendung der vorhandenen Inhalte. Eine einfachere Form der Migration besteht darin, die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Datenbanken, die Konfigurationsdateien und (falls Sie den SharePoint-Modus verwenden) die SharePoint-Inhaltsdatenbanken zu kopieren.  
    
> **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen Modus &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus
  
##  <a name="bkmk_known_issues"></a> Bekannte Upgradeprobleme und Best Practices  
 Eine ausführliche Liste der unterstützten Editionen und Versionen, die aktualisiert werden können, finden Sie unter [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
> [!TIP]  
>  Die neuesten Informationen zu Problemen mit SQL Server finden Sie unter:  
>   
>  -   [Versionsanmerkungen zu SQL Server 2016](http://go.microsoft.com/fwlink/?LinkID=398124)herunter.  
  
  
##  <a name="bkmk_side_by_side"></a> Parallele Installationen  
 SQL Server Reporting Services im einheitlichen Modus kann parallel mit einer Bereitstellung von [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] im einheitlichen Modus installiert sein.  
  
 Parallele Bereitstellungen von Komponenten mit SQL Server Reporting Services im SharePoint-Modus und allen Vorgängerversionen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus werden nicht unterstützt.  
  
  
##  <a name="bkmk_inplace_upgrade"></a> Direktes Upgrade  
 Das Upgrade wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup ausgeführt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup kann verwendet werden, um ein Upgrade von einer oder allen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten, einschließlich [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], durchzuführen. Setup erkennt die vorhandenen Instanzen und fordert Sie auf, das Upgrade durchzuführen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup stellt Upgradeoptionen bereit, die Sie als Befehlszeilenargument oder im Setup-Assistenten angeben können.  
  
 Wenn Sie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup ausführen, können Sie die Option zum Aktualisieren einer der folgenden Versionen auswählen, oder Sie können eine neue SQL Server Reporting Services-Instanz installieren, die parallel zu vorhandenen Installationen ausgeführt wird:  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]finden Sie in folgenden Themen:  

* [Aktualisieren auf SQL Server 2016](../../database-engine/install-windows/upgrade-sql-server.md)
* [Aktualisieren auf SQL Server 2016 mithilfe des Installations-Assistenten &#40;Setup&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)
* [Installieren von SQL Server 2016 von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)
  
  
##  <a name="bkmk_upgrade_checklist"></a> Prüfliste vor dem Upgrade  
 Sehen Sie sich Folgendes an, bevor Sie SQL Server Reporting Services aktualisieren:  
  
-   Überprüfen Sie die Anforderungen, um festzustellen, ob [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]von Ihrer Hard- und Software unterstützt wird. Weitere Informationen finden Sie unter [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Verwenden Sie die Systemkonfigurationsprüfung, um den Berichtsservercomputer auf Bedingungen zu überprüfen, die eine erfolgreiche Installation von SQL Server Reporting Services verhindern könnten. Weitere Informationen finden Sie unter [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md).  
  
-   Lesen Sie bewährte Methoden und Anleitungen hinsichtlich der Sicherheit für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
-   Sichern Sie den symmetrischen Schlüssel. Weitere Informationen finden Sie unter [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
-   Sichern Sie die Berichtsserver-Datenbanken und -Konfigurationsdateien. Weitere Informationen finden Sie unter [Backup and Restore Operations for Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md).  
  
-   Sichern Sie alle Anpassungen von vorhandenen virtuellen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Verzeichnissen in IIS.  
  
-   Entfernen Sie ungültige SSL-Zertifikate.  Dies schließt Zertifikate ein, die abgelaufen sind und vor dem Upgrade von Reporting Services nicht aktualisiert werden sollen.  Ungültige Zertifikate haben Fehler beim Upgrade zur Folge, und die folgende Fehlermeldung wird in die Reporting Services-Protokolldatei geschrieben: **Microsoft.ReportingServices.WmiProvider.WMIProviderException: Ein SSL-Zertifikat (Secure Sockets Layer) ist für die Website nicht konfiguriert.**.  
  
 Bevor Sie eine Produktionsumgebung aktualisieren, führen Sie immer ein Testupgrade in einer Vorproduktionsumgebung aus, die die gleiche Konfiguration wie Ihre Produktionsumgebung aufweist.  
  
  
## <a name="overview-of-migration-scenarios"></a>Übersicht über Migrationsszenarien  
 Wenn Sie von einer unterstützten Version von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aktualisieren, können Sie normalerweise den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup-Assistenten ausführen, um ein Upgrade der Berichtsserver-Programmdateien, der Datenbank und alle zugehörigen Anwendungsdaten durchzuführen.  
  
 Eine manuelle **Migration** der Berichtsserverinstallation ist allerdings erforderlich, wenn eine der folgenden Bedingungen zutrifft:  
  
-   Sie möchten den Typ des in der Bereitstellung verwendeten Berichtsservers ändern. Beispielsweise können Sie keinen Berichtsserver im einheitlichen Modus auf den SharePoint-Modus aktualisieren bzw. konvertieren. Weitere Informationen finden Sie unter [Native to SharePoint Migration (SSRS) (Migration vom einheitlichen Modus zum SharePoint-Modus (SSRS))](../../reporting-services/install-windows/native-to-sharepoint-migration-ssrs.md).  
  
-   Sie möchten die Zeit verkürzen, die der Berichtsserver während des Upgradevorgangs offline geschaltet wird. Die derzeitige Installation bleibt online, während Sie Inhaltsdaten auf eine neue Berichtsserverinstanz kopieren und die Installation testen, ohne dass der Status der vorhandenen Berichtsserverinstallation geändert wird.  
  
-   Sie möchten eine SharePoint 2010-Bereitstellung von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] zu SharePoint 2013/2016 migrieren. SharePoint 2013/2016 unterstützt keine direkten Upgrades aus SharePoint 2010. Weitere Informationen finden Sie unter [Migrieren einer Installation von Reporting Services &#40;SharePoint Modus&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).  
  
  
##  <a name="bkmk_native_scenarios"></a> Upgrade im einheitlichen Modus und Migrationsszenarien  
 **Upgrade:** Direkte Upgrades für den einheitlichen Modus werden für jede der unterstützten Versionen, die oben in diesem Thema aufgeführt sind, gleich ausgeführt. Führen Sie den SQL Server-Installations-Assistenten oder eine Befehlszeileninstallation aus. Nach der Installation wird die Berichtsserver-Datenbank automatisch auf das neue Berichtsserver-Datenbankschema aktualisiert. Weitere Informationen finden Sie im Abschnitt [Direktes Upgrade](#bkmk_inplace_upgrade) in diesem Thema.  
  
 Der Upgradevorgang beginnt, wenn Sie eine vorhandene Berichtsserverinstanz für das Upgrade auswählen.  
  
1.  Falls sich die Berichtsserver-Datenbank auf einem Remotecomputer befindet und Sie nicht über Updateberechtigungen für diese Datenbank verfügen, fordert Setup Sie zur Angabe von Anmeldeinformationen für das Upgrade auf eine Remoteberichtsserver-Datenbank auf. Achten Sie darauf, Anmeldeinformationen bereitzustellen, die über **sysadmin** -Berechtigungen oder Berechtigungen für Datenbankupdates verfügen.  
  
2.  Setup führt eine Prüfung auf Bedingungen und Einstellungen durch, die das Upgrade verhindern, und liest Konfigurationseinstellungen ein. Beispiele hierfür sind benutzerdefinierte Erweiterungen, die auf dem Berichtsserver bereitgestellt werden. Wenn das Upgrade blockiert wird, müssen Sie entweder Ihre Installation so ändern, dass die Blockierung des Upgrades aufgehoben wird, oder eine Migration auf eine neue SQL Server Reporting Services-Instanz durchführen. Weitere Informationen finden Sie in der Dokumentation von Upgrade Advisor.  
  
3.  Wenn das Upgrade fortgesetzt werden kann, fordert das Setup Sie auf, mit dem Upgradevorgang fortzufahren.  
  
4.  Beim Setup werden neue Ordner für SQL Server Reporting Services-Programmdateien erstellt. Die Programmordner für eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Installation enthalten MSRS13.\<*instanzname*>.  
  
5.  Beim Setup werden die Programmdateien des SQL Server Reporting Services-Berichtsservers, die Konfigurationstools und die Befehlszeilenhilfsprogramme hinzugefügt, die zur Berichtsserverfunktion gehören.  
  
    1.  Programmdateien aus der vorherigen Version werden entfernt.  
  
    2.  Tools und Hilfsprogramme für die Berichtsserverkonfiguration, die auf die neue Version aktualisiert werden, sind beispielsweise das Konfigurationstool für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen Modus, die Befehlszeilenhilfsprogramme (z. B. RS.exe) und der Berichts-Generator.  
  
    3.  Andere Clienttools, wie etwa [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , stellen einen separaten Download dar und müssen in einem getrennten Upgrade aktualisiert werden. Weitere Informationen finden Sie unter [Herunterladen von SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).
  
    4.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ist in einem separaten Download erhältlich. Weitere Informationen finden Sie unter [SQL Server Data Tools in Visual Studio 2015](https://msdn.microsoft.com/mt186501).  
  
6.  Das Setup verwendet den Diensteintrag im Dienststeuerungs-Manager für den SQL Server Reporting Services-Berichtsserverdienst erneut. Dieser Diensteintrag enthält das Konto des Berichtserver-Windows-Diensts.  
  
7.  Setup reserviert neue URLs auf der Grundlage von vorhandenen virtuellen Verzeichniseinstellungen in IIS. Setup entfernt möglicherweise keine virtuellen Verzeichnisse in IIS, vergessen Sie also nicht, diese nach Abschluss des Upgrades manuell zu entfernen.  
  
8.  Beim Setup werden die Einstellungen in den Konfigurationsdateien zusammengeführt. Auf der Grundlage der Konfigurationsdateien aus der aktuellen Installation werden neue Einträge hinzugefügt. Veraltete Einträge werden nicht entfernt; sie werden jedoch nach Abschluss des Upgrades nicht mehr vom Berichtsserver gelesen. Beim Upgrade werden alte Protokolldateien, die veraltete Datei RSWebApplication.config oder Einstellungen für virtuelle Verzeichnisse in IIS nicht gelöscht. Beim Upgrade werden ältere Versionen von Berichts-Designer, Management Studio und andere Clienttools nicht entfernt. Wenn Sie diese Dateien und Tools nicht mehr benötigen, müssen Sie sie nach Abschluss des Upgrades entfernen.  
  
 **Migration:** Wenn Sie eine frühere Version einer Installation im einheitlichen Modus zu SQL Server Reporting Services migrieren, sind die Schritte für alle unterstützten Versionen, die oben in diesem Artikel aufgeführt sind, identisch. Weitere Informationen finden Sie unter [Migrieren einer Installation von Reporting Services &#40;Einheitlicher Modus&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md).  
  
  
##  <a name="bkmk_native_scaleout"></a> Aktualisieren einer Bereitstellung für horizontales Skalieren mit Reporting Services im einheitlichen Modus  
 Im Folgenden erhalten Sie eine Übersicht darüber, wie Sie eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bereitstellung im einheitlichen Modus aktualisieren, die horizontal auf mehr als einen Berichtsserver skaliert ist. Bei diesem Vorgang muss die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bereitstellung außer Betrieb gesetzt werden:  
  
1.  Sichern Sie die Berichtsserver-Datenbanken und die Verschlüsselungsschlüssel. Weitere Informationen finden Sie unter [Sicherungs- und Wiederherstellungsvorgänge für Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md) und [Hinzufügen und Entfernen von Verschlüsselungsschlüsseln für die Bereitstellung für horizontales Skalieren (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md).  
  
2.  Verwenden Sie den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager, und entfernen Sie alle Berichtsserver aus der horizontal skalierten Bereitstellung. Weitere Informationen finden Sie unter [Konfigurieren eines Berichtsservers im einheitlichen Modus für Bereitstellungen für horizontales Skalieren &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
3.  Aktualisieren Sie einen der Berichtsserver auf SQL Server Reporting Services.  
  
4.  Verwenden Sie den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager, um die Berichtsserver der Bereitstellung für horizontales Skalieren wieder hinzuzufügen. Weitere Informationen finden Sie unter [Konfigurieren eines Berichtsservers im einheitlichen Modus für Bereitstellungen für horizontales Skalieren &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
     Wiederholen Sie für jeden Server die Schritte für das Upgrade und das horizontale Skalieren.  
  
##  <a name="bkmk_sharePoint_scenarios"></a> Upgrade im SharePoint-Modus und Migrationsszenarien  
 In den folgenden Abschnitten werden die Probleme und grundlegenden Schritte beschrieben, die ausgeführt werden müssen, um von bestimmten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Versionen im SharePoint-Modus auf SQL Server Reporting Services im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-SharePoint-Modus zu aktualisieren oder eine Migration vorzunehmen.  
  
 Zum Upgrade einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bereitstellung im SharePoint-Modus sind zwei Installationskomponenten verfügbar.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
    > [!TIP]  
    >  Verwenden Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint-Cmdlet `Get-SPRSServiceApplicationServers` , um die Server in der SharePoint-Farm zu ermitteln, auf denen derzeit der gemeinsame SharePoint-Dienst für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ausgeführt wird und die deshalb ein Upgrade erfordern.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In für SharePoint-Produkte. Weitere Informationen finden Sie unter [Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  
  
 Ausführliche Schritte zum Migrieren einer Installation im SharePoint-Modus finden Sie unter [Migrate a Reporting Services Installation (SharePoint Mode) (Migrieren einer Reporting Services-Installation (SharePoint Modus))](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).  
  
> [!IMPORTANT]  
>  Bei einigen der folgenden Szenarien muss die SharePoint-Umgebung heruntergefahren werden, damit die verschiedenen Technologien aktualisiert werden können. Wenn in Ihrer Umgebung keine Ausfallzeiten tolerierbar sind, müssen Sie anstelle eines direkten Upgrades eine Migration ausführen.  
  
### <a name="includesssql14includessssql14-mdmd-to-sql-server-reporting-services"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] zu SQL Server Reporting Services  
 **Startumgebung:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP1, SharePoint 2010 oder SharePoint 2013.  
  
 **Endumgebung**: SQL Server Reporting Services, SharePoint 2013 oder SharePoint 2016.   
  
-   **SharePoint 2013/2016:** SharePoint 2013/2016 unterstützt keine direkten Upgrades von SharePoint 2010. Allerdings wird ein **Upgrade mit Anfügen der Datenbanken unterstützt**  .
  
     Wenn Sie über eine in SharePoint 2010 integrierte [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Installation verfügen, kann der SharePoint-Server nicht direkt aktualisiert werden. Sie haben jedoch die Möglichkeit, Inhaltsdatenbanken und Dienstanwendungsdatenbanken von der SharePoint 2010-Farm zu einer SharePoint 2013/2016-Farm zu migrieren.  
  
### <a name="includesssql11includessssql11-mdmd-to-sql-server-reporting-services"></a>[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] zu SQL Server Reporting Services  
 **Startumgebung:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] oder [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)], SharePoint 2010.  
  
 **Endumgebung**: SQL Server Reporting Services, SharePoint 2013 oder SharePoint 2016.   
  
-   **SharePoint 2013/2016:** SharePoint 2013/2016 unterstützt keine direkten Upgrades von SharePoint 2010. Allerdings wird ein **Upgrade mit Anfügen der Datenbanken unterstützt**  .
  
     Wenn Sie über eine in SharePoint 2010 integrierte [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Installation verfügen, kann der SharePoint-Server nicht direkt aktualisiert werden. Sie haben jedoch die Möglichkeit, Inhaltsdatenbanken und Dienstanwendungsdatenbanken von der SharePoint 2010-Farm zu einer SharePoint 2013/2016-Farm zu migrieren.  
  
### <a name="includesskilimanjaroincludessskilimanjaro-mdmd-to-sql-server-reporting-services"></a>[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] zu SQL Server Reporting Services  
 **Startumgebung:** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], SharePoint 2010.  
  
 **Endumgebung**: SQL Server Reporting Services, SharePoint 2013 oder SharePoint 2016.  
 
-   **SharePoint 2013/2016:** SharePoint 2013/2016 unterstützt keine direkten Upgrades von SharePoint 2010. Allerdings wird ein **Upgrade mit Anfügen der Datenbanken unterstützt**  .

    SharePoint muss zuerst migriert werden, bevor Sie Reporting Services aktualisieren können.
  
-   Installieren Sie die SQL Server Reporting Services-Version des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Add-Ins für SharePoint auf jedem Web-Front-End in der Farm. Sie können das Add-In mit dem SQL Server Reporting Services-Installations-Assistenten oder durch Herunterladen des Add-Ins installieren.  
  
-   Führen Sie die Installation von SQL Server Reporting Services aus, um das Upgrade des SharePoint-Modus für jeden „Berichtsserver“ auszuführen. Der SQL Server-Installations-Assistent installiert den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst und erstellt eine neue Dienstanwendung. 
  
  
##  <a name="bkmk_migration_considerations"></a> Migrationsüberlegungen  
 Beim Verschieben von Anwendungsdaten sind folgende Aspekte und Einschränkungen zu beachten:  
  
-   Der Schutz des Verschlüsselungsschlüssels schließt einen Hashcode ein, der die Computeridentität umfasst.  
  
-   Berichtsserver-Datenbanknamen sind fest und können auf dem anderen Computer nicht umbenannt werden.  
  
### <a name="encryption-key-considerations"></a>Überlegungen zu Verschlüsselungsschlüsseln  
 Sichern Sie die Verschlüsselungsschlüssel immer, bevor Sie eine Berichtsserver-Datenbank auf einen anderen Computer verschieben.  
  
 Wenn eine Berichtsserver-Installation auf einen anderen Computer verschoben wird, wird der Hashcode ungültig, der die Verschlüsselungsschlüssel schützt, die für die in der Berichtsserver-Datenbank gespeicherten vertraulichen Daten verwendet werden. Jede Berichtsserver-Instanz, die die Datenbank verwendet, verfügt über eine eigene Kopie des Verschlüsselungsschlüssels, der mit der Identität des auf dem aktuellen Computer definierten Dienstkontos verschlüsselt wird. Wenn Sie die Computer wechseln, kann der Dienst auch dann nicht mehr auf seinen Schlüssel zugreifen, wenn Sie auf dem neuen Computer den gleichen Kontonamen verwenden.  
  
 Sie müssen den zuvor gesicherten Schlüssel wiederherstellen, um auf dem neuen Computer wieder eine umkehrbare Verschlüsselung einzurichten. Der komplette in der Berichtsserver-Datenbank gespeicherte Schlüsselsatz besteht aus einem symmetrischen Schlüsselwert sowie Informationen zur Dienstidentität, mit denen der Zugriff auf den Schlüssel so beschränkt wird, dass diese nur von der Berichtsserverinstanz verwendet werden können, auf denen sie gespeichert wurden. Während der Schlüsselwiederherstellung ersetzt der Berichtsserver vorhandene Kopien des Schlüssels durch neue Versionen. Die neue Version umfasst Werte für die Computer- und Dienstidentität, die auf dem aktuellen Computer definiert wurden. Weitere Informationen finden Sie in folgenden Themen:  
  
-   SharePoint-Modus: Abschnitt „Schlüsselverwaltung“ im Artikel [Verwalten einer Reporting Services-SharePoint-Dienstanwendung](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
-   Einheitlicher Modus: [Sichern und Wiederherstellen von Reporting Services-Verschlüsselungsschlüsseln](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
  
  
### <a name="fixed-database-name"></a>Fester Datenbankname  
 Sie können die Berichtsserver-Datenbank nicht umbenennen. Die Identität der Datenbank wird bei der Datenbankerstellung in auf dem Berichtsserver gespeicherten Prozeduren aufgezeichnet. Wenn die primären oder temporären Berichtsserver-Datenbanken umbenannt werden, treten während der Ausführung der Prozeduren Fehler auf, sodass die Berichtsserver-Installation ungültig wird.  
  
 Wenn der Datenbankname der vorhandenen Installation für die neue Installation ungeeignet ist, sollten Sie eine neue Datenbank mit dem gewünschten Namen erstellen und die vorhandenen Anwendungsdaten mithilfe der in der folgenden Liste beschriebenen Verfahren laden:  
  
-   Schreiben Sie ein [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Skript, das SOAP-Methoden des Berichtsserver-Webdiensts aufruft, um Daten von einer Datenbank in eine andere Datenbank zu kopieren. Zum Ausführen des Skripts können Sie das Hilfsprogramm RS.exe verwenden. Weitere Informationen zu diesem Verfahren finden Sie unter [Skripterstellung und PowerShell mit Reporting Services](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md).  
  
-   Schreiben Sie Code, in dem der WMI-Anbieter aufgerufen wird, um Daten von einer Datenbank in eine andere Datenbank zu kopieren. Weitere Informationen zu diesem Verfahren finden Sie unter [Zugreifen auf den Reporting Services-WMI-Anbieter](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md).  
  
-   Wenn nur wenige Elemente vorliegen, können Sie die Berichte, Berichtsmodelle und freigegebenen Datenquellen vom Berichts-Designer, Modell-Designer und Berichts-Generator aus erneut auf dem neuen Berichtsserver veröffentlichen. Sie müssen Rollenzuweisungen, Abonnements, freigegebene Zeitpläne, Zeitpläne für Berichtmomentaufnahmen, benutzerdefinierte Eigenschaften, die Sie für Berichte und andere Elemente festlegen, Modellelementsicherheit und Eigenschaften, die Sie auf dem Berichtsserver festlegen, erneut erstellen. Die Protokolldaten über Berichtsverlauf und Berichtsausführung gehen verloren.  
  
  
##  <a name="bkmk_additional_resources"></a> Zusätzliche Ressourcen  
  
> [!NOTE]  
>  Weitere Informationen zum SharePoint-Upgrade mit Anfügen der Datenbanken finden Sie unter:  
  
-   [Übersicht über die Verfahren beim Upgrade auf SharePoint 2016](https://technet.microsoft.com/library/cc262483\(v=office.16\)).

-   [Übersicht über die Verfahren beim Upgrade auf SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256688).
  
-   [Vorbereitende Bereinigung vor einem Upgrade auf SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [Aktualisieren von Datenbanken von SharePoint 2013 auf SharePoint 2016](https://technet.microsoft.com/library/cc303436\(v=office.16\)).

-   [Aktualisieren von Datenbanken von SharePoint 2010 auf SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256690).  

## <a name="next-steps"></a>Nächste Schritte

[Aktualisieren von Berichten](../../reporting-services/install-windows/upgrade-reports.md)   
[Aktualisieren auf SQL Server 2016 mithilfe des Installations-Assistenten &#40;Setup&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
