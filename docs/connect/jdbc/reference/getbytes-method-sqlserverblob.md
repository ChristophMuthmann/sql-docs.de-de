---
title: GetBytes-Methode (SQLServerBlob) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerBlob.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea1b810-b5c1-466d-bdc4-561468214632
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8f1139f0deb886265da6c7c56e682372155a0e3b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getbytes-method-sqlserverblob"></a>getBytes-Methode (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft die BLOB-Daten als Bytearray ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public byte[] getBytes(long pos,  
                       int length)  
```  
  
#### <a name="parameters"></a>Parameter  
 *POS*  
  
 Die Startposition, beginnend bei "1" (nicht "0").  
  
 *length*  
  
 Die Länge der abzurufenden Daten.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Byte** Array, das die angeforderten Daten enthält.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetBytes-Methode wird von der GetBytes-Methode in der java.sql.Blob-Schnittstelle angegeben.  
  
 Wenn Sie Null oder 0 (null) BLOB mit der Länge haben, und versuchen, genau 0 Bytes an Position 1, eine leere abzurufen **Byte** Array zurückgegeben (Bytearray der Länge 0).  
  
 Bei einem BLOB mit der Länge Null wird beim Versuch, eine beliebige Länge in Bytes an einer anderen Position als "1" abzurufen, eine Positionsausnahme ausgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerBlob-Methoden](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob-Elemente](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob-Klasse](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
