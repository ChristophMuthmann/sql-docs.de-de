---
title: 'Analysis Services Tutorial Lektion 7: Erstellen von Key Performance Indicators | Microsoft Docs'
description: Beschreibt, wie Key Performance Indicators in Analysis Services Tutorial-Projekt zu erstellen.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: d4036297bdfc8d2c75061951ff329d20378a57a2
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="create-key-performance-indicators"></a>Erstellen von Leistungskennzahlen

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In dieser Lektion erstellen Sie Key Performance Indicators (KPIs). KPIs dienen zur Messung der Leistung eines Werts, der definiert, indem Sie eine *Base* Measure gegen eine *Ziel* Wert, der ebenfalls durch ein Measure oder einen absoluten Wert definiert wird. In Clientanwendungen zur Berichtserstellung erhalten Geschäftsleute mit KPIs einen schnellen und einfachen Einblick in den insgesamten Geschäftserfolg bzw. können Trends leichter identifizieren. Weitere Informationen finden Sie unter [KPIs](../tabular-models/kpis-ssas-tabular.md)
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **15 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  

Dieser Artikel ist Teil eines Lernprogramms zur tabellenmodellierung, das in Reihenfolge absolviert werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 6: Erstellen von Measures](../tutorial-tabular-1400/as-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Erstellen von Leistungskennzahlen  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>So erstellen Sie eine InternetCurrentQuarterSalesPerformance-KPI  
  
1.  Klicken Sie im Modell-Designer auf die **FactInternetSales** Tabelle.  
  
2.  Klicken Sie im Measureraster auf eine leere Zelle.  
  
3.  Geben Sie in der Bearbeitungsleiste über der Tabelle die folgende Formel ein: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Dieses Measure dient als basismeasure für den KPI.  
  
4.  Im measureraster mit der Maustaste **InternetCurrentQuarterSalesPerformance** > **KPI erstellen**.   
  
5.  Klicken Sie im Dialogfeld Key Performance Indicator (KPI) in **Ziel** wählen **Absolutwert**, und geben Sie dann **1.1**.  
  
7.  Geben Sie im linken (unteren) Schiebereglerfeld den Wert **1**und anschließend im rechten (oberen) Schiebereglerfeld **1,07**ein.  
  
8.  Wählen Sie unter **Symbolart auswählen**den Symboltyp Diamant (rot), Dreieck (gelb) oder Kreis (grün) aus.
  
    ![as-lesson7-kpi](../tutorial-tabular-1400/media/as-lesson7-kpi.png)
    
    > [!TIP]  
    > Beachten Sie die erweiterbare **Beschreibungen** Beschriftung unterhalb der verfügbaren symbolarten. Verwenden Sie eine Beschreibung für die verschiedenen KPI-Elemente, um in Clientanwendungen typbeschreibungen.  
  
9. Klicken Sie auf **OK** , um den KPI abzuschließen.  
  
    Im measureraster, beachten Sie das Symbol neben dem **InternetCurrentQuarterSalesPerformance** Measure. Dieses Symbol gibt an, dass das Measure als Basiswert für einen KPI dient.  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a>So erstellen Sie eine InternetCurrentQuarterMarginPerformance-KPI  
  
1.  Im measureraster für die **FactInternetSales** Tabelle, klicken Sie auf eine leere Zelle.  
  
2.  Geben Sie in der Bearbeitungsleiste über der Tabelle die folgende Formel ein:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Mit der rechten Maustaste **InternetCurrentQuarterMarginPerformance** > **KPI erstellen**.  
  
4.  Klicken Sie im Dialogfeld Key Performance Indicator (KPI) in **Ziel** wählen **Absolutwert**, und geben Sie dann **1.25**.   
  
5.  Schieben Sie im Feld linken (unteren) Schieberegler, bis im Feld **0,8**, und klicken Sie dann der rechten (oberen) Schieberegler-Feld, bis im Feld Folie **1.03**.  
  
6.  Wählen Sie unter **Symbolart auswählen**den Symboltyp Diamant (rot), Dreieck (gelb) oder Kreis (grün) aus. Klicken Sie anschließend auf **OK**.  
  
## <a name="whats-next"></a>Wie geht es weiter?

[Lektion 8: Erstellen von Perspektiven](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md).
  
  
