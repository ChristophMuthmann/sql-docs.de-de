---
title: SetWorkstationID-Methode (SQLServerDataSource) | Microsoft Docs
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
apiname: SQLServerDataSource.setWorkstationID
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: c1093615-90bf-4918-9f05-8abd765ffb03
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bd2d1ad16dd1ff622c7d8f4f8394df08bdfd3f6a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
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
  
  
