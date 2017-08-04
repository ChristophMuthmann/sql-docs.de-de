---
title: SELECT FROM &lt;Modell&gt;. DIMENSION_CONTENT (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT
- FROM
- DIMENSION_CONTENT
dev_langs:
- DMX
helpviewer_keywords:
- mining models [Analysis Services], dimension content
- SELECT FROM <model>.DIMENSION_CONTENT statement
ms.assetid: 907fb3fb-2131-4a10-8635-2a39b9a805aa
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f9caf83d8d3d151f1b324f00abf5561549e111ad
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="select-from-ltmodelgtdimensioncontent-dmx"></a>SELECT FROM &lt;Modell&gt;. DIMENSION_CONTENT (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ein Miningmodell kann als Dimension in einem OLAP-Cube verwendet werden, wobei jeder Knoten im Modell als Element der Dimension dargestellt wird. **SELECT FROM \<Modell >. Dimension_CONTENT** -Anweisung gibt den Inhalt des Modells, die sich auf die Verwendung als Dimension beziehen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.Dimension_CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumente  
 *n*  
 Optional. Eine ganze Zahl, die angibt, wie viele Zeilen zurückgegeben werden sollen.  
  
 *Liste der Ausdrücke*  
 Eine durch Trennzeichen getrennte Liste mit Bezeichnern, die aus dem Schemarowset des Inhalts abgeleitet wurden.  
  
 *model*  
 Ein Modellbezeichner.  
  
 *Bedingungsausdruck*  
 Optional. Eine Bedingung, die die Werte einschränkt, die für die Spaltenliste zurückgegeben werden.  
  
 *expression*  
 Optional. Ein Ausdruck, der einen Skalarwert zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Algorithmusanbieter definieren, welcher Inhalt zurückgegeben wird und wie dieser aufgebaut ist. Beispielsweise kann der Anbieter die Anzahl von Knoten begrenzen, die im Dimensionsinhalt beschrieben werden.  
  
 In der folgenden Tabelle sind die Spalten, die für den Dimensionsinhalt abgefragt werden können, sowie für jede Spalte die Funktion aufgeführt, die sie als Data Mining-Dimension hat.  
  
|CONTENT-Rowsetspalte|Funktion in einer Data Mining-Dimension|  
|---------------------------|---------------------------------------|  
|ATTRIBUTE_NAME|Member-Eigenschaft.|  
|NODE_NAME|Member-Eigenschaft.|  
|NODE_UNIQUE_NAME|Schlüsselattribut.|  
|NODE_TYPE|Member-Eigenschaft.|  
|NODE_CAPTION|CaptionColumn für **Schlüssel** Attribut.|  
|CHILDREN_CARDINALITY|Member-Eigenschaft.|  
|PARENT_UNIQUE_NAME|Zugeordnetes Attribut für **Schlüssel** -Attribut (übergeordnetes Attribut in über-/ unterordnungshierarchie).|  
|NODE_DESCRIPTION|Member-Eigenschaft.|  
|NODE_RULE|Member-Eigenschaft.|  
|MARGINAL_RULE|Member-Eigenschaft.|  
|NODE_PROBABILITY|Member-Eigenschaft.|  
|MARGINAL_PROBABILITY|Member-Eigenschaft.|  
|NODE_SUPPORT|Member-Eigenschaft.|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="description"></a>Description  
 In diesem Beispiel werden alle Spalten aus dem Inhalt des `[TM Decision Tree]`-Modells ausgewählt, die sich auf die Verwendung des Modells als Dimension beziehen.  
  
### <a name="code"></a>Code  
  
```  
SELECT *   
FROM [TM Decision Tree].Dimension_Content  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SELECT &#40; DMX &#41;](../dmx/select-dmx.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Datendefinitionsanweisungen](../dmx/dmx-statements-data-definition.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

