---
title: ResyncEnum | Microsoft Docs
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
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79752a7733450fc1e6761f39cd49fb6f808a334b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
