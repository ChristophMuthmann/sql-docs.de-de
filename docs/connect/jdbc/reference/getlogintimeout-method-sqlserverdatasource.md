---
title: GetLoginTimeout-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 316f067c-9e08-456a-af19-b80b0bbd4a5c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba6f8e0a85aba2afbc8cdae99b7cca76d749352b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
  
  

