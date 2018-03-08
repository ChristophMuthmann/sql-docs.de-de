---
title: GetEnablePrepareOnFirstPreparedStatementCall-Methode (SQLServerConnection) | Microsoft Docs
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
apiname:
- SQLServerConnection.getEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 624072532d643d9a335533b861ae0184171ba259
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2018
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
  
  
