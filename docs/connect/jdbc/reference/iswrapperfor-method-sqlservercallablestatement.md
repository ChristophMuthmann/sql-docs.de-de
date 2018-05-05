---
title: IsWrapperFor-Methode (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 71156863-3588-453e-b5a5-0573b2c1bebf
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4b0474c6301b450bcb8f43ffaaad66cfdcb56aa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="iswrapperfor-method-sqlservercallablestatement"></a>isWrapperFor-Methode (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt an, ob es sich bei diesem Anweisungsobjekt um einen Wrapper für die angegebene Schnittstelle handelt.  
  
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
 Die [IsWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md) Methode und die [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md) Methode definiert sind, von der java.sql.Wrapper-Schnittstelle, die in JDBC 4.0 eingeführt wird.  
  
 Wenn diese Methode zurückgibt **"true"** Aufrufen [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md) mit dem gleichen Argument wird erfolgreich ausgeführt.  
  
 Weitere Informationen finden Sie unter [Wrapper und Schnittstellen](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Unwrap-Methode &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement-Klasse](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
