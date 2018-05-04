---
title: GetLoginTimeout-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 316f067c-9e08-456a-af19-b80b0bbd4a5c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 607cc4a0e9de863e9253a6767396aa3b9b4cfbe9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getlogintimeout-method-sqlserverdatasource"></a>getLoginTimeout-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt die Anzahl von Sekunden zurück, die von diesem [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) -Objekt beim Versuch zum Herstellen eine Verbindung gewartet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int getLoginTimeout()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** Wert, der die Anzahl der Sekunden darstellt.  
  
## <a name="remarks"></a>Hinweise  
 Wird von der Anwendung kein expliziter Timeoutwert angegeben, werden von dieser Methode standardmäßig 15 Sekunden zurückgegeben.  
  
 Diese GetLoginTimeout-Methode wird von der GetLoginTimeout-Methode in der javax.sql.DataSource-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
