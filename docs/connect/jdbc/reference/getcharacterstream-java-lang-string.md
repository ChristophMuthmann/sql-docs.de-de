---
title: GetCharacterStream (java.lang.String) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.getCharacterStream(String paramName)
apilocation:
- SQLServerCallableStatement.getCharacterStream(String paramName)
apitype: Assembly
ms.assetid: 5281e1b8-19b8-4fe5-83be-929d1987e25d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1e7771acd514a07296dfbc3a5075aa8086514858
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getcharacterstream-javalangstring"></a>getCharacterStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Parameters unter Berücksichtigung des Parameternamens als java.io.Reader-Objekt ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final java.io.Reader getCharacterStream(java.lang.String paramName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *paramName*  
  
 Ein **Zeichenfolge** , der den Namen des Parameters angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Readerobjekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>Siehe auch  
 [GetCharacterStream-Methode &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement-Klasse](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

