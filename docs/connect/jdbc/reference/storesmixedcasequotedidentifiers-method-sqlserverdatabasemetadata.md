---
title: StoresMixedCaseQuotedIdentifiers-Methode | Microsoft Docs
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
apiname: SQLServerDatabaseMetaData.storesMixedCaseQuotedIdentifiers
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 1ffa599c-d0c8-43b6-8e9b-7c856a846630
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: afc4461b677bc2e993f743cd53a235f08828a8bc
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="storesmixedcasequotedidentifiers-method-sqlserverdatabasemetadata"></a>storesMixedCaseQuotedIdentifiers-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft ab, ob bei SQL-Bezeichnern mit gemischter Groß-/Kleinschreibung, die in Anführungszeichen gesetzt sind, die Groß-/Kleinschreibung nicht berücksichtigt wird und die Bezeichner mit gemischter Groß-/Kleinschreibung gespeichert werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean storesMixedCaseQuotedIdentifiers()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn die Bezeichner in gemischter Schreibung gespeichert werden. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese StoresMixedCaseQuotedIdentifiers-Methode wird von der StoresMixedCaseQuotedIdentifiers-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
