---
title: GetHoldability-Methode (SQLServerResultSet) | Microsoft Docs
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
ms.assetid: 4508d90f-c3c4-4eac-8001-fb0b93b66734
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ae5a5d40381cd6b7939e7e67b5950e3d0e3644d3
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getholdability-method-sqlserverresultset"></a>getHoldability-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft die Haltbarkeit dieses ab [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** Wert, der einen der folgenden haltbarkeitsstufen enthält:  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetHoldability-Methode wird von der GetHoldability-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Anwendungen können zum Festlegen der Holdability festlegen möchten, verwenden die [SetHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse. Nach der [SetHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) -Methode aufgerufen wird und das Statement-Objekt und seine Resultsetobjekt werden erstellt, und die Anweisung ausgeführt wird, die Anwendung muss möglicherweise die Haltbarkeit erneut zu ändern.  
  
 Servercursor Wenn wirkt sich auf SQL Server 2005 oder höher verbunden Festlegen der Haltbarkeit nur auf die Haltbarkeit neuer Resultsets, die noch für diese Verbindung erstellt werden. Bei SQL Server 2000 wirkt sich das Festlegen der Haltbarkeit jedoch sowohl auf die Haltbarkeit vorhandener als auch neuer, noch für die Verbindung zu erstellender Resultsets aus.  
  
 Wenn die Holdability zurückgesetzt und die GetHoldability-Methode wird aufgerufen, auf die zuvor erstelltes Resultsetobjekt, der von dieser Methode zurückgegebene Wert sind ggf. anders als der Holdability-Wert, der mithilfe der folgenden Methoden zurückgegeben: Statement.getResultSetHoldability , Connection.getHoldability oder DatabaseMetaData.getResultSetHoldability.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

