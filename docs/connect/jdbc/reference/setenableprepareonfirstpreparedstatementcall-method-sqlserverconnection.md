---
title: SetEnablePrepareOnFirstPreparedStatementCall-Methode (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.setEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea672e1cd3b5998ca6829fb0f4c9fae29773d9d2
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2018
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>SetEnablePrepareOnFirstPreparedStatementCall-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Gibt das Verhalten für eine bestimmte Verbindung-Instanz. Falls der Wert "false" die erste Ausführung Sp_executesql aufgerufen wird und keine Anweisung vorbereiten, sobald die zweite Ausführung erfolgt, wird er Sp_prepexec aufrufen und tatsächlich einem vorbereiteten Anweisungshandle einrichten. Nach der Ausführung wird Sp_execute aufgerufen. Dies entlastet die Notwendigkeit Sp_unprepare für vorbereitete Anweisung schließen, wenn die Anweisung nur einmal ausgeführt wird.

## <a name="syntax"></a>Syntax  
  
```  
  
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)  
```  
  
#### <a name="parameters"></a>Parameter  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 Der neue Wert für die **EnablePrepareOnFirstPreparedStatementCall** Connection-Eigenschaft.  
 
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Hinweise  
 Diese Methode wird von JDBC Driver, Version 6.4 verfügbar und Weitergabe.
 
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
