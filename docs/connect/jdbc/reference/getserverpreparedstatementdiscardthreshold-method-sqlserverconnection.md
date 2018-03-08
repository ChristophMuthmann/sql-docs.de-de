---
title: GetServerPreparedStatementDiscardThreshold-Methode (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.getServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 680c7fe2fe0802054f56008701af48baea4ac98b
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2018
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>GetServerPreparedStatementDiscardThreshold-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Gibt den Wert der **ServerPreparedStatementDiscardThreshold** Connection-Eigenschaft. Diese Einstellung steuert, wie viele ausstehenden verwerfen Anweisung vorbereitet, die Aktionen (Sp_unprepare) Blockierungsvorgang pro Verbindung bleiben können, bevor ein Aufruf zum Bereinigen der ausstehende Handles auf dem Server ausgeführt wird. Wenn die Einstellung < = 1, unprepare Aktionen sofort auf Schließen die vorbereitete Anweisung ausgeführt werden. Wenn sie auf > 1 festgelegt ist, sind diese Aufrufe zusammen als Batch ausgeführt um Sp_unprepare zu häufig aufrufen verbundenen Aufwand zu vermeiden. Der Standardwert für diese Option kann durch Aufrufen von getDefaultServerPreparedStatementDiscardThreshold() geändert werden.

## <a name="syntax"></a>Syntax  
  
```  
  
public int getServerPreparedStatementDiscardThreshold()  
```  

## <a name="return-value"></a>Rückgabewert
 Ein **Int** , enthält den Wert der **ServerPreparedStatementDiscardThreshold** Connection-Eigenschaft.

## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Hinweise  
 Diese Methode wird von JDBC Driver, Version 6.4 verfügbar und Weitergabe.
 
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
