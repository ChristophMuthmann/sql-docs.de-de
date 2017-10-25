---
title: CreateStatement-Methode (Int, Int) | Microsoft Docs
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
- SQLServerConnection.createStatement (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 90dbf639-c3d8-4519-9300-5447c79aec17
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a9229e66b071f4fd33077c4e3c7c780f9a1059aa
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="createstatement-method-int-int"></a>createStatement-Methode (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Erstellt eine [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, generiert [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte mit dem angegebenen Typ und der Parallelität.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.Statement createStatement(int resultSetType,  
                                          int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>Parameter  
 *resultSetType*  
  
 Die **Int** Wert, der den Resultsettyp darstellt.  
  
 *resultSetConcurrency*  
  
 Die **Int** Wert, der die Parallelität Resultsettyp darstellt.  
  
## <a name="return-value"></a>Rückgabewert  
 Das Statement-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese CreateStatement-Methode wird von der CreateStatement-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [CreateStatement-Methode &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

