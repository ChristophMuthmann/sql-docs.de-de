---
title: SetDateTimeOffset-Methode (SQLServerPreparedStatement) | Microsoft Docs
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
ms.assetid: 5014dba9-1755-4769-b070-6cbeecee864e
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e043ac3d0d38bc985fa05909f07ff32a7d63810a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setdatetimeoffset-method-sqlserverpreparedstatement"></a>setDateTimeOffset-Methode (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Diese Methode wurde hinzugefügt, [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0.  
  
 Legt den Wert der angegebenen Spalte auf die ["DateTimeOffset"-Klasse](../../../connect/jdbc/reference/datetimeoffset-class.md) Wert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final void setDateTimeOffset(int n, microsoft.sql.DateTimeOffset x)  
```  
  
#### <a name="parameters"></a>Parameter  
 *n*  
  
 Die nullbasierte Ordinalzahl einer Spalte.  
  
 *x*  
  
 Die ["DateTimeOffset"-Klasse](../../../connect/jdbc/reference/datetimeoffset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerPreparedStatement-Elemente](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement-Klasse](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

