---
title: GetTimestamp-Methode (Int, java.util.Calendar) | Microsoft Docs
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
- SQLServerCallableStatement.getTimestamp (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 161c559a-8651-44ba-a914-15eb6a612417
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42c3ccd58cc8e3c7775d701ea0a48e1619e9a588
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="gettimestamp-method-int-javautilcalendar"></a>getTimestamp-Methode (int, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Parameters als java.sql.Timestamp-Objekt in der Programmiersprache Java ab, Berücksichtigung des parameterindexes und unter Verwendung eines Kalenders-Objekts ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.Timestamp getTimestamp(int index,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parameter  
 *index*  
  
 Ein **Int** , der die Indexnummer des Parameters angibt.  
  
 *CAL*  
  
 Ein Kalenderobjekt.  
  
## <a name="return-value"></a>Rückgabewert  
 Eine Timestamp-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetTimestamp-Methode wird von der GetTimestamp-Methode in der java.sql.CallableStatement-Schnittstelle angegeben.  
  
 Diese Methode gibt nur Werte aus [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **"DateTime"** und **Smalldatetime** Spalten.  
  
## <a name="see-also"></a>Siehe auch  
 [GetTimestamp-Methode &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement-Klasse](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
