---
title: SetCharacterStream-Methode (SQLServerClob) | Microsoft Docs
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
- SQLServerClob.setCharacterStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c02778f2-6681-4a84-a58b-2bcfac4233e4
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e511d31aaef8dbd550472b1f9e3ebf9393643fe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setcharacterstream-method-sqlserverclob"></a>setCharacterStream-Methode (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt einen Datenstrom zurück, der verwendet wird, um ab der angegebenenPosition einen Unicode-Zeichendatenstrom in das CLOB zu schreiben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.io.Writer setCharacterStream(long pos)  
```  
  
#### <a name="parameters"></a>Parameter  
 *POS*  
  
 Die Position, an der Daten in das CLOB-Objekt geschrieben werden sollen.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Datenstrom, in den Unicode-codierte Zeichen geschrieben werden können.  
  
## <a name="exceptions"></a>Ausnahmen  
 java.sql.SQLException  
  
## <a name="remarks"></a>Hinweise  
 Diese SetCharacterStream-Methode wird von der SetCharacterStream-Methode in der java.sql.Clob-Schnittstelle angegeben.  
  
 Zeichendaten im CLOB werden beginnend mit der angegebenen Position vom Schreiber überschrieben, und sie können die ursprüngliche Länge des CLOB übersteigen. Durch Angeben eines Werts vom Typ Position+1 werden Zeichen angefügt. Durch Angeben eines Werts vom Typ Position+2 oder größer (oder null oder weniger) wird ein Positionsfehler ausgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerClob-Methoden](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob-Elemente](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob-Klasse](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
