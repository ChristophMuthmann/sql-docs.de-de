---
title: StringFormatEnum | Microsoft Docs
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
f1_keywords: StringFormatEnum
helpviewer_keywords: StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e2d5b9159798855e75217f105122025092e25c06
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="stringformatenum"></a>StringFormatEnum
Gibt das Format an, wenn das Abrufen einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) als Zeichenfolge.  
  
|Konstante|value|Description|  
|--------------|-----------|-----------------|  
|**adClipString**|2|Begrenzt Zeilen durch *RowDelimiter*, Spalten nach *ColumnDelimiter*, und null-Werte von *NullExpr*. Diese drei Parameter von der [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) Methode gelten nur für eine *StringFormat* von **AdClipString**.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>Gilt für  
 [GetString-Methode (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
