---
title: PersistFormatEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: PersistFormatEnum
helpviewer_keywords: PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2695db14fdbdf05aba5b0a1b14b063ff6672a928
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
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
