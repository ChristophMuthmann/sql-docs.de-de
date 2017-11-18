---
title: SetAsciiStream-Methode (Int, java.io.InputStream) | Microsoft Docs
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
ms.assetid: 02c2443d-44e1-4f16-a0d5-08d197838214
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2d3931ee99e966d9359b78db7d05f82173d3c750
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setasciistream-method-int-javaioinputstream"></a>setAsciiStream-Methode (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt die angegebene Parameternummer auf das angegebene java.io.InputStream-Objekt fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final void setAsciiStream(int parameterIndex,  
                                 java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parameter  
 *parameterIndex*  
  
 Ein **Int** , der die Parameteranzahl angibt.  
  
 *x*  
  
 Ein java.io.InputStream-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetAsciiStream-Methode wird von der SetAsciiStream-Methode in der java.sql.PreparedStatement-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SetAsciiStream-Methode &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement-Elemente](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  

