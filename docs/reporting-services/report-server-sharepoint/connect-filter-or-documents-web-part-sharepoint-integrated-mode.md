---
title: Filters oder Dokumentwebparts-Webpart mit einem Reporting Services-Berichts-Viewer-Webpart verbinden | Microsoft Docs
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
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 87d4b4a3f0c01804329f3a7b0688632c20ed6c9b
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="connect-filter-or-documents-web-part-with-a-reporting-services-report-viewer-web-part"></a>Verbinden Sie Filters oder Dokumentwebparts-Webpart mit einem Reporting Services-Berichts-Viewer-Webpart

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Wenn Sie eine SharePoint-Produkts verwenden, können Sie ein Dashboard oder das Webpart Seite erstellen, die ein Filterwebpart oder Dokumentewebpart und ein Berichts-Viewer-Webpart enthält. Unterstützte Versionen sind [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] oder [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]. Ebenfalls unterstützt wird [!INCLUDE[winSPServ3](../../includes/winspserv3-md.md)] oder [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007. Durch Verbinden eines Filterwebparts können können Benutzer, die Filterwerte in einem Filterwebpart auswählen, den Wert für einen parametrisierten Bericht auf derselben Seite senden. Durch Verbinden eines dokumentewebparts können können Benutzer, die auf Berichte in der Bibliothek Dokumente klicken Sie auf den Bericht in einem angrenzenden Berichts-Viewer-Webpart anzeigen.

> [!NOTE]
> Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.

 Das Filterwebpart wird zum Senden von Werten an einen oder mehrere Parameter in einem Bericht. Um ein Filterwebpart verwenden zu können, muss der Bericht Parameter definiert haben, die mit den Werten, den Datentyp und den vom Webpart gesendeten Format kompatibel sind.  
  
 Das Dokumentewebpart ist der Bibliothek Dokumente der Website Home zugeordnet. Klicken Sie auf **Alle Websiteinhalte einblenden**, um Elemente aus der Bibliothek Dokumente anzuzeigen, hinzuzufügen oder zu entfernen. Klicken Sie in Bibliotheken auf **Dokumente**. Mit den Menüs **Neu**, **Upload**und **Aktionen** können Sie die Elemente in der Bibliothek Dokumente verwalten.  
  
## <a name="connect-a-filter-web-part"></a>Verbinden eines Filterwebparts
  
1.  Öffnen Sie oder erstellen Sie eine Webpartseite oder Dashboard.  
  
2.  Klicken Sie im Menü **Websiteaktionen** auf **Seite bearbeiten**.  
  
3.  Klicken Sie auf **Webpart hinzufügen**.  
  
4.  In **alle Webparts**in der **Sonstiges** Kategorie wählen **SQL Server Reporting Services Berichts-Viewer**.  
  
5.  Klicken Sie auf **Hinzufügen**. Das Webpart wird am oberen Rand der Zone hinzugefügt.  
  
6.  Klicken Sie auf einer anderen Zone auf derselben Webpartseite oder demselben Dashboard auf **Webpart hinzufügen**.  
  
7.  In **alle Webparts**in der **Filter** Abschnitt, wählen Sie ein Webpart.  
  
8.  Klicken Sie auf **Hinzufügen**. Das Webpart wird am oberen Rand der Zone hinzugefügt.  
  
9. Klicken Sie in der Zone, die das Webpart enthält, auf das Webpart **bearbeiten** Sie im Menü **Verbindungen**, zeigen Sie auf **Filterwerte senden an**, und wählen Sie dann **Bericht Viewer** - *Berichtsname*.  
  
10. Checken Sie Ihre Änderungen ein, und speichern Sie die Seite.  
  
## <a name="connect-a-documents-web-part"></a>Verbinden eines dokumentewebparts  
  
1.  Öffnen Sie oder erstellen Sie eine Webpartseite oder Dashboard.  
  
2.  Klicken Sie im Menü **Websiteaktionen** auf **Seite bearbeiten**.  
  
3.  Klicken Sie auf **Webpart hinzufügen**.  
  
4.  In **alle Webparts**in der **Listen und Bibliotheken** Abschnitt **Dokumente.**  
  
5.  Klicken Sie auf **Hinzufügen**. Das Webpart wird am oberen Rand der Zone hinzugefügt.  
  
6.  Klicken Sie unten im Toolbereich auf **Anwenden** , und klicken Sie anschließend auf **OK** , um den Bereich zu schließen.  
  
7.  Klicken Sie auf einer anderen Zone auf derselben Webpartseite oder demselben Dashboard auf **Webpart hinzufügen**.  
  
8.  In **alle Webparts**in der **Sonstiges** Kategorie wählen **SQL Server Reporting Services Berichts-Viewer.**  
  
9. Klicken Sie auf **Hinzufügen**. Das Webpart wird am oberen Rand der Zone hinzugefügt.  
  
10. Klicken Sie in der Zone, die das Webpart enthält, auf das Webpart **bearbeiten** Sie im Menü **Verbindungen**, zeigen Sie auf **Berichtsdefinitionen Abrufen von**, und wählen Sie dann  **Dokumente**.  
  
11. Checken Sie Ihre Änderungen ein, und speichern Sie die Seite.  
  
## <a name="see-also"></a>Siehe auch

 [Der Berichts-Viewer-Webpart zu einer Webseite hinzufügen](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)   
 [Berichts-Viewer-Webpart auf einer SharePoint-Website](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Customize the Report Viewer Web Part (Anpassen des Berichts-Viewer-Webparts)](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
