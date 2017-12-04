---
title: "Browserunterstützung für Reporting Services und Power View | Microsoft-Dokumentation"
ms.custom: SQL2016_New_Updated
ms.date: 07/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- displaying reports
- scripts [Reporting Services], requirements
- viewing reports
- browsers [Reporting Services]
- Web browsers [Reporting Services], about browser support
- browsing reports [Reporting Services]
- components [Reporting Services], browsers
- Web browsers [Reporting Services]
ms.assetid: 48a75bbb-0029-4c43-891d-dc8f4fc0ebe1
caps.latest.revision: "121"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: f6dcf1d4b0423517113345f9ed6532fb6baf07e0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="browser-support-for-reporting-services-and-power-view"></a>Browserunterstützung für Reporting Services und Power View

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Erfahren Sie, welche Browserversionen zum Verwalten und Anzeigen von SQL Server Reporting Services, der ReportViewer-Steuerelemente und Power View unterstützt werden.

> [!NOTE]
> Die Integration von Reporting Services in SharePoint ist nach SQL Server 2016 nicht mehr möglich.

## <a name="browser-requirements-for-the-web-portal"></a>Browseranforderungen für das Webportal

Im Folgenden finden Sie die aktuelle Liste der unterstützten Browser für das Webportal.

**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*
- Microsoft Edge (+)
- Microsoft Internet Explorer 10 oder 11
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple iOS**  
*iPhone und iPad mit iOS 9*

- Apple Safari (+)

**Google Android**  
*Smartphones und Tablets mit Android 4.4 (KitKat) oder höher*

- Google Chrome (+)

 **(+)** neueste öffentlich freigegebene Version

## <a name="browser-requirements-for-the-reportviewer-web-control-2015"></a>Browseranforderungen für das ReportViewer-Websteuerelement (2015)

 Im Folgenden finden Sie die aktuelle Liste der Browser, die mit dem ReportViewer-Websteuerelement (2015) unterstützt werden. Der Berichts-Viewer unterstützt die Anzeige von Berichten vom [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Webportal und von den SharePoint-Bibliotheken.  

**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*

- Microsoft Edge (+)
- Microsoft Internet Explorer 10 oder 11
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)

 **(+)** neueste öffentlich freigegebene Version

 Informationen bei Verwendung eines SharePoint-Produkts, das in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]integriert ist, finden Sie unter  [Planen der Browserunterstützung in SharePoint 2016](http://technet.microsoft.com//library/cc263526\(v=office.16\).aspx).

### <a name="authentication-requirements"></a>Authentifizierungsanforderungen

 Browser unterstützen spezifische Authentifizierungsschemas, die vom Berichtsserver verarbeitet werden müssen, damit die Clientanforderung nicht fehlschlägt. In der folgenden Tabelle sind die Standardauthentifizierungstypen angegeben, die von den einzelnen unter einem Windows-Betriebssystem ausgeführten Browsern unterstützt werden.

|**Browsertyp**|**Unterstützt**|**Browserstandard**|**Serverstandard**|
|----------------------|------------------|-------------------------|------------------------|
|**Microsoft Edge** (+)|Negotiate, Kerberos, NTLM, Basic|Aushandeln|Ja. Die Standardauthentifizierungseinstellungen können mit Edge verwendet werden.|
|**Microsoft Internet Explorer**|Negotiate, Kerberos, NTLM, Basic|Aushandeln|Ja. Die Standardauthentifizierungseinstellungen können mit Internet Explorer verwendet werden.|
|**Google Chrome**(+)|Negotiate, NTLM, Basic|Aushandeln|Ja. Die Standardauthentifizierungseinstellungen können mit Chrome verwendet werden.|
|**Mozilla Firefox**(+)|NTLM, Standard|NTLM|Ja. Die Standardauthentifizierungseinstellungen können mit Firefox verwendet werden.|
|**Apple Safari**(+)|NTLM, Standard|Standard|Ja. Die Standardauthentifizierungseinstellungen können mit Safari verwendet werden.|

 **(+)** neueste öffentlich freigegebene Version

### <a name="script-requirements-for-viewing-reports"></a>Skriptanforderungen zum Anzeigen von Berichten

 Um den Berichts-Viewer zu verwenden, konfigurieren Sie den Browser für die Ausführung von Skripts.

 Wenn die Skripterstellung nicht aktiviert ist, wird beim Öffnen eines Berichts eine Fehlermeldung ähnlich der folgenden angezeigt:

- **Der Browser unterstützt keine Skripts oder ist so konfiguriert, dass die Ausführung von Skripts nicht zulässig ist. Klicken Sie hier, um den Bericht ohne Skripts anzuzeigen**.

 Wenn Sie den Bericht ohne Skriptunterstützung anzeigen, wird der Bericht ohne Funktionen des Berichts-Viewers, wie z. B. die Berichtssymbolleiste oder die Dokumentstruktur, in HTML gerendert.

> [!NOTE]
> Die Berichtssymbolleiste ist Teil der HTML-Viewerkomponente. Die Symbolleiste wird standardmäßig oberhalb der jeweiligen in einem Browserfenster gerenderten Berichte angezeigt. Der Berichts-Viewer stellt Funktionen bereit, mit denen Sie den Bericht nach Informationen durchsuchen, einen Bildlauf zu einer bestimmten Seite durchführen und die Seitengröße aus Darstellungsgründen anpassen können. Weitere Informationen zur Berichtssymbolleiste oder zum HTML-Viewer finden Sie unter [HTML Viewer and the Report Toolbar](../reporting-services/html-viewer-and-the-report-toolbar.md).

## <a name="browser-support-for-reportviewer-web-server-controls-in-visual-studio"></a>Browserunterstützung für ReportViewer-Webserversteuerelemente in Visual Studio

 Das ReportViewer-Webserversteuerelement wird verwendet, um Berichtsfunktionen in eine ASP.NET-Webanwendung einzubetten. Die Steuerelemente sind in Visual Studio enthalten und unterstützen andere Browser und Browserversionen als die anderen in diesem Thema beschriebenen Komponenten. Der Browsertyp, mit dem die Anwendung angezeigt wird, bestimmt die Art der ReportViewer-Funktionalität, die Sie in der Anwendung bereitstellen können. Ermitteln Sie mithilfe der Tabelle in diesem Thema, welche der unterstützten Browser Einschränkungen bei den Berichtsfunktionen unterliegen und welche Plattformen unterstützt werden.  

 Verwenden Sie einen Browser, in dem die Skriptunterstützung aktiviert ist. Wenn der Browser keine Skripts ausführen kann, können Sie den Bericht nicht anzeigen.

**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*

- Microsoft Edge (+)
- Microsoft Internet Explorer 10 oder 11
- Google Chrome (+)
- Mozilla Firefox (+)

 **(+)** neueste öffentlich freigegebene Version

## <a name="power-view-browser-support"></a>Power View-Browserunterstützung

**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*

- Microsoft Internet Explorer 10 oder 11
- Mozilla Firefox (+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)

 **(+)** neueste öffentlich freigegebene Version

 Weitere Informationen zur SharePoint 2016-Browserunterstützung finden Sie unter [Planen der Browserunterstützung in SharePoint 2013](http://technet.microsoft.com//library/cc263526\(v=office.16\).aspx).

## <a name="next-steps"></a>Nächste Schritte

[Finding and Viewing Reports in the web portal (Suchen und Anzeigen von Berichten im Webportal)](report-builder/finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)  
[Reporting Services-Tools](../reporting-services/tools/reporting-services-tools.md)  
[Webportal (einheitlicher SSRS-Modus)](http://msdn.microsoft.com/en-us/7349e626-6ed5-4d21-b05f-cf042ad9ad70)  
[HTML Viewer and the Report Toolbar](../reporting-services/html-viewer-and-the-report-toolbar.md)  
[URL Access Parameter Reference (URL-Zugriffsparameterverweis)](../reporting-services/url-access-parameter-reference.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)

