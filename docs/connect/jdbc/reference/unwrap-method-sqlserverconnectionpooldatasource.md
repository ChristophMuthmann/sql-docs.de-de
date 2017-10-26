---
title: Unwrap-Methode (SQLServerConnectionPoolDataSource) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f5c9b734-2096-4ae4-a284-6b4d1b4a00d4
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8e19a9c15e6bced2f9b0df99e491cdbb0ac8240a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="unwrap-method-sqlserverconnectionpooldatasource"></a>unwrap-Methode (SQLServerConnectionPoolDataSource)
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
 Die [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md) Methode definiert ist, von der java.sql.Wrapper-Schnittstelle, die in der JDBC 4.0-Spezifikationen eingeführt wird.  
  
 Der JDBC-API-Erweiterungen, die für spezifisch sind, den Zugriff auf Anwendungen müssen möglicherweise die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Die Unwrap-Methode unterstützt das Entpacken öffentlichen Klassen, die dieses Objekt erweitert, wenn es sich bei den Klassen herstellererweiterungen verfügbar gemacht.  
  
 Die [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) -Klasse erweitert die [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Klasse. Wenn diese Methode aufgerufen wird, wird das Objekt in entpackt die [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Klasse und die [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) Klasse.  
  
 Weitere Informationen finden Sie unter [Wrapper und Schnittstellen](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnectionPoolDataSource-Methoden](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [SQLServerConnectionPoolDataSource-Elemente](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [SQLServerConnectionPoolDataSource-Klasse](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  

