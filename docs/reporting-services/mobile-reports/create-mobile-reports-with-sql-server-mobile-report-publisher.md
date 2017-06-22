---
title: Mobile Berichte mit SQL Server Mobile Report Publisher erstellen | Microsoft Docs
description: "Erfahren Sie mehr über Reporting Services mobile Berichte für mobile Geräte, die mit lokalen Daten, wobei eine Sammlung von datenvisualisierungen verbunden."
ms.custom:
- SQL2016_New_Updated
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: a5a8dbf6-4c3a-435d-8188-d6656c32f229
caps.latest.revision: 35
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4fe797ac21e1f659b1a2a196be3f860a65b36896
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="create-mobile-reports-with-sql-server-mobile-report-publisher"></a>Erstellen und Veröffentlichen von mobilen Berichten mit dem Publisher für mobile Berichte von SQL Server
Erfahren Sie mehr über mobile [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Berichte, die für mobile Geräte optimiert sind, mit lokalen Daten verbunden sind und über eine Sammlung von Datenvisualisierungen verfügen. 

>[!NOTE]
>  Müssen Sie zum Migrieren von Datazen Serverinhalt z. B. Dashboards und KPIs auf eine SQL Server 2016 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Server? Versuchen Sie es mit dem [SQL Server Migration Assistant für Datazen](https://www.microsoft.com/en-us/download/details.aspx?id=53128). 
 
![SS_MRP_LayoutTabSm](../../reporting-services/media/ss-mrp-layouttabsm.png)  

Mit [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)]können Sie schnell mobile [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Berichte erstellen, die für mobile Geräte und eine Vielzahl anderer Formfaktoren optimiert sind. Mobile Berichte stellen eine Reihe von Visualisierungen zur Verfügung, von Zeit-, Kategorie- und Vergleichsdiagrammen über Treemap-Diagramme bis hin zu benutzerdefinierten Karten. 

* Verbinden Sie Ihre mobilen Berichte mit einer Reihe von Datenquellen, einschließlich lokalen SQL Server- und Analysis Services-Daten. 
* Gestalten Sie Ihre mobilen Berichte auf einer Entwurfsoberfläche mit anpassbaren Rasterzeilen und -spalten und flexiblen Elementen für mobile Berichte, die sich gut auf jede Bildschirmgröße skalieren lassen. 
* Klicken Sie dann diese mobilen Berichte in einer Reporting Services-Server speichern und anzeigen und in einem Browser oder in der mobilen Power BI-app auf iPads, iPhones, Android-Telefone und Tablet-PCs und Windows 10-Geräten mit ihnen interagieren.
  
## <a name="create-includessrsnoversionmdincludesssrsnoversion-mdmd--mobile-reports"></a>Erstellen von mobilen [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]  -Berichten  
  
Diese Artikel helfen Ihnen beim Einstieg.
-  Download des [Publishers für mobile Berichte von SQL Server](http://go.microsoft.com/fwlink/?LinkID=733527)  
-  [Erstellen eines mobilen Berichts in Reporting Services](../../reporting-services/mobile-reports/create-a-reporting-services-mobile-report.md)  
-  [End-to-end walkthrough: Create mobile reports and KPIs in SQL Server 2016 Reporting Services](http://christopherfinlan.com/2015/12/21/how-to-create-mobile-reports-and-kpis-in-sql-server-reporting-services-2016-an-end-to-end-walkthrough/) (Durchgängige exemplarische Vorgehensweise: Erstellen mobiler Berichte und KPIs in SQL Server 2016 Reporting Services) (Blog von Christopher Finlan)  
- [„Erst Entwurf“ oder „Erst Daten“](../../reporting-services/mobile-reports/design-first-or-data-first-when-creating-in-reporting-services-mobile-reports.md): Entscheiden Sie, ob Sie den Bericht zuerst mit simulierten Daten entwerfen oder mit Ihren eigenen Daten beginnen.  
- [Daten für mobile Reporting Services-Berichte](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md): Verwenden Sie Daten aus freigegebenen Datasets, oder bereiten Sie Daten aus Excel-Arbeitsmappen auf das Verwenden in Ihren mobilen Berichten vor.
- [How data refresh works in mobile reports and KPIs in Reporting Services (Funktionsweise der Aktualisierung der Daten in mobilen Berichte und KPIs in Reporting Services)](http://christopherfinlan.com/2016/02/10/so-refreshinghow-data-refresh-works-with-mobile-reports-and-kpis-in-reporting-services/) (Christopher Finlans Blog): Erfahren Sie mehr über das Einrichten der Zwischenspeicherung für freigegebene Datasets, um zu steuern, wie oft Daten aktualisiert werden, und um die Berichterstellung zu beschleunigen.
- [Visualisierungen in mobilen Berichten](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
- [Messgeräte in mobilen Berichten](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
- [Karten in mobilen Berichten](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
- [Branding Ihres Webportals und mobiler Berichte](../../reporting-services/branding-the-web-portal.md) mit den Farben und dem Logo Ihres Unternehmens
  
## <a name="ssrs-mobile-reports-in-the-power-bi-mobile-apps"></a>Mobile SSRS-Berichte in den mobilen Power BI-Apps

-  Ansicht [mobile Reporting Services-Berichte und KPIs in der mobilen iOS-app](https://powerbi.microsoft.com/documentation/powerbi-mobile-iphone-kpis-mobile-reports)
-  Ansicht [mobile Reporting Services-Berichte und KPIs in Power BI-app für Android-Geräte](https://powerbi.microsoft.com/documentation/powerbi-mobile-android-kpis-mobile-reports)
-  Anzeigen von [mobilen Reporting Services-Berichten und KPIs in der Power BI-App für Windows 10-Geräte](https://powerbi.microsoft.com/documentation/powerbi-mobile-win10-kpis-mobile-reports/)    

## <a name="see-also"></a>Siehe auch  
  
-   [Erstellen, Ändern und Löschen von freigegebenen Datenquellen (SSRS)](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)  
-   [Verwalten von freigegebenen Datasets](../../reporting-services/report-data/manage-shared-datasets.md)  
-  [Arbeiten mit KPIs in Reporting Services](../../reporting-services/working-with-kpis-in-reporting-services.md)  
- [Aktivieren eines Berichtsservers für einen Zugang zu Power BI von Mobilgeräten](../../reporting-services/report-server/enable-a-report-server-for-power-bi-mobile-access.md)  

  
  


