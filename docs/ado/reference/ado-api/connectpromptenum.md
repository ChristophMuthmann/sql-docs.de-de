---
title: ConnectPromptEnum | Microsoft Docs
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
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b8f01de20cabf1ec5d7cefdb645fb1fc08b69d31
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
Gibt an, ob ein Dialogfeld angezeigt werden soll, um fehlende Parameter beim Öffnen einer Verbindung mit einer Datenquelle anzufordern.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|Immer aufgefordert.|  
|**adPromptComplete**|2|Werden Sie aufgefordert, wenn Sie weitere Informationen erforderlich sind.|  
|**adPromptCompleteRequired**|3|Werden Sie aufgefordert, wenn weitere Informationen erforderlich sind, aber optionale Parameter sind nicht zulässig.|  
|**adPromptNever**|4|Fordert nie auf.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.ConnectPrompt.ALWAYS|  
|AdoEnums.ConnectPrompt.COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums.ConnectPrompt.NEVER|  
  
## <a name="applies-to"></a>Gilt für  
 [Dynamische Eigenschaft Prompt (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
