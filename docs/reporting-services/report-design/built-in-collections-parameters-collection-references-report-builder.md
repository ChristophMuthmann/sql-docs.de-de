---
title: Parameter-Auflistungsverweise (Berichts-Generator und SSRS) | Microsoft Docs
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
ms.assetid: c4b47e15-0484-4c13-9182-898db825f01f
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 17698a3c268e824d2f638042b71b3ec21f994e86
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="built-in-collections---parameters-collection-references-report-builder"></a>Integrierte Auflistungen - Verweise auf Parameters-Auflistungen (Berichts-Generator)
  Berichtsparameter gehören zu den integrierten Auflistungen, auf die Sie aus einem Ausdruck heraus verweisen können. Indem Sie Parameter in einen Ausdruck einschließen, können Sie die Berichtsdaten und die Darstellung von Berichten anhand der Auswahlen eines Benutzers anpassen. Ausdrücke können verwendet werden, für jede Eigenschaft eines Berichtselements oder Text-Eigenschaft, die bereitstellt der (*Fx*) oder \< **Ausdruck**> Option. Ausdrücke werden auch zum Steuern des Berichtsinhalts und der Darstellung eines Berichts auf andere Weise verwendet. Weitere Informationen finden Sie unter [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md).  
  
 Wenn Sie Parameterwerte mit Dataset-Feldwerten zur Laufzeit vergleichen, müssen die Datentypen der beiden verglichenen Elemente identisch sein. Berichtsparameter können einen der folgenden Typen aufweisen: Boolean, DateTime, Integer, Float oder Text (steht für den zugrunde liegenden Datentyp String). Es kann erforderlich sein, dass Sie den Datentyp des Parameterwerts konvertieren, damit er dem Datasetwert entspricht. Weitere Informationen finden Sie unter [Datentypen in Ausdrücken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md).  
  
 Wenn Sie einen Parameterverweis in einen Ausdruck einfügen möchten, müssen Sie wissen, wie die korrekte Syntax für den Parameterverweis angegeben wird. Diese variiert je nachdem, ob der Parameter ein ein- oder mehrwertiger Parameter ist.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Single"></a> Verwenden von einwertigen Parametern in Ausdrücken  
 Die folgende Tabelle enthält Beispiele für die zu verwendende Syntax zum Verweisen auf einwertige Parameter beliebigen Datentyps in einem Ausdruck.  
  
|Beispiel|Description|  
|-------------|-----------------|  
|`=Parameters!` *\<ParameterName >*`.IsMultiValue`|Gibt **False**zurück.<br /><br /> Überprüft, ob ein Parameter mehrwertig ist. Wenn **True**zurückgegeben wird, ist der Parameter mehrwertig und stellt eine Auflistung von Objekten dar. Wenn **FALSE**zurückgegeben wird, ist der Parameter einwertig und stellt ein einzelnes Objekt dar.|  
|`=Parameters!` *\<ParameterName >*`.Count`|Gibt den Ganzzahlwert 1 zurück. Für einwertige Parameter ist der Wert stets 1.|  
|`=Parameters!` *\<ParameterName >*`.Label`|Gibt die Parameterbezeichnung zurück, die häufig als Anzeigename in einer Dropdownliste der verfügbaren Werte verwendet wird.|  
|`=Parameters!` *\<ParameterName >*`.Value`|Gibt den Parameterwert zurück. Wenn die Label-Eigenschaft nicht festgelegt ist, wird dieser Wert in der Dropdownliste der verfügbaren Werte angezeigt.|  
|`=CStr(Parameters!`  *\<ParameterName >*`.Value)`|Gibt den Parameterwert als Zeichenfolge zurück.|  
|`=Fields(Parameters!` *\<ParameterName >*`.Value).Value`|Gibt den Wert für das Feld zurück, das den gleichen Namen wie der Parameter besitzt.|  
  
 Weitere Informationen zum Verwenden von Parametern in einem Filter finden Sie unter [Hinzufügen von Datasetfiltern, Datenbereichsfiltern und Gruppenfiltern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md).  
  
##  <a name="Multi"></a> Verwenden eines mehrwertigen Parameters in einem Ausdruck  
 Die folgende Tabelle enthält Beispiele für die zu verwendende Syntax zum Verweisen auf mehrwertige Parameter beliebigen Datentyps in einem Ausdruck.  
  
|Beispiel|Description|  
|-------------|-----------------|  
|`=Parameters!` *\<MultivalueParameterName >*`.IsMultiValue`|Gibt **True** oder **False**zurück.<br /><br /> Überprüft, ob ein Parameter mehrwertig ist. Wenn **True**zurückgegeben wird, ist der Parameter mehrwertig und stellt eine Auflistung von Objekten dar. Wenn **FALSE**zurückgegeben wird, ist der Parameter einwertig und stellt ein einzelnes Objekt dar.|  
|`=Parameters!` *\<MultivalueParameterName >*`.Count`|Gibt eine ganze Zahl zurück.<br /><br /> Bezieht sich auf die Anzahl der Werte. Für einwertige Parameter ist der Wert stets 1. Für mehrwertige Parameter ist der Wert 0 oder höher.|  
|`=Parameters!` *\<MultivalueParameterName >*`.Value(0)`|Gibt den ersten Wert eines mehrwertigen Parameters zurück.|  
|`=Parameters!` *\<MultivalueParameterName >* `.Value(Parameters!`  *\<MultivalueParameterName >*`.Count-1)`|Gibt den letzten Wert eines mehrwertigen Parameters zurück.|  
|`=Split("Value1,Value2,Value3",",")`|Gibt ein Array von Werten zurück.<br /><br /> Erstellt ein Array von Werten für einen mehrwertigen **String** -Parameter. Sie können ein beliebiges Trennzeichen im zweiten Parameter von Split verwenden. Mit diesem Ausdruck können Standardwerte für einen mehrwertigen Parameter festgelegt werden oder ein mehrwertiger Parameter zum Senden an einen Unterbericht oder Drillthroughbericht erstellt werden.|  
|`=Join(Parameters!` *\<MultivalueParameterName >*`.Value,", ")`|Gibt eine **Zeichenfolge** zurück, die eine Liste von durch Trennzeichen getrennten Werten in einem mehrwertigen Parameter enthält. Sie können ein beliebiges Trennzeichen im zweiten Parameter von Join verwenden.|  
  
 Weitere Informationen zur Verwendung von Parametern in einem Filter finden Sie unter [Berichtsparameter &#40; Berichts-Generator und Berichts-Designer &#41; ](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Häufig verwendete Filter &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md)   
 [Fügen Sie hinzu, ändern oder löschen Sie einen Berichtsparameter &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Lernprogramm: Hinzufügen eines Parameters zum Bericht &#40; Berichts-Generator &#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Lernprogramme für den Berichts-Generator](../../reporting-services/report-builder-tutorials.md)   
 [Integrierte Auflistungen in Ausdrücken &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)  
  
  
