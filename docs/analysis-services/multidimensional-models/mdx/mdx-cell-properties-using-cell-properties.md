---
title: Verwenden von Zelleigenschaften (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- intrinsic cell properties [MDX]
- cells [MDX]
- cell properties [MDX]
- CELL PROPERTIES keyword
ms.assetid: a593c74d-8c5e-485e-bd92-08f9d22451d4
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d66dddc93eb3293ea79d306095aa21bf78f4ea58
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-cell-properties---using-cell-properties"></a>MDX-Cell Properties - Verwenden von Zelleneigenschaften
  Zelleigenschaften in MDX (Multidimensional Expressions) enthalten Informationen zum Inhalt und Format von Zellen in einer mehrdimensionalen Datenquelle, wie einem Cube.  
  
 MDX unterstützt das CELL PROPERTIES-Schlüsselwort in einer MDX-Anweisung zum Abrufen von systeminternen Zelleigenschaften. Systeminterne Zelleigenschaften werden am häufigsten für die visuelle Darstellung von Zellendaten verwendet.  
  
## <a name="cell-properties-keyword-syntax"></a>Syntax des CELL PROPERTIES-Schlüsselworts  
 Das **CELL PROPERTIES** -Schlüsselwort der MDX- **SELECT** -Anweisung hat folgende Syntax:  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
[<cell_props>]  
```  
  
 Die folgende Syntax zeigt das Format des `<cell_props>` -Werts und zeigt, wie für diesen Wert das **CELL PROPERTIES** -Schlüsselwort zusammen mit intrinsischen Zelleigenschaften verwendet wird:  
  
```  
<cell_props> ::= CELL PROPERTIES <property> [, <property>...]  
```  
  
## <a name="supported-intrinsic-cell-properties"></a>Unterstützte systeminterne Zelleigenschaften  
 In der folgenden Tabelle sind die unterstützten systeminternen Zelleigenschaften aufgelistet, die im `<property>` -Wert verwendet werden.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**ACTION_TYPE**|Eine Bitmaske, die die Arten der Aktionen für die Zelle angibt. Diese Eigenschaft kann einen der folgenden Werte haben:<br /><br /> **MDACTION_TYPE_URL**<br /><br /> **MDACTION_TYPE_HTML**<br /><br /> **MDACTION_TYPE_STATEMENT**<br /><br /> **MDACTION_TYPE_DATASET**<br /><br /> **MDACTION_TYPE_ROWSET**<br /><br /> **MDACTION_TYPE_COMMANDLINE**<br /><br /> **MDACTION_TYPE_PROPRIETARY**<br /><br /> **MDACTION_TYPE_REPORT**<br /><br /> **MDACTION_TYPE_DRILLTHROUGH**<br /><br /> <br /><br /> Hinweis: Drillthroughaktionen werden nicht für Abfragen eingeschlossen, die in der WHERE-Klausel eine Menge enthalten.|  
|**BACK_COLOR**|Die Hintergrundfarbe zum Anzeigen der **VALUE** - oder der **FORMATTED_VALUE** -Eigenschaft. Weitere Informationen finden Sie unter [FORE_COLOR und BACK_COLOR – Inhalte &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md).|  
|**CELL_ORDINAL**|Die Ordinalzahl der Zelle im Dataset.|  
|**FONT_FLAGS**|Die Bitmaske, die Auswirkungen auf die Schriftart detailliert angibt. Der Wert ist das Ergebnis einer bitweisen OR-Operation von einem oder mehreren der folgenden Konstanten:<br /><br /> **MDFF_BOLD** = 1<br /><br /> **MDFF_ITALIC** = 2<br /><br /> **MDFF_UNDERLINE** = 4<br /><br /> **MDFF_STRIKEOUT** = 8<br /><br /> <br /><br /> Der Wert 5 stellt z.B. die Kombination der Schriftarteffekte Fett (**MDFF_BOLD**) und Unterstrichen (**MDFF_UNDERLINE**) dar.|  
|**FONT_NAME**|Die Schriftart, die zum Anzeigen der Eigenschaft **VALUE** oder **FORMATTED_VALUE** verwendet werden sollte.|  
|**FONT_SIZE**|Die Schriftgröße, die zum Anzeigen der Eigenschaft **VALUE** oder **FORMATTED_VALUE** verwendet werden sollte.|  
|**FORE_COLOR**|Die Vordergrundfarbe zum Anzeigen der **VALUE** - oder **FORMATTED_VALUE** -Eigenschaft. Weitere Informationen finden Sie unter [FORE_COLOR und BACK_COLOR – Inhalte &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md).|  
|**FORMAT**|Identisch mit **FORMAT_STRING**.|  
|**FORMAT_STRING**|Die Formatzeichenfolge, mit der der Wert der **FORMATTED_VALUE** -Eigenschaft erstellt wird. Weitere Informationen finden Sie unter [FORMAT_STRING-Inhalt &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md).|  
|**FORMATTED_VALUE**|Die Zeichenfolge, die eine formatierte Anzeige der **VALUE** -Eigenschaft darstellt.|  
|**LANGUAGE**|Das Gebietsschema, in dem **FORMAT_STRING** angewendet wird. **LANGUAGE** wird i. d. R. zur Währungskonvertierung verwendet.|  
|**UPDATEABLE**|Ein Wert, der angibt, ob die Zelle aktualisiert werden kann. Diese Eigenschaft kann einen der folgenden Werte haben:|  
||**MD_MASK_ENABLED** (0x00000000) Die Zelle kann aktualisiert werden.|  
||**MD_MASK_NOT_ENABLED** (0x10000000) Die Zelle kann nicht aktualisiert werden.|  
||**CELL_UPDATE_ENABLED** (0x00000001) Die Zelle kann in das Cellset aktualisiert werden.|  
||**CELL_UPDATE_ENABLED_WITH_UPDATE** (0x00000002) Die Zelle kann mit einer UPDATE-Anweisung aktualisiert werden. Das Update kann einen Fehler erzeugen, wenn eine Blattzelle aktualisiert werden soll, für die der Schreibzugriff nicht aktiviert ist.|  
||**CELL_UPDATE_NOT_ENABLED_FORMULA** (0x10000001) Die Zelle kann nicht aktualisiert werden, weil sie in ihren Koordinaten ein berechnetes Element hat (die Zelle wurde mit einer Menge in der WHERE-Klausel abgerufen). Eine Zelle kann selbst dann aktualisiert werden, wenn sich eine Formel oder eine berechnete Zelle auf den Wert der Zelle auswirkt (sich irgendwo im Verlauf des Aggregationspfades befindet). In diesem Szenario ist der endgültige Wert der Zelle möglicherweise nicht mit dem aktualisierten Wert identisch, weil sich die Berechnung auf das Ergebnis ausgewirkt hat.|  
||**CELL_UPDATE_NOT_ENABLED_NONSUM_MEASURE** (0x10000002) Die Zelle kann nicht aktualisiert werden, weil Nichtsummenmeasures (Count, Min, Max, Distinct Count, semiadditive Measures) nicht aktualisiert werden können.|  
||**CELL_UPDATE_NOT_ENABLED_NACELL_VIRTUALCUBE** (0x10000003) Die Zelle kann nicht aktualisiert werden, weil es die Zelle nicht gibt, denn sie befindet sich am Schnittpunkt eines Measure- und eines Dimensionselements, die nicht mit der Measuregruppe des Measures verknüpft sind.|  
||**CELL_UPDATE_NOT_ENABLED_SECURE** (0x10000005) Die Zelle kann nicht aktualisiert werden, weil sie geschützt ist.|  
||**CELL_UPDATE_NOT_ENABLED_CALCLEVEL** (0x10000006) Für die zukünftige Verwendung reserviert.|  
||**CELL_UPDATE_NOT_ENABLED_CANNOTUPDATE** (0x10000007) Die Zelle kann wegen interner Gründe nicht aktualisiert werden.|  
||**CELL_UPDATE_NOT_ENABLED_INVALIDDIMENSIONTYPE** (0x10000009) Die Zelle kann nicht aktualisiert werden, weil Aktualisieren in Miningmodell-, indirekten oder Data Mining-Dimensionen nicht unterstützt wird.|  
|**VALUE**|Der unformatierte Wert der Zelle.|  
  
 Nur die Zelleigenschaften **CELL_ORDINAL**, **FORMATTED_VALUE**und **VALUE** werden benötigt. Alle Zelleigenschaften, intrinsische wie anbieterspezifische, sind einschließlich ihrer Datentypen und der Anbieterunterstützung im **PROPERTIES** -Schemarowset definiert. Weitere Informationen zum **PROPERTIES** -Schemarowset finden Sie unter [MDSCHEMA_PROPERTIES-Rowset](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-properties-rowset.md).  
  
 Wenn das Schlüsselwort **CELL PROPERTIES** nicht verwendet wird, sind die zurückgegebenen Zelleigenschaften standardmäßig **VALUE**, **FORMATTED_VALUE**und **CELL_ORDINAL** (in dieser Reihenfolge). Ist das **CELL PROPERTIES** -Schlüsselwort angegeben, werden nur die Zelleigenschaften zurückgegeben, die explizit mit dem Schlüsselwort angegeben sind.  
  
 Das folgende Beispiel zeigt die Verwendung des **CELL PROPERTIES** -Schlüsselworts in einer MDX-Abfrage:  
  
```  
SELECT  
   {[Measures].[Reseller Gross Profit]} ON COLUMNS,  
   {[Reseller].[Reseller Type].[Reseller Name].Members} ON ROWS  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORMAT_STRING, FORE_COLOR, BACK_COLOR  
```  
  
 Für MDX-Abfragen, die vereinfachte Rowsets zurückgeben, werden keine Zelleigenschaften zurückgegeben. In diesem Fall wird jede Zelle so dargestellt, als würde nur die Zelleigenschaft **FORMATTED_VALUE** zurückgegeben.  
  
## <a name="setting-cell-properties"></a>Festlegen von Zelleigenschaften  
 Zelleigenschaften können in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] an verschiedenen Orten festgelegt werden. Beispielsweise kann die Eigenschaft Formatzeichenfolge für reguläre Measures auf der Registerkarte Cubestruktur des Cube-Editors in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]festgelegt werden. Die gleiche Eigenschaft kann für im Cube definierte berechnete Measures auf der Registerkarte Berechnungen des Cube-Editors festgelegt werden. Dort wird auch die Formatzeichenfolge von berechneten Measures definiert, die ihrerseits in der WITH-Klausel einer Abfrage definiert sind. Die folgende Abfrage veranschaulicht, wie Zelleigenschaften für ein berechnetes Measure festgelegt werden können:  
  
```  
WITH MEMBER MEASURES.CELLPROPERTYDEMO AS [Measures].[Internet Sales Amount]  
, FORE_COLOR=RGB(0,0,255)  
, BACK_COLOR=IIF([Measures].[Internet Sales Amount]>7000000, RGB(255,0,0), RGB(0,255,0))  
, FONT_SIZE=10  
, FORMAT_STRING='#,#.000'  
SELECT MEASURES.CELLPROPERTYDEMO ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS ON 1  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORE_COLOR, BACK_COLOR, FONT_SIZE  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu MDX-Abfragen &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  

