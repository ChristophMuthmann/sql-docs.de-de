---
title: Unwrap-Methode (SQLServerXADataSource) | Microsoft Docs
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
ms.assetid: d97c99b3-2224-4abb-8b32-40aff49fe759
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 38c0d70d3818acea0b786f8646555650d2318c8e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="unwrap-method-sqlserverxadatasource"></a>unwrap-Methode (SQLServerXADataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt ein Objekt, das für den Zugriff auf die angegebene Schnittstelle implementiert die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-spezifischen Methoden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>Parameter  
 *iface*  
  
 Eine Klasse des Typs **T** zum Definieren einer Schnittstelle.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Objekt, von dem die angegebene Schnittstelle implementiert wird.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Die [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) Methode definiert ist, von der java.sql.Wrapper-Schnittstelle, die in der JDBC 4.0-Spezifikationen eingeführt wird.  
  
 Der JDBC-API-Erweiterungen, die für spezifisch sind, den Zugriff auf Anwendungen müssen möglicherweise die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Die Unwrap-Methode unterstützt das Entpacken öffentlichen Klassen, die dieses Objekt erweitert, wenn es sich bei den Klassen herstellererweiterungen verfügbar gemacht.  
  
 Die [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md) -Klasse erweitert die [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) -Klasse, die von erweitert wird die [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Klasse. Wenn diese Methode aufgerufen wird, wird das Objekt in der folgenden Klassen entpackt: [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md), [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md), und [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md).  
  
 Weitere Informationen finden Sie unter [Wrapper und Schnittstellen](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerXADataSource-Methoden](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [SQLServerXADataSource-Elemente](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [SQLServerXADataSource-Klasse](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  

