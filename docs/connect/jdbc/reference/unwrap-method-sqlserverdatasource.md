---
title: Unwrap-Methode (SQLServerDataSource) | Microsoft Docs
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
ms.assetid: eb8abe29-f3ec-4752-a590-1d5dc3e48f08
caps.latest.revision: "19"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d3519e11a7fb461e444525ea827908e0929dab1
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="unwrap-method-sqlserverdatasource"></a>unwrap-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt ein Objekt, das für den Zugriff auf die angegebene Schnittstelle implementiert die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-spezifischen Methoden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>Parameter  
 *iface*  
  
 Eine Klasse vom Typ T zum Definieren einer Schnittstelle.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Objekt, von dem die angegebene Schnittstelle implementiert wird.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Die [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) Methode definiert ist, von der java.sql.Wrapper-Schnittstelle, die in der JDBC 4.0-Spezifikationen eingeführt wird.  
  
 Der JDBC-API-Erweiterungen, die für spezifisch sind, den Zugriff auf Anwendungen müssen möglicherweise die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Die Unwrap-Methode unterstützt das Entpacken in öffentliche Klassen, die dieses Objekt erstreckt, sofern es sich bei den Klassen herstellererweiterungen verfügbar gemacht.  
  
 Wenn diese Methode aufgerufen wird, wird das Objekt in entpackt die [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Klasse.  
  
 Weitere Informationen finden Sie unter [Wrapper und Schnittstellen](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Siehe auch  
 [IsWrapperFor-Methode &#40; SQLServerDataSource &#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)   
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
