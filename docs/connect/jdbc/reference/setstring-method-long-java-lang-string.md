---
title: SetString-Methode (long, java.lang.String) | Microsoft Docs
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
- SQLServerClob.setString (long, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1b2190e9-5ace-497a-8554-0e913ea9b0cb
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48082cf2a16fe499fbde2ef8cb29f89e028eee15
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
  
 *S*  
  
 Die **Zeichenfolge** in das CLOB geschrieben werden.  
  
## <a name="return-value"></a>Rückgabewert  
 Die Anzahl der geschriebenen Zeichen.  
  
## <a name="exceptions"></a>Ausnahmen  
 java.sql.SQLException  
  
## <a name="remarks"></a>Hinweise  
 Diese SetString-Methode wird von der SetString-Methode in der java.sql.Clob-Schnittstelle angegeben.  
  
 Zeichendaten werden beginnend mit der angegebenen Position überschrieben, und sie können die ursprüngliche Länge des CLOB übersteigen. Durch Angeben eines Werts vom Typ "Position+1" wird die Zeichenfolge angefügt. Angeben einer Position + 2 oder größer (oder 0 (null) oder kleiner) Werte, werden ein positionsfehler ausgelöst wird.  
  
## <a name="see-also"></a>Siehe auch  
 [SetString-Methode &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)   
 [SQLServerClob-Methoden](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob-Elemente](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob-Klasse](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
