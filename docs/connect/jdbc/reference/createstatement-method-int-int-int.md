---
title: CreateStatement-Methode (Int, Int, Int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.createStatement (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2e4fa385-8f61-4394-8f75-3e839930a57d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a98b5be003546b2573a1ecb844d4c5a08c7f6913
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="createstatement-method-int-int-int"></a>createStatement-Methode (int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Erstellt eine [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, generiert [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte mit dem angegebenen Typ, Parallelität und Haltbarkeit.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.Statement createStatement(int nType,  
                                          int nConcur,  
                                          int nHold)  
```  
  
#### <a name="parameters"></a>Parameter  
 *ResultSetType*  
  
 Die **Int** resultsettyps der Wert, der das Ergebnis darstellt.  
  
 *nConcur*  
  
 Die **Int** Parallelitätstyp legen Sie Wert, der das Ergebnis darstellt.  
  
 *nHold*  
  
 Die **Int** Wert, der die Haltbarkeit darstellt.  
  
## <a name="return-value"></a>Rückgabewert  
 Das Statement-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese CreateStatement-Methode wird von der CreateStatement-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [CreateStatement-Methode &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
