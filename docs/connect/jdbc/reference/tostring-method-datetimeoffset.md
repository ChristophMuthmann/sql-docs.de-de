---
title: ToString-Methode (DateTimeOffset) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4b0c31538c7260b81a88822099f56a05b70a0a96
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="tostring-method-datetimeoffset"></a>toString-Methode (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt eine Zeichenfolgendarstellung der **"DateTimeOffset"** Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Eine Zeichenfolgendarstellung der **"DateTimeOffset"** Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Die Zeichenfolge hat das Format *YYYY*-*MM*-*DD**"hh"*:*mm*: *ss*[.* FFFFFFF*] [+ |-]*"hh"*:*mm*.  
  
 Die Sekundenbruchteile der zurückgegebenen Zeichenfolge werden bis zur angegebenen Genauigkeit mit Nullen aufgefüllt. Z. B. eine **datetimeoffset(6)** mit einem Wert von "2010-03-10-12:34:56.78-08: 00" formatiert von DateTimeOffset.toString als "2010-03-10-12:34:56.780000-08: 00".  
  
## <a name="see-also"></a>Siehe auch  
 ["DateTimeOffset"-Klasse](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset-Elemente](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  

