---
title: DeleteRow-Methode (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.deleteRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aa04a644-c7c2-4738-8b6e-7fea566d2c16
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd06dec2dccd3e124d702131aa4520a394ecd9fa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="deleterow-method-sqlserverresultset"></a>DeleteRow-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Löscht die aktuelle Zeile aus dieser[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt und der zugrunde liegenden Datenbank.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void deleteRow()  
```  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese DeleteRow-Methode wird von der DeleteRow-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Diese Methode kann nicht aufgerufen werden, wenn sich der Cursor in der Einfügezeile befindet.  
  
 Bei der Verwendung von Keysetcursorn wird von dieser Methode eine Lücke im Resultset hinterlassen. Sie können diese Lücke testen, indem die [RowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) Methode. Die Zeilennummern der Zeilen im Resultset ändern sich nicht.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
