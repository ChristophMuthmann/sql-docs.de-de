---
title: IsReadOnly-Methode (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.isReadOnly
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 902fd2c1-05e0-436e-9779-c048cdb8475a
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aac3bcc065ba1e02a17091113bea98d61b3c668e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="isreadonly-method-sqlserverconnection"></a>isReadOnly-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt an, ob dies [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt befindet sich im schreibgeschützten Modus.  
  
> [!NOTE]  
>  Diese Methode wird derzeit nicht unterstützt durch die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean isReadOnly()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** im Nur-Lese Modus ist die Verbindung **"false"** wird jedoch nicht.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese IsReadOnly-Methode wird von der IsReadOnly-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
