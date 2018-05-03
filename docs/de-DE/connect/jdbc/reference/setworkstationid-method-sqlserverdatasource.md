---
title: SetWorkstationID-Methode (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.setWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c1093615-90bf-4918-9f05-8abd765ffb03
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e505445d3ea1a7f9ba96b46b2764893d4628ed3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setworkstationid-method-sqlserverdatasource"></a>setWorkstationID-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den Namen des Clients Computernamen, die für die Verbindung mit der Datenquelle verwendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setWorkstationID(java.lang.String workstationID)  
```  
  
#### <a name="parameters"></a>Parameter  
 *workstationID*  
  
 Ein **Zeichenfolge** , enthält der Name des Clientcomputers.  
  
## <a name="remarks"></a>Hinweise  
 Die workstationID ist der Name des Clientcomputers oder der Workstation. Wenn die WorkstationID-Eigenschaft nicht festgelegt ist, wird der Standardwert durch Aufrufen der Methode InetAddress.getLocalHost().getHostName() erstellt. Wenn GetHostName einen leeren Wert zurückgibt, wird die getHostAddress().toString()-Methode aufgerufen.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
