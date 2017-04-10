---
title: "Interaktive Sortierung (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: 00cafed5-1a3c-4ce0-a1fb-ff1e2613f495
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 7
---
# Interaktive Sortierung (Berichts-Generator und SSRS)
  Sie können Schaltflächen für die interaktive Sortierung hinzufügen, um Benutzern das Umschalten zwischen der auf- und absteigenden Reihenfolge für Zeilen in einer Tabelle oder für Zeilen und Spalten in einer Matrix zu ermöglichen. Die häufigste Verwendung der interaktiven Sortierung besteht im Hinzufügen einer Sortierungsschaltfläche für die einzelnen Spaltenkopfzeilen. Benutzer können dann die Spalte auswählen, anhand derer die Sortierung erfolgen soll.  
  
 Interaktive Sortierungsschaltflächen können grundsätzlich jedem Textfeld hinzugefügt werden. Beispielsweise können Sie für ein Textfeld in einer Zeile außerhalb einer Zeilengruppe eine Sortierung für die übergeordneten Gruppenzeilen oder -spalten sowie für untergeordneten Gruppenzeilen oder -spalten oder für die Detailzeilen oder -spalten angeben. Sie können auch Felder in einem Gruppenausdruck kombinieren und eine Sortierung anhand mehrerer Felder durchführen.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Beim Hinzufügen einer interaktiven Sortierung müssen folgende Elemente angegeben werden:  
  
-   **Sortierungselement:** z. B. Zeilen oder Spalten.  
  
-   **Sortierungskriterium:** z. B. ein Feld, das in einer Tabellenspalte angezeigt wird. ein Feld, das nicht angezeigt wird.  
  
-   **Sortierungskontext:** Sie können z. B. nach Zeilen sortieren, die Zeilengruppen zugeordnet sind, oder nach Spalten, die Spaltengruppen zugeordnet sind. Ebenso können Sie nach Detailzeilen oder nach untergeordneten Gruppen in einer übergeordneten Gruppe sortieren sowie nach über- und untergeordneten Gruppen.  
  
-   **Textfeld für die Sortierungsschaltfläche:** z. B. Spaltenkopf oder Gruppenzeilenkopf.  
  
-   **Synchronisierung der Sortierung mehrerer Datenbereiche:** Sie können einen Bericht so gestalten, dass beim Umschalten der Sortierreihenfolge andere Datenbereiche mit dem gleichen Vorgänger ebenfalls neu sortiert werden.  
  
 Eine Schritt-für-Schritt-Anleitung finden Sie unter [Hinzufügen einer interaktiven Sortierung zu einer Tabelle oder Matrix &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md).  
  
 In der folgenden Tabelle werden die Funktionen von interaktiven Sortierschaltflächen zusammengefasst.  
  
|Aktion|Sortierungselement|Positionierung der Sortierschaltfläche|Sortierungskriterium|Sortierungsbereich|  
|------------|------------------|----------------------------------|---------------------|----------------|  
|Sortierung von Detailzeilen für eine Tabelle ohne Gruppen|Details|Spaltenkopfzeile|Datasetfeld, das an diese Spalte gebunden ist|Datenbereich|  
|Sortieren von Gruppeninstanzen der obersten Ebene für eine Matrix|Gruppen|Spaltenkopfzeile|Gruppierungsausdruck für übergeordnete Gruppe|Datenbereich|  
|Sortierung von Detailzeilen für eine untergeordnete Gruppe in einer Tabelle|Details|Untergeordnete Gruppenkopfzeile|Datasetfeld für die Sortierung|Untergeordnete Gruppe|  
|Sortieren von Zeilen für mehrere Zeilengruppen und Detailzeilen in einer Tabelle|Gruppen (Neudefinierung des Gruppenausdrucks erforderlich)|Spaltenkopfzeile|Aggregat des Datasetfelds für die Sortierung|Datenbereich|  
|Synchronisieren der Sortierreihenfolge für mehrere Datenbereiche|Gruppen|Spaltenkopf (Standard)|Gruppierungsausdruck|Dataset|  
  
 Die interaktive Sortierung wird vom Berichtsprozessor nach Anwendung aller Datenbereichs- und Gruppensortierungsausdrücke angewendet. Weitere Informationen finden Sie unter [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
## Hinzufügen der interaktiven Sortierung für mehrere Gruppen  
 Sie können einer Tabelle mit geschachtelten Zeilengruppen, die jeweils auf einem Datasetfeld basieren, eine Schaltfläche für die interaktive Sortierung hinzufügen, um übergeordnete Gruppenwerte, untergeordnete Gruppenwerte oder Detailzeilen zu sortieren. Dabei können Sie Benutzern auch die Möglichkeit geben, die Tabelle sowohl nach übergeordneten als auch nach untergeordneten Werten zu sortieren, ohne mehrfach auf die Schaltfläche klicken zu müssen.  
  
 Hierzu müssen Sie die Tabelle umgestalten, um nach einem Ausdruck zu gruppieren, der mehrere Felder kombiniert. Wenn die Werte in der ursprünglichen Tabelle für ein Dataset mit Lagerbeständen beispielsweise erst nach der Größe und anschließend nach der Farbe sortiert werden, können Sie die beiden Kriterien mithilfe eines Gruppierungsausdrucks in einer Gruppe zusammenfassen. Weitere Informationen finden Sie unter [Hinzufügen einer interaktiven Sortierung zu einer Tabelle oder Matrix &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md).  
  
## Siehe auch  
 [Sortieren von Daten in einem Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Hinzufügen einer interaktiven Sortierung zu einer Tabelle oder Matrix &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  