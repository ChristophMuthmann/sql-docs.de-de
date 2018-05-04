---
title: SetServerPreparedStatementDiscardThreshold-Methode (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.setServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a2461ae9f0728971b54d033b2b215092becc0ae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>SetServerPreparedStatementDiscardThreshold-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Gibt das Verhalten für eine bestimmte Verbindung-Instanz. Diese Einstellung steuert, wie viele ausstehenden verwerfen Anweisung vorbereitet, die Aktionen (Sp_unprepare) Blockierungsvorgang pro Verbindung bleiben können, bevor ein Aufruf zum Bereinigen der ausstehende Handles auf dem Server ausgeführt wird. Wenn die Einstellung ist < = 1 un-vorbereiten Aktionen sofort auf Schließen die vorbereitete Anweisung ausgeführt werden. Wenn der Wert 1 > festgelegt ist werden diese Aufrufe zusammen als Batch ausgeführt um Sp_unprepare zu häufig aufrufen verbundenen Aufwand zu vermeiden.


## <a name="syntax"></a>Syntax  
  
```  
  
public void setServerPreparedStatementDiscardThreshold(boolean thresholdValue)  
```  

#### <a name="parameters"></a>Parameter  
 *thresholdValue*  
 
 Der neue Wert für die **ServerPreparedStatementDiscardThreshold** Connection-Eigenschaft.  
 
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Hinweise  
 Diese Methode wird von JDBC Driver, Version 6.4 verfügbar und Weitergabe.
 
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
