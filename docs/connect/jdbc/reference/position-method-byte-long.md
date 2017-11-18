---
title: Position-Methode (Byte, long) | Microsoft Docs
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
apiname:
- SQLServerBlob.position (byte[], long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 787412c2-4342-49c8-9ca2-7a9ddcd3277c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6d6a9eaec4548bbeff5e6c0879240f783301d211
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="position-method-byte-long"></a>Position-Methode (Byte, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt die Position eines angegebenen Musters im BLOB auf der Grundlage der angegebenen **Byte** array-Musters und des Startindexes.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public long position(byte[] bPattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>Parameter  
 *bPattern*  
  
 Das zu suchende Muster.  
  
 *Starten*  
  
 Der Startindex, in dem gesucht werden soll.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **lange** Wert, der die Position, in denen das Muster gefunden wurde, oder -1, wenn es nicht gefunden wurde.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese Position-Methode wird von der Position-Methode in der java.sql.Blob-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Positionieren Sie die Methode &#40; SQLServerBlob &#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [SQLServerBlob-Methoden](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob-Elemente](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob-Klasse](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

