---
title: "Daten für mobile Berichte von Reporting Services | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 02/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 91138ef8-ddb4-4ac5-a1e4-fa4cf1c58dcc
caps.latest.revision: 15
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 9cf879fae78095f5fa6cb6f10d20cb0dfe6d12a1
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="data-for-reporting-services-mobile-reports"></a>Daten für mobile Berichte von Reporting Services
Das [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] -Datenmodell ist einfach. Daten werden in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] als eine Sammlung von Datasets importiert. Formale Beziehungen zwischen Datasets sind nicht erforderlich. Suchvorgänge aus einem Dataset in einem anderen funktionieren, solange die Schlüsselwerte übereinstimmen. Datum/Uhrzeit-Aggregationen werden von der Laufzeitumgebung der mobilen Berichte behandelt und stimmen zwischen den verschiedenen Datasets überein, selbst wenn sich die Granularität der Datum/Uhrzeit-Daten zwischen den Datasets unterscheidet.   
  
Sie können Daten aus zwei Arten von Quellen importieren:   
  
* **Lokale Excel-Dateien**: Wählen Sie ein Excel-Dokument aus und wählen Sie aus, welches Arbeitsblatt bzw. welche Arbeitsblätter Sie importieren möchten. Nach dem Import werden die Daten in der mobilen Berichtsdefinition gespeichert. Verwenden Sie den Befehl **Daten aktualisieren** rechts oben auf der [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] **Data** tab. Erfahren Sie mehr über [Vorbereiten von Excel-Daten für mobile SSRS-Berichte](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md).  
  
* **[!INCLUDE[PRODUCT_NAME](../../includes/server-product-name.md)]Freigegebene Datasets**: Durchsuchen Sie die Liste der veröffentlichten Datasets auf dem Server, und wählen Sie diejenigen aus, die für den mobilen Bericht hinzufügen. Auf Serverdaten basierende mobile Berichte erhalten immer die Verbindung mit den ursprünglichen Datasets und spiegeln den aktuellsten Zustand der Daten auf dem Server wider. Sehen Sie sich eine [Liste unterstützter Datenquellen](https://msdn.microsoft.com/library/ms159219.aspx)an.   
  
  Erfahren Sie mehr über das [Abrufen von Daten aus freigegebenen Datasets im Publisher für mobile Berichte](../../reporting-services/mobile-reports/get-data-from-shared-datasets-in-reporting-services-mobile-reports.md).  
  
Nachdem Sie Daten in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]importiert haben, ist die übrige Erstellung und Entwurfserfahrung der mobilen Berichte gleich, unabhängig davon, woher die Daten stammen.   
  
## <a name="connect-mobile-report-elements-to-data"></a>Verbinden von Elementen mobiler Berichte mit Daten ##  
  
Jedes [!INCLUDE[PRODUCT_NAME](../../includes/short-product-name.md)] -Element enthält eine oder mehrere Dateneinstellungen. Das Element „Radiales Messgerät“ enthält beispielsweise zwei Dateneinstellungen: Hauptwert und Vergleichswert. Jede dieser Einstellungen verweist auf genau ein Feld (eine Spalte) in einem spezifischen Dataset.   
  
Die Laufzeitumgebung mobiler Berichte stellt aggregierte Werte für das Messgerät basierend auf der Auswahl des Benutzers bereit. Beachten Sie, dass der Vergleichswert der gleichen „Radiales Messgerät“-Instanz an ein Feld aus einem anderen Dataset gebunden sein kann.   
  
### <a name="see-also"></a>Siehe auch  
-  [Vorbereiten von Daten für mobile Reporting Services-Berichte](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Erstellen und Veröffentlichen von mobilen Berichten mit dem Publisher für mobile Berichte von SQL Server)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
- [Abrufen von Daten aus freigegebenen Datasets](../../reporting-services/mobile-reports/get-data-from-shared-datasets-in-reporting-services-mobile-reports.md)
- [Retain date formatting for Analysis Services in mobile reports (Datumsformatierung für Analysis Services in mobilen Berichten beibehalten)](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md) 
  
  


