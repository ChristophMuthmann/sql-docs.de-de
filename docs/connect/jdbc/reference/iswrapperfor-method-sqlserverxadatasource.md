---
title: IsWrapperFor-Methode (SQLServerXADataSource) | Microsoft Docs
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
ms.assetid: d612461d-4c3f-46db-b968-ff4c80b2aa7c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1ddb50ed8c8e8cc58ec2e8f14d6af51c1d8dcff
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="iswrapperfor-method-sqlserverxadatasource"></a>isWrapperFor-Methode (SQLServerXADataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt an, ob es sich bei diesem Objekt um einen Wrapper für die angegebene Schnittstelle handelt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>Parameter  
 *iface*  
  
 Ein **Klasse** zum Definieren einer Schnittstelle.  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** wenn diesem Objekt die Schnittstelle implementiert oder dient als Wrapper für ein Objekt, das die Schnittstelle implementiert. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Die [IsWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md) Methode und die [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) Methode definiert sind, von der java.sql.Wrapper-Schnittstelle, die in der JDBC 4.0-Spezifikationen eingeführt wird.  
  
 Wenn diese Methode gibt "true" zurück, der Aufruf von [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) mit dem gleichen Argument wird erfolgreich ausgeführt.  
  
 Weitere Informationen finden Sie unter [Wrapper und Schnittstellen](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Unwrap-Methode &#40;SQLServerXADataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)   
 [SQLServerXADataSource-Methoden](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [SQLServerXADataSource-Elemente](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [SQLServerXADataSource-Klasse](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
