---
title: SQLServerException-Klasse | Microsoft Docs
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
ms.assetid: af5ef257-7cf6-4db3-b1ee-07d22d82bef1
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 250d20c0277287c490b925e18ea49fb4f87288f8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
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
  
  
