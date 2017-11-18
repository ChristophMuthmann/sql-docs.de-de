---
title: SupportsMultipleResultSets-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.supportsMultipleResultSets
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cb4d0b91-db1d-4a6f-a87c-8ea125215afc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9c693199080ed166fd51d069e402ccd6fcb9352d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="supportsmultipleresultsets-method-sqlserverdatabasemetadata"></a>supportsMultipleResultSets-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft ab, ob dieser Datenbank unterstützt mehrere erste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte aus einem einzigen Aufruf der [ausführen](../../../connect/jdbc/reference/execute-method.md) Methode der [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)Klasse.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean supportsMultipleResultSets()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** unterstützt. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SupportsMultipleResultSets-Methode wird von der SupportsMultipleResultSets-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

