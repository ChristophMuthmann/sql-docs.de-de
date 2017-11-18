---
title: SupportsStoredFunctionsUsingCallSyntax-Methode | Microsoft Docs
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
ms.assetid: 0e5c0579-84b5-4717-b128-0bcd512f6022
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: de585c13ec1d8234cdf9087525b2eb1c8c2e99ed
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="supportsstoredfunctionsusingcallsyntax-method-sqlserverdatabasemetadata"></a>supportsStoredFunctionsUsingCallSyntax-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt an, ob von der aktuellen Datenbank das Aufrufen benutzer- oder herstellerdefinierter Funktionen mithilfe der Escapesyntax für gespeicherte Prozeduren unterstützt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean supportsStoredFunctionsUsingCallSyntax()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** unterstützt. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SupportsStoredFunctionsUsingCallSyntax-Methode wird von der SupportsStoredFunctionsUsingCallSyntax-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

