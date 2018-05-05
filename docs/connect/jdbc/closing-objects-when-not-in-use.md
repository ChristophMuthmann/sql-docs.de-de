---
title: Schließen von Objekten, die nicht In Gebrauch | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ce8f9b35-c761-4b0c-9a46-985eef2c2e0b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 644f3f22d544940e1f0f72cdfbfd5351fee6f519
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="closing-objects-when-not-in-use"></a>Schließen von nicht verwendeten Objekten
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Beim Arbeiten mit Objekten des [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], insbesondere [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) oder eine der Anweisung Objekte, z. B. [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [sqlserverpreparedstatement-Klasse ](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) oder [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), Sie sollten diese explizit schließen, indem Sie mit den entsprechenden-Methoden schließen, wenn sie nicht mehr benötigt werden. So wird die Leistung verbessert, da Treiber- und Serverressourcen so schnell wie möglich freigegeben werden und nicht erst darauf gewartet wird, dass dies durch den Garbage Collector der Java Virtual Machine erfolgt.  
  
 Das Schließen von Objekten ist besonders wichtig zum Erhalten der Parallelität auf dem Server, wenn Sie Rollen-Sperren verwenden. Rollen-Sperren im Fetchpuffer, auf den zuletzt zugegriffen wurde, werden beibehalten, bis das Resultset geschlossen wurde. Auf ähnliche Weise werden Handles für vorbereitete Anweisungen bis zum Schließen der Anweisung beibehalten. Wenn Sie eine Verbindung für mehrere Anweisungen wiederverwenden, führt das Schließen der Anweisungen, bevor sie den Bereich verlassen, dazu, dass der Server die vorbereiteten Handles früher bereinigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Verbessern von Leistung und Zuverlässigkeit mit dem JDBC-Treiber](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
