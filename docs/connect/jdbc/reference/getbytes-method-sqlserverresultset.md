---
title: GetBytes-Methode (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d16a0aea-6144-4fcb-bcbc-5d7daa36d327
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a853def1f840a6dec5b17b56771e6b253678cd74
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getbytes-method-sqlserverresultset"></a>getBytes-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **Byte** Array in der Programmiersprache Java ab.  
  
## <a name="overload-list"></a>Überladungsliste  
  
|Name|Description|  
|----------|-----------------|  
|[GetBytes (Int)](../../../connect/jdbc/reference/getbytes-method-int-sqlserverresultset.md)|Ruft den Wert des angegebenen Spaltenindexes in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **Byte** Array in der Programmiersprache Java ab.|  
|[GetBytes (java.lang.String)](../../../connect/jdbc/reference/getbytes-method-java-lang-string-sqlserverresultset.md)|Ruft den Wert des angegebenen Spaltennamens in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **Byte** Array in der Programmiersprache Java ab.|  
  
## <a name="remarks"></a>Hinweise  
 In einer früheren Version von den [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], Sie mithilfe von "sqlserverresultset.GetBytes" Werte zwischen Bytearrays konvertieren und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentyp **Datum**, **Zeit**,  **datetime2**, oder **"DateTimeOffset"**. Nun wird durch Verwendung der Methode mit diesen Datentypen eine Ausnahme ausgelöst, die angibt, dass die Konvertierung nicht unterstützt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

