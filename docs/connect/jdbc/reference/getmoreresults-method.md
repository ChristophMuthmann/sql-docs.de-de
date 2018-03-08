---
title: GetMoreResults-Methode () | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerStatement.getMoreResults ()
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: df89db50-0b2f-4094-820a-30be25ad72fe
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2cf885b73a0d4e0f2d5b8aa1f75255f74001c59d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="getmoreresults-method-"></a>getMoreResults-Methode ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Wechselt zum nächsten Ergebnis dieses [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final boolean getMoreResults()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn das zurückgegebene Ergebnis ein Resultset handelt. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetMoreResults-Methode wird von der GetMoreResults-Methode in der java.sql.Statement-Schnittstelle angegeben.  
  
 Die GetMoreResults-Methode implizit aufrufen schließt alle aktuell geöffneten Resultsetobjekte, die mit abgerufen werden die [GetResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) Methode.  
  
## <a name="see-also"></a>Siehe auch  
 [GetMoreResults-Methode &#40; SQLServerStatement &#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement-Elemente](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
