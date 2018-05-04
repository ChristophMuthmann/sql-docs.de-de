---
title: IsValid-Methode (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3b0a8bbf-9369-4456-9ab8-1434ccacdd7e
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c1e65ecb40137e0da2de7abd8b5d40e7e744752
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="isvalid-method-sqlserverconnection"></a>isValid-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt an, ob dies [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt wurde nicht geschlossen, und noch gültig ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean isValid(int timeout)  
```  
  
#### <a name="parameters"></a>Parameter  
 *timeout*  
  
 Ein **Int** , die die Anzahl der Sekunden für die Überprüfung der Verbindung angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** Wenn die Verbindung gültig ist. **"false"** , wenn die Verbindung ungültig ist, oder die Gültigkeit der Verbindung kann nicht vor Ablauf des Timeouts ermittelt werden.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese IsValid-Methode wird von der IsValid-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
