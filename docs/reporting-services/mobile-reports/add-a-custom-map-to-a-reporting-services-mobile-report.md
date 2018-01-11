---
title: "Hinzufügen einer benutzerdefinierten Karte zu einem mobilen Reporting Services-Bericht | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fd259b95-bb58-4eb1-a436-6aa12fc6f5f2
caps.latest.revision: "6"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4fbd722f5304835d6e288a13054edf9962985889
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="add-a-custom-map-to-a-reporting-services-mobile-report"></a>Hinzufügen einer benutzerdefinierten Karte zu einem mobilen Reporting Services-Bericht
Benutzerdefinierte Karten erfordern zwei Dateien:  
* Eine SHP-Datei für Shape-Geometrien  
* Eine DBF-Datei für Metadaten  
  
Informieren Sie sich über [benutzerdefinierte Karten in mobilen Reporting Services-Berichten](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md).  
  
Speichern Sie die beiden Dateien im selben Ordner. Die Dateinamen müssen übereinstimmen (z.B. "canada.shp" und "canada.dbf"). Die Metadaten (DBF-Datei) müssen das Feld "NAME" mit dem Namen (Schlüssel) der entsprechenden Shape enthalten, die beim Auffüllen der Karte mit Daten verwendet werden soll.   
  
## <a name="load-a-custom-map"></a>Laden einer benutzerdefinierten Karte  
  
1. Wählen Sie auf der Registerkarte **Layout** einen Kartentyp aus: **Gradient Heat Map**, **Range Stop Heat Map**oder **Bubble Map**. Ziehen Sie ihn auf die Entwurfsoberfläche, und stellen Sie ihn auf die gewünschte Größe ein.  
  
   ![SSMRP_MapsGallery](../../reporting-services/mobile-reports/media/ssmrp-mapsgallery.png)  
  
2. Wählen Sie in der Ansicht **Layout** im Bereich **Eigenschaften visueller Elemente** unter **Karte** die **benutzerdefinierte Karte in einer Datei aus**.   
  
   ![SSMRP_SelectCustomMap](../../reporting-services/mobile-reports/media/ssmrp-selectcustommap.png)  
  
3. Navigieren Sie im Dialogfeld **Öffnen** zum Speicherort der SHP- und DBF-Dateien, und wählen Sie beide aus.   
  
   ![SSMRP_SelectDBFandSHP](../../reporting-services/mobile-reports/media/ssmrp-selectdbfandshp.png)  
  
## <a name="connect-data-to-a-custom-map"></a>Verbinden von Daten an einer benutzerdefinierten Karte  
Wenn Sie die benutzerdefinierte Karte erstmals einem Bericht hinzufügen, wird sie von [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] mit simulierten geografischen Daten aufgefüllt.  
  
![SSMRP_MapsData](../../reporting-services/mobile-reports/media/ssmrp-mapsdata.png)  
  
Echte Daten zeigen Sie in Ihrer benutzerdefinierten Karte genauso wie in den vordefinierten Karten an. Führen Sie die Schritte unter [Karten in mobilen Reporting Services-Berichten](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md) aus, um Ihre Daten anzuzeigen.  
  
### <a name="see-also"></a>Siehe auch  
- [Custom maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)  
- [Karten in mobilen Reporting Services-Berichten](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [Erstellen und Veröffentlichen von mobilen Berichten mit dem Publisher für mobile Berichte von SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
  
