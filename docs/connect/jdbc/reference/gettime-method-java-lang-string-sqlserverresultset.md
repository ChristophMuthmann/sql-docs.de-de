---
title: GetTime-Methode (java.lang.String) (SQLServerResultSet) | Microsoft Docs
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
apiname: SQLServerResultSet.getTime (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: e0efc0b3-4da4-45fc-9e8d-5edd9da7a42d
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b0722cfe59a9d5dc47c58469823a1f566fe4e5b1
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="gettime-method-javalangstring-sqlserverresultset"></a>GetTime-Methode (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Spaltennamens in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekts als java.sql.Time-Objekt in der Programmiersprache Java ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.Time getTime(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnName*  
  
 Ein **Zeichenfolge** , die den Namen der Spalte enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetTime-Methode wird von der GetTime-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Diese Methode gibt einen gültigen Uhrzeitteil des eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datetime oder Smalldatetime-Datentyp, mit der Date-Teil der Java-grunddatum 1970/01/01 festgelegt.  
  
## <a name="see-also"></a>Siehe auch  
 [GetTime-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
