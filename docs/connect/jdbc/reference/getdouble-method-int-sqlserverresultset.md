---
title: GetDouble-Methode (Int) (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.getDouble (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 128df26a-9063-4bdf-a4fb-a077cbe7cfe1
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c75edf6d4a934dae8a0b04a9d1251237df7b977
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getdouble-method-int-sqlserverresultset"></a>GetDouble-Methode (Int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Spaltenindexes in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **doppelte** in der Programmiersprache Java ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public double getDouble(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnIndex*  
  
 Ein **Int** , der den Spaltenindex angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **doppelte** Wert.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetDouble-Methode wird von der GetDouble-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Diese Methode gibt alle zahlenbasierten Datentypen mit Java **doppelte** Genauigkeit.  
  
## <a name="see-also"></a>Siehe auch  
 [GetDouble-Methode &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdouble-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
