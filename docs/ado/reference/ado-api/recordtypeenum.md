---
title: RecordTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
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
ms.openlocfilehash: 1f84fecc2ecac03ba6d8a18588d2f0163930b701
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
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
