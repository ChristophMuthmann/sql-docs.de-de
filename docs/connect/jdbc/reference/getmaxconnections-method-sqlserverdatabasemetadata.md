---
title: GetMaxConnections-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getMaxConnections
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 745410f7-e59b-4423-9728-c903adedc399
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 00c41ad1f036617c9812a251cd52da338712f027
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getmaxconnections-method-sqlserverdatabasemetadata"></a>getMaxConnections-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft die maximal mögliche Anzahl gleichzeitiger Verbindungen mit dieser Datenbank ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int getMaxConnections()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** , der die maximale Anzahl zulässiger gleichzeitiger Verbindungen angibt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetMaxConnections-Methode wird von der GetMaxConnections-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

