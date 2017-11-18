---
title: SetLastUpdateCount-Methode (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.setLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5487631a-1107-4169-84ca-b77fd09bea66
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: caa3caa684088a38b732dddae8b17b7c88cf76bb
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setlastupdatecount-method-sqlserverdatasource"></a>setLastUpdateCount-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt eine **booleschen** -Wert, der angibt, ob die LastUpdateCount-Eigenschaft aktiviert ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setLastUpdateCount(boolean lastUpdateCount)  
```  
  
#### <a name="parameters"></a>Parameter  
 *"lastupdatecount"*  
  
 **"true"** Wenn "lastupdatecount" aktiviert ist. Andernfalls lautet der Wert **false**.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die LastUpdateCount-Eigenschaft, um festgelegt wird **"true"**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] zurück nur die letzte updatezählung aus einer SQL-Anweisung an den Server übergeben. Wenn die LastUpdateCount-Eigenschaft, um festgelegt wird **"false"**, der Treiber alle updatezählungen zurückgegeben, durch Trigger, die möglicherweise ausgelöst haben – einschließlich jener zurück. Wenn die LastUpdateCount-Eigenschaft nicht festgelegt ist, die [GetLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md) Methodenrückgabe den Standardwert von **"true"**.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

