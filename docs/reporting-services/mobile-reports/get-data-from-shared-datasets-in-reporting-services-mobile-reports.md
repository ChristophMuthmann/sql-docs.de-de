---
title: Abrufen von Daten aus freigegebenen Datasets in der mobilen Reporting Services-Berichte | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b846451-c8d0-412c-802d-a42bb1ff8c63
caps.latest.revision: 18
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c081588c29dddd792d0b92e6cd9573beeb09fa4f
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="get-data-from-shared-datasets-in-reporting-services-mobile-reports"></a>Abrufen von Daten aus freigegebenen Datasets in mobilen Reporting Services-Berichten
Neben [Laden von Daten aus Excel-Dateien](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md), SQL Server Mobile Report Publisher können auch auf Daten aus nahezu beliebigen Quellen zugreifen. Zugreifen auf Daten muss eine freigegebene Datenquelle auf einem Reporting Services-Webportal konfiguriert. Erfahren Sie mehr über das [Erstellen freigegebener Datenquellen](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) und das [Erstellen freigegebener Datasets](../../reporting-services/report-data/manage-shared-datasets.md).  
  
Nachdem freigegebene Datenquellen und freigegebene Datasets auf dem Reporting Services-Server konfiguriert sind, können Sie diese in mobilen Berichten, die Sie in erstellen [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].   
  
Nachdem Sie eine Verbindung mit einem [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] -Server aus der [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]hergestellt haben, ist das Verbinden eines mobilen Berichts mit einem freigegebener Dataset einfach.   
  
1. Wählen Sie auf der Registerkarte **Daten** **Daten hinzufügen**aus.  
  
2. Wählen Sie **Berichtsserver**aus.   
  
3.  Falls Sie sich zum ersten Mal mit dem Server verbinden, geben Sie den Servernamen und Ihren Namen sowie Ihr Kennwort ein. Fügen Sie den Namen des Servers im Adressfeld in folgendem Format ein:  
  
    \<"Servername" > /reports/  
  
    In diesem Beispiel:  
       
    ![SSMRP_ConnectToServer](../../reporting-services/mobile-reports/media/ssmrp-connecttoserver.png)  
      
  
4. Bei der Auswahl des [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] -Servers, werden verfügbare Datasets in Ordnern angezeigt. Wählen Sie ein Dataset zum Importieren der Daten in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].  
  
   ![SS_MRP_ServerData](../../reporting-services/mobile-reports/media/ss-mrp-serverdata.png)  
  
Nachdem Sie das Dataset importiert haben, können Sie den mobilen Bericht entwerfen, und zwar genau so wie mit simulierten Daten oder lokale Daten aus einer Excel-Datei.  
  
Standardmäßig besitzt das freigegebene Dataset immer die aktuellsten Daten, da SQL Server jedes Mal, wenn ein Benutzer einen mobilen Bericht basierend auf diesem Dataset anzeigt, die zugrunde liegende Abfrage durchführt und die aktuellen Daten zurückgibt. Sollten viele Personen Ihren Bericht abrufen, ist dies natürlich nicht ideal. Deshalb können Sie mithilfe der Zwischenspeicherung dafür sorgen, dass die Abfrage periodisch ausgeführt und das Dataset zwischengespeichert wird. In diesem Blogbeitrag wird erläutert [wie Zwischenspeicherung und Datenaktualisierung im Webportal funktioniert](http://christopherfinlan.com/2016/02/10/so-refreshinghow-data-refresh-works-with-mobile-reports-and-kpis-in-reporting-services/).  
  
## <a name="add-edit-or-remove-a-report-server"></a>Hinzufügen, Bearbeiten oder Entfernen eines Berichtsservers  
  
Wenn Sie bereits mit einem Berichtsserver verbunden sind, wird Ihnen bei der Auswahl **Daten hinzufügen** auf der Registerkarte „Daten“ keine Option zum Hinzufügen eines anderen Berichtsservers angezeigt. Befolgen Sie stattdessen diese Schritte.  
  
1. Wählen Sie in der oberen linken Ecke die Option **Verbindungen**.  
  
   ![SSMRP_AddConnectionIcon](../../reporting-services/mobile-reports/media/ssmrp-addconnectionicon.png)  
     
   Der Bereich „Serververbindung“ wird auf der rechten Seite geöffnet.  
     
   ![SSMRP_ServerConnectnPane](../../reporting-services/mobile-reports/media/ssmrp-serverconnectnpane.png)  
     
2. Fügen Sie eine neue Serververbindung hinzu, oder bearbeiten bzw. entfernen Sie vorhandene Verbindungen.  
  
### <a name="see-also"></a>Siehe auch  
- [Erstellen und Veröffentlichen von mobilen Berichten mit dem Publisher für mobile Berichte von SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [Webportal (einheitlicher SSRS-Modus)](../../reporting-services/web-portal-ssrs-native-mode.md)  
-  Anzeigen von [mobilen SQL Server-Berichten und KPIs in der iPad-App](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI für iOS)  
-  Anzeigen von [mobilen SQL Server-Berichten und KPIs in der iPhone-App](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI für iOS)  
  
  
  
  


