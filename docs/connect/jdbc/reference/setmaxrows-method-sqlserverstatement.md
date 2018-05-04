---
title: SetMaxRows-Methode (SQLServerStatement) | Microsoft Docs
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
- SQLServerStatement.setMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cccc0667-589b-4655-8ea8-14ae8b2eb9dc
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 949c7a7d0b9d28c2ba14b4130db657ba357be2de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setmaxrows-method-sqlserverstatement"></a>setMaxRows-Methode (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Das Limit für die maximale Anzahl von Zeilen, die von jedem legt [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt enthalten kann, auf die angegebene Anzahl.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final void setMaxRows(int max)  
```  
  
#### <a name="parameters"></a>Parameter  
 *max*  
  
 Ein **Int** , die die maximale Anzahl von Zeilen, oder 0 gibt an, wenn kein Limit vorhanden ist.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetMaxRows-Methode wird durch die SetMaxRows-Methode in der java.sql.Statement-Schnittstelle angegeben.  
  
 Diese SetMaxRows-Methode hat keine Auswirkungen für dynamische, scrollfähige Cursor. Von der Anwendung sollte die Anzahl von Zeilen, die von potenziell umfangreichen Resultsets zurückgegeben wird, mithilfe der SQL-Syntax "SELECT TOP N" eingeschränkt werden.  
  
 Wenn die SetMaxRows-Methode aufgerufen wird, die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] das Festlegen der ROWCOUNT-SQL-Anweisung ausführt, beim Ausführen der anwendungsabfrage. Dies bewirkt, dass den JDBC-Treiber die maximale Anzahl der von allen betroffenen Zeilen beschränkt die [!INCLUDE[tsql](../../../includes/tsql_md.md)] Anweisungen, die von dieser Abfrage ausgeführt, nicht nur die Anzahl der Zeilen, die von dieser Abfrage zurückgegeben. Wenn die Anwendung festgelegt werden nur auf der obersten Ebene muss [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt, sollten sie SELECT TOP N SQL-Syntax in der Abfrage anstelle der SetMaxRows-Methode verwenden.  
  
 Weitere Informationen zur ZEILENANZAHL Festlegen des SQL-Anweisung finden Sie unter der "[SET ROWCOUNT (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=139522)" im Thema [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerStatement-Elemente](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
