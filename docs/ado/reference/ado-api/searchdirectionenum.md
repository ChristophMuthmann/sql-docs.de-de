---
title: SearchDirectionEnum | Microsoft Docs
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
f1_keywords: SearchDirectionEnum
helpviewer_keywords: SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f4d5e78b7f636c4fb6094a217a0b1249babe9b2f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
Gibt die Richtung einer Datensatz Suche innerhalb einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|Sucht nach hinten, beenden am Anfang der **Recordset**. Wenn eine Übereinstimmung gefunden wird, wird am Zeiger für den Datensatz positioniert [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md).|  
|**adSearchForward**|1|Sucht vorwärts, beenden am Ende der **Recordset**. Wenn eine Übereinstimmung gefunden wird, wird am Zeiger für den Datensatz positioniert [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md).|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>Gilt für  
 [Find-Methode (ADO)](../../../ado/reference/ado-api/find-method-ado.md)
