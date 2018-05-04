---
title: GetCharacterStream-Methode (long, Long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d70f502f-f60f-436a-83e6-797a0ed71bf3
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea78140d5a0bd24a71d9ab4c846ded3e74822f18
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getcharacterstream-method-long-long"></a>getCharacterStream-Methode (long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt die **Clob** Daten als Readerobjekt oder als zeichendatenstrom mit der angegebenen Position und Länge.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                         long length)  
```  
  
#### <a name="parameters"></a>Parameter  
 *POS*  
  
 Ein **lange** , die angibt, dass des Offsets zum ersten Zeichen des abzurufenden abgerufen werden sollen.  
  
 *length*  
  
 Ein **lang** , der angibt, dass der Länge in Zeichen des abzurufenden abgerufen werden sollen.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Readerobjekt, enthält die **Clob** Daten.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetCharacterStream-Methode wird von der GetCharacterStream-Methode in der java.sql.Clob-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [GetCharacterStream-Methode &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)   
 [SQLServerClob-Methoden](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob-Elemente](../../../connect/jdbc/reference/sqlserverclob-members.md)  
  
  
