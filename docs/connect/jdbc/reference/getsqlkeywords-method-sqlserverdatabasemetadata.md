---
title: GetSQLKeywords-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getSQLKeywords
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a2a0dfbb-11ec-429f-aea6-8f44148ebb8e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 35e4a13f00a95becbfa4637c13e93cba6750d2a5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getsqlkeywords-method-sqlserverdatabasemetadata"></a>getSQLKeywords-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine durch Trennzeichen getrennte Liste mit allen SQL-Schlüsselwörtern dieser Datenbank ab, bei denen es sich nicht gleichzeitig um SQL92-Schlüsselwörter handelt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getSQLKeywords()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** , enthält die SQL-Schlüsselwörter.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetSQLKeywords-Methode wird von der GetSQLKeywords-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

