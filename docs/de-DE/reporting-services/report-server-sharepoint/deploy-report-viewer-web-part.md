---
title: Bereitstellen des Webparts des Berichts-Viewers für SQL Server Reporting Services auf einer SharePoint-Website | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: df39b0b38363f7990609214abddeda8b5b6e54a9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-site"></a>Bereitstellen des Webparts des Berichts-Viewers für SQL Server Reporting Services auf einer SharePoint-Website

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Das Berichts-Viewer-Webpart ist ein benutzerdefiniertes Webpart, das verwendet werden kann, um SQL Server Reporting Services-Berichte (im einheitlichen Modus) auf Ihrer SharePoint-Website anzuzeigen. Sie können mit dem Webpart Berichte auf einem Berichtsserver anzeigen lassen, drucken und exportieren sowie in Berichten navigieren. Das Berichts-Viewer-Webpart ist mit den Berichtsdefinitionsdateien (RDL) verknüpft, die von einem SQL Server Reporting Services-Berichtsserver oder Power BI-Berichtsserver verarbeitet werden. Das Berichts-Viewer-Webpart kann nicht mit Power BI-Berichten verwendet werden, die in Power BI-Berichtsserver gehostet werden.

Verwenden Sie die folgenden Anweisungen, um zwei Lösungspakete manuell bereitzustellen, die einer SharePoint Server 2013- oder SharePoint Server 2016-Umgebung das Berichts-Viewer-Webpart hinzufügen. Die Bereitstellung der Lösung ist für die Konfiguration des Webparts erforderlich.

**Das Berichts-Viewer-Webpart ist ein eigenständiges Lösungspaket und ist nicht dem integrierten SharePoint-Modus für SQL Server Reporting Services verknüpft.**

## <a name="requirements"></a>Anforderungen

> [!IMPORTANT]
> Sie können dieses Webpart derzeit nicht installieren, wenn Sie bereits den integrierten SharePoint-Modus von Reporting Services konfiguriert haben.
>

**Unterstützte SharePoint Server-Versionen:**
* SharePoint Server 2016
* SharePoint Server 2013

**Unterstützte Reporting Services-Versionen:**  
* SQL Server 2008 Reporting Services und höher (einheitlicher Modus).
* Power BI-Berichtsserver

## <a name="download-the-report-viewer-web-part-solution-package"></a>Das Herunterladen des Projektmappenpakets des Berichts-Viewer-Webparts

Das Berichts-Viewer-Webpart ist im Microsoft Download Center verfügbar.

[Herunterladen des Projektmappenpakets des Berichts-Viewer-Webparts](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="deploy-the-farm-solution"></a>Bereitstellen der Farmlösung

In diesem Abschnitt erfahren Sie, wie Sie das Lösungspaket für Ihre SharePoint-Farm bereitstellen. Diese Aufgabe muss nur einmal ausgeführt werden.

1. Öffnen Sie auf einem SharePoint-Server die SharePoint-Verwaltungsshell unter Verwendung der Option **Als Administrator ausführen**.

2. Führen Sie [Add-SPSolution](https://technet.microsoft.com/library/ff607552(v=office.16).aspx) aus, um die Farmlösung hinzuzufügen.

    ```
    Add-SPSolution –LiteralPath "{path to file}\ReportViewerWebPart.wsp"
    ```

    Das Cmdlet gibt den Namen der Lösung, deren Lösungs-ID und "Deployed=False" zurück. Im nächsten Schritt wird die Lösung bereitgestellt.

3. Führen Sie das nächste [Install-SPSolution](https://technet.microsoft.com/library/ff607534(v=office.16).aspx)-Cmdlet aus, um die Farmlösung bereitzustellen.

    **SharePoint 2013**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -CompatibilityLevel "14,15" -GACDeployment -WebApplication {URL to web application}
    ```

    **SharePoint 2016**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -GACDeployment -WebApplication {URL to web application}
    ```

## <a name="activate-feature"></a>Aktivieren der Funktion

1. Klicken Sie auf Ihrer SharePoint-Website auf das **Zahnradsymbol** in der oberen linken Ecke und anschließend auf **Site Settings** (Websiteeinstellungen).

    ![Websiteeinstellungen über das Zahnradsymbol.](media/sharepoint-site-settings.png)

    Standardmäßig wird auf SharePoint-Webanwendungen über Port 80 zugegriffen. Dies bedeutet, dass Sie häufig auf eine SharePoint-Website zugreifen können, indem Sie *http://<computer name>* eingeben, um die Stammwebsitesammlung zu öffnen.

3. Klicken Sie unter **Websitesammlungsverwaltung** auf **Site collection features** (Websitesammlungsfeatures).

4. Scrollen Sie auf der Seite nach unten, bis Sie auf die **Berichts-Viewer-Webparts**-Funktion stoßen.

5. Wählen Sie **Aktivieren**aus.

    ![Aktivieren der Berichts-Viewer-Webparts-Funktion](media/web-part-activiate-feature.png)

6. Wiederholen Sie den Schritt für zusätzliche Websitesammlungen, indem Sie jede Website öffnen und auf „Websiteaktionen“ klicken.

Alternativ können Sie auch PowerShell verwenden, um diese Funktion für alle Websites zu aktivieren, die das [Enable-SPFeature](https://technet.microsoft.com/library/ff607803.aspx)-Cmdlet verwenden.

```
Get-SPWebApplication "<web application url>" | Get-SPSite -Limit ALL | 
        ForEach-Object {
            Write-Host "Enabling feature for $($_.URL)"
            Enable-SPFeature -identity "ReportViewerWebPart" -URL $_.URL -ErrorAction Continue
        }
```

## <a name="remove-the-solution"></a>Entfernen der Lösung

Obwohl in der SharePoint-Zentraladministration das Zurückziehen der Lösung möglich ist, müssen Sie die **ReportViewerWebPart.wsp**-Datei nur entfernen, wenn Sie systematisch ein Installations- oder ein Patchbereitstellungsproblem behandeln.

1. Klicken Sie in der SharePoint-Zentraladministration unter **Systemeinstellungen** auf **Farmlösungen verwalten**.

2. Klicken Sie auf **ReportViewerWebPart.wsp**.

3. Klicken Sie auf „Lösung zurückziehen“.

### <a name="remove-the-web-part-from-site-settings"></a>Entfernen des Webparts aus den Websiteeinstellungen

Durch das Zurückziehen der Lösung wird das Berichts-Viewer-Webpart nicht aus der Webpartliste auf Ihrer SharePoint-Website entfernt. Führen Sie folgende Schritte aus, um das Berichts-Viewer-Webpart zu entfernen.

1. Klicken Sie auf Ihrer SharePoint-Website auf das **Zahnradsymbol** in der oberen linken Ecke und anschließend auf **Site Settings** (Websiteeinstellungen).

    ![Websiteeinstellungen über das Zahnradsymbol.](media/sharepoint-site-settings.png)

    Standardmäßig wird auf SharePoint-Webanwendungen über Port 80 zugegriffen. Dies bedeutet, dass Sie häufig auf eine SharePoint-Website zugreifen können, indem Sie *http://<computer name>* eingeben, um die Stammwebsitesammlung zu öffnen.

2. Klicken Sie unter **Web-Designer-Kataloge** auf **Webparts**.

3. Klicken Sie auf das **Symbol „Bearbeiten“** neben **ReportViewerNativeMode.dwp**. Möglicherweise ist diese nicht auf der ersten Seite der Ergebnisse aufgelistet.

4. Klicken Sie auf **Symbol bearbeiten**.

    ![Bearbeiten und Löschen des Berichts-Viewer-Webparts im einheitlichen Modus](media/report-viewer-native-mode-edit-delete.png)

Sie können versuchen, das Webpart mithilfe von PowerShell zu löschen. Es gibt dafür allerdings keinen direkten Befehl. Ein Beispiel für ein Skript finden Sie unter [How to delete web parts from the web part Gallery (Löschen von Webparts aus dem Webpartkatalog)](https://gallery.technet.microsoft.com/office/How-to-delete-Web-Parts-1132701f).

## <a name="supported-languages"></a>Unterstützte Sprachen

Für das Webpart werden die folgenden Sprachen unterstützt:

* Englisch (EN)
* Deutsch (DE)
* Spanisch (ES)
* Französisch (FR)
* Italienisch (IT)
* Japanisch (JA)
* Koreanisch (KO)
* Portugiesisch (PT)
* Russisch (RU)
* Chinesisch (vereinfacht: zh-HANS und zh-CHS)
* Chinesisch (traditionell: zh-HANT und zh-CHT)

## <a name="troubleshoot"></a>Problembehandlung

* Fehler beim Deinstallieren von SSRS, wenn Sie den integrierten SharePoint-Modus konfiguriert haben:

    Install-SPRSService : [A] Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService cannot be cast to [B]Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService. ([A] Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService kann nicht in [B] Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService umgewandelt werden.) Type A originates from 'Microsoft.ReportingServices.SharePoint.SharedService,Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' in the context 'Default' at location 'C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll'. (Typ A stammt von 'Microsoft.ReportingServices.SharePoint.SharedService,Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' im Kontext 'Default' am Speicherort 'C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll'.) Type B originates from 'Microsoft.ReportingServices.SharePoint.SharedService,Version=12.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' in the context 'Default' at location 'C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll'. (Typ A stammt von 'Microsoft.ReportingServices.SharePoint.SharedService,Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' im Kontext 'Default' am Speicherort 'C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll'.)
    
    Lösung:
    1. Entfernen des Berichts-Viewer-Webparts
    2. Deinstallieren von SSRS
    3. Neuinstallieren des Berichts-Viewer-Webparts

* Fehler beim Upgrade von SharePoint, wenn Sie den integrierten SharePoint-Modus konfiguriert haben:

    Could not load file or assembly 'Microsoft.ReportingServices.Alerting.ServiceContract, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. (Die Datei oder Assembly 'Microsoft.ReportingServices.Alerting.ServiceContract, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' oder eine Abhängigkeit davon wurde nicht gefunden.) Die angegebene Datei wurde nicht gefunden. 00000000-0000-0000-0000-000000000000
    
    Lösung:
    1. Entfernen des Berichts-Viewer-Webparts
    2. Deinstallieren von SSRS
    3. Neuinstallieren des Berichts-Viewer-Webparts

## <a name="next-steps"></a>Nächste Schritte

Wenn das Berichts-Viewer-Webpart bereitgestellt und aktiviert wurde, können Sie das Webpart zu eine SharePoint-Seite hinzufügen. Weitere Informationen finden Sie unter [Add Report Viewer web part to a SharePoint page (Hinzufügen des Berichts-Viewer-Webparts zu einer SharePoint-Website)](add-report-viewer-web-part-to-page.md).

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
