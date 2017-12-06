---
title: "Hinzufügen von Reporting Services-Inhaltstypen zu einer SharePoint-Bibliothek | Microsoft-Dokumentation"
ms.custom: 
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server-sharepoint
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ac9136c8-9ef4-484c-8e9d-05008a186db5
caps.latest.revision: "7"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: a9074f9125c1e1e67717cd1f5bb70710dbb6dff6
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="add-reporting-services-content-types-to-a-sharepoint-library"></a>Hinzufügen von Reporting Services-Inhaltstypen zu einer SharePoint-Bibliothek

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Für SharePoint werden vordefinierte Inhaltstypen bereitgestellt, die zum Verwalten freigegebener Datenquellendateien (RSDS), Berichtsmodelldateien (SMDL) und Berichtsgenerator-Berichtsdefinitionsdateien (RDL) verwendet werden können. Wenn einer Bibliothek ein Inhaltstyp ( **Berichts-Generator-Bericht**, **Berichtsmodell**und **Berichtsdatenquelle** ) hinzugefügt wird, wird der Befehl **Neu** aktiviert, sodass Sie neue Dokumente des betreffenden Typs erstellen können.

> [!NOTE]
> Die Integration von Reporting Services in SharePoint ist nach SQL Server 2016 nicht mehr möglich.

 Wenn Sie einer Bibliothek Inhaltstypen hinzufügen möchten, müssen Sie Websiteadministrator sein oder über die Berechtigungsstufe "Vollzugriff" verfügen.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Inhaltstypen sowie die Verwaltung dieser Inhaltstypen werden in allen Dokumentbibliotheken für vorhandene Websitesammlungen, die von folgenden Websitevorlagentypen erstellt wurden, automatisch aktiviert:  
  
-   **Business Intelligence Center**  
  
 Für Websites, die nach der Integration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] erstellt wurden, sind die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Inhaltstypen nicht aktiviert.  
  
> [!TIP]  
>  Wenn Sie zuvor **keine** Inhaltstypen für eine Bibliothek konfiguriert haben, aktivieren Sie zunächst die Verwaltung von Inhaltstypen und dann die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Inhaltstypen. Siehe die Verfahren zum Aktivieren der Inhaltstypverwaltung in einer einzelnen Dokumentbibliothek.  
  
 **Kurzvideo:** [(SSRS) Enabling Content Types in SharePoint2010.wmv](http://www.youtube.com/watch?v=yqhm3DrtT1w) ((SSRS) Aktivieren von Inhaltstypen in Sharepoint 2010; http://www.youtube.com/watch?v=yqhm3DrtT1w).  
  
 **In diesem Thema:**  
  
-   [Aktivieren von Inhaltstypen in allen Dokumentbibliotheken eines vorhandenen Business Intelligence Centers](#bkmk_enable_all)  
  
-   [So aktivieren Sie die Inhaltstypverwaltung für eine einzelne Dokumentbibliothek (SharePoint 2013)](#bkmk_enable_content_management)  
  
-   [So fügen Sie Reporting Services-Inhaltstypen hinzu (SharePoint 2013)](#bkmk_add_single)  
  
-   [So aktivieren Sie die Inhaltstypverwaltung für eine einzelne Dokumentbibliothek (SharePoint 2010)](#bkmk_enable_content_management_2010)  
  
-   [So fügen Sie Berichtsserver-Inhaltstypen hinzu (SharePoint 2010)](#bkmk_add_single_2010)  
  
-   [So aktivieren Sie Inhaltstypen und die Inhaltsverwaltung für mehrere BI-Websites](#bkmk_enable_multiple_sites)  
  
##  <a name="bkmk_enable_all"></a> Aktivieren von Inhaltstypen in allen Dokumentbibliotheken eines vorhandenen Business Intelligence Centers  
  
1.  Um Inhaltstypen sowie die Inhaltsverwaltung in allen Dokumentbibliotheken einer vorhandenen **Business Intelligence Center** -Website zu aktivieren, können Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Integrationsfunktion aktivieren/deaktivieren.  
  
2.  Wechseln Sie zu **Siteeinstellungen**.  
  
    -   Klicken Sie in SharePoint 2013 auf das **Einstellungssymbol**. ![SharePoint-Einstellungen](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint Settings")  
  
    -   Klicken Sie in SharePoint 2010 auf **Websiteaktionen**und auf **Siteeinstellungen**.  
  
3.  Klicken Sie auf **Websitesammlungsfeatures**.  
  
4.  Suchen Sie die **Berichtsserver-Integrationsfunktion** , und klicken Sie auf **Deaktivieren**.  
  
     ![rs_berichtsserver_integration_aktiviert](../../reporting-services/report-server-sharepoint/media/rs-reportserver-integration-active.gif "rs_reportserver_integration_active")  
  
5.  Aktualisieren Sie den Browser, und klicken Sie unter **Berichtsserver-Integrationsfunktion** auf **Aktivieren**.  
  
     ![rs_berichtsserver_integration_deaktiviert](../../reporting-services/report-server-sharepoint/media/rs-reportserver-integration-deactive.gif "rs_reportserver_integration_deactive")  
  
##  <a name="bkmk_enable_content_management"></a> So aktivieren Sie die Inhaltstypverwaltung für eine einzelne Dokumentbibliothek (SharePoint 2013)  
  
1.  Öffnen Sie die Bibliothek, für die Sie mehrere Inhaltstypen aktivieren möchten.  
  
2.  Klicken Sie im Menüband auf **Bibliothek** .  
  
     ![rs_SharePoint2013_BibliothekMenüband](../../reporting-services/report-server-sharepoint/media/rs-sharepoint2013-libraryribbon.gif "rs_SharePoint2013_LibraryRibbon")  
  
3.  Klicken Sie im Menüband **Bibliothek** auf **Bibliothekeinstellungen**. Falls **Bibliothekseinstellungen** nicht angezeigt wird oder die Schaltfläche deaktiviert ist, sind Sie nicht berechtigt, Bibliothekseinstellungen sowie Inhaltstypen zu konfigurieren.  
  
     ![rs_SharePoint2013_BibliothekEinstellungen](../../reporting-services/report-server-sharepoint/media/rs-sharepoint2013-librarysettings.gif "rs_SharePoint2013_LibrarySettings")  
  
4.  Klicken Sie im Abschnitt **Allgemeine Einstellungen** auf **Erweiterte Einstellungen**.  
  
     ![rs_SharePoint2013_BibliothekEinstellungen_ErweiterteEinstellungen](../../reporting-services/report-server-sharepoint/media/rs-sharepoint2013-librarysettings-advancedsettings.gif "rs_SharePoint2013_LibrarySettings_AdvancedSettings")  
  
5.  Wählen Sie im Abschnitt **Inhaltstypen** die Option **Ja** aus, um die Verwaltung von Inhaltstypen zuzulassen.  
  
6.  Klicken Sie auf **OK**.  
  
##  <a name="bkmk_add_single"></a> So fügen Sie Reporting Services-Inhaltstypen hinzu (SharePoint 2013)  
  
1.  Öffnen Sie die Bibliothek, für die Sie Reporting Services-Inhaltstypen hinzufügen möchten.  
  
2.  Klicken Sie im Menüband auf **Bibliothek**.  
  
3.  Klicken Sie auf **Bibliothekeinstellungen**.  
  
4.  Klicken Sie unter **Inhaltstypen**auf **Aus vorhandenen Websiteinhaltstypen hinzufügen**.  
  
5.  Wählen Sie unter **Websiteinhaltstypen auswählen aus**die Option **SQL Server Reporting Services-Inhaltstypen**aus.  
  
6.  Klicken Sie in der Liste **Verfügbare Websiteinhaltstypen** auf **Berichts-Generator**, und klicken Sie dann auf **Hinzufügen** , um den ausgewählten Inhaltstyp in die Liste **Hinzuzufügende Inhaltstypen** zu verschieben.  
  
7.  Wiederholen Sie den vorherigen Schritt, um die Inhaltstypen **Berichtsmodell** und **Berichtsdatenquelle** hinzuzufügen.  
  
8.  Nachdem Sie alle gewünschten Inhaltstypen hinzugefügt haben, klicken Sie auf **OK**.  
  
    > [!NOTE]  
    >  Die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Inhaltstypgruppe **SQL Server Reporting Services-Inhaltstypen** wird unter folgenden Bedingungen auf der Seite **Inhaltstypen hinzufügen** nicht angezeigt:  
  
    -   Das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In für SharePoint-Produkte wurde nicht installiert. Weitere Informationen finden Sie unter [Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md). Das Thema enthält Informationen zum Installieren des Add-Ins und es wird Schritt für Schritt erläutert, wie Sie eine Nur-Datei-Installation des Add-Ins ausführen können, um Probleme zu umgehen.  
  
    -   Das Add-In wird installiert, aber die **Funktion für die Berichtsserverintegration** für die Websitesammlung ist nicht aktiv. Prüfen Sie die Websitesammlungsfunktion unter **Siteeinstellungen**.  
  
    -   Der Bibliothek wurden bereits sämtliche [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Inhaltstypen hinzugefügt. Wenn alle Inhaltstypen einer Bibliothek angehören, wird die Gruppe von der Seite **Inhaltstypen hinzufügen** entfernt. Nachdem mindestens ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Inhaltstyp gelöscht wurde, wird die Gruppe **SQL Server Reporting Services-Inhaltstypen** auf der Seite **Inhaltstypen hinzufügen** angezeigt.  
  
##  <a name="bkmk_enable_content_management_2010"></a> So aktivieren Sie die Inhaltstypverwaltung für eine einzelne Dokumentbibliothek (SharePoint 2010)  
  
1.  Öffnen Sie die Bibliothek, für die Sie mehrere Inhaltstypen aktivieren möchten. Auf der Menüleiste der Bibliothek sollten die folgenden Menüs angezeigt werden: **Neu**, **Upload**, **Aktionen**und **Einstellungen**. Falls **Einstellungen**nicht angezeigt wird, sind Sie nicht berechtigt, Inhaltstypen hinzuzufügen.  
  
2.  Klicken Sie im Menüband **Bibliothekstools** auf **Bibliothek**.  
  
     ![rs_SharePoint2010_BibliothekMenüband](../../reporting-services/report-server-sharepoint/media/rs-sharepoint2010-libraryribbon.gif "rs_SharePoint2010_LibraryRibbon")  
  
3.  Klicken Sie in der Menübandgruppe **Einstellungen** auf **Bibliothekseinstellungen**.  
  
4.  Klicken Sie unter **Allgemeine Einstellungen**auf **Erweiterte Einstellungen**.  
  
5.  Wählen Sie im Abschnitt **Inhaltstypen** die Option **Ja** aus, um die Verwaltung von Inhaltstypen zuzulassen.  
  
6.  Klicken Sie auf **OK**.  
  
##  <a name="bkmk_add_single_2010"></a> So fügen Sie Berichtsserver-Inhaltstypen hinzu (SharePoint 2010)  
  
1.  Öffnen Sie die Bibliothek, für die Sie Reporting Services-Inhaltstypen hinzufügen möchten.  
  
2.  Klicken Sie auf den Registerkarten des Menübands **Bibliothekstools** auf die Registerkarte **Bibliothek**.  
  
3.  Klicken Sie in der Menübandgruppe **Einstellungen** auf **Bibliothekseinstellungen**.  
  
4.  Klicken Sie unter **Inhaltstypen**auf **Aus vorhandenen Websiteinhaltstypen hinzufügen**.  
  
5.  Klicken Sie im Abschnitt **Inhaltstypen auswählen** in der Liste **Websiteinhaltstypen auswählen aus**auf den Pfeil, um **SQL Server Reporting Services-Inhaltstypen**auszuwählen.  
  
6.  Klicken Sie in der Liste **Verfügbare Websiteinhaltstypen** auf **Berichts-Generator**, und klicken Sie dann auf **Hinzufügen** , um den ausgewählten Inhaltstyp in die Liste **Hinzuzufügende Inhaltstypen** zu verschieben.  
  
7.  Wiederholen Sie den vorherigen Schritt, um die Inhaltstypen **Berichtsmodell** und **Berichtsdatenquelle** hinzuzufügen.  
  
8.  Nachdem Sie alle gewünschten Inhaltstypen hinzugefügt haben, klicken Sie auf **OK**.  
  
##  <a name="bkmk_enable_multiple_sites"></a> So aktivieren Sie Inhaltstypen und die Inhaltsverwaltung für mehrere BI-Websites  
  
1.  Bei Berichtsservern unter SQL Server Reporting Services 2008 und 2008 R2 können Inhaltstypen sowie die Inhaltsverwaltung für mehrere Business Intelligence Center-Websites aktiviert werden:  
  
2.  Klicken Sie in der SharePoint-Zentraladministration auf **Allgemeine Anwendungseinstellungen**. Klicken Sie im Abschnitt **SQL Server Reporting Services (2008 und 2008 R2)** auf **Reporting Services-Integration**.  
  
     ![rs_allgemeine_app_einstellungen](../../reporting-services/report-server-sharepoint/media/rs-general-app-settings.gif "rs_general_app_settings")  
  
3.  Klicken Sie auf **Funktion in allen vorhandenen Websitesammlungen aktivieren**.  
  
     ![rs_allgemeine_app_einstellungen_alte_integrationen](../../reporting-services/report-server-sharepoint/media/rs-general-app-settings-old-integrations.gif "rs_general_app_settings_old_integrations")  
  
4.  Klicken Sie auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
 [Referenz zu SharePoint-Website- und Listenberechtigungen für Berichtsserverelemente](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)   
 [Start Report Builder (Starten des Berichts-Generators.)](../../reporting-services/report-builder/start-report-builder.md)  
  
  
