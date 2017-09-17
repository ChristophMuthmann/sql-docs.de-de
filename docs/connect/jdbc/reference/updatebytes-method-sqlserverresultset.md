---
title: UpdateBytes-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.updateBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3050c836-fbb3-4475-99e5-05637a48a932
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e20e126945f11a2cba5d4b1171dc762f2a2efbac
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="updatebytes-method-sqlserverresultset"></a>updateBytes-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte mit einem Array von **Byte** Werte.  
  
## <a name="overload-list"></a>Überladungsliste  
  
|Name|Description|  
|----------|-----------------|  
|[UpdateBytes (Int, Byte &#91; &#93;)](../../../connect/jdbc/reference/updatebytes-method-int-byte.md)|Aktualisiert die angegebene Spalte mit einem Array von **Byte** Werte Berücksichtigung des Spaltenindexes.|  
|[UpdateBytes (java.lang.String, Byte &#91; &#93;)](../../../connect/jdbc/reference/updatebytes-method-java-lang-string-byte.md)|Aktualisiert die angegebene Spalte mit einem Array von **Byte** Werte Berücksichtigung des Spaltennamens.|  
  
## <a name="remarks"></a>Hinweise  
 In einer früheren Version von [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], Sie mithilfe von "sqlserverresultset.updateBytes" Werte zwischen Bytearrays konvertieren und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentyp **Datum**, **Zeit**, ** datetime2**, oder **"DateTimeOffset"**. Nun wird durch Verwendung der Methode mit diesen Datentypen eine Ausnahme ausgelöst, die angibt, dass die Konvertierung nicht unterstützt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
