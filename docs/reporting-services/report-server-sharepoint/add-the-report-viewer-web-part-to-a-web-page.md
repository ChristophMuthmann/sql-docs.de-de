---
title: "Der Berichts-Viewer-Webpart zu einer Webseite hinzufügen | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
ms.assetid: cac75345-2380-467d-a394-0a2140908a5a
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 0fd8adf79a7eeccb66b5efd6fc90e1312020973a
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="add-the-report-viewer-web-part-to-a-web-page"></a>Hinzufügen des Berichts-Viewer-Webparts zu einer Webseite
  Mithilfe des Berichts-Viewer-Webparts können Sie Berichte anzeigen, die auf einem Berichtsserver ausgeführt werden, der für die Ausführung im integrierten SharePoint-Modus konfiguriert ist. Mithilfe des Webparts können im Berichts-Generator oder Berichts-Designer erstellte und in eine Bibliothek hochgeladene Berichtsdefinitionsdateien (RDL) angezeigt werden.  
  
 Sie können das Berichts-Viewer-Webpart einer Webseite hinzufügen, wenn Sie einen Bericht in diese Seite einbetten möchten.  
  
> [!NOTE]  
>  Obwohl ihre Namen identisch sind, unterscheidet sich das über das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In installierte Berichts-Viewer-Webpart von dem in der Datei RSWebParts.cab enthaltenen Berichts-Viewer-Webpart. Die Anleitungen in diesem Thema sind speziell für den Berichts-Viewer-Webpart gedacht, der durch das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In installiert wurde.  
  
 Sie müssen über die Berechtigung zum Hinzufügen und Anpassen von Seiten auf Websiteebene verfügen, um einer Webseite ein Webpart hinzufügen zu können. Wenn Sie Standardsicherheitseinstellungen verwenden, wird diese Berechtigung Mitgliedern der Gruppe **Besitzer** erteilt, die über Berechtigungen für den Vollzugriff verfügen.  
  
### <a name="to-embed-a-report-in-a-web-page"></a>So betten Sie einen Bericht in eine Webseite ein  
  
1.  Öffnen oder erstellen Sie eine Webpartseite oder ein Dashboard.  
  
2.  Klicken Sie unter **Websiteaktionen**auf **Seite bearbeiten**.  
  
3.  Klicken Sie auf **Webpart hinzufügen**.  
  
4.  Wählen Sie in der Liste der Webpartkategorien die Kategorie **Sonstiges** aus, und wählen Sie dann **Berichts-Viewer für SQL Server Reporting Services**aus.  
  
5.  Klicken Sie auf **Hinzufügen**. Der Webpart wird oben in der Zone hinzugefügt. Sie können ihn an eine andere Stelle in der Zone ziehen.  
  
6.  Klicken Sie innerhalb des Viewers auf **Hier klicken, um den Toolbereich zu öffnen.**.  
  
7.  Wählen Sie einen Bericht aus einer Bibliothek in der aktuellen Websitesammlung aus, indem Sie auf die Schaltfläche zum Durchsuchen (**...**) klicken. Sie können auch die Berichts-URL eingeben. Wenn Sie die URL für einen Bericht bestimmen möchten, klicken Sie mit der rechten Maustaste auf den Bericht, und wählen Sie **Eigenschaften**aus. Klicken Sie nicht auf den Pfeil nach unten neben dem Bericht. Die Berichts-URL wird auf der Seite Eigenschaften anzeigen des Elements nicht angezeigt. Wenn Sie die URL aus dem Dialogfeld **Eigenschaften** kopieren und einfügen, müssen Sie die URL-Codierung "%20" durch ein Leerzeichen ersetzen ("Company%20Sales" sollte z. B. "Company Sales" lauten).  
  
    > [!NOTE]  
    >  In jedem Berichts-Viewer-Webpart ist ein einzelner Bericht enthalten. Die URL muss der vollqualifizierte Pfad zu einem Bericht sein, der sich auf der aktuellen SharePoint-Website oder auf einer Website innerhalb derselben Webanwendung oder Webfarm befindet. Die URL muss in eine Dokumentbibliothek oder in einen Ordner innerhalb einer Dokumentbibliothek mit dem Bericht aufgelöst werden. Die Berichts-URL muss die Dateierweiterung RDL enthalten. Wenn der Bericht von einem Modell oder freigegebenen Datenquellendateien abhängt, müssen Sie diese Dateien nicht in der URL angeben. Der Bericht enthält Verweise auf die erforderlichen Dateien.  
  
8.  Während der Toolbereich geöffnet ist, können Sie Eigenschaften festlegen, um die Standarddarstellung und das Layout zu ändern.  
  
9. Klicken Sie unten im Toolbereich auf **Anwenden** , und klicken Sie anschließend auf **OK** , um den Bereich zu schließen.  
  
## <a name="see-also"></a>Siehe auch  
 [Berichts-Viewer-Webpart auf einer SharePoint-Website](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Anpassen des Berichts-Viewer-Webparts](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)   
 [Erteilen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
