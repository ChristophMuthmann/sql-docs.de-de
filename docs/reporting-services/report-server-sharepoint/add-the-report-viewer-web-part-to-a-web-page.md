---
title: "Hinzufügen des Berichts-Viewer-Webparts zu einer Webseite | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server-sharepoint
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: ff1ed8a3dd760b02ed2c4db209009a310f0ace91
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="add-the-report-viewer-web-part-to-a-web-page"></a>Hinzufügen des Berichts-Viewer-Webparts zu einer Webseite

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Mithilfe des Berichts-Viewer-Webparts können Sie Berichte anzeigen, die auf einem Berichtsserver ausgeführt werden, der für die Ausführung im integrierten SharePoint-Modus konfiguriert ist. Mithilfe des Webparts können im Berichts-Generator oder Berichts-Designer erstellte und in eine Bibliothek hochgeladene Berichtsdefinitionsdateien (RDL) angezeigt werden.

Sie können das Berichts-Viewer-Webpart einer Webseite hinzufügen, wenn Sie einen Bericht in diese Seite einbetten möchten.

> [!NOTE]
> Dieser Artikel bezieht sich auf das Berichts-Viewer-Webpart, das im Reporting Services-Add-In für SharePoint-Produkte enthalten ist. Die Integration von Reporting Services in SharePoint ist nach SQL Server 2016 nicht mehr möglich.

Sie müssen über eine Berechtigung zum Hinzufügen und Anpassen von Seiten auf Websiteebene verfügen, um einer Webseite ein Webpart hinzufügen zu können. Wenn Sie Standardsicherheitseinstellungen verwenden, wird diese Berechtigung Mitgliedern der Gruppe **Besitzer** erteilt, die über Berechtigungen für den Vollzugriff verfügen.

## <a name="to-embed-a-report-in-a-web-page"></a>Einbetten eines Berichts in eine Webseite

1.  Öffnen oder erstellen Sie eine Webpartseite oder ein Dashboard.  
  
2.  Klicken Sie unter **Websiteaktionen**auf **Seite bearbeiten**.  
  
3.  Klicken Sie auf **Webpart hinzufügen**.  
  
4.  Wählen Sie in der Liste der Webpartkategorien die Kategorie **Sonstiges** aus, und wählen Sie dann **Berichts-Viewer für SQL Server Reporting Services**aus.  
  
5.  Klicken Sie auf **Hinzufügen**. Das Webpart wird oben in der Zone hinzugefügt. Sie können ihn an eine andere Stelle in der Zone ziehen.  
  
6.  Klicken Sie innerhalb des Viewers auf **Hier klicken, um den Toolbereich zu öffnen**.  
  
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
