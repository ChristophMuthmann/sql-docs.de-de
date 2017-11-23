---
title: GetTimestamp-Methode (Int, java.util.Calendar) | Microsoft Docs
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
apiname: SQLServerResultSet.getTimestamp (int, java.util.Calendar)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: f2dd5688-7344-437a-8716-7024fb8e9c31
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e85bc61b8bca45a332195cae5da2bd5ea154404a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="gettimestamp-method-int-javautilcalendar-sqlserverresultset"></a>GetTimestamp-Methode (Int, java.util.Calendar) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Spaltenindexes in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekts als java.sql.Timestamp-Objekt in der Programmiersprache Java mithilfe eines Objekts dar.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.Timestamp getTimestamp(int columnIndex,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnIndex*  
  
 Ein **Int** , der den Spaltenindex angibt.  
  
 *CAL*  
  
 Ein Kalenderobjekt.  
  
## <a name="return-value"></a>Rückgabewert  
 Eine Timestamp-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetTimestamp-Methode wird von der GetTimestamp-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Diese Methode gibt nur Werte aus [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] DateTime- und Smalldatetime-Spalten.  
  
## <a name="see-also"></a>Siehe auch  
 [GetTimestamp-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
