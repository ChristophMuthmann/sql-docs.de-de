---
title: SetBinaryStream-Methode (SQLServerBlob) | Microsoft Docs
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
- SQLServerBlob.setBinaryStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: abcec31f-1a60-4765-9725-8cf7e9f1f8ab
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c32868257eeebc4cfc24945d853e1440e34ee78
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setbinarystream-method-sqlserverblob"></a>setBinaryStream-Methode (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft einen Datenstrom ab, mit dem in den BLOB-Wert geschrieben werden kann.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.io.OutputStream setBinaryStream(long pos)  
```  
  
#### <a name="parameters"></a>Parameter  
 *POS*  
  
 Die Position im BLOB-Wert, an der geschrieben werden soll.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Ausgabedatenstrom.  
  
## <a name="exceptions"></a>Ausnahmen  
 java.sql.SQLException  
  
## <a name="remarks"></a>Hinweise  
 Diese SetBinaryStream-Methode wird von der SetBinaryStream-Methode in der java.sql.Blob-Schnittstelle angegeben.  
  
 Daten im BLOB werden beginnend mit der angegebenen Position vom Ausgabedatenstrom überschrieben, und sie können die ursprüngliche Länge des BLOB übersteigen. Durch Angeben einer Position + Wert 1 werden Bytes angefügt werden. Durch Weitergeben eines Werts vom Typ Position+2 oder größer (oder null oder weniger) wird ein Positionsfehler ausgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerBlob-Methoden](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob-Elemente](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob-Klasse](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
