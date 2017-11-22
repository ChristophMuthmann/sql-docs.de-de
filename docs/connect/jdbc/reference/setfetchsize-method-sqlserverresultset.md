---
title: SetFetchSize-Methode (SQLServerResultSet) | Microsoft Docs
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
apiname: SQLServerResultSet.setFetchSize
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 233bf4f8-4758-42d0-a80b-33e34fa78027
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a143006cbd2a5482bd919b4e2cd648d91290291d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="setfetchsize-method-sqlserverresultset"></a>SetFetchSize-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt dem JDBC-Treiber für die Anzahl der Zeilen, die aus der Datenbank abgerufen werden sollen, wenn weitere Zeilen, für diesen benötigt werden [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Zeilen*  
  
 Ein **Int** , der die Anzahl der abzurufenden Zeilen angibt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetFetchSize-Methode wird von der SetFetchSize-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Ist die angegebene Abrufgröße NULL, wird der Wert vom JDBC-Treiber ignoriert und die korrekte Abrufgröße geschätzt. Der Standardwert wird durch Festlegen der [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, das Resultset erstellt. Die Abrufgröße kann jedoch jederzeit geändert werden.  
  
 Mit dieser Methode wird die Blockabrufgröße für Servercursor geändert. Die Änderungen treten beim nächsten Aufruf von "sp_cursorfetch" durch den JDB-Treiber in Kraft. Durch das Festlegen der Abrufgröße auf NULL wird die Standardabrufgröße für den momentan verwendeten Cursortyp wiederhergestellt.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
