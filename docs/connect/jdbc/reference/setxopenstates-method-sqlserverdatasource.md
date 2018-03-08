---
title: SetXopenStates-Methode (SQLServerDataSource) | Microsoft Docs
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
apiname: SQLServerDataSource.setXopenStates
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 9723591f-e987-426f-b70a-07f5c70dc094
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb9d14bebdbb8f6d7e2569cd5081541ca9080431
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="setxopenstates-method-sqlserverdatasource"></a>setXopenStates-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt eine **booleschen** -Wert, der angibt, ob das Konvertieren von SQL-Status zu XOPEN-kompatiblen Status aktiviert ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setXopenStates(boolean xopenStates)  
```  
  
#### <a name="parameters"></a>Parameter  
 *xopenstates-Eigenschaft*  
  
 **"true"** Wenn Konvertieren von SQL-Status zu XOPEN-kompatiblen Status aktiviert ist. Andernfalls lautet der Wert **false**.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die XopenStates-Eigenschaft, um festgelegt wird **"true"**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] SQL-Status in XOPEN-kompatiblen Status konvertiert. Die Standardeinstellung ist **"false"**, wodurch der JDBC-Treiber SQL 99-Statuscodes. Wenn die xopenstates-Eigenschaft nicht festgelegt ist, die [GetXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md) Methodenrückgabe den Standardwert von **"false"**.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
