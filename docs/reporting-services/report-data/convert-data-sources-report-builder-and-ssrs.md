---
title: "Konvertieren von Datenquellen (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenquellen [Reporting Services], eingebettet"
  - "Datenquellen [Reporting Services], freigegeben"
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
caps.latest.revision: 16
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 16
---
# Konvertieren von Datenquellen (Berichts-Generator und SSRS)
  Jede Datenquelle im Berichtsdatenbereich ist eingebettet und bezieht sich speziell auf den Bericht, oder sie ist freigegeben. In Berichts-Generator verweist eine freigegebene Datenquelle auf eine veröffentlichte freigegebene Datenquelle auf einem Berichtsserver oder einer SharePoint-Website. In Berichts-Designer verweist eine freigegebene Datenquellenreferenz auf eine freigegebene Datenquelle im Ordner **Freigegebene Datenquellen** in Projektmappen-Explorer.  
  
 Weitere Informationen zu den Unterschied zwischen eingebetteten und freigegebenen Datenquellen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../Topic/Embedded%20and%20Shared%20Data%20Connections%20or%20Data%20Sources%20\(Report%20Builder%20and%20SSRS\).md).  
  
 Weitere Informationen zum Erstellen einer freigegebenen Datenquelle finden Sie unter [Erstellen einer eingebettete oder freigegebenen Datenquelle &#40;SSRS&#41;](../Topic/Create%20an%20Embedded%20or%20Shared%20Data%20Source%20\(SSRS\).md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Berichts-Designer  
  
#### So konvertieren Sie eine Datenquelle von "eingebettet" in "freigegeben"  
  
-   Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf die Datenquelle, und klicken Sie anschließend auf **In freigegebene Datenquelle konvertieren**.  
  
    > [!NOTE]  
    >  Zum Anzeigen des Berichtsdatenbereichs klicken Sie im Menü **Ansicht** auf **Berichtsdaten**. Wenn der Bereich als unverankertes Fenster geöffnet wird, können Sie es andocken. Weitere Informationen finden Sie unter [Andocken des Berichtsdatenbereichs im Berichts-Designer &#40;SSRS&#41;](../../reporting-services/tools/dock-the-report-data-pane-in-report-designer-ssrs.md).  
  
     Im Berichtsdatenbereich ändert sich das Datenquellensymbol in das Symbol für freigegebene Datenquellen. Im Projektmappen-Explorer wird eine freigegebene Datenquelle mit demselben Namen im Ordner **Freigegebene Datenquelle** angezeigt.  
  
### So konvertieren Sie eine Datenquelle von "freigegeben" in "eingebettet"  
  
-   Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf die Datenquelle, öffnen Sie das Dialogfeld **Datenquelleneigenschaften**, und klicken Sie anschließend auf **Eingebettete Verbindung**. Geben Sie die erforderlichen Informationen ein.  
  
     Im Berichtsdatenbereich ändert sich das Datenquellensymbol in das Symbol für freigegebene Datenquellen.  
  
## Berichts-Generator  
  
#### So konvertieren Sie eine Datenquelle von "eingebettet" in "freigegeben"  
  
-   Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf die Datenquelle, öffnen Sie das Dialogfeld **Datenquelleneigenschaften**, und klicken Sie anschließend auf **Eingebettete Verbindung**. Geben Sie die erforderlichen Informationen ein.  
  
     Im Berichtsdatenbereich ändert sich das Datenquellensymbol in das Symbol für freigegebene Datenquellen.  
  
#### So konvertieren Sie eine Datenquelle von "freigegeben" in "eingebettet"  
  
-   Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf die Datenquelle, öffnen Sie das Dialogfeld **Datenquelleneigenschaften**, und klicken Sie anschließend auf **Eingebettete Verbindung**. Geben Sie die erforderlichen Informationen ein.  
  
     Im Berichtsdatenbereich ändert sich das Datenquellensymbol in das Symbol für freigegebene Datenquellen.  
  
## Siehe auch  
 [Verwalten von Berichtsdatenquellen](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  