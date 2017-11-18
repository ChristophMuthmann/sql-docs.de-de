---
title: NativeSQL-Methode (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.nativeSQL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2188a6e1-792f-47bd-b207-1d01741231b2
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d369669f3bcd8aff09cf14906b7b3a163385384f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="nativesql-method-sqlserverconnection"></a>nativeSQL-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Konvertiert die angegebene SQL-Anweisung zur systemeigenen SQL-Grammatik des Datenbankservers.  
  
> [!NOTE]  
>  Diese Methode wird derzeit nicht unterstützt durch die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String nativeSQL(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parameter  
 *SQL*  
  
 Ein **Zeichenfolge** , die eine SQL-Anweisung enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** , die die konvertierte SQL-Anweisung enthält.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese NativeSQL-Methode wird von der NativeSQL-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

