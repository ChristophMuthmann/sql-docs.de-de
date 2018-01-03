---
title: XactAttributeEnum | Microsoft Docs
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
f1_keywords: XactAttributeEnum
helpviewer_keywords: XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 27f9e93ee75b4efcf427bbf7a69737180f7141b2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="xactattributeenum"></a>XactAttributeEnum
Gibt die Transaktionsattribute von einem [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt.  
  
|Konstante|value|Description|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|Führt Sie durch den Aufruf beibehaltene Abbrüche [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) automatisch eine neue Transaktion gestartet. Nicht alle Anbieter unterstützen dieses Verhalten.|  
|**adXactCommitRetaining**|131072|Führt Sie durch Aufrufen aufbewahren Commits [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) automatisch eine neue Transaktion gestartet. Nicht alle Anbieter unterstützen dieses Verhalten.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>Gilt für  
 [Attributes-Eigenschaft (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
