---
title: GetObject-Methode (Int, java.util.Map) (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.getObject (int, java.util.Map)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: df85a514-ab43-4bf6-98dd-f7f37fad1850
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 67ee98b215083afee0f763e79e555b105e1a0eba
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getobject-method-int-javautilmap-sqlserverresultset"></a>getObject-Methode (int, java.util.Map) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Spaltenindexes in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als Objekt in der Programmiersprache Java mithilfe der angegebenen Map-Objekts.  
  
> [!NOTE]  
>  Diese Methode wird derzeit nicht unterstützt durch die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Bei Verwendung dieser Methode wird immer die Standardzuordnung zurückgegeben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.Object getObject(int i,  
                                  java.util.Map map)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Ich*  
  
 Ein **Int** , der den Spaltenindex angibt.  
  
 *Zuordnung*  
  
 Map-Objekt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Objekt** Wert.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetObject-Methode wird von der GetObject-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Von dieser Methode wird der Wert der angegebenen Spalte als Java-Objekt zurückgegeben. Beim Typ des Java-Objekts handelt es sich um den standardmäßigen Java-Objekttyp, der dem SQL-Typ der Spalte entspricht. Die Grundlage hierfür bildet die in der JDBC-Spezifikation angegebene Zuordnung für integrierte Typen. Bei einem SQL-NULL-Wert wird vom Treiber ein Java-NULL-Wert zurückgegeben.  
  
 Diese Methode kann auch zum Lesen datenbankspezifischer, abstrakter Datentypen verwendet werden. In der JDBC 2.0-API wird das Verhalten der GetObject-Methode erweitert, um Daten von SQL-benutzerdefinierte Typen zu materialisieren. Wenn eine Spalte einen strukturierten oder unterschiedlichen Wert enthält, wird das Verhalten dieser Methode ist, als handele es sich um einen Aufruf von `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`.  
  
 Ab der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0:  
  
-   Ein Date-Wert wird als java.sql.Date-Objekt zurückgegeben.  
  
-   Ein Time-Wert wird als java.sql.Time-Objekt zurückgegeben.  
  
-   Ein Datetime2-Wert wird als java.sql.Timestamp-Objekt zurückgegeben.  
  
-   Ein Datetimeoffset-Wert wird als microsoft.sql.DateTimeOffset-Objekt zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [GetObject-Methode &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
