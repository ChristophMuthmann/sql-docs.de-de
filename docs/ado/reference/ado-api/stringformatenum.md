---
title: StringFormatEnum | Microsoft Docs
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
f1_keywords: StringFormatEnum
helpviewer_keywords: StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a7fd230d7e9a52d34c470dca8c0ea666c4436bb5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stringformatenum"></a>StringFormatEnum
Gibt das Format an, wenn das Abrufen einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) als Zeichenfolge.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adClipString**|2|Begrenzt Zeilen durch *RowDelimiter*, Spalten nach *ColumnDelimiter*, und null-Werte von *NullExpr*. Diese drei Parameter von der [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) Methode gelten nur für eine *StringFormat* von **AdClipString**.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>Gilt für  
 [GetString-Methode (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
