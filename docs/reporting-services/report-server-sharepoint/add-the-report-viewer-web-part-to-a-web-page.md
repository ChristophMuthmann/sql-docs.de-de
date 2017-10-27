---
title: "Der Berichts-Viewer-Webpart zu einer Webseite hinzufügen | Microsoft Docs"
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
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 26080938c9849d6021f30d970ab2262f405df00c
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="add-the-report-viewer-web-part-to-a-web-page"></a>Der Berichts-Viewer-Webpart zu einer Webseite hinzufügen

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Der Berichts-Viewer-Webpart können Sie Berichte anzeigen, führen Sie auf dem Berichtsserver konfiguriert ist zum Ausführen in SharePoint-Modus integrierten. Das Webpart können Sie Berichtsdefinitionsdateien (RDL) anzeigen, die Sie im Berichts-Generator oder Berichts-Designer erstellt und in eine Bibliothek hochgeladen.

Sie können das Berichts-Viewer-Webpart zu einer Webseite hinzufügen, wenn Sie einen Bericht auf dieser Seite einbetten möchten.

> [!NOTE]
> Dieser Artikel bezieht sich auf den Berichts-Viewer-Webpart, die mit dem Reporting Services-Add-in für SharePoint-Produkte geliefert wurden. Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.

Um ein Webpart zu einer Webseite hinzufügen, müssen Sie die Berechtigung hinzufügen und Anpassen von Seiten auf Websiteebene verfügen. Wenn Sie Standardsicherheitseinstellungen verwenden, wird diese Berechtigung Mitgliedern der Gruppe **Besitzer** erteilt, die über Berechtigungen für den Vollzugriff verfügen.

## <a name="to-embed-a-report-in-a-web-page"></a>Um einen Bericht auf einer Webseite einbetten

1.  Öffnen Sie oder erstellen Sie eine Webpartseite oder Dashboard.  
  
2.  Klicken Sie unter **Websiteaktionen**auf **Seite bearbeiten**.  
  
3.  Klicken Sie auf **Webpart hinzufügen**.  
  
4.  Wählen Sie in der Liste der Webpartkategorien die Kategorie **Sonstiges** aus, und wählen Sie dann **Berichts-Viewer für SQL Server Reporting Services**aus.  
  
5.  Klicken Sie auf **Hinzufügen**. Das Webpart wird am oberen Rand der Zone hinzugefügt. Sie können ihn an eine andere Stelle in der Zone ziehen.  
  
6.  Klicken Sie innerhalb des Viewers auf **Hier klicken, um den Toolbereich zu öffnen.**.  
  
7.  Wählen Sie einen Bericht aus einer Bibliothek in der aktuellen Websitesammlung aus, indem Sie auf die Schaltfläche zum Durchsuchen (**...**) klicken. Sie können auch die Berichts-URL eingeben. Wenn Sie die URL für einen Bericht bestimmen möchten, klicken Sie mit der rechten Maustaste auf den Bericht, und wählen Sie **Eigenschaften**aus. Klicken Sie nicht auf den Pfeil nach unten neben dem Bericht. Die Berichts-URL wird auf der Seite Eigenschaften anzeigen des Elements nicht angezeigt. Wenn Sie die URL aus dem Dialogfeld **Eigenschaften** kopieren und einfügen, müssen Sie die URL-Codierung "%20" durch ein Leerzeichen ersetzen ("Company%20Sales" sollte z. B. "Company Sales" lauten).  
  
    > [!NOTE]  
    >  In jedem Berichts-Viewer-Webpart enthält einen einzelnen Bericht. Die URL muss der vollqualifizierte Pfad zu einem Bericht sein, der sich auf der aktuellen SharePoint-Website oder auf einer Website innerhalb derselben Webanwendung oder Webfarm befindet. Die URL muss in eine Dokumentbibliothek oder in einen Ordner innerhalb einer Dokumentbibliothek mit dem Bericht aufgelöst werden. Die Berichts-URL muss die Dateierweiterung RDL enthalten. Wenn der Bericht von einem Modell oder freigegebenen Datenquellendateien abhängt, müssen Sie diese Dateien nicht in der URL angeben. Der Bericht enthält Verweise auf die erforderlichen Dateien.  
  
8.  Während der Toolbereich geöffnet ist, können Sie Eigenschaften festlegen, um die Standarddarstellung und das Layout zu ändern.  
  
9. Klicken Sie unten im Toolbereich auf **Anwenden** , und klicken Sie anschließend auf **OK** , um den Bereich zu schließen.  
  
## <a name="see-also"></a>Siehe auch

 [Berichts-Viewer-Webpart auf einer SharePoint-Website](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Anpassen des Berichts-Viewer-Webparts](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)   
 [Erteilen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  

