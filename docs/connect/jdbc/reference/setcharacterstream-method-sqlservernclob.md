---
title: SetCharacterStream-Methode (SQLServerNClob) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 09042ee9-dfb1-4d0b-82bd-d1224b0aea80
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 54ea45119a144852daff92dac5037b6f7407d259
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setcharacterstream-method-sqlservernclob"></a>setCharacterStream-Methode (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft einen Datenstrom verwendet werden soll, schreiben einen Stream von Unicode-Zeichen ab der **NCLOB** Wert, den diese **java.sql.NClob** -Objekt darstellt, ab der angegebenen Position.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.io.Writer setCharacterStream(long pos)  
```  
  
#### <a name="parameters"></a>Parameter  
 *POS*  
  
 Die Position, an dem Daten geschrieben werden, die **NCLOB** Wert; die erste Position ist 1.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Writerobjekt, das den Datenstrom steht, in welche Unicode codierte Zeichen geschrieben werden können.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetCharacterStream-Methode wird von der SetCharacterStream-Methode in der java.sql.NClob-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerNClob-Methoden](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob-Elemente](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob-Klasse](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  

