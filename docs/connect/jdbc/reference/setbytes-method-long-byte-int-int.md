---
title: SetBytes-Methode (long, Byte, Int, Int) | Microsoft Docs
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
- SQLServerBlob.setBytes (long.byte[], int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7def226c-b211-459e-8c1a-08592d75d4a4
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b18005c16cd62358eb5f269504fc9d80eadb6de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setbytes-method-long-byte-int-int"></a>SetBytes-Methode (long, Byte, Int, Int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Schreibt alle oder einen Teil des angegebenen Arrays von Bytes in das BLOB, ab der angegebenen Position, den Offset und die Länge. und gibt dann die Anzahl der geschriebenen Bytes zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes,  
                    int offset,  
                    int len)  
```  
  
#### <a name="parameters"></a>Parameter  
 *POS*  
  
 Die Position (1-basiert) im BLOB, ab der Daten geschrieben werden.  
  
 *Bytes*  
  
 Das in den BLOB zu schreibende Bytearray.  
  
 *offset*  
  
 Der Offset im array, wo Sie beginnen, Lesen von Daten aus der **Byte** Array.  
  
 *len*  
  
 Die Anzahl von Bytes, die aus dem Bytearray in das BLOB geschrieben werden sollen.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** mit der Anzahl der geschriebenen Bytes.  
  
## <a name="exceptions"></a>Ausnahmen  
 java.sql.SQLException  
  
## <a name="remarks"></a>Hinweise  
 Diese SetBytes-Methode wird von der SetBytes-Methode in der java.sql.Blob-Schnittstelle angegeben.  
  
 Daten werden beginnend mit der angegebenen Position überschrieben und Sie können die ursprüngliche Länge des BLOB übersteigen. Durch Angeben eines Werts vom Typ Position+1 werden Bytes an die Zeichenfolge angefügt. Durch Weitergeben eines Werts vom Typ Position+2 oder größer (oder null oder weniger) wird ein Positionsfehler ausgelöst. Übergeben eine leere **Byte** Array gibt 0 (null) zurück, weil keine Bytes geschrieben wurden.  
  
## <a name="see-also"></a>Siehe auch  
 [SetBytes-Methode &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [SQLServerBlob-Methoden](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob-Elemente](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob-Klasse](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
