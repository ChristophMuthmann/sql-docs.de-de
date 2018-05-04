---
title: SetBytes-Methode (long, Byte) | Microsoft Docs
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
- SQLServerBlob.setBytes (long.byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ffb8f107-0f9d-4410-957f-62b718e1e872
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76cef0c2fb651669528b9aceeb76138a8033cf91
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setbytes-method-long-byte"></a>SetBytes-Methode (long, Byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Schreibt das angegebene Bytearray ab der angegebenen Position in das BLOB und gibt anschließend die Anzahl der geschriebenen Bytes zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes)  
```  
  
#### <a name="parameters"></a>Parameter  
 *POS*  
  
 Die Position (1-basiert) im BLOB, an dem Schreiben der Daten beginnen.  
  
 *Bytes*  
  
 Das in den BLOB zu schreibende Bytearray.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **lange** Wert, der die Anzahl der geschriebenen Bytes angibt.  
  
## <a name="exceptions"></a>Ausnahmen  
 java.sql.SQLException  
  
## <a name="remarks"></a>Hinweise  
 Diese SetBytes-Methode wird von der SetBytes-Methode in der java.sql.Blob-Schnittstelle angegeben.  
  
 Daten werden beginnend mit der angegebenen Position überschrieben, und sie können die ursprüngliche Länge des BLOB übersteigen. Durch Angeben eines Werts vom Typ Position+1 werden Bytes an die Zeichenfolge angefügt. Durch Weitergeben eines Werts vom Typ Position+2 oder größer (oder null oder weniger) wird ein Positionsfehler ausgelöst. Übergeben eine leere **Byte** Array gibt 0 (null) zurück, weil keine Bytes geschrieben wurden.  
  
## <a name="see-also"></a>Siehe auch  
 [SetBytes-Methode &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [SQLServerBlob-Methoden](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob-Elemente](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob-Klasse](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
