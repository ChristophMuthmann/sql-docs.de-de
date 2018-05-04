---
title: GetFloat-Methode (Int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getFloat (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 40178471-4f35-4df9-b3fb-80cdf43de274
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca66ca18cc5f3a6f16a2c23d9c0c7297177b6959
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getfloat-method-int"></a>getFloat-Methode (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Parameters als eine **"float"** in der Berücksichtigung des parameterindexes Programmiersprache Java ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public float getFloat(int index)  
```  
  
#### <a name="parameters"></a>Parameter  
 *index*  
  
 Ein **Int** , der die Indexnummer des Parameters angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **"float"** Wert.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetFloat-Methode wird von der GetFloat-Methode in der java.sql.CallableStatement-Schnittstelle angegeben.  
  
 Diese Methode gibt alle zahlenbasierten Typen mit Java **"float"** Genauigkeit.  
  
## <a name="see-also"></a>Siehe auch  
 [GetFloat-Methode &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getfloat-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement-Klasse](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
