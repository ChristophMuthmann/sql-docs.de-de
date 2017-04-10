---
title: "Einf&#252;gen oder L&#246;schen einer Spalte (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: e9db79e2-7e7d-4359-a706-cb746c94182a
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Einf&#252;gen oder L&#246;schen einer Spalte (Berichts-Generator und SSRS)
  Sie können in einem paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Bericht Spalten einem Tablix-Datenbereich hinzufügen bzw. daraus entfernen. Der Tablix-Datenbereich kann eine Tabelle, eine Matrix oder eine Liste sein. Die folgenden Vorgehensweisen gelten nicht für Diagramm- und Messgerätdatenbereiche.  
  
 In Tablix-Datenbereichen können Spalten hinzugefügt werden, die mit einer Gruppe verknüpft sind (innerhalb einer Gruppe) oder die nicht mit einer Gruppe verknüpft sind (außerhalb einer Gruppe). Eine Spalte in einer Gruppe wiederholt sich einmal pro eindeutigem Gruppenwert. So wiederholt sich zum Beispiel eine Spalte in einer Gruppe, die auf dem Wert in einer Datenspalte mit Farbnamen basiert, einmal pro eindeutigem Farbnamen. Bei geschachtelten Gruppen kann sich die Spalte außerhalb der untergeordneten Gruppe, aber innerhalb der übergeordneten Gruppe befinden. In diesem Fall wiederholt sich die Zeile einmal für jeden eindeutigen Wert in der übergeordneten Gruppe.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## So wählen Sie einen Datenbereich aus und zeigen die Zeilen- und Spaltenziehpunkte an  
  
-   Klicken Sie in der Entwurfsansicht auf die obere linke Ecke des Tablix-Datenbereichs, sodass die Spalten- und Zeilenziehpunkte über und neben dem Datenbereich angezeigt werden.  
  
     Weitere Informationen zu Datenbereichen finden Sie unter [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
## So fügen Sie eine Spalte in einen ausgewählten Datenbereich ein  
  
-   Klicken Sie mit der rechten Maustaste auf einen Spaltenziehpunkt an der Stelle, an der Sie eine Spalte einfügen möchten. Klicken Sie auf **Spalte einfügen** und dann auf **Links** bzw. **Rechts**.  
  
     oder  
  
-   Klicken Sie mit der rechten Maustaste auf eine Zelle in dem Datenbereich, in dem Sie eine Spalte einfügen möchten. Klicken Sie auf **Spalte einfügen** und dann auf **Links** bzw. **Rechts**.  
  
## So löschen Sie eine Spalte aus einem ausgewählten Datenbereich  
  
-   Wählen Sie die Spalten aus, die Sie löschen möchten, klicken Sie mit der rechten Maustaste auf den Ziehpunkt für eine der ausgewählten Spalten, und klicken Sie dann auf **Spalten löschen**.  
  
     oder  
  
-   Klicken Sie mit der rechten Maustaste auf eine Zelle in dem Datenbereich, in dem Sie eine Spalte löschen möchten, und klicken Sie dann auf **Spalten löschen**.  
  
## So fügen Sie eine Spalte in eine Gruppe in einem ausgewählten Datenbereich ein  
  
-   Klicken Sie mit der rechten Maustaste auf eine Spaltengruppenzelle im Spaltengruppenbereich eines Tablix-Datenbereichs, in dem Sie eine Spalte einfügen möchten, klicken Sie auf **Spalte einfügen**, und klicken Sie dann auf **Links - Außerhalb von Gruppe**, **Links - Innerhalb von Gruppe**, **Rechts - Innerhalb von Gruppe** oder **Rechts - Außerhalb von Gruppe**.  
  
     Die Spalte wird entweder innerhalb oder außerhalb der Gruppe eingefügt, die durch die Spaltengruppenzelle, auf die Sie geklickt haben, repräsentiert wird.  
  
## So löschen Sie eine Spalte aus einer Gruppe in einem ausgewählten Datenbereich  
  
-   Klicken Sie mit der rechten Maustaste auf eine Spaltengruppenzelle im Spaltengruppenbereich eines Tablix-Datenbereichs, aus dem Sie eine Spalte löschen möchten, und klicken Sie dann auf **Spalten löschen**.  
  
## Siehe auch  
 [Grundlegendes zu Gruppen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [Tablix-Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tabellen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrizen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)      
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  