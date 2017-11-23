---
title: SetUnicodeStream-Methode (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerPreparedStatement.setUnicodeStream
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 0a413e83-e0a4-41f8-9fe0-33ce4d368ee4
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e39cd2346c7f7c720f120c675b1540f90e81d5fe
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="setunicodestream-method-sqlserverpreparedstatement"></a>SetUnicodeStream-Methode (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt die angegebene Parameternummer auf den angegebenen Eingabedatenstrom, mit der angegebenen Anzahl von Bytes fest.  
  
> [!NOTE]  
>  Diese Methode wurde in der JDBC-Spezifikation als veraltet angegeben. Bei Aufruf der Methode wird eine Ausnahme vom Typ "Nicht implementiert" ausgelöst.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final void setUnicodeStream(int n,  
                                   java.io.InputStream x,  
                                   int length)  
```  
  
#### <a name="parameters"></a>Parameter  
 *n*  
  
 Ein **Int** , der die Parameteranzahl angibt.  
  
 *x*  
  
 Ein InputStream-Objekt.  
  
 *length*  
  
 Die Anzahl der Bytes.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetUnicodeStream-Methode wird von der SetUnicodeStream-Methode in der java.sql.PreparedStatement-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerPreparedStatement-Elemente](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement-Klasse](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
