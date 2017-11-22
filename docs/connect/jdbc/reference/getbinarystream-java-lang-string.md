---
title: GetBinaryStream (java.lang.String) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerCallableStatement.getBinaryStream(String paramName)
apilocation: SQLServerCallableStatement.getBinaryStream(String paramName)
apitype: Assembly
ms.assetid: 17f1ea5d-47f8-4a66-a0fc-d6554b8e3866
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 56c943dc5287fbb160bb8984d0be1545f88efc32
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="getbinarystream-javalangstring"></a>getBinaryStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft unter Berücksichtigung des Parameternamens den Wert des angegebenen Parameters als Binärdatenstrom mit unterbrechungsfreien Bytes ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final java.io.InputStream getBinaryStream(java.lang.String paramName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *paramName*  
  
 Ein **Zeichenfolge** , der den Namen des Parameters angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein InputStream-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>Siehe auch  
 [GetBinaryStream-Methode &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement-Klasse](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
