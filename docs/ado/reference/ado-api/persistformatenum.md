---
title: PersistFormatEnum | Microsoft Docs
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
- PersistFormatEnum
helpviewer_keywords:
- PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 141590f2755323422f44aacb4617905191d3a154
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="persistformatenum"></a>PersistFormatEnum
Gibt das Format zum Speichern einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|Gibt Microsoft Advanced Data TableGram (ADTG)-Format an.|  
|**adPersistADO**|1|Gibt an, dass der ADO-Extensible Markup Language (XML)-Format verwendet wird. Dieser Wert ist AdPersistXML und Gründen der Abwärtskompatibilität enthalten.|  
|**adPersistXML**|1|Gibt die Extensible Markup Language (XML)-Format an.|  
|**adPersistProviderSpecific**|2|Gibt an, dass der Anbieter beibehält der **Recordset** mit einem eigenen Format.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.PersistFormat.ADTG|  
|AdoEnums.PersistFormat.XML|  
  
## <a name="applies-to"></a>Gilt für  
 [Save-Methode](../../../ado/reference/ado-api/save-method.md)
