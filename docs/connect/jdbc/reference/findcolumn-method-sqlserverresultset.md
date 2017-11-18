---
title: FindColumn-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.findColumn
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7c29994a-0b53-420b-8a9b-82a9eef08587
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3e2ce20105ebb38f579cbc28b68cd83fd2010116
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="findcolumn-method-sqlserverresultset"></a>FindColumn-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Index des ersten übereinstimmenden Spalte für den angegebenen Spaltennamen in dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int findColumn(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnName*  
  
 Ein **Zeichenfolge** , die den Namen der Spalte enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** , der den Spaltenindex angibt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese FindColumn-Methode wird von der FindColumn-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Wenn mehrere Spalten mit dem gleichen Namen vorhanden sind, erfolgt die Methodenrückgabe FindColumn-der ersten Übereinstimmung für die Groß-/Kleinschreibung beachtet. Ist keine Groß-/Kleinschreibung berücksichtigende Übereinstimmung vorhanden, wird von der Methode die erste die Groß-/Kleinschreibung nicht berücksichtigende Übereinstimmung zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

