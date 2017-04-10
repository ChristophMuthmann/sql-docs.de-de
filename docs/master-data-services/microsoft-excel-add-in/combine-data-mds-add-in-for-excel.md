---
title: "Kombinieren von Daten (MDS-Add-In f&#252;r Excel) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a867dc15-5a0d-457c-8304-ac323bcf9377
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# Kombinieren von Daten (MDS-Add-In f&#252;r Excel)
  Kombinieren Sie in [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]Daten aus zwei Arbeitsblättern, wenn Sie Daten vor der Veröffentlichung vergleichen möchten. In diesem Verfahren kombinieren Sie Daten aus zwei Arbeitsblättern in einem Arbeitsblatt. Anschließend können Sie weitere Vergleiche ausführen und bestimmen, welche Daten ggf. im MDS-Repository veröffentlicht werden sollen.  
  
## Erforderliche Komponenten  
  
-   Sie müssen über ein Arbeitsblatt mit von MDS verwalteten Daten verfügen. Weitere Informationen finden Sie unter [Daten nach Excel exportieren, von Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md).  
  
-   Sie müssen über ein Arbeitsblatt verfügen, in dem Daten enthalten sind, die Sie mit von MDS verwalteten Daten kombinieren möchten. Dieses Blatt muss über eine Kopfzeile verfügen.  
  
### So kombinieren Sie nicht verwaltete Daten zu einem von MDS verwalteten Blatt  
  
1.  Auf das Blatt, das MDS verwalteten Daten, in enthält der **Veröffentlichen und validieren** auf **Kombinieren von Daten**.  
  
2.  Klicken Sie im Dialogfeld **Daten kombinieren** neben dem Textfeld **Mit MDS-Daten zu kombinierender Bereich** auf das Symbol. Das Dialogfeld wird reduziert.  
  
3.  Klicken Sie auf das Blatt mit den Daten, die Sie kombinieren möchten.  
  
4.  Heben Sie alle Zellen im Blatt hervor, die Sie kombinieren möchten, einschließlich der Kopfzeile.  
  
5.  Klicken Sie im Dialogfeld **Daten kombinieren** auf das Symbol. Das Dialogfeld wird erweitert.  
  
6.  Wählen Sie unter **Entsprechende Spalte**eine Spalte für eine unter der MDS-Entität aufgeführte Spalte aus. Es sind nicht für alle MDS-Spalten entsprechende Spalten erforderlich.  
  
7.  Klicken Sie auf **Kombinieren**. Eine Spalte **QUELLE** wird angezeigt und gibt an, ob die Daten aus MDS oder einer externen Quelle stammen.  
  
## Nächste Schritte  
  
-   Die Ähnlichkeit zwischen den MDS verwalteten und externen Daten finden Sie unter [Übereinstimmung ähnlicher Daten & #40; MDS-Add-in für Excel & #41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md).  
  
## Siehe auch  
 [Übersicht: Exportieren von Daten in Excel & #40; MDS-Add-in für Excel & #41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [Data Quality-Abgleich im MDS-Add-In für Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
  