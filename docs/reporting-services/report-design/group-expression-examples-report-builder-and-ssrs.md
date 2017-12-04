---
title: "Beispiele für Gruppierungsausdrücke (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data [Reporting Services], grouping
- grouping data
- expressions [Reporting Services], adding
- groups [Reporting Services], expressions
ms.assetid: 34cd0249-fc74-4cf2-ba11-7b072992bfd2
caps.latest.revision: "24"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: ce8b9f9e26b56846aaa2da95533d76ee4c422e8e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="group-expression-examples-report-builder-and-ssrs"></a>Beispiele für Gruppierungsausdrücke (Berichts-Generator und SSRS)
  In einem Datenbereich können Sie Daten nach einem einzelnen Feld gruppieren oder komplexe Ausdrücke erstellen, mit denen die Daten identifiziert werden, nach denen gruppiert wird. Komplexe Ausdrücke schließen Verweise auf mehrere Felder oder Parameter, Bedingungsanweisungen oder benutzerdefinierten Code ein. Wenn Sie für einen Datenbereich eine Gruppe definieren, fügen Sie diese Ausdrücke den **Gruppeneigenschaften** hinzu. Weitere Informationen finden Sie unter [Hinzufügen oder Löschen einer Gruppe in einem Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
 Um zwei oder mehr Gruppen zusammenzuführen, die auf einfachen Feldausdrücken basieren, fügen Sie jedes Feld der Gruppenausdrucksliste in der Gruppendefinition hinzu.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="examples-of-group-expressions"></a>Beispiele für Gruppenausdrücke  
 In der folgenden Tabelle sind Beispiele für Gruppenausdrücke aufgeführt, die Sie zum Definieren einer Gruppe verwenden können.  
  
|Description|expression|  
|-----------------|----------------|  
|Gruppieren nach dem `Region` -Feld.|`=Fields!Region.Value`|  
|Gruppieren Sie nach Nachnamen und Vornamen.|`=Fields!LastName.Value`<br /><br /> `=Fields!FirstName.Value`|  
|Gruppieren nach dem ersten Buchstaben des Nachnamens.|`=Fields!LastName.Value.Substring(0,1)`|  
|Gruppieren Sie auf Grundlage der Benutzerauswahl nach Parameter.<br /><br /> In diesem Beispiel muss der Parameter `GroupBy` auf einer verfügbaren Werteliste basieren, die eine gültige Auswahl für eine Gruppierung bietet.|`=Fields(Parameters!GroupBy.Value).Value`|  
|Gruppieren Sie nach drei separaten Altersgruppen:<br /><br /> "Unter 21", "Zwischen 21 und 50" und "Über 50".|`=IIF(First(Fields!Age.Value)<21,"Under 21",(IIF(First(Fields!Age.Value)>=21 AND First(Fields!Age.Value)<=50,"Between 21 and 50","Over 50")))`|  
|Gruppieren Sie nach vielen Altersgruppen. In diesem Beispiel wird benutzerdefinierter Code veranschaulicht, der in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET geschrieben ist und der eine Zeichenfolge für die folgenden Bereiche zurückgibt:<br /><br /> 25 oder darunter<br /><br /> 26 bis 50<br /><br /> 51 bis 75<br /><br /> Über 75|`=Code.GetRangeValueByAge(Fields!Age.Value)`<br /><br /> Benutzerdefinierter Code:<br /><br /> `Function GetRangeValueByAge(ByVal age As Integer) As String`<br /><br /> `Select Case age`<br /><br /> `Case 0 To 25`<br /><br /> `GetRangeValueByByAge = "25 or Under"`<br /><br /> `Case 26 To 50`<br /><br /> `GetRangeValueByByAge = "26 to 50"`<br /><br /> `Case 51 to 75`<br /><br /> `GetRangeValueByByAge = "51 to 75"`<br /><br /> `Case Else`<br /><br /> `GetRangeValueByByAge = "Over 75"`<br /><br /> `End Select`<br /><br /> `Return GetRangeValueByByAge`<br /><br /> `End Function`|  
  
## <a name="see-also"></a>Siehe auch  
 [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Benutzerdefinierter Code und Assemblyverweise in Ausdrücken in Berichts-Designer &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)  
  
  
