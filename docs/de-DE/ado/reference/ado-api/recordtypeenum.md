---
title: RecordTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordTypeEnum
helpviewer_keywords:
- RecordTypeEnum enumeration [ADO]
ms.assetid: f557e537-015d-4ba7-8a41-a6f00b366a91
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5c7678d492e41396d3b0893aab66a3bb531e1b7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="recordtypeenum"></a>RecordTypeEnum
Gibt den Typ des [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) Objekt.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adSimpleRecord**|0|Gibt eine *einfache* Datensatz (enthält keine untergeordneten Knoten).|  
|**adCollectionRecord**|1|Gibt eine *Auflistung* Datensatz (enthält untergeordnete Knoten).|  
|**adRecordUnknown**|-1|Gibt an, dass der Typ dieses **Datensatz** ist unbekannt.|  
|**adStructDoc**|2|Gibt an, eine spezielle Art von *Auflistung* Datensatz, der COM-strukturierte Dokumente.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Diese Konstanten keine ADO/WFC-Entsprechungen.  
  
## <a name="applies-to"></a>Gilt für  
 [RecordType-Eigenschaft (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)
