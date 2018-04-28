---
title: GetConnection-Methode (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerDataSource.getConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 78db89d6-a8a0-4116-8885-548e627220ed
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6aee1b8785ade7b3fc1a9c286357bdbc82338ddc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="getconnection-method-javalangstring-javalangstring"></a>getConnection-Methode (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Versucht, die zum Herstellen einer Verbindung mit den Daten Datenquelle, die von diesem [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Objekt darstellt, mit den angegebenen Benutzernamen und Kennwort.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.Connection getConnection(java.lang.String username,  
                                         java.lang.String password)  
```  
  
#### <a name="parameters"></a>Parameter  
 *username*  
  
 Ein **Zeichenfolge** , die den Benutzernamen enthält.  
  
 *password*  
  
 Ein **Zeichenfolge** , die das Kennwort enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 java.sql.SQLException  
  
## <a name="remarks"></a>Hinweise  
 Diese GetConnection-Methode wird durch die GetConnection-Methode in der javax.sql.DataSource-Schnittstelle angegeben.  
  
 Aufrufen der GetConnection ersetzt Methode mit einem nicht-Null-Benutzername oder Kennwort Benutzereigenschaften Name und Kennwort, die in der SQLServerDataSource-Klasse festgelegt werden, wenn das SQLServerConnection-Objekt zu initialisieren. Wenn der Aufrufer aufgerufen hat z. B. [SetUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) und [SetPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) für der Datenquelle, und klicken Sie dann GetConnection-Aufrufe und stellt eine nicht-Null-Benutzernamen oder ein Kennwort ungleich Null, den Benutzernamen und das Kennwort festgelegt wird SetUser und SetPassword werden durch den Benutzernamen und Kennwort GetConnection übergebenen ersetzt.  
  
> [!NOTE]  
>  Der Benutzername und das Kennwort, die in der URL festgelegt sind, mithilfe eines Aufrufs an die [SetURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md) Methode wird in diesem Fall nicht geändert werden.  
  
## <a name="see-also"></a>Siehe auch  
 [GetConnection-Methode &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
