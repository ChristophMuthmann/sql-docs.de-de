---
title: GetFetchSize-Methode (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.getFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8115ca58-8ae9-46ce-8515-7905d7bb25fe
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37cc952b4386130902eb126f2eb688a7c851a870
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getfetchsize-method-sqlserverstatement"></a>GetFetchSize-Methode (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft die Anzahl der Resultsets festgelegt, der die standardmäßige Abrufgröße für Objekte, die von diesem generierten Resultset Zeilen [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final int getFetchSize()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** , die angibt, dass der Abrufgröße, der durch angegeben ist die [SetFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md) Methode.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetFetchSize-Methode wird von der GetFetchSize-Methode in der java.sql.Statement-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerStatement-Elemente](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
