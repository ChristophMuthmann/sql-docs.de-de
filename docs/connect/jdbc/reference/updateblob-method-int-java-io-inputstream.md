---
title: UpdateBlob-Methode (Int, java.io.InputStream) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d0263018-d326-4a7b-bf6f-5f508db899d4
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cd8fe5107041959e95493adcab96175058c25523
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="updateblob-method-int-javaioinputstream"></a>updateBlob-Methode (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte unter Verwendung des angegebenen Eingabedatenstroms.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void updateBlob(int columnIndex,  
                       java.io.InputStream inputStream)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnIndex*  
  
 Ein **Int** , der den Spaltenindex angibt.  
  
 *inputStream*  
  
 Ein InputStream-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese UpdateBlob-Methode wird von der UpdateBlob-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateBlob-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
