---
title: GetReference-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b3fb1a97-86ee-4977-adca-c35ae199dbb3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ec73d5918cebbc5a3c8ccd8261fc492717d8660
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getreference-method-sqlserverdatasource"></a>getReference-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt einen Verweis auf diese [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Verweis-Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Diese GetReference-Methode wird von der GetReference-Methode in der javax.naming.Referenceable-Schnittstelle angegeben.  
  
 Vor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0 SQLServerDataSource.setTrustStorePassword für ein SQLServerDataSource-Objekt, das Kennwort würde werden im von SQLServerDataSource.getReference, und mit dem Objekt verwendet werden, um zurückgegebene Objekt vorhanden Stellen Sie zusätzliche Verbindungen. In JDBC Driver 3.0 muss das Kennwort für das von "SQLServerDataSource.getReference" zurückgegebene Objekt festgelegt werden, bevor Verbindungen mit dem Objekt hergestellt werden.  
  
 Wenn Sie "SQLServerDataSource.setTrustStorePassword" vor dem Binden der Datenquelleneigenschaften festlegen, muss "SQLServerDataSource.setTrustStorePassword" vor dem Herstellen der Verbindung aufgerufen werden. Beispiel:  
  
```  
ctx = new InitialContext(System.getProperties());  
  
SQLServerDataSource ds1 = (SQLServerDataSource) ctx.lookup(jndiName);  
  
ds1.setTrustStorePassword("XXXXX");  
Connection con = ds1.getConnection("user", "XXXXXX");  
  
ctx.rebind(jndiName, ds1);  
SQLServerDataSource ds2 = (SQLServerDataSource) ctx.lookup(jndiName);  
ds2.setTrustStorePassword("XXXXX");   // reset the truststore password  
con = ds2.getConnection("user", "XXXXXX");   // provide userid and password again  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
