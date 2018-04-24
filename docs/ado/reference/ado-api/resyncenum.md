---
title: ResyncEnum | Microsoft Docs
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
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ebe06f65c1fbbe5201eb09c88d4ae12328bc0d21
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="resyncenum"></a>ResyncEnum
Gibt an, ob die zugrunde liegenden Werte überschrieben werden, durch den Aufruf von [Resync](../../../ado/reference/ado-api/resync-method.md).  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|Standard. Daten werden überschrieben, und die ausstehende Updates werden abgebrochen.|  
|**adResyncUnderlyingValues**|1|Daten werden nicht überschrieben, und ausstehende Updates nicht abgebrochen werden.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>Gilt für  
 [Resync-Methode](../../../ado/reference/ado-api/resync-method.md)
