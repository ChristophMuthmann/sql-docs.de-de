---
title: TableNotification-Element (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- TableNotification Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#TableNotification
- microsoft.xml.analysis.tablenotification
- http://schemas.microsoft.com/analysisservices/2003/engine#TableNotification
helpviewer_keywords:
- TableNotification element
ms.assetid: 097b0d53-cb0b-4454-963f-60964fd429e0
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6441e2564466b62c6b3e2cb23127de0b86dda4d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="tablenotification-element-xmla"></a>TableNotification-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Stellt eine Tabellenbenachrichtigung für einen [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md) -Befehl dar.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<TableNotifications>  
   ...  
   <TableNotification>  
      <DbSchemaName>...</DbSchemaName>  
      <DbTableName>...</DbTableName>  
   </TableNotification>  
   ...  
</TableNotifications>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[TableNotifications](../../../analysis-services/xmla/xml-elements-properties/tablenotifications-element-xmla.md)|  
|Untergeordnete Elemente|[DbSchemaName](../../../analysis-services/xmla/xml-elements-properties/dbschemaname-element-xmla.md), [DbTableName](../../../analysis-services/xmla/xml-elements-properties/dbtablename-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankeigenschaften & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
