---
title: GetWorkstationID-Methode (SQLServerDataSource) | Microsoft Docs
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
apiname: SQLServerDataSource.getWorkstationID
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: f6a701de-a8fa-4668-9310-99a8c6e32c88
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f246bdc08ac9486da5fb5bee00b32128f2092fa
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="getworkstationid-method-sqlserverdatasource"></a>getWorkstationID-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt den Namen des Clientcomputers zurück, der zum Herstellen einer Verbindung mit der Datenquelle verwendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getWorkstationID()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** , enthält der Name des Clientcomputers.  
  
## <a name="remarks"></a>Hinweise  
 Die workstationID ist der Name des Clientcomputers oder der Workstation. Wenn die WorkstationID-Eigenschaft nicht festgelegt ist, wird der Standardwert durch Aufrufen der Methode InetAddress.getLocalHost().getHostName() erstellt. Wenn GetHostName einen leeren Wert zurückgibt, wird die getHostAddress().toString()-Methode aufgerufen.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
