---
title: Arbeiten mit Anweisungen und Resultsets | Microsoft Docs
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
ms.assetid: cc917534-f5f8-4844-87c8-597c48b4e06d
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ce65afcf2086b4b3383f45fd6f0174668eeb1e1a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="working-with-statements-and-result-sets"></a>Arbeiten mit Anweisungen und Resultsets
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Beim Arbeiten mit der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] und die Anweisung und der ResultSet-Objekte, gibt es gibt mehrere Verfahren, die Sie verwenden können, um die Leistung und Zuverlässigkeit der Anwendungen zu verbessern.  
  
## <a name="use-the-appropriate-statement-object"></a>Verwenden des geeigneten Statement-Objekts  
 Bei Verwendung einer der JDBC-Treiber Statement-Objekte, z. B. die [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), oder die [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Objekt Stellen Sie sicher, dass Sie das entsprechende Objekt für den Auftrag verwenden.  
  
-   Wenn Sie keine OUT-Parameter verfügen, müssen Sie nicht die SQLServerCallableStatement-Objekt verwendet wird. Verwenden Sie stattdessen die SQLServerStatement oder die SQLServerPreparedStatement-Objekt.  
  
-   Wenn Sie nicht die Anweisung mehrmals ausführen möchten oder keine in- oder OUT-Parameter ist, müssen Sie nicht SQLServerCallableStatement oder SQLServerPreparedStatement-Objekt verwenden. Verwenden Sie stattdessen die SQLServerStatement-Objekt.  
  
## <a name="use-the-appropriate-concurrency-for-resultset-objects"></a>Verwenden der geeigneten Parallelität für ResultSet-Objekte  
 Verwenden Sie beim Erstellen von Anweisungen, die Resultsets erzeugen, keine aktualisierbare Parallelität, wenn die Ergebnisse nicht aktualisiert werden sollen. Das Standardmodell mit schreibgeschütztem Vorwärtscursor weist beim Lesen von kleinen Resultsets die höchste Leistung auf.  
  
## <a name="limit-the-size-of-your-result-sets"></a>Einschränken der Größe von Resultsets  
 Erwägen Sie die [SetMaxRows](../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) -Methode (oder SET ROWCOUNT oder SELECT TOP N SQL-Syntax), um die Anzahl der Zeilen zu beschränken, die von möglicherweise umfangreichen Resultsets zurückgegeben. Bei der Verarbeitung von umfangreichen Resultsets sollten Sie eine adaptive Antwortpufferung verwenden, indem Sie die Verbindungszeichenfolgeneigenschaft "responseBuffering" auf "adaptive" (den Standardmodus) festlegen. So kann die Anwendung große Resultsets verarbeiten, ohne serverseitige Cursor verwenden zu müssen, und die Anwendungsspeicherauslastung minimieren. Weitere Informationen finden Sie unter [mithilfe der adaptiven Pufferung](../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="use-the-appropriate-fetch-size"></a>Verwenden der geeigneten Fetchgröße  
 Bei schreibgeschützten Servercursorn muss ein Kompromiss zwischen den Roundtrips zum Server und dem im Treiber verwendeten Speicher gefunden werden. Bei aktualisierbaren Servercursorn beeinflusst außerdem die Abrufgröße die Sensitivität des Resultsets gegenüber Änderungen und die Parallelität des Servers. Updates von Zeilen im aktuellen Fetchpuffer sind nicht sichtbar, bis eine explizite [RefreshRow](../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md) -Methode ausgegeben wird oder bis der Cursor den Fetchpuffer verlässt. Große Fetchpuffer weisen eine höhere Leistung (weniger Serverroundtrips) aber eine geringere Sensitivität gegenüber Änderungen auf und verringern die Parallelität des Servers, wenn CONCUR_SS_SCROLL_LOCKS (1009) verwendet wird. Verwenden Sie die Abrufgröße "1", um die Sensitivität gegenüber Änderungen zu maximieren. Beachten Sie jedoch, dass dabei für jede abgerufene Zeile ein Roundtrip zum Server erforderlich ist.  
  
## <a name="use-streams-for-large-in-parameters"></a>Verwenden von Datenströmen für umfangreiche IN-Parameter  
 Verwenden Sie Datenströme oder BLOBs und CLOBs, die inkrementell gefüllt werden, um umfangreiche Spaltenwerte zu aktualisieren oder umfangreiche IN-Parameter zu senden. Der JDBC-Treiber sendet diese blockweise in mehreren Roundtrips an den Server, sodass Werte festgelegt und aktualisiert werden können, die größer sind als der verfügbare Speicher.  
  
## <a name="see-also"></a>Siehe auch  
 [Verbessern von Leistung und Zuverlässigkeit mit dem JDBC-Treiber](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
