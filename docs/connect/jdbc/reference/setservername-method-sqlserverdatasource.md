---
title: SetServerName-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
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
- SQLServerDataSource.setServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 70920828-eda0-4064-be9f-c1e460db8f00
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2efdbb68c0d546776b7027c9130e7589c92322ea
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setservername-method-sqlserverdatasource"></a>setServerName-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den Namen des Computers, der ausgeführt wird [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setServerName(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *serverName*  
  
 Ein **Zeichenfolge** , die den Namen des Servers enthält.  
  
## <a name="remarks"></a>Hinweise  
 Der Servername ist der Hostname des Zielcomputers, auf denen ausgeführt wird, ist [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Wenn die ServerName-Eigenschaft nicht festgelegt ist, [GetServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md) gibt den Standardwert NULL zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

