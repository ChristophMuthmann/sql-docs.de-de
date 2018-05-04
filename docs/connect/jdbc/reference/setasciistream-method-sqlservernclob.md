---
title: SetAsciiStream-Methode (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 617ece92-0fb1-4f95-b32d-29b5b56eb3fb
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 89906ee626bc16d1b3c5b1b4f83fa5b4c4b8f15d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setasciistream-method-sqlservernclob"></a>setAsciiStream-Methode (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft ein Stream zum Schreiben von ASCII zu verwendende Zeichen, um die **NCLOB** Wert, den diese **java.sql.NClob** -Objekt darstellt, ab der angegebenen Position.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.io.OutputStream setAsciiStream(long pos)  
```  
  
#### <a name="parameters"></a>Parameter  
 *POS*  
  
 Die Position, an dem Daten geschrieben werden, die **NCLOB** Objekt; die erste Position ist 1.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein OutputStream-Objekt, das den Datenstrom steht, den ASCII-Zeichen codierte, geschrieben werden können.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetAsciiStream-Methode wird von der SetAsciiStream-Methode in der java.sql.NClob-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerNClob-Methoden](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob-Elemente](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob-Klasse](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
