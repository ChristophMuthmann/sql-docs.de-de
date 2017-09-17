---
title: SQLServerException-Klasse | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: af5ef257-7cf6-4db3-b1ee-07d22d82bef1
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd894bf23d8b1643722691451ccf3ae29ec6cd54
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverexception-class"></a>SQLServerException-Klasse
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Stell die fehlerhafte oder unvollständige Ausführung einer SQL-Anweisung dar.  
  
 **Paket:** com.microsoft.sqlserver.jdbc  
  
 **Erweitert:** "java.SQL.SqlException"  
  
 **Implementiert:** java.io.Serializable  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final class SQLServerException  
```  
  
## <a name="remarks"></a>Hinweise  
 Die SQLServerException-Klasse behandelt sowohl SQL 92-als auch XOPEN-Statuscodes. Diese verwenden eine vom Benutzer angegebene Verbindungseigenschaft und sind daher wechselbar. Ausnahmen werden in die angegebenen offenen Protokolldateien geschrieben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerException-Elemente](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [API-Referenz für JDBC-Treiber](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
