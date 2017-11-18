---
title: supportsANSI92FullSQL-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.supportsANSI92FullSQL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8877dc8c-26cd-4374-8ae8-ff7d20621130
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 291b31461c0659099e4d4bd98661bb6f94351090
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="supportsansi92fullsql-method-sqlserverdatabasemetadata"></a>supportsANSI92FullSQL-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft ab, ob von dieser Datenbank die vollständige ANSI92-SQL-Grammatik unterstützt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean supportsANSI92FullSQL()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** unterstützt. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese supportsANSI92FullSQL-Methode wird von der supportsANSI92FullSQL-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

