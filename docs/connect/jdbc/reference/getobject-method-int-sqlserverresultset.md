---
title: GetObject-Methode (Int) (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.getObject (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 94e59366-ca34-4cd5-a6ec-ae32d475ef36
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ec9e7c35152eafd09841994955fc0bd86f84ec01
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getobject-method-int-sqlserverresultset"></a>GetObject-Methode (Int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Spaltenindexes in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als Objekt in der Programmiersprache Java ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.Object getObject(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnIndex*  
  
 Ein **Int** , der den Spaltenindex angibt.  
  
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
 [GetObject-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

