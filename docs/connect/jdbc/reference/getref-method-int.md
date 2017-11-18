---
title: GetRef-Methode (Int) | Microsoft Docs
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
apiname:
- SQLServerCallableStatement.getRef (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 905dd02a-0c7f-475b-8be4-341b4359c766
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0bbf1804e4bd35a86b6a0ac15e96ff5436a25609
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getref-method-int"></a>getRef-Methode (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Parameters als Ref-Objekt in der Programmiersprache Java Berücksichtigung des parameterindexes ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.Ref getRef(int i)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Ich*  
  
 Ein **Int** , der die Indexnummer des Parameters angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Ref-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetRef-Methode wird von der GetRef-Methode in der java.sql.CallableStatement-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [GetRef-Methode &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getref-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement-Klasse](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

