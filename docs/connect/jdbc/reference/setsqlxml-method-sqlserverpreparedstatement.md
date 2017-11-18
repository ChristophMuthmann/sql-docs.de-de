---
title: SetSQLXML-Methode (SQLServerPreparedStatement) | Microsoft Docs
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
ms.assetid: 70bbdde0-75f7-4169-88c5-dbbe2c4bcd03
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 68b390784de414df69b9dfb3a6bf1979a89aac97
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setsqlxml-method-sqlserverpreparedstatement"></a>setSQLXML-Methode (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den angegebenen Parameter mit dem angegebenen SQLXML-Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final void setSQLXML(int parameterIndex,  
                            java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>Parameter  
 *parameterIndex*  
  
 Ein **Int** , der die Indexnummer des Parameters angibt.  
  
 *xmlObject*  
  
 Ein SQLXML-Objekt, das den Parameterwert enthält.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetSQLXML-Methode wird von der SetSQLXML-Methode in der java.sql.PreparedStatement-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerPreparedStatement-Elemente](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  

