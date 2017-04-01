---
title: "Abrufen von Daten aus freigegebenen Datasets in mobilen Reporting Services-Berichten | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/30/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0b846451-c8d0-412c-802d-a42bb1ff8c63
caps.latest.revision: 18
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 16
---
# Abrufen von Daten aus freigegebenen Datasets in mobilen Reporting Services-Berichten
Neben dem Laden von [Daten aus Excel-Dateien](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md), kann [!INCLUDE[PRODUCT_NAME](../../includes/product-name.md)] auch auf Daten aus nahezu beliebigen Quellen zugreifen. Zum Zugriff auf Daten wird eine freigegebene Datenquelle benötigt, die auf einem [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] konfiguriert ist. Erfahren Sie mehr über das [Erstellen freigegebener Datenquellen](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) und das [Erstellen freigegebener Datasets](../../reporting-services/report-data/manage-shared-datasets.md).  
  
Nachdem freigegebene Datenquellen und freigegebene Datasets auf dem [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)]-Server konfiguriert wurden, können Sie diese in mobilen Berichten verwenden, die Sie im [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] erstellt haben.   
  
Nachdem Sie eine Verbindung mit einem [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)]-Server aus der [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] hergestellt haben, ist das Verbinden eines mobilen Berichts mit einem freigegebener Dataset einfach.   
  
1. Wählen Sie auf der Registerkarte **Daten** **Daten hinzufügen** aus.  
  
2. Wählen Sie **Berichtsserver** aus.   
  
3.  Falls Sie sich zum ersten Mal mit dem Server verbinden, geben Sie den Servernamen und Ihren Namen sowie Ihr Kennwort ein. Fügen Sie den Namen des Servers im Adressfeld in folgendem Format ein:  
  
    \<"Servername">/Berichte/  
  
    In diesem Beispiel:  
       
    ![SSMRP_ConnectToServer](../../reporting-services/mobile-reports/media/ssmrp-connecttoserver.png)  
      
  
4. Bei der Auswahl des [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)]-Servers, werden verfügbare Datasets in Ordnern angezeigt. Wählen Sie ein Dataset zum Importieren der Daten in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].  
  
   ![SS_MRP_ServerData](../../reporting-services/mobile-reports/media/ss-mrp-serverdata.png)  
  
Nachdem Sie das Dataset importiert haben, können Sie den mobilen Bericht entwerfen, und zwar genau so wie mit simulierten Daten oder lokale Daten aus einer Excel-Datei.  
  
Standardmäßig besitzt das freigegebene Dataset immer die aktuellsten Daten, da SQL Server jedes Mal, wenn ein Benutzer einen mobilen Bericht basierend auf diesem Dataset anzeigt, die zugrunde liegende Abfrage durchführt und die aktuellen Daten zurückgibt. Sollten viele Personen Ihren Bericht abrufen, ist dies natürlich nicht ideal. Deshalb können Sie mithilfe der Zwischenspeicherung dafür sorgen, dass die Abfrage periodisch ausgeführt und das Dataset zwischengespeichert wird. In diesem Blogbeitrag wird erläutert [wie Zwischenspeicherung und Datenaktualisierung im Webportal funktioniert](http://christopherfinlan.com/2016/02/10/so-refreshinghow-data-refresh-works-with-mobile-reports-and-kpis-in-reporting-services/).  
  
## Hinzufügen, Bearbeiten oder Entfernen eines Berichtsservers  
  
Wenn Sie bereits mit einem Berichtsserver verbunden sind, wird Ihnen bei der Auswahl **Daten hinzufügen** auf der Registerkarte „Daten“ keine Option zum Hinzufügen eines anderen Berichtsservers angezeigt. Befolgen Sie stattdessen diese Schritte.  
  
1. Wählen Sie in der oberen linken Ecke die Option **Verbindungen**.  
  
   ![SSMRP_AddConnectionIcon](../../reporting-services/mobile-reports/media/ssmrp-addconnectionicon.png)  
     
   Der Bereich „Serververbindung“ wird auf der rechten Seite geöffnet.  
     
   ![SSMRP_ServerConnectnPane](../../reporting-services/mobile-reports/media/ssmrp-serverconnectnpane.png)  
     
2. Fügen Sie eine neue Serververbindung hinzu, oder bearbeiten bzw. entfernen Sie vorhandene Verbindungen.  
  
### Siehe auch  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Erstellen und Veröffentlichen von mobilen Berichten mit dem Publisher für mobile Berichte von SQL Server)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [Reporting Services, Webportal](../../reporting-services/web-portal-ssrs-native-mode.md)  
-  Anzeigen von [mobilen SQL Server-Berichten und KPIs in der iPad-App](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-ipad-kpis-mobile-reports) (Power BI für iOS)  
-  Anzeigen von [mobilen SQL Server-Berichten und KPIs in der iPhone-App](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI für iOS)  
  
  
  
  
