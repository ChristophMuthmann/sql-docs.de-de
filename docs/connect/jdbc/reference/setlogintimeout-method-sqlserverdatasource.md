---
title: SetLoginTimeout-Methode (SQLServerDataSource) | Microsoft Docs
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
apiname: SQLServerDataSource.setLoginTimeout
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4a65f835792fc342cbbcc3803c9a3be6d0bb9214
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>setLoginTimeout-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt die Anzahl der Sekunden, die dies [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) -Objekt beim Versuch zum Herstellen eine Verbindung gewartet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Anmeldungstimeout*  
  
 Ein **Int** Wert, der die Anzahl der Sekunden darstellt. Mit dem Wert "0" wird angegeben, dass es sich bei dem Timeout um das Standardsystemtimeout (standardmäßig 15 Sekunden) handelt.  
  
## <a name="remarks"></a>Hinweise  
 Diese SetLoginTimeout-Methode wird von der SetLoginTimeout-Methode in der javax.sql.DataSource-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
