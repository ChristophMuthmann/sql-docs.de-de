---
title: SeekEnum | Microsoft Docs
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
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0fcf7dabb3c12f7919c317c7ecabeaf51995fe85
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="seekenum"></a>SeekEnum
Gibt den Typ des [Seek](../../../ado/reference/ado-api/seek-method.md) ausgeführt.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|Sucht den ersten Schlüssel gleich *KeyValues*.|  
|**adSeekLastEQ**|2|Sucht das letzte Schlüssel gleich *KeyValues*.|  
|**adSeekAfterEQ**|4|Sucht entweder einen Schlüssel gleich *KeyValues* oder unmittelbar nach entsprechen, in denen stattgefunden hätten.|  
|**adSeekAfter**|8|Sucht einen Schlüssel direkt hinter Where eine Übereinstimmung mit *KeyValues* würde stattgefunden haben.|  
|**adSeekBeforeEQ**|16|Sucht entweder einen Schlüssel gleich *KeyValues*Markierung oder kurz vor, in denen diese Übereinstimmung stattgefunden hätten.|  
|**adSeekBefore**|32|Unmittelbar vor dem sucht einen Schlüssel, wenn eine Übereinstimmung mit *KeyValues* würde stattgefunden haben.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.Seek.FIRSTEQ|  
|AdoEnums.Seek.LASTEQ|  
|AdoEnums.Seek.AFTEREQ|  
|AdoEnums.Seek.AFTER|  
|AdoEnums.Seek.BEFOREEQ|  
|AdoEnums.Seek.BEFORE|  
  
## <a name="applies-to"></a>Gilt für  
 [Seek-Methode](../../../ado/reference/ado-api/seek-method.md)
