---
title: PrepareCall-Methode (java.lang.String) | Microsoft Docs
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
apiname: SQLServerConnection.prepareCall (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: cb83b567-4ce5-447a-93cc-895d4eaf3a05
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1d908f7417a637f86c743af36e4a1ec624192663
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="preparecall-method-javalangstring"></a>prepareCall-Methode (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Erstellt eine [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) Objekt für die Datenbank gespeicherten Prozeduren aufrufen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parameter  
 *SQL*  
  
 Ein **Zeichenfolge** , die eine SQL-Anweisung enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein CallableStatement-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese PrepareCall-Methode wird von der PrepareCall-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [PrepareCall-Methode &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
