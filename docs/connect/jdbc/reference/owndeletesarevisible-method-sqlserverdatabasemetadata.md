---
title: OwnDeletesAreVisible-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.ownDeletesAreVisible
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2dd6d976-9f8f-4a24-9354-ff239cfd4364
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2ec3f4e2d9facb5b82e1189636d0a20d499aedf5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="owndeletesarevisible-method-sqlserverdatabasemetadata"></a>ownDeletesAreVisible-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft ab, ob die eigenen Löschvorgänge eines Resultsets sichtbar sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean ownDeletesAreVisible(int type)  
```  
  
#### <a name="parameters"></a>Parameter  
 *type*  
  
 Ein **Int** , der angibt, das Resultset-Datentyp, der einen der folgenden Werte sein kann, wie in der java.sql.ResultSet "oder" SQLServerResultSet definiert:  
  
## <a name="javasqlresultset-types"></a>java.sql.ResultSet-Typen  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>SQLServerResultSet-Typen  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn die Löschvorgänge sichtbar sind. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese OwnDeletesAreVisible-Methode wird von der OwnDeletesAreVisible-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

