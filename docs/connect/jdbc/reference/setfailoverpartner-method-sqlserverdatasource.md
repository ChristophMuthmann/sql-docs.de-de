---
title: SetFailoverPartner-Methode (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.setFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5310b7c2-9d10-474f-ad3a-218fe5da694b
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 256c8da2fa3fd814057f7d81c4d1b0840c8b6919
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setfailoverpartner-method-sqlserverdatasource"></a>setFailoverPartner-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den Namen des Failoverservers, der verwendet wird, in einer Datenbank-Spiegelungskonfiguration fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setFailoverPartner(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *serverName*  
  
 Ein **Zeichenfolge** , die dem Namen des Failoverservers enthält.  
  
## <a name="remarks"></a>Hinweise  
 Der von dieser Methode festgelegte Wert wird im Falle eines Fehlers beim erstmaligen Herstellen einer Verbindung mit dem Prinzipalserver verwendet. Sobald die Verbindung hergestellt wurde, wird dieser Wert ignoriert. Die [SetDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md) Methode sollte auch in Verbindung mit dieser Methode verwendet werden, oder es wird eine Ausnahme ausgelöst.  
  
 Bei festgelegtem Failoverservernamen wird das Angeben der Portnummer des Failoverservers vom Treiber nicht unterstützt. Bei Aufruf der [SetServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md) Methode und die [SetInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md) Methode mit dem [SetFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) Methode wird unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

