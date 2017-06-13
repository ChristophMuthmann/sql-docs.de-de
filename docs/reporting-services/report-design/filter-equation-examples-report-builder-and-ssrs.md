---
title: "Beispiele für Filtergleichungen (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filtering data [Reporting Services], filter equation examples
ms.assetid: 66bec93d-7c3b-4d4a-8cb6-7a7bb2f34ec6
caps.latest.revision: 18
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e6bbd95ac20afbeb00b331efa13492a0036fff20
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="filter-equation-examples-report-builder-and-ssrs"></a>Beispiele für Filtergleichungen (Berichts-Generator und SSRS)
  Zum Erstellen eines Filters müssen Sie mindestens eine Filtergleichung angeben. Eine Filtergleichung schließt einen Ausdruck, einen Datentyp, einen Operator und einen Wert ein. Dieses Thema enthält Beispiele für häufig verwendete Filter.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="filter-examples"></a>Beispiele für Filter  
 In der folgenden Tabelle werden Beispiele für Filtergleichungen dargestellt, die andere Datentypen und andere Operatoren verwenden. Der Bereich für den Vergleich wird von dem Berichtselement bestimmt, für das ein Filter definiert wird. Beispiel: Bei einem für ein Dataset definierten Filter bezeichnet **Erste % 10** die ersten 10 Prozent der Werte im Dataset. Im Falle eines für eine Gruppe definierten Filters bedeutet **Erste % 10** die ersten 10 Prozent der Werte in der Gruppe.  
  
|Einfacher Ausdruck|Datentyp|Operator|Wert|Description|  
|-----------------------|---------------|--------------|-----------|-----------------|  
|`[SUM(Quantity)]`|**Integer**|**>**|`7`|Schließt Datenwerte ein, die größer als 7 sind.|  
|`[SUM(Quantity)]`|**Integer**|**TOP N**|`10`|Schließt die ersten 10 Datenwerte ein.|  
|`[SUM(Quantity)]`|**Integer**|**TOP %**|`20`|Schließt die ersten 20 % der Datenwerte ein.|  
|`[Sales]`|**Text**|**>**|`=CDec(100)`|Schließt alle Werte des Typs System.Decimal (SQL-Datentyp "money") größer als $100 ein.|  
|`[OrderDate]`|**DateTime**|**>**|`2008-01-01`|Schließt alle Datumsangaben vom 1. Januar 2008 bis zum gegenwärtigen Datum ein.|  
|`[OrderDate]`|**DateTime**|**BETWEEN**|`2008-01-01`<br /><br /> `2008-02-01`|Schließt Datumsangaben vom 1. Januar 2008 bis zum 1. Februar 2008 einschließlich ein.|  
|`[Territory]`|**Text**|**LIKE**|`*east`|Alle Gebietsnamen, die auf "east" enden.|  
|`[Territory]`|**Text**|**LIKE**|`%o%th*`|Alle Gebietsnamen, die mit "North" und "South" beginnen.|  
|`=LEFT(Fields!Subcat.Value,1)`|**Text**|**IN**|`B, C, T`|Alle Unterkategoriewerte, die mit B, C oder T beginnen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Hinzufügen von Datasetfiltern, Datenbereichsfiltern und Gruppenfiltern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Datentypen in Ausdrücken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ausdrucksverwendungen in Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
