---
title: Migrieren einer Installation von Reporting Services (SharePoint-Modus) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 61290949-690a-4e19-b078-57c99b6b30fa
caps.latest.revision: "23"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 515fb60031f75d0c3743628a345e415770a731fe
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="migrate-a-reporting-services-installation-sharepoint-mode"></a>Migrieren einer Installation von Reporting Services (SharePoint-Modus)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  Dieses Thema bietet eine Übersicht über die Schritte, die erforderlich sind, um eine Bereitstellung von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus zwischen SharePoint-Umgebungen zu migrieren. Die jeweiligen Schritte können sich abhängig von der Version unterscheiden, von der aus Sie migrieren. Weitere Informationen zu Upgrade- und Migrationsszenarien für den SharePoint-Modus finden Sie unter [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md). Wenn Sie nur die Berichtselemente von einem Server auf einen anderen kopieren möchten, finden Sie entsprechende Informationen unter [Reporting Services-Beispielskript für „rs.exe“ zum Kopieren von Inhalten zwischen Berichtsservern](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
 Informationen zum Migrieren einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bereitstellung im einheitlichen Modus finden Sie unter [Migrieren einer Reporting Services-Installation &#40;einheitlicher Modus&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md).  
  
 Ein häufiger Grund für eine Migration liegt vor, wenn Sie Ihre SharePoint 2010-Bereitstellung auf SharePoint 2013/2016 aktualisieren möchten. SharePoint 2013/2016 unterstützt keine direkten Upgrades von SharePoint 2010. Daher müssen Sie die Schritte für ein **Upgrade mit Anfügen der Datenbanken** oder eine reine Migration von Inhalten ausführen.  
  
 Weitere Informationen zum Aktualisieren von SharePoint 2013/2016 finden Sie unter:  

-   [Übersicht über die Verfahren beim Upgrade auf SharePoint 2016](https://technet.microsoft.com/library/cc262483\(v=office.16\)).

-   [Übersicht über die Verfahren beim Upgrade auf SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256688).
  
-   [Vorbereitende Bereinigung vor einem Upgrade auf SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [Aktualisieren von Datenbanken von SharePoint 2013 auf SharePoint 2016](https://technet.microsoft.com/library/cc303436\(v=office.16\)).

-   [Aktualisieren von Datenbanken von SharePoint 2010 auf SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256690).
  
-   [Verschieben von Inhaltsdatenbanken in SharePoint 2016](https://technet.microsoft.com/library/cc262792\(v=office.16\).aspx).

-   [Verschieben von Inhaltsdatenbanken in SharePoint 2013](http://technet.microsoft.com/library/cc262792.aspx).
  
##  <a name="bkmk_prior_versions"></a> Migrieren von Reporting Services-Versionen im SharePoint-Modus vor SQL Server 2012  
 Die Architektur von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus wurde in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]geändert. Die Änderungen betreffen auch das Datenbankschema der Dienstanwendung. Wenn Sie von einer Version vor [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] auf [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] im SharePoint-Modus migrieren möchten, erstellen Sie zuerst die neue SharePoint-Umgebung, indem Sie SharePoint und SQL Server 2016 Reporting Services im SharePoint-Modus installieren. Weitere Informationen finden Sie unter [Installieren des SharePoint-Modus von Reporting Services](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
 Sobald die neue SharePoint-Umgebung ausgeführt wird, können Sie zwischen der reinen Migration von Inhalten oder einer vollständigen Migration auf Datenbankebene (einschließlich Inhaltsdatenbanken) auswählen.  
  
###  <a name="bkmk_content_only_migration"></a> Reine Inhaltsmigration  
 **Nur Reporting Services-Inhalt migrieren:** Wenn Sie den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Inhalt in eine neue Farm kopieren möchten, benötigen Sie Tools wie **rs.exe** , um den Inhalt in die neue SharePoint-Installation zu kopieren. Weitere Informationen zur reinen Migration von Inhalten finden Sie unter:  
  
-   **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] RSS-Skripts:** Die Skripts können Inhalte und Ressourcen zwischen Berichtsservern im einheitlichen Modus und im SharePoint-Modus migrieren. Weitere Informationen finden Sie unter [Reporting Services-Beispielskript für „rs.exe“ zum Kopieren von Inhalten zwischen Berichtsservern](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md) und [Reporting Services-Skript „RS.exe“ zum Migrieren von Inhalten von einem Berichtsserver zu einem anderen](http://azuresql.codeplex.com/releases/view/115207).  
  
-   **Reporting Services-Migrationstool:** Das Tool kann Ihre Berichtselemente von einem Server im einheitlichen Modus zu einem Server im SharePoint-Modus kopieren. Weitere Informationen finden Sie unter [Reporting Services-Migrationstool](http://www.microsoft.com/download/details.aspx?id=29560) (http://www.microsoft.com/download/details.aspx?id=29560).  
  
###  <a name="bkmk_full_migration"></a> Vollständige Migration  
 **Vollständige Migration:** Wenn Sie SharePoint-Inhaltsdatenbanken zusammen mit den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Katalogdatenbanken zu einer neuen Farm migrieren, können Sie eine Reihe von Sicherungs- und Wiederherstellungsoptionen verwenden, die in diesem Thema zusammengefasst sind. In einigen Fällen müssen Sie in der Wiederherstellungsphase ein anderes Tool verwenden als in der Sicherungsphase. Beispielsweise können Sie den Konfigurations-Manager für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwenden, um Verschlüsselungsschlüssel einer Vorgängerversion von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] zu sichern. In diesem Fall müssen Sie jedoch die SharePoint-Zentraladministration oder PowerShell verwenden, um die Verschlüsselungsschlüssel in einer SQL Server 2016 Reporting Services-Installation im SharePoint-Modus wiederherzustellen.  
  
####  <a name="bkmk_databases"></a> Datenbanken, die in der abgeschlossenen Migration angezeigt werden  
 In der folgenden Tabelle sind die SQL Server-Datenbanken von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] beschrieben, die nach der erfolgreichen Migration der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Installation im SharePoint-Modus zur Verfügung stehen:  
  
|Datenbank|Beispielname||  
|--------------|------------------|-|  
|Katalogdatenbank|ReportingService_[GUID der Dienstanwendung] **(\*)**|Wird vom Benutzer migriert.|  
|Temporäre Datenbank|ReportingService_[GUID der Dienstanwendung]TempDB **(\*)**|Wird vom Benutzer migriert.|  
|Warnungsdatenbank|ReportingService_[GUID der Dienstanwendung]_Alerting|Wird zusammen mit einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung erstellt.|  
  
 **(\*)** Die in der Tabelle angezeigten Beispielnamen folgen der Namenskonvention, die von SSRS beim Erstellen einer neuen SSRS-Dienstanwendung verwendet wird. Wenn Sie von einem anderen Server migrieren, verfügen Ihr Katalog und die tempDBs über die entsprechenden Namen der ursprünglichen Installation.  
  
####  <a name="bkmk_backup_operations"></a> Sicherungsvorgänge  
 In diesem Abschnitt werden die zu migrierenden Informationstypen und die Tools bzw. die Vorgehensweise zum Abschließen des Sicherungsvorgangs beschrieben.  
  
 ![Einfaches Diagramm der SSRS SharePoint-Migration](../../reporting-services/install-windows/media/rs-sharepoint-migration.gif "Basic diagram of SSRS SharePoint Migration")  
  
||Objekte|Methode|Hinweise|  
|-|-------------|------------|-----------|  
|**1**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Verschlüsselungsschlüssel.|**Rskeymgmt.exe** oder [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager. Weitere Informationen finden Sie unter [Sichern und Wiederherstellen von Reporting Services-Verschlüsselungsschlüsseln](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).|Die angegebenen Tools können für die Sicherung verwendet werden, für die Wiederherstellung werden jedoch die Verwaltungsseiten für die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung oder PowerShell verwendet.|  
|**2**|SharePoint-Inhaltsdatenbanken.||Sichern Sie die Datenbank, und trennen Sie sie.<br /><br /> Informationen finden Sie im Abschnitt „Upgrade mit Anfügen der Datenbanken“ in [Bestimmen der Upgrademethode (SharePoint Server 2010) (http://technet.microsoft.com/library/cc263447.aspx)](http://technet.microsoft.com/library/cc263447.aspx).|  
|**3**|SQL Server-Datenbank, die der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Katalogdatenbank entspricht.|Sichern und Wiederherstellen von SQL Server-Datenbanken<br /><br /> oder<br /><br /> Trennen und erneutes Anfügen der SQL Server-Datenbank||  
|**4**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationsdateien|Einfacher Dateikopiervorgang|Wenn Sie Änderungen an der Datei vorgenommen haben, müssen Sie nur „rsreportserver.config“ kopieren. Beispiel für den Standardspeicherort von Dateien: C:\Programme\Gemeinsame Dateien\Microsoft Shared\Web-Server Extensions\15\WebServices\Reporting\\*:<br /><br /> <br /><br /> Rsreportserver.config<br /><br /> Rssvrpolicy.config<br /><br /> "Web.config" für die Berichtsserver-ASP.NET-Anwendung.<br /><br /> "Machine.config" für ASP.NET.|  
  
####  <a name="bkmk_restore_operations"></a> Wiederherstellungsvorgänge  
 In diesem Abschnitt werden die zu migrierenden Informationstypen und die Tools bzw. die Vorgehensweise zum Abschließen des Wiederherstellungsvorgangs beschrieben. Die zur Wiederherstellung verwendeten Tools können sich von den Tools unterscheiden, die Sie für die Sicherung verwendet haben.  
  
 Bevor Sie die Wiederherstellungsschritte ausführen, müssen Sie die neue SharePoint-Farm und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint Modus installieren und konfigurieren. Weitere Informationen zur einfachen Installation des SharePoint-Modus von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] finden Sie unter [Installieren des SharePoint-Modus von Reporting Services](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
||Objekte|Methode|Hinweise|  
|-|-------------|------------|-----------|  
|**1**|Stellen Sie SharePoint-Inhaltsdatenbanken in der neuen Farm wieder her.|SharePoint-Upgrade mit Anfügen der Datenbanken.|Grundlegende Schritte:<br /><br /> 1) Stellen Sie die Datenbank auf dem neuen Server wieder her.<br /><br /> 2) Fügen Sie die Inhaltsdatenbank an eine Webanwendung an, indem Sie die URL angeben.<br /><br /> 3) "Get-SPWebapplication" listet alle Webanwendungen und die URLs auf.<br /><br /> <br /><br /> Weitere Informationen finden Sie im Abschnitt „Upgrade mit Anfügen der Datenbanken“ in [Bestimmen der Upgrademethode (SharePoint Server 2010) (http://technet.microsoft.com/en-us/library/cc263447.aspx)](http://technet.microsoft.com/library/cc263447.aspx)und [Anfügen von Datenbanken und Durchführen eines Upgrades auf SharePoint Server 2010 (http://technet.microsoft.com/en-us/library/cc263299.aspx)](http://technet.microsoft.com/library/cc263299.aspx).|  
|**2**|Stellen Sie die SQL Server-Datenbank wieder her, die der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Katalogdatenbank (ReportServer) entspricht.|Sichern und Wiederherstellen von SQL-Datenbanken<br /><br /> **oder**<br /><br /> Anfügen und Trennen von SQL Server-Datenbanken|Wenn die Datenbank erstmalig verwendet wird, aktualisiert [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] das Datenbankschema nach Bedarf, damit es in der SQL Server 2016-Umgebung funktioniert.|  
|**3**|Erstellen Sie eine neue [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung.|Erstellen Sie eine neue [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung.|Wenn Sie die neue Dienstanwendung erstellen, konfigurieren Sie sie für die Verwendung der kopierten Berichtsserver-Datenbank.<br /><br /> Weitere Informationen zur Verwendung der SharePoint-Zentraladministration finden Sie im Abschnitt „Schritt 3: Erstellen einer neuen Reporting Services-Dienstanwendung“ unter [Installieren des ersten Berichtsservers im SharePoint-Modus](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md).<br /><br /> Beispiele für die Verwendung von PowerShell finden Sie im Abschnitt "Erstellen einer Reporting Services-Dienstanwendung mit PowerShell" unter [Reporting Services SharePoint Service and Service Applications](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).|  
|**4**|Stellen Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationsdateien wieder her.|Einfacher Dateikopiervorgang|Beispiel für den Standardspeicherort von Dateien: C:\Programme\Gemeinsame Dateien\Microsoft Shared\Web-Server Extensions\15\WebServices\Reporting|  
|||||  
|**5**|Stellen Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Verschlüsselungsschlüssel wieder her.|Stellen Sie die Hauptsicherungsdatei mithilfe der Seite "SystemSettings" der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung wieder her.<br /><br /> **oder**<br /><br /> PowerShell|Weitere Informationen finden Sie im Abschnitt „Schlüsselverwaltung“ des Themas [Verwalten einer Reporting Services-SharePoint-Dienstanwendung](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)|   
  
##  <a name="bkmk_migrate_from_ctp"></a> Migrieren von einer SQL Server 2012- oder SQL Server 2014-Bereitstellung  
 In einer aus mehreren Servern bestehenden Farm befinden sich die Inhalts- und die Katalogdatenbank wahrscheinlich auf unterschiedlichen Computern. In diesem Fall müssen Sie der SharePoint-Farm nur einen neuen Server mit installiertem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst hinzufügen und den alten Server entfernen. Das Kopieren der Datenbanken ist nicht erforderlich.  
  
### <a name="backup-operations"></a>Sicherungsvorgänge  
  
1.  Sichern Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Verschlüsselungsschlüssel.  
  
2.  Sichern Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung in der SharePoint-Zentraladministration (oder verwenden Sie PowerShell). Auf diese Weise sichern Sie auch die Datenbanken der Dienstanwendung in SharePoint. Weitere Informationen finden Sie im Artikel  [Sichern und Wiederherstellen von Reporting Services-SharePoint-Dienstanwendungen](../../reporting-services/report-server-sharepoint/backup-and-restore-reporting-services-sharepoint-service-applications.md).  
  
3.  Wenn Sie über ein Konto für die unbeaufsichtigte Ausführung (Unattended Execution Account, UEA) verfügen und die Windows-Authentifizierung verwenden, sollten Sie sich die Anmeldeinformationen für den Wiederherstellungsvorgang notieren.  
  
4.  Weitere Informationen finden Sie unter [Sichern von Dienstanwendungen in SharePoint 2013](http://technet.microsoft.com/library/ee428318.aspx).  
  
### <a name="restore-operations"></a>Wiederherstellungsvorgänge  
  
1.  Stellen Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung mithilfe der SharePoint-Zentraladministration wieder her. Alternativ können Sie PowerShell verwenden.  
  
2.  Stellen Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Verschlüsselungsschlüssel wieder her.  
  
     Weitere Informationen finden Sie im Abschnitt „Schlüsselverwaltung“ des Themas [Verwalten einer Reporting Services-SharePoint-Dienstanwendung](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
3.  Konfigurieren Sie die Anmeldeinformationen für UEA und Windows in der Dienstanwendung.  
  
4.  Weitere Informationen finden Sie unter [Wiederherstellen von Dienstanwendungen in SharePoint 2013](http://technet.microsoft.com/library/ee428305.aspx).  
  
##  <a name="bkmk_additional_resources"></a> Zusätzliche Ressourcen  
  
-   [Erste Schritte beim Upgrade auf SharePoint 2013 (http://technet.microsoft.com/en-us/library/ee833948.aspx)](http://technet.microsoft.com/library/ee833948.aspx).  
  
-   [Übersicht über die Verfahren beim Upgrade auf SharePoint 2013 (http://technet.microsoft.com/en-us/library/cc262483.aspx)](http://technet.microsoft.com/library/cc262483.aspx).  

## <a name="next-steps"></a>Nächste Schritte

[Aktualisieren und Migrieren von Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Migrieren einer Installation von Reporting Services](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
