---
title: SetSavepoint-Methode (java.lang.String) | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLServerConnection.setSavepoint (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1cf15ec4-d9d9-4ab3-bfee-2ea43ff609a6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 27e8f14b96b7b0f95e5134703d9fd480ae778e1f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setsavepoint-method-javalangstring"></a>setSavepoint-Methode (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Erstellt einen Sicherungspunkt mit dem angegebenen Namen in der aktuellen Transaktion und gibt die neue [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) Objekt, das sie darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.Savepoint setSavepoint(java.lang.String sName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *sName*  
  
 Ein **Zeichenfolge** Wert, der den Namen des Sicherungspunkts enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Sicherungspunkt-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetSavePoint-Methode wird von der SetSavePoint-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
 Die *sName* Argument wird automatisch mit Escapezeichen versehen von der [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [SetSavepoint-Methode &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)   
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
