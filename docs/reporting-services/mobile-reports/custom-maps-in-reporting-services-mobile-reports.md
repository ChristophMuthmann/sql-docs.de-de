---
title: "Benutzerdefinierte Karten in mobilen Reporting Services-Berichten | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 59a4ebad-587a-4770-afcd-c69216b8afd9
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Benutzerdefinierte Karten in mobilen Reporting Services-Berichten
Geografische Karten in [!INCLUDE[PRODUCT_NAME](../../includes/product-name.md)] sind in einem als *ESRI-Shape-Dateien* bezeichneten Format definiert.  
  
Dieses wurde ursprünglich von einem privaten Unternehmen entwickelt und ist inzwischen ein weitverbreitetes halboffenes Format, das in vielen Geoinformationssystem-Anwendungen verwendet wird. Entsprechend diesem Format erfordert [!INCLUDE[PRODUCT_NAME](../../includes/short-product-name.md)], dass beim Definieren einer Karte zwei Dateien bereitgestellt werden:  
  
- Eine SHP-Datei für Shapegeometrien  
- Eine DBF-Datei für Metadaten  
  
Die Basisdateinamen müssen übereinstimmen (z. B. *canada.shp* und *canada.dbf*). Die Metadaten müssen das Feld *NAME* mit dem Namen (Schlüssel) der entsprechenden Shape enthalten, die beim Auffüllen der Karte mit Daten verwendet werden soll.  
  
> **Hinweis:**: Die beiden Kartendateien – die SHP-Datei und die DBF-Datei – dürfen zusammen nicht größer als 512 KB sein. Wenn die Kartendateien zu groß sind, verkleinern Sie sie mit einem Tool, z.B. [http://mapshaper.org/](http://mapshaper.org/).  
  
Erfahren Sie, wie Sie [mobilen Berichten benutzerdefinierte Karten hinzufügen](../../reporting-services/mobile-reports/add-a-custom-map-to-a-reporting-services-mobile-report.md).  
  
## Technische Informationen  
  
- Die offizielle Spezifikation: [http://www.esri.com/library/whitepapers/pdfs/shapefile.pdf](http://www.esri.com/library/whitepapers/pdfs/shapefile.pdf)  
- Der Wikipedia-Artikel zu Shape-Dateien: [http://de.wikipedia.org/wiki/Shapefile](http://en.wikipedia.org/wiki/Shapefile)  
  
## Erstellen und Bearbeiten der Kartengeometrie  
  
Das Erstellen und Bearbeiten von Shape-Dateien ist ein komplexer Prozess, dessen Erläuterung den Rahmen dieses Dokuments sprengen würde. Sie können für die ersten Schritte die folgenden Ressourcen und Anwendungen verwenden:  
  
- ArcGIS: [http://www.arcgis.com/](http://www.arcgis.com/)  
- MAPublisher-Plug-In für Adobe Illustrator: [http://www.avenza.com/mapublisher](http://www.avenza.com/mapublisher)  
- QuantumGIS (kostenlos): [http://www.qgis.org/](http://www.qgis.org/)  
- Manco Shapefile Editor: [http://www.mancosoftware.com/ShapeFileEditor](http://www.mancosoftware.com/ShapeFileEditor)  
  
## Vorhandene Shape-Dateien  
  
Aus dem Web können viele vorhandene Shape-Dateien heruntergeladen werden, z. B. von den folgenden Websites:  
  
- Diva-GIS: [http://www.diva-gis.org/Data](http://www.diva-gis.org/Data)  
- OpenStreetMap: [http://openstreetmapdata.com/data](http://openstreetmapdata.com/data)  
- GeoCommons: [http://www.geocommons.com/](http://www.geocommons.com/)  
  
### Siehe auch  
- [Karten in mobilen Reporting Services-Berichten](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Erstellen und Veröffentlichen von mobilen Berichten mit dem Publisher für mobile Berichte von SQL Server)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
