---
title: "Lektion 8: Erstellen von Leistungskennzahlen | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: a6c8ac2b-64ba-456f-b418-7bf0afe145d1
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lektion 8: Erstellen von Leistungskennzahlen
In dieser Lektion erstellen Sie Leistungskennzahlen (Key Performance Indicators, KPIs). KPIs dienen zum Messen der Leistung eines Werts, der durch ein *Basismeasure* definiert wird, anhand eines *Zielwerts*, der ebenfalls durch ein Measure oder durch einen absoluten Wert definiert wird. In Clientanwendungen zur Berichtserstellung erhalten Geschäftsleute mit KPIs einen schnellen und einfachen Einblick in den insgesamten Geschäftserfolg bzw. können Trends leichter identifizieren. Weitere Informationen finden Sie unter [KPIs &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/kpis-ssas-tabular.md).  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **15 Minuten**  
  
## Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Sie sollten vor dem Ausführen der Aufgaben in dieser Lektion die vorherige Lektion abgeschlossen haben: [Lektion 7: Erstellen von Measures](../analysis-services/lesson-7-create-measures.md).  
  
## Erstellen von Leistungskennzahlen  
  
#### So erstellen Sie einen KPI zur Internetverkaufsleistung des aktuellen Quartals  
  
1.  Klicken Sie im Modell-Designer auf die Tabelle (Registerkarte) **Internet Sales**.  
  
2.  Klicken Sie im Measureraster auf eine leere Zelle.  
  
3.  Geben Sie in der Bearbeitungsleiste über der Tabelle die folgende Formel ein:  
  
    **Internet Current Quarter Sales Performance :=IFERROR([Internet Current Quarter Sales]/[Internet Previous Quarter Sales Proportion to QTD],BLANK())**  
  
    Drücken Sie nach dem Erstellen der Formel die EINGABETASTE.  
  
    Dieses Measure dient als Basismeasure für den KPI.  
  
4.  Klicken Sie im Measureraster mit der rechten Maustaste auf das Measure **Internet Current Quarter Sales Performance** und anschließend auf **KPI erstellen**.  
  
    Das Dialogfeld **Key Performance Indicator** wird geöffnet.  
  
5.  Wählen Sie im Dialogfeld **Key Performance Indicator (KPI)** unter **Zielwert** die Option **Absoluter Wert** aus.  
  
6.  Geben Sie im Feld **Absoluter Wert** den Wert **1.1** ein, und drücken Sie anschließend die EINGABETASTE.  
  
7.  Geben Sie im linken (unteren) Schiebereglerfeld den Wert **1** und anschließend im rechten (oberen) Schiebereglerfeld **1,07** ein.  
  
8.  Wählen Sie unter **Symbolart auswählen** den Symboltyp Diamant (rot), Dreieck (gelb) oder Kreis (grün) aus.  
  
    > [!TIP]  
    > Achten Sie auf das erweiterbare Feld **Beschreibungen** unterhalb der verfügbaren Symbolarten. Sie können Typbeschreibungen eingeben, damit sich die verschiedenen KPI-Elemente in Clientanwendungen leichter identifizieren lassen.  
  
9. Klicken Sie auf **OK**, um den KPI abzuschließen.  
  
    Achten Sie im Measureraster auf das Symbol neben dem Measure **Internet Current Quarter Sales Performance**. Dieses Symbol gibt an, dass das Measure als Basiswert für einen KPI dient.  
  
#### So erstellen Sie einen KPI zur Internetumsatzleistung des aktuellen Quartals  
  
1.  Klicken Sie im Measureraster für die Tabelle **Internet Sales** auf eine leere Zelle.  
  
2.  Geben Sie in der Bearbeitungsleiste über der Tabelle die folgende Formel ein:  
  
    **Internet Current Quarter Margin Performance :=IF([Internet Previous Quarter Margin Proportion to QTD]<>0,([Internet Current Quarter Margin]-[Internet Previous Quarter Margin Proportion to QTD])/[Internet Previous Quarter Margin Proportion to QTD],BLANK())**  
  
    Drücken Sie nach dem Erstellen der Formel die EINGABETASTE.  
  
3.  Klicken Sie im Measureraster mit der rechten Maustaste auf das Measure **Internet Current Quarter Margin Performance** und anschließend auf **KPI erstellen**.  
  
4.  Wählen Sie im Dialogfeld **Key Performance Indicator** unter **Zielwert definieren** die Option **Absoluter Wert** aus.  
  
5.  Geben Sie im Feld **Absoluter Wert** den Wert **1,25** ein.  
  
6.  Verschieben Sie unter **Statusschwellenwerte definieren** den linken (unteren) Schieberegler, bis im Feld der Wert **0,8** angezeigt wird. Verschieben Sie anschließend den rechten (oberen) Schieberegler, bis im Feld **1,03** angezeigt wird.  
  
7.  Wählen Sie unter **Symbolart auswählen** den Symboltyp Diamant (rot), Dreieck (gelb) oder Kreis (grün) aus. Klicken Sie anschließend auf **OK**.  
  
## Nächster Schritt  
Wenn Sie mit diesem Tutorial fortfahren möchten, wechseln Sie zur nächsten Lektion: [Lektion 9: Erstellen von Perspektiven](../Topic/Lesson%209:%20Create%20Perspectives.md).  
  
  
  
