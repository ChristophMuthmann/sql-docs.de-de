---
title: "Lektion 13: Analysieren in Excel | Microsoft Docs"
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
ms.assetid: ce717071-193b-4c99-9654-c7a613e16327
caps.latest.revision: 22
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lektion 13: Analysieren in Excel
In dieser Lektion verwenden Sie die Funktion In Excel analysieren in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], um Microsoft Excel zu öffnen, automatisch eine Datenquellenverbindung mit der Datenbank für Modellarbeitsbereiche herzustellen und dem Arbeitsblatt automatisch eine PivotTable hinzuzufügen. Die Funktion In Excel analysieren stellt eine schnelle und einfache Methode dar, um die Wirksamkeit Ihres Modellentwurfs vor der Modellbereitstellung zu testen. Sie führen in dieser Lektion keine Datenanalyse aus. Der Zweck dieser Lektion ist es, Sie, den Modellautor, mit den Tools vertraut zu machen, die Sie zum Testen des Modellentwurfs verwenden können. Die Funktion In Excel analysieren ist für Modellentwickler vorgesehen, während Endbenutzer zum Herstellen einer Verbindung mit bereitgestellten Modelldaten und zum Durchsuchen dieser Daten Clientberichtsanwendungen, z. B. Excel oder [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], verwenden.  
  
Um diese Lektion abzuschließen, muss Excel auf dem gleichen Computer wie [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] installiert sein. Weitere Informationen finden Sie unter [Analysieren in Excel &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **20 Minuten**  
  
## Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Sie sollten vor dem Ausführen der Aufgaben in dieser Lektion die vorherige Lektion abgeschlossen haben: [Lektion 11: Erstellen von Partitionen](../analysis-services/lesson-11-create-partitions.md).  
  
## Durchsuchen mit der Standardperspektive und der Internet Sales-Perspektive  
In diesen ersten Aufgaben durchsuchen Sie das Modell mit der Standardperspektive, die alle Modellobjekte enthält, und mit der Internet Sales-Perspektive, die Sie in "Lektion 8: Erstellen von Perspektiven" erstellt haben. Die Internet Sales-Perspektive enthält nicht das Customer-Tabellenobjekt.  
  
#### So durchsuchen Sie das Modell mit der Standardperspektive  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]auf das Menü **Modell** und dann auf **In Excel analysieren**.  
  
2.  Klicken Sie im Dialogfeld **In Excel analysieren** auf **OK**.  
  
    Excel wird mit einer neuen Arbeitsmappe geöffnet. Es wird eine Datenquellenverbindung mit dem aktuellen Benutzerkonto erstellt, und zum Definieren von Anzeigefeldern wird die Standardperspektive verwendet. Dem Arbeitsblatt wird automatisch eine PivotTable hinzugefügt.  
  
3.  Beachten Sie, dass in Excel in der **PivotTable-Feldliste** die Measures **Date** und **Internet Sales** sowie die Tabellen **Customer**, **Date**, **Geography**, **Product**, **Product Category**, **Product Subcategory** und **Internet Sales** mit allen entsprechenden Spalten angezeigt werden.  
  
4.  Schließen Sie Excel, ohne die Arbeitsmappe zu speichern.  
  
#### So durchsuchen Sie das Modell mit der Internet Sales-Perspektive  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]auf das Menü **Modell** und dann auf **In Excel analysieren**.  
  
2.  Lassen Sie im Dialogfeld **In Excel analysieren** die Option **Aktueller Windows-Benutzer** aktiviert, wählen Sie im Dropdownlistenfeld **Perspektive** den Eintrag **Internet Sales** aus, und klicken Sie anschließend auf **OK**. Excel wird geöffnet.  
  
3.  Beachten Sie, dass in Excel in der **PivotTable-Feldliste** die Tabelle Customer aus der Feldliste ausgeschlossen ist.  
  
4.  Schließen Sie Excel, ohne die Arbeitsmappe zu speichern.  
  
## Durchsuchen mit Rollen  
Rollen sind wesentlicher Bestandteil sämtlicher tabellarischer Modelle. Benutzer können keine Daten mit Ihrem Modell aufrufen und analysieren, wenn sie nicht mindestens einer Rolle als Mitglieder hinzugefügt wurden. Die Funktion In Excel analysieren bietet eine Möglichkeit zum Testen der Rollen, die Sie definiert haben.  
  
#### So durchsuchen Sie das Modell mit der Internet Sales Manager-Benutzerrolle  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]auf das Menü **Modell** und dann auf **In Excel analysieren**.  
  
2.  Wählen Sie im Dialogfeld **In Excel analysieren** in **Geben Sie den Benutzernamen oder die Benutzerrolle zum Herstellen einer Verbindung mit dem Modell an** die Option **Rolle** aus, wählen Sie im Dropdownlistenfeld **Internet Sales Manager** aus, und klicken Sie anschließend auf **OK**.  
  
    Excel wird mit einer neuen Arbeitsmappe geöffnet. Es wird automatisch eine PivotTable erstellt. Die PivotTable-Feldliste enthält alle Datenfelder, die im neuen Modell verfügbar sind.  
      
3.  Schließen Sie Excel, ohne die Arbeitsmappe zu speichern.  
  
## Nächste Schritte  
Wenn Sie mit diesem Tutorial fortfahren möchten, wechseln Sie zur nächsten Lektion: [Lektion 14: Bereitstellen](../analysis-services/lesson-14-deploy.md).  
  
  
  
