---
title: StringFormatEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 86a1f884f237596895dce6671d3dc42fb6461b1e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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

