---
title: Konfigurieren von Measureeigenschaften | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f853302ed7504d18aae8c962adb3ab3f14730bae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configure-measure-properties"></a>Konfigurieren von Measureeigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Measures haben Eigenschaften, die es Ihnen ermöglichen, die Funktionsweise von Measures zu definieren und die Anzeige von Measures für Benutzer zu steuern.  
  
 Sie können beim Erstellen oder Bearbeiten eines Cubes oder Measures Eigenschaften in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] festlegen. Sie können sie mit MDX oder AMO auch programmgesteuert festlegen. Einzelheiten finden Sie unter [Erstellen von Measures und Measuregruppen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md), [CREATE MEMBER-Anweisung &#40;MDX&#41;](../../mdx/mdx-data-definition-create-member.md) oder [Programmieren von AMO OLAP Basic-Objekten](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-basic-objects.md).  
  
## <a name="measure-properties"></a>Eigenschaften von Measures  
 Measures erben bestimmte Eigenschaften von der Measuregruppe, zu der sie gehören, sofern diese Eigenschaften nicht auf Measureebene überschrieben werden. Measureeigenschaften bestimmen die Art der Aggregation von Measures, ihren Datentyp, den dem Benutzer angezeigten Namen, den Anzeigeordner von Measures, die Formatzeichenfolge, mögliche Measureausdrücke, zugrunde liegende Quellspalten und die Sichtbarkeit für Benutzer.  
  
|Eigenschaft|Definition|  
|--------------|----------------|  
|**AggregateFunction**|Erforderlich. Bestimmt, wie Measures aggregiert werden. **Sum** ist die Standardaggregation. Weitere Informationen und eine Beschreibung zu den einzelnen Funktionen finden Sie unter [Use Aggregate Functions](../../analysis-services/multidimensional-models/use-aggregate-functions.md) .|  
|**DataType**|Erforderlich. Gibt den Datentyp der zugrunde liegenden Faktentabellenspalte an, an die das Measure gebunden ist. Dieser Wert wird standardmäßig aus der Quellspalte geerbt.|  
|**Beschreibung**|Stellt eine Beschreibung des Measures bereit, das in Clientanwendungen möglicherweise offen gelegt wird.|  
|**DisplayFolder**|Gibt den Ordner an, in dem das Measure angezeigt wird, wenn Benutzer die Verbindung zu dem Cube erstellen. Wenn ein Cube viele Measures enthält, können Sie sie mithilfe von Anzeigeordnern kategorisieren und dem Benutzer das Durchsuchen erleichtern.|  
|**FormatString**|Sie können das Format, das für die Anzeige der Measurewerte für Benutzer verwendet wird, mithilfe der **FormatString** -Eigenschaft des Measures auswählen.<br /><br /> Obwohl eine Liste der Anzeigeformate in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]verfügbar ist, können Sie viele zusätzliche Formate angeben, die nicht in der Liste enthalten sind. Sie können jedes beliebige benannte oder benutzerdefinierte Format angeben, das in Microsoft Visual Basic gültig ist.|  
|**ID**|Erforderlich. Zeigt den eindeutigen Bezeichner (ID) des Measures an. Diese Eigenschaft ist schreibgeschützt.|  
|**MeasureExpression**|Gibt einen eingeschränkten MDX-Ausdruck an, der den Wert des Measures definiert. Der Ausdruck wird vor der Aggregation auf der Blattebene ausgewertet und ermöglicht die Gewichtung eines Werts. Beispielsweise bei der Währungsumrechnung, bei der ein Betrag der Verkäufe nach dem Wechselkurs gewichtet wird.|  
|**Name**|Erforderlich. Gibt den Namen des Measures an.|  
|**Quelle**|Erforderlich. Gibt die Spalte in der Datenquellensicht an, an die das Measure gebunden ist. Siehe [Datenquellen und Bindungen &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).|  
|**Visible**|Bestimmt die Sichtbarkeit des Measures in Clientanwendungen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Measuregruppeneigenschaften](../../analysis-services/multidimensional-models/configure-measure-group-properties.md)   
 [Ändern von Measures](../../analysis-services/lesson-3-1-modifying-measures.md)  
  
  
