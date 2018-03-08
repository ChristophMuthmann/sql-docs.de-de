---
title: GetBytes-Methode (SQLServerCallableStatement) | Microsoft Docs
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
apiname: SQLServerCallableStatement.getBytes
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: b6e88cea-54b3-4d18-a9af-db54abf19f45
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d1006144e75fd3e7e4366a29b1235dcca893c895
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="getbytes-method-sqlservercallablestatement"></a>getBytes-Methode (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Parameters als Bytearray ab.  
  
## <a name="overload-list"></a>Überladungsliste  
  
|Name|Description|  
|----------|-----------------|  
|[GetBytes (Int)](../../../connect/jdbc/reference/getbytes-method-int.md)|Ruft den Wert des angegebenen Parameters unter Berücksichtigung des Parameterindexes als ein Array von Bytewerten ab.|  
|[GetBytes (java.lang.String)](../../../connect/jdbc/reference/getbytes-method-java-lang-string.md)|Ruft den Wert des angegebenen Parameters unter Berücksichtigung des Parameternamens als ein Array von Bytewerten ab.|  
  
## <a name="remarks"></a>Hinweise  
 In einer früheren Version von den [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], Sie mithilfe von "sqlservercallablestatement.GetBytes" Werte zwischen Bytearrays konvertieren und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentyp **Datum**, **Zeit**, **datetime2**, oder **"DateTimeOffset"**. Nun wird durch Verwendung der Methode mit diesen Datentypen eine Ausnahme ausgelöst, die angibt, dass die Konvertierung nicht unterstützt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement-Klasse](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
