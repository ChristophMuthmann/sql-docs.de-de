---
title: TableBinding-Datentyp (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- TableBinding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TableBinding
helpviewer_keywords:
- TableBinding data type
ms.assetid: 3195dca4-82bf-46b7-a31f-5383586e3573
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2f47a88fa3a5afe592387536297601eac027196a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="tablebinding-data-type-assl"></a>TableBinding-Datentyp (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Definiert einen abgeleiteten Datentyp, der eine Bindung mit einer Tabelle darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<TableBinding>  
   <!-- The following elements extend TabularBinding -->  
   <DataSourceID>...</DataSourceID>  
   <DbTableName>...</DbTableName>  
   <DbSchemaName>...</DbSchemaName>  
</TableBinding>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|[TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|Abgeleitete Datentypen|Keine|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[DataSourceID](../../../analysis-services/scripting/properties/datasourceid-element-assl.md), [DbSchemaName](../../../analysis-services/scripting/properties/dbschemaname-element-assl.md), [DbTableName](../../../analysis-services/scripting/properties/dbtablename-element-assl.md)|  
|Abgeleitete Elemente|Siehe [Binding](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Hinweise  
 Beachten Sie, dass Verweise auf andere Tabellen im Filterausdruck durch eine untergeordnete SELECT-Anweisung Auswirkungen auf die Leistung in einigen Datenquellen haben können. Der Designer hat jedoch die vollständige Kontrolle über die SQL-Ausdrücke, indem er eine benannte Abfrage in der Datenquellensicht definiert und anschließend darauf verweist.  
  
 Die Methoden zum Definieren der Bindungen für eine Partition sind unabhängig von der Verwendung partitionierter Tabellen in der Datenquellensicht.  
  
 Ein Beispiel: Eine Measuregruppe verfügt über die Standardtabelle "Sales" und weist die Spalten "Date", "ProductID", "Qty", "Price" und "Amount" auf (in der Datenquellensicht berechnet). Dann könnte die Partition "Sales97" die Tabelle "Sales97" mit dem Filter "Year(Sales.Date) = 97" verwenden.  
  
 Die effektive Abfrage lautet:  
  
```  
SELECT Date, Product ID, Qty, Price, Qty * Price AS Amount   
   FROM Sales97 As Sales  
   WHERE Year(Sales.Date) = 97  
```  
  
 Der berechnete Ausdruck ist auch dann noch gültig, wenn der Ausdruck qualifizierte Tabellennamen (z. B. "Sales.Qty") verwendet hat. Dasselbe gilt, wenn stattdessen die Tabelle durch eine Abfrage "SELECT..." ersetzt wurden. Die oben genannten FROM-Klausel werden "FROM SELECT... As Sales" werden.  
  
 Weitere Informationen zu den **binden** Typ, einschließlich Tabellen, die von Analysis Services Scripting Language (ASSL) von Objekten des Typs **binden** und der Vererbungshierarchie der **binden** , finden Sie unter [Binding-Datentyp &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Einen Überblick über datenbindungen in ASSL finden Sie unter [& #40; Datenquellen und Bindungen SSAS – mehrdimensional & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.TableBinding>.  
  
## <a name="see-also"></a>Siehe auch  
 [Binding-Datentyp & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [Datenquellen und-Bindungen &#40;SSAS – mehrdimensional&#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)   
 [Analysis Services Scripting Language-XML-Datentypen & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
