---
title: GetUser-Methode (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.getUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3513dd7f-6ae5-4010-bde0-454ac4365bce
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7cd095dc3968ae89dfedb110cc5a75eb1b19844a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getuser-method-sqlserverdatasource"></a>getUser-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt den Benutzernamen zurück, der zum Herstellen einer Verbindung mit der Datenquelle verwendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getUser()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** , die den Benutzernamen enthält.  
  
## <a name="remarks"></a>Hinweise  
 Die [SetUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) Methode legt fest, der Benutzername, der verwendet wird, wenn die Verbindung mit der Instanzstatus von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Ist der Wert für den Benutzernamen nicht festgelegt, wird von der getUser-Methode der Standardwert (NULL) zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
