---
title: SeekEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: SeekEnum
helpviewer_keywords: SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e6f60ed06b2f23bceec62822f43b77f5c10c3ce1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="seekenum"></a>SeekEnum
Gibt den Typ des [Seek](../../../ado/reference/ado-api/seek-method.md) ausgeführt.  
  
|Konstante|value|Description|  
|--------------|-----------|-----------------|  
|**Nordwind.mdb**|1|Sucht den ersten Schlüssel gleich *KeyValues*.|  
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
