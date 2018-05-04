---
title: IsWrapperFor-Methode (SQLServerDataSource) | Microsoft Docs
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
ms.assetid: f77af027-c021-4a17-b264-1ee592bfdd84
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1862175c31876c2391d2076929d146ec7a5a31a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="iswrapperfor-method-sqlserverdatasource"></a>isWrapperFor-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt an, ob es sich bei diesem Datenquellenobjekt um einen Wrapper für die angegebene Schnittstelle handelt.  
  
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
 Die [IsWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md) Methode und die [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) Methode definiert sind, von der java.sql.Wrapper-Schnittstelle, die in der JDBC 4.0-Spezifikationen eingeführt wird.  
  
 Wenn diese Methode gibt "true" zurück, der Aufruf von [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) mit dem gleichen Argument wird erfolgreich ausgeführt.  
  
 Weitere Informationen finden Sie unter [Wrapper und Schnittstellen](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Unwrap-Methode &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)   
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
