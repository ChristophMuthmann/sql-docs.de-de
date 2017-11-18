---
title: GetTimeDateFunctions-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getTimeDateFunctions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a56e08ae-6f4e-4dc6-b175-ff457d0d7a81
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d26d4a2adf59b27b9c8146799902074cbcfb7e2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="gettimedatefunctions-method-sqlserverdatabasemetadata"></a>getTimeDateFunctions-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine durch Trennzeichen getrennte Liste mit den Uhrzeit- und Datumsfunktionen ab, die für diese Datenbank verfügbar sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getTimeDateFunctions()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** eine Liste der Funktionen für Datum und Uhrzeit enthält.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetTimeDateFunctions-Methode wird von der GetTimeDateFunctions-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

