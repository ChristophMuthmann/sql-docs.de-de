---
title: GetEnablePrepareOnFirstPreparedStatementCall-Methode (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
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
- SQLServerConnection.getEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b35678bdf98ee856bca40bfe1cb1b45ad680e2b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>GetEnablePrepareOnFirstPreparedStatementCall-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Gibt den Wert der **EnablePrepareOnFirstPreparedStatementCall** Connection-Eigenschaft. Wenn "false" die erste Ausführung Sp_executesql aufgerufen wird und nicht vorbereitet werden wird eine Anweisung, sobald die zweite Ausführung Vorgang erfolgt Sp_prepexec aufrufen und tatsächlich einem vorbereiteten Anweisungshandle einrichten. Nach der Ausführung wird Sp_execute aufgerufen. Dies entlastet die Notwendigkeit Sp_unprepare für vorbereitete Anweisung schließen, wenn die Anweisung nur einmal ausgeführt wird. Der Standardwert für diese Option kann durch Aufrufen von setDefaultEnablePrepareOnFirstPreparedStatementCall() geändert werden.

## <a name="syntax"></a>Syntax  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>Rückgabewert
 Ein **booleschen** , enthält den Wert der **EnablePrepareOnFirstPreparedStatementCall** Connection-Eigenschaft.

## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Hinweise  
 Diese Methode wird von JDBC Driver, Version 6.4 verfügbar und Weitergabe.
 
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
