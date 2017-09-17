---
title: SupportsGroupByBeyondSelect-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.supportsGroupByBeyondSelect
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: eadd2c37-d9ec-4b47-a91e-ed90b1eaf4b4
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d1d6c10301b9beeac028489c733c2bc17a55c1a8
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="supportsgroupbybeyondselect-method-sqlserverdatabasemetadata"></a>supportsGroupByBeyondSelect-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft ab, ob von dieser Datenbank die Verwendung von Spalten, die sich nicht in einer SELECT-Anweisung befinden, in einer GROUP BY-Klausel unterstützt wird, wenn gewährleistet ist, dass alle Spalten aus der SELECT-Anweisung in der GROUP BY-Klausel enthalten sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean supportsGroupByBeyondSelect()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** unterstützt. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SupportsGroupByBeyondSelect-Methode wird von der SupportsGroupByBeyondSelect-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
