---
title: SetString-Methode (long, java.lang.String) | Microsoft Docs
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
- SQLServerClob.setString (long, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1b2190e9-5ace-497a-8554-0e913ea9b0cb
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0b1bcd2dc8f6e6509099eb4529e57335942c9d6d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setstring-method-long-javalangstring"></a>setString-Methode (long, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Schreibt die angegebenen **Zeichenfolge** ab der angegebenenposition in das CLOB.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int setString(long pos,  
                     java.lang.String s)  
```  
  
#### <a name="parameters"></a>Parameter  
 *POS*  
  
 Die Position, an der Daten in das CLOB geschrieben werden sollen.  
  
 *s*  
  
 Die **Zeichenfolge** in das CLOB geschrieben werden.  
  
## <a name="return-value"></a>Rückgabewert  
 Die Anzahl der geschriebenen Zeichen.  
  
## <a name="exceptions"></a>Ausnahmen  
 java.sql.SQLException  
  
## <a name="remarks"></a>Hinweise  
 Diese SetString-Methode wird von der SetString-Methode in der java.sql.Clob-Schnittstelle angegeben.  
  
 Zeichendaten werden beginnend mit der angegebenen Position überschrieben, und sie können die ursprüngliche Länge des CLOB übersteigen. Durch Angeben eines Werts vom Typ "Position+1" wird die Zeichenfolge angefügt. Angeben einer Position + 2 oder größer (oder 0 (null) oder kleiner) Werte, werden ein positionsfehler ausgelöst wird.  
  
## <a name="see-also"></a>Siehe auch  
 [SetString-Methode &#40; SQLServerClob &#41;](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)   
 [SQLServerClob-Methoden](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob-Elemente](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob-Klasse](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

