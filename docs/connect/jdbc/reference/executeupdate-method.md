---
title: ExecuteUpdate-Methode () | Microsoft Docs
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
- SQLServerPreparedStatement.executeUpdate ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ca534c6b-ef4d-4ae8-8cc3-514728623cff
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01d42e7e0d8874f73d82b9d8a72ce95c3434870a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="executeupdate-method-"></a>executeUpdate-Methode ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Führt die SQL-Anweisung in diesem [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) -Objekt, dem muss eine SQL INSERT, UPDATE, MERGE oder DELETE-Anweisung oder eine SQL-Anweisung, die nichts, z. B. eine DDL-Anweisung zurückgegeben werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int executeUpdate()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** , der die Anzahl der betroffenen Zeilen, oder 0 bei Verwendung einer DDL-Anweisung angibt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese ExecuteUpdate-Methode wird von der ExecuteUpdate-Methode in der java.sql.PreparedStatement-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [ExecuteUpdate-Methode &#40;sqlserverpreparedstatement-Klasse&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement-Elemente](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement-Klasse](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
