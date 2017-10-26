---
title: SQLServerResultSet-Klasse | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eaffcff1-286c-459f-83da-3150778480c9
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ac9db37012a51c8ba365b22dd7e56b30ae5b5b6d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverresultset-class"></a>SQLServerResultSet-Klasse
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Stellt ein JDBC-Resultset dar.  
  
 **Paket:** com.microsoft.sqlserver.jdbc  
  
 **Implementiert:** [ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final class SQLServerResultSet  
```  
  
## <a name="remarks"></a>Hinweise  
 Zwei Arten von Resultsets stehen zur Verfügung: clientseitige und serverseitige Resultsets.  
  
 Clientseitige Resultsets werden verwendet, wenn die Ergebnisse in den Clientprozessspeicher passen. Diese Ergebnisse bieten die höchste Geschwindigkeit und werden durch Lesen der [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] vollständig aus der Datenbank. Bei diesen Resultsets entstehen für die Datenbank keine zusätzlichen Lasten, da keine serverseitigen Cursor erstellt werden müssen. Allerdings können diese Resultsettypen nicht aktualisiert werden.  
  
 Serverseitige Resultsets können verwendet werden, wenn die Ergebnisse nicht in den Clientprozessspeicher passen oder wenn das Resultset aktualisierbar sein muss. Bei dieser Art von Resultset wird vom JDBC-Treiber ein serverseitiger Cursor erstellt, und die Zeilen des Resultsets werden transparent abgerufen, während der Benutzer einen Bildlauf ausführt.  
  
 SQLServerResultSet-Klasse bietet viele Methoden, um das Resultset mit beliebigen systemeigenen Java-Datentyps und viele Java-Objekttypen aktualisieren können.  
  
 Diese Klasse unterstützt das Entpacken in die SQLServerResultSet-Klasse, ISQLServerResultSet-Schnittstelle und java.sql.ResultSet-Schnittstelle. Weitere Informationen finden Sie unter [Wrapper und Schnittstellen](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [API-Referenz für JDBC-Treiber](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

