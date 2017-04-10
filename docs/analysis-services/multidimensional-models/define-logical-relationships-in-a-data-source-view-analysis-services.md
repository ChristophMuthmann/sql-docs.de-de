---
title: "Definieren von logischen Beziehungen in einer Datenquellensicht (Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Hinzufügen von Beziehungen"
  - "Beziehungen [Analysis Services], Datenquellensichten"
  - "Datenquellensichten [Analysis Services], Beziehungen"
ms.assetid: a20d6dae-e769-4131-8a59-7ef56f174220
caps.latest.revision: 37
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 37
---
# Definieren von logischen Beziehungen in einer Datenquellensicht (Analysis Services)
  Im Datenquellensicht-Assistenten und im Datenquellensicht-Designer werden automatisch Beziehungen zwischen Tabellen definiert, die einer Datenquellensicht (Data Source View, DSV) hinzugefügt werden. Das Definieren der Beziehungen erfolgt auf Grundlage der Beziehungen in der zugrunde liegenden Datenbank oder auf Grundlage der von Ihnen angegebenen Namensübereinstimmungskriterien.  
  
 Wenn Sie Daten aus mehreren Datenquellen verwenden, müssen Sie zur Ergänzung der automatisch definierten Beziehungen in der DSV u. U. logische Beziehungen manuell definieren. In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sind Beziehungen erforderlich, um Fakten- und Dimensionstabellen zu identifizieren, Abfragen zum Abrufen von Daten und Metadaten aus den zugrunde liegenden Datenquellen zu erstellen und die erweiterten Business Intelligence-Funktionen nutzen zu können.  
  
 Sie können die folgenden Arten von Beziehungen im Datenquellensicht-Designer definieren:  
  
-   Eine Beziehung von einer Tabelle zu einer anderen Tabelle in derselben Datenquelle.  
  
-   Eine Beziehung von einer Tabelle zu sich selbst, wie in einer Über-/Unterordnungsbeziehung.  
  
-   Eine Beziehung von einer Tabelle in einer Datenquelle zu einer anderen Tabelle in einer anderen Datenquelle.  
  
> [!NOTE]  
>  Die in einer DSV definierten Beziehungen sind logischer Natur und geben möglicherweise nicht die in der zugrunde liegenden Datenquelle definierten tatsächlichen Beziehungen wieder. Sie können im Datenquellensicht-Designer Beziehungen erstellen, die es in der zugrunde liegenden Datenquelle nicht gibt, und Beziehungen entfernen, die vom Datenquellensicht-Designer aus vorhandenen Fremdschlüsselbeziehungen in der zugrunde liegenden Datenquelle erstellt wurden.  
  
 Beziehungen sind zielgerichtet. Jedem Wert in der Quellspalte ist ein entsprechender Wert in der Zielspalte zugeordnet. In einem Datenquellensicht-Diagramm, wie z. B. den im Bereich **Diagramm** angezeigten Diagrammen, weist ein Pfeil in der Zeile zwischen zwei Tabellen auf die Richtung der Beziehung hin.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [So fügen Sie eine Beziehung zwischen Tabellen, benannten Abfragen oder Sichten hinzu](#bkmk_addRel)  
  
 [So können Sie eine Beziehung im Bereich "Diagramm" anzeigen oder ändern](#bkmk_diagrampane)  
  
 [So können Sie eine Beziehung im Bereich "Tabellen" anzeigen oder ändern](#bkmk_tablespane)  
  
##  <a name="bkmk_addRel"></a> So fügen Sie eine Beziehung zwischen Tabellen, benannten Abfragen oder Sichten hinzu  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das Projekt, oder stellen Sie eine Verbindung mit der Datenbank her, das bzw. die die Datenquellensicht enthält, in der Sie eine logische Beziehung hinzufügen möchten.  
  
2.  Erweitern Sie im Projektmappen-Explorer den Ordner **Datenquellensichten**, und doppelklicken Sie anschließend auf die Datenquellensicht, um sie im **Datenquellensicht-Designer** zu öffnen.  
  
3.  Klicken Sie im Bereich **Tabellen** mit der rechten Maustaste auf die Tabelle, benannte Abfrage oder Sicht, der Sie eine Beziehung hinzufügen möchten, und klicken Sie anschließend auf **Neue Beziehung**.  
  
    > [!NOTE]  
    >  Zum Suchen nach einer Tabelle, Sicht oder benannten Abfrage können Sie die Option **Tabelle suchen** verwenden, indem Sie entweder auf das Menü **Datenquellensicht** klicken oder mit der rechten Maustaste auf einen offenen Bereich im Bereich **Tabelle** oder **Diagramm** klicken.  
  
4.  Führen Sie im Dialogfeld **Beziehung angeben** folgende Schritte aus:  
  
    1.  Wählen Sie die geeignete Tabelle, benannte Abfrage oder Sicht in der Liste **Quelltabelle (Fremdschlüsseltabelle)** aus.  
  
    2.  Wählen Sie die geeignete Tabelle, benannte Abfrage oder Sicht in den Listen **Zieltabelle (Primärschlüsseltabelle)** aus.  
  
    3.  Wählen Sie in den Listen **Quellspalten** und **Zielspalten** Spalten aus, um eine Beziehung zwischen den beiden Tabellen zu erstellen.  
  
         Wenn in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durch das stichprobenartige Untersuchen der Daten in der zugrunde liegenden Tabelle, Sicht oder benannten Abfrage erkannt wird, dass Sie die Beziehung in der falschen Richtung (vom Primärschlüssel zum Fremdschlüssel anstatt vom Fremdschlüssel zum Primärschlüssel) definiert haben, werden Sie aufgefordert, die Richtung umzukehren. Sie können die Richtung schnell umkehren, indem Sie auf **Umkehren**klicken.  
  
         Wenn in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erkannt wird, dass bereits eine Beziehung für die ausgewählten Spalten vorhanden ist, wird eine entsprechende Meldung angezeigt. Es ist nicht möglich, doppelte Beziehungen zu definieren.  
  
    4.  Geben Sie optional im Feld **Beschreibung** eine Beschreibung für die Beziehung ein.  
  
##  <a name="bkmk_diagrampane"></a> So können Sie eine Beziehung im Bereich "Diagramm" anzeigen oder ändern  
  
-   Klicken Sie im Bereich **Diagramm** im **Datenquellensicht-Designer** mit der rechten Maustaste auf die Beziehung, die Sie anzeigen möchten, und klicken Sie auf **Beziehung bearbeiten** (oder doppelklicken Sie einfach auf den Beziehungspfeil).  Verwenden Sie das Dialogfeld **Beziehung bearbeiten** , um die Beziehung zu ändern.  
  
##  <a name="bkmk_tablespane"></a> So können Sie eine Beziehung im Bereich "Tabellen" anzeigen oder ändern  
  
1.  Suchen und erweitern Sie im Bereich **Tabelle** im **Datenquellensicht-Designer**die Tabelle, Sicht oder benannte Abfrage, die die Beziehung enthält, die Sie anzeigen oder ändern möchten.  
  
2.  Erweitern Sie den Ordner **Beziehungen** .  Die Beziehungen zwischen der ausgewählten Tabelle, Sicht oder benannten Abfrage und anderen Tabellen, Sichten und benannten Abfragen werden zusammen mit der Beziehungsspalte angezeigt.  
  
3.  Klicken Sie mit der rechten Maustaste auf die zu ändernde Beziehung, und klicken Sie anschließend auf **Beziehung bearbeiten**.  
  
## Siehe auch  
 [Datenquellsichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  