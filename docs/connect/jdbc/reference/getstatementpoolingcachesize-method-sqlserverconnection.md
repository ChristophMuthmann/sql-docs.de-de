---
title: GetStatementPoolingCacheSize-Methode (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.getStatementPoolingCacheSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d8216c6d918a0333fdc88b3254736bd73f4be0bb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getstatementpoolingcachesize-method-sqlserverconnection"></a>GetStatementPoolingCacheSize-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Gibt die Größe des Caches vorbereitete Anweisung für diese Verbindung zurück. '0' bedeutet Zwischenspeichern nicht aktiviert.

## <a name="syntax"></a>Syntax  
  
```  
  
public int getStatementPoolingCacheSize()  
```  

## <a name="return-value"></a>Rückgabewert
 Ein **Int** , enthält den Wert der **StatementPoolingCacheSize** Connection-Eigenschaft.

## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Hinweise  
 Diese Methode wird von JDBC Driver, Version 6.4 verfügbar und Weitergabe.
 
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
