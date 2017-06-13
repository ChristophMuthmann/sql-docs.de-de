---
title: Berichts-Viewer-Webpart-Programmierbarkeit in SharePoint-Integration | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 714017b7-1bd6-4950-a3c6-d0df8450a877
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6e176aafa062c1184ff120cc1e886b9f5e244712
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="report-viewer-web-part-programmability-in-sharepoint-integration"></a>Berichts-Viewer-Webpart-Programmierbarkeit in SharePoint-Integration
  Der Berichts-Viewer-Webpart ist ein Serversteuerelement, das einen Satz von öffentlichen Anwendungsprogrammierschnittstellen (API), die Entwicklern ermöglicht enthält, benutzerdefinierte SharePoint-Anwendungen zu erstellen. Sie können benutzerdefinierte Webparts erstellen, die den Berichtspfad und Parameter für den Berichts-Viewer-Webparts, die unter Verwendung von Webparts-Verbindungen angeben. Sie können auch das Webpart in eine benutzerdefinierte SharePoint-Webpartseite einbetten und es mit der öffentlichen API anpassen.  
  
## <a name="connecting-to-report-viewer-web-part-with-custom-web-parts"></a>Herstellen einer Verbindung mit Berichts-Viewer-Webpart mit benutzerdefinierten Webparts  
 Der Berichts-Viewer-Webpart ist ein Verbindungsconsumer zu SharePoint-Webparts, die implementieren <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> oder T:Microsoft.SharePoint.WebPartPages.IFilterValues. Ein <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> -Webpart, z. B. die **Dokumente** -Webpart kann einen Berichtspfad zu einem Bericht-Viewer-Webpart Wenn es auf der gleichen Webpartseite wie der Berichts-Viewer-Webpart platziert angeben. Ebenso ein T:Microsoft.SharePoint.WebPartPages.IFilterValues-Webpart, z. B. die **Textfilter** oder **Auswahlfilter**, einen Berichtsparameter zu einem Bericht-Viewer-Webpart Wenn es auf der gleichen Webpartseite wie der Berichts-Viewer-Webpart platziert angeben können.  
  
### <a name="implementing-a-report-path-provider-with-iwebpartrow"></a>Implementieren eines Berichtspfadanbieters mit IWebPartRow  
 Um durch Webpartverbindungen einen Berichtspfad zum Berichts-Viewer-Webpart anzugeben, gehen Sie wie folgt vor:  
  
1.  Erstellen Sie einen Webpart, der die <xref:System.Web.UI.WebControls.WebParts.IWebPartRow>-Schnittstelle implementiert.  
  
2.  Fügen Sie den Webpart zur selben Webpartseite wie den Berichts-Viewer-Webpart hinzu.  
  
3.  Verbinden Sie den Webpart mit dem Berichts-Viewer-Webpart in der webbasierten Webpart-Entwurfsbenutzeroberfläche.  
  
    > [!NOTE]  
    >  Verbindung wird nur eine <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Webparts für das Berichts-Viewer-Webpart, wodurch Sie kann keine Verbindung hergestellt sowohl eine <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> -Webpart und einem T:Microsoft.SharePoint.WebPartPages.IFilterValues-Webpart auf der Berichts-Viewer-Webpart zur selben Zeit.  
  
 Für Ihre <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> -Webpart, mit der T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart ordnungsgemäß funktionieren müssen Sie die folgenden Schritte ausführen, der <xref:System.Web.UI.WebControls.WebParts.IWebPartRow.GetRowData%2A> Methode:  
  
-   Rufen Sie die Rückrufmethode mit einem <xref:System.Data.DataRowView>-Objekt als Eingabeparameter auf.  
  
-   Stellen Sie sicher, dass das <xref:System.Data.DataRowView>-Objekt eine Spalte mit dem Namen "DocUrl" enthält, die den Berichtspfad enthält.  
  
    > [!NOTE]  
    >  Das Berichts-Viewer-Webpart im Add-In für [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2010 unterstützt auch das Empfangen von Berichtspfaden, die die Spalte "FileRef" verwenden.  
  
### <a name="implementing-a-report-parameter-provider-with-ifiltervalues"></a>Implementieren eines Berichtsparameteranbieters mit IFilterValues  
 Ein Webpart, das T:Microsoft.SharePoint.WebPartPages.IFilterValues implementiert kann einen Parameterwert für den Berichts-Viewer-Webpart angeben. Der an den Berichts-Viewer-Webpart gesendete Parameterwert unterliegt gemäß der Angabe in der Berichtsdefinition denselben Einschränkungen wie der Berichtsparameter, zum Beispiel Datentyp, gültige Werte usw.  
  
 Um dem Berichts-Viewer-Webpart einen Berichtsparameter bereitzustellen, gehen Sie wie folgt vor:  
  
1.  Erstellen Sie ein Webpart, der T:Microsoft.SharePoint.WebPartPages.IFilterValues-Schnittstelle implementiert.  
  
2.  Das Webpart wird auf derselben Seite wie die T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart hinzufügen.  
  
3.  Verbinden Sie Ihre T:Microsoft.SharePoint.WebPartPages.IFilterValues-Webpart, mit der Berichts-Viewer-Webpart in der webbasierten Webpart-Entwurfsbenutzeroberfläche.  
  
    > [!NOTE]  
    >  Sie können mehrere T:Microsoft.SharePoint.WebPartPages.IFilterValues-Webparts zu einem Zeitpunkt auf der Berichts-Viewer-Webpart verbinden. Allerdings kann keine Verbindung hergestellt sowohl eine <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> -Webpart und einem T:Microsoft.SharePoint.WebPartPages.IFilterValues-Webpart auf der Berichts-Viewer-Webpart zur selben Zeit.  
  
  
