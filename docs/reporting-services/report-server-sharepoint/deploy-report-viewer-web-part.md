---
title: Das SQL Server Reporting Services Berichts-Viewer-Webpart auf einer SharePoint-Website bereitstellen | Microsoft Docs
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: a75ad193204e17e1d053aa4e00adba5f551d684b
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---

# <a name="deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-site"></a>Bereitstellen Sie das SQL Server Reporting Services Berichts-Viewer-Webpart auf einer SharePoint-Website

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Der Berichts-Viewer-Webpart ist ein benutzerdefiniertes Webpart, das verwendet werden kann, um Berichte von SQL Server Reporting Services (einheitlicher Modus) innerhalb der SharePoint-Website anzuzeigen. Sie können das Webpart verwenden, um anzuzeigen, navigieren, Drucken und Exportieren von Berichten auf einem Berichtsserver. Der Berichts-Viewer-Webpart ist Berichtsdefinitionsdateien (RDL), die von einem SQL Server Reporting Services-Berichtsserver oder einem Power BI-Berichtsserver verarbeitet werden zugeordnet. Dieses Berichts-Viewer-Webpart kann nicht mit Power BI-Berichten in Power BI-Berichtsserver gehostet verwendet werden.

Gehen Sie folgendermaßen vor, das Lösungspaket, die der Berichts-Viewer-Webpart einer SharePoint Server 2013 oder SharePoint Server 2016-Umgebung hinzufügen manuell bereitstellen. Bereitstellen der Lösung ist ein erforderlicher Schritt zum Konfigurieren des Webparts.

**Der Berichts-Viewer-Webpart ist ein eigenständiges Lösungspaket und ist nicht mit den integrierten SharePoint-Modus für SQL Server Reporting Services verknüpft.**

## <a name="requirements"></a>Anforderungen

**Unterstützung von SharePoint Server-Versionen:**  
* SharePoint Server 2016
* SharePoint Server 2013

**Reporting Services-Versionen werden unterstützt:**  
* SQL Server 2008 Reporting Services (einheitlicher Modus) und höher.
* Power BI-Berichtsserver

## <a name="download-the-report-viewer-web-part-solution-package"></a>Herunterladen des Berichts-Viewer Web Teil-Lösungspakets

Der Berichts-Viewer-Webpart ist im Microsoft Download Center verfügbar.

[Herunterladen von Berichts-Viewer Web Teil-Lösungspaket](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="deploy-the-farm-solution"></a>Bereitstellen der farmlösung

In diesem Abschnitt wird gezeigt, wie das Lösungspaket zur SharePoint-Farm bereitstellen. Diese Aufgabe muss nur einmal ausgeführt werden.

1. Öffnen Sie auf einem SharePoint-Server eine SharePoint-Verwaltungsshell mit der **als Administrator ausführen** Option.

2. Führen Sie [Add-SPSolution](https://technet.microsoft.com/library/ff607552(v=office.16).aspx) um die farmlösung hinzuzufügen.

    ```
    Add-SPSolution –LiteralPath "{path to file}\ReportViewerWebPart.wsp"
    ```

    Das Cmdlet gibt den Namen der Lösung, deren Lösungs-ID und "Deployed=False" zurück. Im nächsten Schritt wird die Lösung bereitgestellt.

3. Führen Sie die [Install-SPSolution](https://technet.microsoft.com/library/ff607534(v=office.16).aspx) Cmdlet, um die farmlösung bereitzustellen.

    **SharePoint 2013**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -CompatibilityLevel "14,15" -GACDeployment -WebApplication {URL to web application}
    ```

    **SharePoint 2016**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -GACDeployment -WebApplication {URL to web application}
    ```

## <a name="activate-feature"></a>Aktivieren der Funktion

1. Wählen Sie in der SharePoint-Website, die **Zahnradsymbol** Symbol in der oberen linken Ecke aus, und wählen **Standorteinstellungen*.

    ![Standorteinstellungen aus dem Zahnradsymbol.](media/sharepoint-site-settings.png)

    Standardmäßig wird auf SharePoint-Webanwendungen über Port 80 zugegriffen. Dies bedeutet, dass Sie eine SharePoint-Website häufig durch Eingabe zugreifen können *http://<computer name>*  um die Stammwebsitesammlung zu öffnen.

3. In **Websitesammlungsverwaltung**Option **Websitesammlungs-Features**.

4. Führen Sie einen Bildlauf nach unten bis Sie finden die **Berichts-Viewer-Webpart** Funktion.

5. Wählen Sie **Aktivieren**aus.

    ![Berichts-Viewer-Webpart webfunktion aktivieren](media/web-part-activiate-feature.png)

6. Wiederholen Sie für zusätzliche Websitesammlungen, indem Sie jede Website öffnen und auf Website-Aktionen.

Optional, Sie können auch PowerShell zum Aktivieren dieser Funktion auf allen Standorten, die mit der [Enable-SPFeature](https://technet.microsoft.com/library/ff607803.aspx) Cmdlet.

```
Get-SPWebApplication "<web application url>" | Get-SPSite -Limit ALL | 
        ForEach-Object {
            Write-Host "Enabling feature for $($_.URL)"
            Enable-SPFeature -identity "ReportViewerWebPart" -URL $_.URL -ErrorAction Continue
        }
```

## <a name="remove-the-solution"></a>Entfernen Sie die Projektmappe

Obwohl SharePoint-Zentraladministration Zurückziehen der Lösung enthält, müssen Sie nicht entfernen der **ReportViewerWebPart.wsp** Datei, es sei denn, Sie systematisch ein Installations- oder Patch-Bereitstellung-Konfigurationsproblem beheben möchten.

1. In der SharePoint-Zentraladministration in **Systemeinstellungen**Option **farmlösungen verwalten**.

2. Wählen Sie **ReportViewerWebPart.wsp**.

3. Wählen Sie die Lösung zurückziehen.

### <a name="remove-the-web-part-from-site-settings"></a>Entfernen Sie das Webpart aus der Seite siteeinstellungen

Zurückziehen der Lösung wird der Berichts-Viewer-Webpart nicht aus der Liste der Webparts in der SharePoint-Website entfernt. Führen Sie folgende Schritte aus, um den Berichts-Viewer-Webpart zu entfernen.

1. Wählen Sie in der SharePoint-Website, die **Zahnradsymbol** Symbol in der oberen linken Ecke aus, und wählen **Standorteinstellungen*.

    ![Standorteinstellungen aus dem Zahnradsymbol.](media/sharepoint-site-settings.png)

    Standardmäßig wird auf SharePoint-Webanwendungen über Port 80 zugegriffen. Dies bedeutet, dass Sie eine SharePoint-Website häufig durch Eingabe zugreifen können *http://<computer name>*  um die Stammwebsitesammlung zu öffnen.

2. Klicken Sie unter **Web-Designer-Kataloge**Option **-Webparts**.

3. Wählen Sie die **Symbol "Bearbeiten"** neben **ReportViewerNativeMode.dwp**. Es kann nicht auf der ersten Seite der Ergebnisse aufgelistet werden.

4. Wählen Sie **Element löschen**.

    ![Bearbeiten Sie und löschen Sie die im einheitlichen Modus von Berichts-Viewer-Webpart](media/report-viewer-native-mode-edit-delete.png)

Löschen des Webparts kann versucht werden, mithilfe von PowerShell, aber es ist kein direkter Befehl dafür. Ein-Skript-Beispiel finden Sie unter [Löschen von Webparts aus dem Webpartkatalog](https://gallery.technet.microsoft.com/office/How-to-delete-Web-Parts-1132701f).

## <a name="supported-languages"></a>Unterstützte Sprachen

Mit dem Webpart werden die folgenden Sprachen unterstützt:

* Englisch (En)
* Deutsch (Deutschland)
* Spanisch (sp)
* Französisch (fr)
* Italienisch (it)
* Japanisch (Japan)
* Koreanisch (Ko)
* Portugiesisch (pt)
* Russisch (ru)
* Chinesisch (vereinfacht - Zh-HANS und Zh-CHS)
* Chinesisch (traditionell - Zh-HANT und Zh-CHT)

## <a name="next-steps"></a>Nächste Schritte

Nachdem der Berichts-Viewer-Webpart bereitgestellt wurde und aktiviert, können Sie das Webpart zu einer SharePoint-Seite hinzufügen. Weitere Informationen finden Sie unter [Hinzufügen von Berichts-Viewer-Webpart auf einer SharePoint-Seite](add-report-viewer-web-part-to-page.md).

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)

