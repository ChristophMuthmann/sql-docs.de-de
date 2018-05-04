---
title: SQLServerResultSet-Klasse | Microsoft Docs
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
ms.assetid: eaffcff1-286c-459f-83da-3150778480c9
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 305e314c58b5860b8c171d2854abf71adda265d6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
  
  
