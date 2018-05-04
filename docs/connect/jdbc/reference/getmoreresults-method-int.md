---
title: GetMoreResults-Methode (Int) | Microsoft Docs
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
- SQLServerStatement.getMoreResults (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6419e5a8-8b3a-4d5b-8226-95865c52c723
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36a9cf3bfb2b6032694f9e33895b379bd83713ec
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getmoreresults-method-int"></a>getMoreResults-Methode (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Wechselt zum nächsten Ergebnis dieses [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt und Geschäfte mit dem alle aktuell geöffneten Ergebnis ereignissatzobjekte gemäß den Anweisungen durch den angegebenen Modus.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final boolean getMoreResults(int mode)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Modus*  
  
 Ein **Int** , der derzeit geöffneten Resultsetobjekte behandeln angibt. Dabei muss es sich um eine der folgenden Konstanten sein:  
  
 CLOSE_CURRENT_RESULT  
  
 KEEP_CURRENT_RESULT (vom JDBC-Treiber nicht unterstützt)  
  
 CLOSE_ALL_RESULTS  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn das zurückgegebene Ergebnis ein Resultset handelt. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetMoreResults-Methode wird von der GetMoreResults-Methode in der java.sql.Statement-Schnittstelle angegeben.  
  
 Wenn Sie die GetMoreResults-Methode aufgerufen wird, bevor Ergebnisse abgerufen werden, verhält es sich entsprechend den Angaben von der *Modus* Argument und wechselt zum nächsten Ergebnis.  
  
> [!NOTE]  
>  Die Verwendung der Konstante KEEP_CURRENT_RESULT wird vom JDBC-Treiber nicht unterstützt. Bei ihrer Verwendung wird eine Ausnahme ausgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 [GetMoreResults-Methode &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement-Elemente](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
