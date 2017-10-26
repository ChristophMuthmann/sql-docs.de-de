---
title: GetSuperTypes-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getSuperTypes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5b8e78e6-2bb0-4dc7-9c77-a5609654cb05
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0891d0d68cea6e84f0f95d23fe5f18497f92549b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getsupertypes-method-sqlserverdatabasemetadata"></a>getSuperTypes-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Beschreibung der benutzerdefinierten Typhierarchien ab, die in einem bestimmten Schema in dieser Datenbank definiert sind.  
  
> [!NOTE]  
>  Diese Methode wird derzeit nicht unterstützt mit dem [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Bei Verwendung der Methode wird immer ein leeres Resultset zurückgegeben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.ResultSet getSuperTypes(java.lang.String catalog,  
                                        java.lang.String schemaPattern,  
                                        java.lang.String typeNamePattern)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Katalog*  
  
 Ein **Zeichenfolge** , enthält der Name des Katalogs.  
  
 *schemaPattern*  
  
 Ein **Zeichenfolge** , die dem schemanamenmuster enthält.  
  
 *tableNamePattern*  
  
 Ein **Zeichenfolge** , der dem Namensmuster für die Tabelle enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetSuperTypes-Methode wird von der GetSuperTypes-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

