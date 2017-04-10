---
title: "Erstellen von rekursiven Hierarchiegruppen (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Erstellen von rekursiven Hierarchiegruppen (Berichts-Generator und SSRS)
Legen Sie den Gruppenausdruck des Datenbereichs basierend auf dem untergeordneten Feld und die übergeordnete Eigenschaft basierend auf dem übergeordneten Feld fest, um rekursive Daten in paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Berichten anzuzeigen (wobei die Beziehung zwischen übergeordnetem und untergeordnetem Feld von Feldern im Dataset dargestellt wird).  
  
 Eine hierarchische Anzeige von Daten wird häufig für rekursive Hierarchiegruppen verwendet, z. B. für Angestellte in einem Unternehmensdiagramm. Das Dataset enthält eine Liste mit Mitarbeitern und Managern, wobei die Namen der Manager auch in der Mitarbeiterliste enthalten sind.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Erstellen von rekursiven Hierarchien  
 Sie müssen den Gruppenausdruck auf das Feld festlegen, das die untergeordneten Daten enthält, und die übergeordnete Eigenschaft der Gruppe auf das Feld, das die übergeordneten Daten enthält, um eine rekursive Hierarchie in einem Tablix-Datenbereich zu erstellen. Legen Sie z.B. für ein Dataset, das Felder für die Mitarbeiter-ID und die Manager-ID enthält (wobei die Mitarbeiter an die Manager berichten) den Gruppenausdruck auf die Mitarbeiter-ID und die übergeordnete Eigenschaft auf die Manager-ID fest.  
  
 Eine Gruppe, die als rekursive Hierarchie definiert ist (also eine Gruppe, die die übergeordnete Eigenschaft verwendet), kann nur über einen einzelnen Gruppenausdruck verfügen. Mit der **Level** -Funktion können Sie die Auffüllung in Textfeldern bestimmen, um die Mitarbeiternamen entsprechend ihrer Ebene in der Hierarchie einzurücken.  
  
 Weitere Informationen finden Sie unter [Hinzufügen oder Löschen einer Gruppe in einem Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) und unter [Erstellen einer rekursiven Hierarchiegruppe &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md).  
  
### Aggregatfunktionen zur Unterstützung der Rekursion  
 Sie können Reporting Services-Aggregatfunktionen verwenden, die den Parameter *Rekursiv* akzeptieren, um Zusammenfassungsdaten für eine rekursive Hierarchie zu berechnen. Die folgenden Funktionen akzeptieren **Recursive** als Parameter: [Sum](../../reporting-services/report-design/sum-function-report-builder-and-ssrs.md), [Avg](../../reporting-services/report-design/avg-function-report-builder-and-ssrs.md), [Count](../../reporting-services/report-design/count-function-report-builder-and-ssrs.md), [CountDistinct](../../reporting-services/report-design/countdistinct-function-report-builder-and-ssrs.md), [CountRows](../../reporting-services/report-design/countrows-function-report-builder-and-ssrs.md), [Max](../../reporting-services/report-design/max-function-report-builder-and-ssrs.md), [Min](../../reporting-services/report-design/min-function-report-builder-and-ssrs.md), [StDev](../../reporting-services/report-design/stdev-function-report-builder-and-ssrs.md), [StDevP](../../reporting-services/report-design/stdevp-function-report-builder-and-ssrs.md), [Sum](../../reporting-services/report-design/sum-function-report-builder-and-ssrs.md), [Var](../../reporting-services/report-design/var-function-report-builder-and-ssrs.md)und [VarP](../../reporting-services/report-design/varp-function-report-builder-and-ssrs.md). Weitere Informationen finden Sie unter [Aggregatfunktionsreferenz &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md).  
  
## Siehe auch  
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Tablix-Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Aggregatfunktionsreferenz &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md)   
 [Tabellen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrizen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)    
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  