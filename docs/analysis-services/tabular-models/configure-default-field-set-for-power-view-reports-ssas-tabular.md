---
title: "Konfigurieren eines Standardfeldsatzes f&#252;r Power View-Berichte (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ql12.asvs.bidtoolset.deffieldset.f1"
ms.assetid: 6836b42f-28b8-4a98-a86d-2c3c109f0189
caps.latest.revision: 7
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Konfigurieren eines Standardfeldsatzes f&#252;r Power View-Berichte (SSAS – tabellarisch)
  Ein Standardfeldsatz ist eine vordefinierte Liste von Spalten und Measures, die einem [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] -Berichtszeichenbereich automatisch hinzugefügt werden, wenn Sie in der Berichtsfeldliste die Tabelle auswählen. Ersteller tabellarischer Modelle können ein Standardfeld generieren, das für die Berichtsautoren, die das Modell für ihre Berichte verwenden, auf die Eliminierung redundanter Schritte abzielt. Wenn Sie beispielsweise wissen, dass die meisten Berichtsautoren, die Kundenkontaktdaten verwenden, immer einen Kontaktnamen, eine primäre Telefonnummer, eine E-Mail-Adresse und einen Unternehmensnamen benötigen, können Sie diese Spalten im Voraus auswählen, sodass sie dem Berichtszeichenbereich immer hinzugefügt werden, sobald der Autor auf die Kundenkontakttabelle klickt.  
  
> [!NOTE]  
>  Ein Standardfeldsatz gilt nur für ein tabellarisches Modell, das in [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]als Datenmodell verwendet wird. Standardfeldsätze werden in Excel-Pivotberichten nicht unterstützt.  
  
## Erstellen eines Standardfeldsatzes  
 Sie können bestimmen, welche Felder ggf. standardmäßig eingefügt werden, wenn eine bestimmte Tabelle in [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]ausgewählt wird. Sie können auch die Reihenfolge bestimmen, in der die Felder in der Liste angezeigt werden. Sie können einen Standardfeldsatz angeben, indem Sie Berichtseigenschaften im tabellarischen Modellprojekt festlegen.  
  
#### So fügen Sie einen Standardfeldsatz hinzu  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] auf die Tabelle (Registerkarte), für die Sie eine Standardfeldliste konfigurieren.  
  
2.  Klicken Sie im **Eigenschaftenfenster** in der Eigenschaft **Standardfeldsatz** auf **Zum Bearbeiten klicken**.  
  
3.  Wählen Sie im Standardfeldsatz ein oder mehrere Felder aus. Sie können jedes beliebige Feld, einschließlich Measures, in der Tabelle auswählen. Halten Sie die UMSCHALTTASTE gedrückt, um mehrere aufeinander folgende Felder auszuwählen, bzw. die STRG-TASTE, um einzelne Felder auszuwählen.  
  
4.  Klicken Sie auf **Hinzufügen** , um die Felder dem Standardfeldsatz hinzuzufügen.  
  
5.  Mithilfe der NACH-OBEN-TASTE und der NACH-UNTEN-TASTE können Sie die Reihenfolge in der Feldliste festlegen. Felder werden dem Bericht in der Reihenfolge hinzugefügt, in der sie im Feldsatz definiert sind.  
  
6.  Wiederholen Sie diese Schritte für weitere Tabellen in der Arbeitsmappe.  
  
## Nächster Schritt  
 Nach dem Erstellen eines Standardfeldsatzes können Sie die Benutzerfreundlichkeit des Berichtsentwurfs weiter beeinflussen, indem Sie Standardbezeichnungen, Standardbilder, Standardgruppenverhalten oder die Anordnung von Zeilen mit gleichem Wert gruppiert in einer Zeile oder einzeln angeben. Weitere Informationen finden Sie unter [Konfigurieren von Tabellenverhaltenseigenschaften für Power View-Berichte &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/configure-table-behavior-properties-for-power-view-reports-ssas-tabular.md).  
  
  