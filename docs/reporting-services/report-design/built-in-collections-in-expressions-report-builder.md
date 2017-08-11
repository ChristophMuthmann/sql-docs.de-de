---
title: "Integrierte Auflistungen in Ausdrücken (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 78d5e3b8-9320-4e4b-a025-e2de3cf7afa7
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ff834d00c915ae81179ff9b0bebed19e7c9ec6c1
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="built-in-collections-in-expressions-report-builder"></a>Integrierte Auflistungen in Ausdrücken (Berichts-Generator)
  Sie können Verweise auf die folgenden integrierten Auflistungen in einen Ausdruck in einem Bericht aufnehmen: Berichtselemente, Parameter, Felder, Datasets, Datenquellen, Variablen und integrierte Felder für globale Informationen wie Berichtsnamen. Nicht alle Auflistungen werden im Dialogfeld **Ausdruck** angezeigt. Die DataSets-Auflistung und die DataSources-Auflistung sind nur zur Laufzeit für veröffentlichte Berichte auf einem Berichtsserver verfügbar. Die ReportItems-Auflistung umfasst Textfelder in einem Berichtsbereich, z. B. Textfelder auf einer Seite oder in einem Seitenkopf.  
  
 Weitere Informationen finden Sie unter [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Collections"></a> Grundlegendes zu integrierten Auflistungen  
 In der folgenden Tabelle sind die integrierten Auflistungen aufgeführt, die beim Schreiben eines Ausdrucks verfügbar sind. Jede Zeile enthält den programmatischen Namen für die Auflistung, bei dem die Groß-/Kleinschreibung beachtet werden muss. Außerdem ist die Angabe enthalten, ob Sie über das Dialogfeld Ausdruck einen Verweis auf die Auflistung interaktiv hinzufügen können, ferner ein Beispiel und eine Beschreibung mit der Angabe, wann die Auflistungswerte initialisiert werden und verfügbar sind.  
  
|Integrierte Auflistung|Kategorie im Dialogfeld Ausdruck|Beispiel|Description|  
|--------------------------|-------------------------------------------|-------------|-----------------|  
|**Globale Variablen**|Integrierte Felder|`=Globals.ReportName`<br /><br /> `- or -`<br /><br /> `=Globals.PageNumber`|Stellt globale Variablen dar, die für Berichte nützlich sind, wie z. B. der Berichtsname oder die Seitenzahl. Immer verfügbar.<br /><br /> Weitere Informationen finden Sie unter [Integrierte globale Werte und Benutzerverweise &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).|  
|**Benutzer**|Integrierte Felder|`=User.UserID`<br /><br /> - oder -<br /><br /> `=User.Language`|Stellt eine Auflistung der Daten über den Benutzer dar, der den Bericht ausführt, z. B. die Spracheinstellung oder die Benutzer-ID. Immer verfügbar.<br /><br /> Weitere Informationen finden Sie unter [Integrierte globale Werte und Benutzerverweise &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).|  
|**Parameter**|Parameter|`=Parameters("ReportMonth").Value`<br /><br /> - oder -<br /><br /> `=Parameters!ReportYear.Value`|Stellt die Auflistung der Berichtsparameter dar, von denen jeder einwertig oder mehrwertig sein kann. Erst nach Abschluss der Verarbeitungsinitialisierung verfügbar. Weitere Informationen finden Sie unter [Verweise auf Parametersammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md).|  
|**Felder (**  *\<Dataset >* **)**|Felder|`=Fields!Sales.Value`|Stellt die Auflistung der im Bericht verfügbaren Felder des Datasets dar. Verfügbar, nachdem Daten aus einer Datenquelle in ein Dataset abgerufen wurden. Weitere Informationen finden Sie unter [Verweise auf Datasetfeld-Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-dataset-fields-collection-references-report-builder.md).|  
|**DataSets**|Nicht angezeigt|`=DataSets("TopEmployees").CommandText`|Stellt die Auflistung der Datasets dar, auf die im Text einer Berichtsdefinition verwiesen wird. Enthält nicht die Datenquellen, die nur in Seitenköpfen oder Seitenfüßen verwendet werden. Nicht verfügbar in der Vorschau. Weitere Informationen finden Sie unter [Verweise auf DataSources- und DataSets-Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-datasources-and-datasets-references-report-builder.md).|  
|**DataSources**|Nicht angezeigt|`=DataSources("AdventureWorks2012").Type`|Stellt die Auflistung der Datenquellen dar, auf die im Textkörper eines Berichts verwiesen wird. Enthält nicht die Datenquellen, die nur in Seitenköpfen oder Seitenfüßen verwendet werden. Nicht verfügbar in der Vorschau. Weitere Informationen finden Sie unter [Verweise auf DataSources- und DataSets-Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-datasources-and-datasets-references-report-builder.md).|  
|**Variablen**|`Variables`|`=Variables!CustomTimeStamp.Value`|Stellt die Auflistung von Berichtsvariablen und Gruppenvariablen dar. Weitere Informationen finden Sie unter [Verweise auf Berichts- und Gruppenvariablensammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md).|  
|**Berichtselemente**|Nicht angezeigt|`=ReportItems("Textbox1").Value`|Stellt die Auflistung von Textfeldern für ein Berichtselement dar. Diese Auflistung kann verwendet werden, um Elemente auf der Seite zusammenzufassen und sie in einen Seitenkopf oder einen Seitenfuß einzubeziehen. Weitere Informationen finden Sie unter [Verweise auf ReportItems-Auflistungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-reportitems-collection-references-report-builder.md).|  
  
##  <a name="Syntax"></a> Verwenden von Auflistungssyntax in einem Ausdruck  
 Wenn Sie von einem Ausdruck auf eine Auflistung verweisen möchten, können Sie die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Standardsyntax für ein Element in einer Auflistung verwenden. Die folgende Tabelle zeigt Beispiele für die Auflistungssyntax:  
  
|Syntax|Beispiel|  
|------------|-------------|  
|*Auflistung!Objektname.Eigenschaft*|`=Fields!Sales.Value`|  
|*Auflistung!Objektname("Eigenschaft")*|`=Fields!Sales("Value")`|  
|*Auflistung("Objektname").Eigenschaft*|`=Fields("Sales").Value`|  
|*Auflistung("Element")*|`=User("Language")`|  
|*Auflistung.Element*|`=User.Language`|  
  
## <a name="see-also"></a>Siehe auch  
 [Fügen Sie einen Ausdruck &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
