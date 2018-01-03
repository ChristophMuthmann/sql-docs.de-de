---
title: PositionEnum | Microsoft Docs
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
f1_keywords: PositionEnum
helpviewer_keywords: PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 36461d4d522a6bed7b09de6580232ec4cbd9306d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="positionenum"></a>PositionEnum
Gibt die aktuelle Position des Datensatzzeigers innerhalb einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Konstante|value|Description|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|Gibt an, dass der Zeiger auf den aktuellen Datensatz am Dateianfang ist (d. h. die [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) Eigenschaft **"true"**).|  
|**adPosEOF**|-3|Gibt an, dass der Zeiger auf den aktuellen Datensatz am Dateiende ist (d. h. die [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) Eigenschaft **"true"**).|  
|**adPosUnknown**|-1|Gibt an, dass die **Recordset** ist leer ist, die aktuelle Position ist unbekannt oder der Anbieter unterstützt nicht die [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) oder [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) Eigenschaft.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.Position.BOF|  
|AdoEnums.Position.EOF|  
|AdoEnums.Position.UNKNOWN|  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[AbsolutePage-Eigenschaft (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)|[AbsolutePosition-Eigenschaft (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|
