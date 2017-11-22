---
title: DbTableName-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DbTableName Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#DbTableName
- microsoft.xml.analysis.dbtablename
- urn:schemas-microsoft-com:xml-analysis#DbTableName
helpviewer_keywords: DbTableName element
ms.assetid: 0ffda645-2a88-4f42-8929-9d7385c19a74
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 37326c78577bbee960f9fea63b4c39de094caf13
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="dbtablename-element-xmla"></a>DbTableName-Element (XMLA)
  Enthält den Namen der Tabelle verwendet wird, die die übergeordneten [TableNotification](../../../analysis-services/xmla/xml-elements-properties/tablenotification-element-xmla.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<TableNotification>  
   ...  
   <DbTableName>...</DbTableName>  
   ...  
</TableNotification>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[TableNotification](../../../analysis-services/xmla/xml-elements-properties/tablenotification-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [DbSchemaName-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/dbschemaname-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
