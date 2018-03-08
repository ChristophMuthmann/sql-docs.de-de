---
title: SQLServerException-Konstruktor (java.lang.String, java.lang.String, Int, "java.lang.Throwable") | Microsoft Docs
ms.custom: 
ms.date: 01/19/2018
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
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 98606e1dfa903c49ecd1152e49ca7d16406b167a
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2018
---
# <a name="sqlserverexception-constructor-javalangstring-javalangstring-int-javalangthrowable"></a>SQLServerException-Konstruktor (java.lang.String, java.lang.String, Int, "java.lang.Throwable")
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Initialisiert eine neue Instanz der der [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) Klasse, sofern eine **Zeichenfolge** -Objekt, eine **Zeichenfolge** -Objekt, ein **Int**, und eine **auslösbares** Objekt.

## <a name="syntax"></a>Syntax  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState errState,
            int errNum,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>Parameter  
 *errText*  
  
 Eine Zeichenfolge mit dem Fehlertext.
  
 *errState*  
  
 Eine Zeichenfolge, die den Status des Fehlers enthält.
 
 *errNum*  
  
 Einen int-Wert, der den Fehlercode für die ausgelöste Ausnahme enthält.
 
 *cause*  
  
 Ein auslösbares-Objekt, das die Ursache der Ausnahme enthält.
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerException-Konstruktoren](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException-Elemente](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException-Klasse](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
