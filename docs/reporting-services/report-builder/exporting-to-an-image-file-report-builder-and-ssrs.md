---
title: "Exportieren in eine Bilddatei (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 020d8ea2-de07-4212-a2bb-2ed0df2c8db8
caps.latest.revision: 12
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 11
---
# Exportieren in eine Bilddatei (Berichts-Generator und SSRS)
  Die Bildrenderingerweiterung rendert einen paginierten Bericht als Bitmap- oder Metadatei. Standardmäßig erstellt die Bildrenderingerweiterung eine TIFF-Datei des Berichts, die auf mehreren Seiten angezeigt werden kann. Nachdem der Client das Bild erhalten hat, kann es in einem Image Viewer angezeigt und gedruckt werden. Dieses Thema enthält für das Bildrendering spezifische Informationen und beschreibt Ausnahmen zu den Renderingregeln.  
  
 Die Bildrenderingerweiterung kann Dateien in allen von [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]unterstützten Formaten generieren: BMP, EMF, EMFPlus, GIF, JPEG, PNG und TIFF. Für TIFF lautet der Dateiname des primären Datenstromes *ReportName*.tif. Für alle anderen Formate, die als Einzelseite pro Datei gerendert werden, lautet der Dateiname *ReportName_Page.ext*. Dabei ist*ext* die Dateierweiterung für das ausgewählte Format. Geben Sie eine der oben aufgeführten Zeichenfolgen in der **OutputFormatDeviceInfo**-Einstellung an, um eine Datei in einem anderen bildunterstützten Format zu erstellen.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="SupportedImageFormats"></a> Unterstützte Bildformate  
 In der folgenden Tabelle werden die Dateierweiterung und der MIME-Typ für jedes Bildrendererformat angezeigt.  
  
|**Typ**|**Erweiterung**|**MIMEType**|  
|--------------|-------------------|------------------|  
|BMP|bmp|image/bmp|  
|GIF|gif|image/gif|  
|JPEG|jpeg|image/jpeg|  
|PNG|png|image/png|  
|TIFF|tif|image/tiff|  
|EMF|emf|image/emf|  
|EMFPlus|emf|image/emf|  
  
 ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [Zurück zum Anfang](#BackToTop)  
  
##  <a name="RenderingMultiplePages"></a> Rendern von mehreren Seiten  
 TIFF ist das einzige Format, das mehrseitige Dokumente in einer einzelnen Datei unterstützt. Andere Formate, wie JPG oder PNG, geben jeweils nur eine Seite aus und erfordern für jede Seite einen separaten Aufruf der Renderingerweiterung.  
  
 ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [Zurück zum Anfang](#BackToTop)  
  
##  <a name="Interactivity"></a> Interaktivität  
 Interaktivität wird von keinem der durch diesen Renderer generierten Bildformate unterstützt. Die folgenden interaktiven Elemente werden nicht gerendert:  
  
-   Hyperlinks  
  
-   Anzeigen oder ausblenden  
  
-   Dokumentstruktur  
  
-   Drillthrough oder Links mit Durchklicken  
  
-   Endbenutzersortierung  
  
-   Feste Berichtsköpfe  
  
-   Lesezeichen  
  
 ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [Zurück zum Anfang](#BackToTop)  
  
##  <a name="DeviceInfo"></a> Geräteinformationseinstellungen  
 Sie können einige Standardeinstellungen für diesen Renderer ändern, indem Sie die Geräteinformationseinstellungen ändern. Weitere Informationen finden Sie unter [Image Device Information Settings](../../reporting-services/image-device-information-settings.md).  
  
 ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [Zurück zum Anfang](#BackToTop)  
  
## Siehe auch  
 [Paginierung in Reporting Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Renderingverhalten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Interaktive Funktionalität für verschiedene Berichtsrenderingerweiterungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/interactive functionality - different report rendering extensions.md)   
 [Rendern von Berichtselementen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  