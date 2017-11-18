---
title: GetUDTs-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getUDTs
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c4396453-dcb0-4132-8325-06b3c7896b3b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5d15d63bbb6d39696664331d6eb29b225ac74d2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getudts-method-sqlserverdatabasemetadata"></a>getUDTs-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Beschreibung der benutzerdefinierten Typen ab, die in einem bestimmten Schema definiert sind.  
  
> [!NOTE]  
>  Diese Methode wird derzeit nicht unterstützt mit [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Bei Verwendung der Methode wird immer ein leeres Resultset zurückgegeben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.ResultSet getUDTs(java.lang.String catalog,  
                                  java.lang.String schemaPattern,  
                                  java.lang.String typeNamePattern,  
                                  int[] types)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Katalog*  
  
 Ein **Zeichenfolge** , enthält der Name des Katalogs.  
  
 *schemaPattern*  
  
 Ein **Zeichenfolge** , die dem schemanamenmuster enthält.  
  
 *typeNamePattern*  
  
 Ein **Zeichenfolge** , die dem typnamenmuster enthält.  
  
 *Typen*  
  
 Ein Array von int-Werten mit den einzubeziehenden Datentypen. Mit "NULL" wird angegeben, dass alle Typen einbezogen werden sollen.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetUDTs-Methode wird von der GetUDTs-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

