---
title: GetNString-Methode (java.lang.String) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b351e999-85bf-498b-915a-f91d89134bce
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c6a228bf0087d5af7b5f44ce2888b29d9ed73351
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getnstring-method-javalangstring"></a>getNString-Methode (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert der festgelegten **NCHAR**, **NVARCHAR**, oder **LONGNVARCHAR** Parameter als eine Zeichenfolge in der Java-Programmiersprache.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final java.lang.String getNString(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *parameterName*  
  
 Ein **Zeichenfolge** , die den Namen des Parameters enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 AStringobject.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetNString-Methode wird von der GetNString-Methode in der java.sql.CallableStatement-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [GetNString-Methode &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement-Methoden](../../../connect/jdbc/reference/sqlservercallablestatement-methods.md)  
  
  

