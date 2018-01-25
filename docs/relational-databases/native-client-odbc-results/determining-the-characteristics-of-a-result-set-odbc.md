---
title: Bestimmen der Eigenschaften eines Resultsets (ODBC) legen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-results
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], characteristics
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- SQLDescribeCol function
- metadata [ODBC]
- SQLColAttribute function
- SQLNumResultCols function
ms.assetid: 90be414c-04b3-46c0-906b-ae7537989b7d
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 43b848d7a0987ac6573478159f14f2365d9ee97c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="determining-the-characteristics-of-a-result-set-odbc"></a>Bestimmen der Eigenschaften eines Resultsets (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Metadaten sind Daten, die andere Daten beschreiben. Resultsetmetadaten beschreiben beispielsweise die Merkmale eines Resultsets, wie die Spaltenanzahl im Resultset, die Datentypen in diesen Spalten, ihre Namen, Genauigkeit und NULL-Zulässigkeit.  
  
 ODBC liefert Metadaten an Anwendungen durch seine API-Katalogfunktionen. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber implementiert zahlreiche der ODBC-API-Katalogfunktionen als Aufrufe an eine entsprechende [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Katalogprozedur.  
  
 Anwendungen erfordern Metadaten für die meisten Resultsetvorgänge. Die Anwendung verwendet z. B. den Datentyp einer Spalte, um zu bestimmen, welche Art von Variable an diese Spalte gebunden werden soll. Sie verwendet die Bytelänge einer Zeichenspalte, um zu bestimmen, wie viel Platz zur Anzeige von Daten aus dieser Spalte erforderlich ist. Wie eine Anwendung die Metadaten für eine Spalte bestimmt, hängt vom Typ der Anwendung ab.  
  
 Vertikale Anwendungen funktionieren i. d. R. mit vordefinierten Tabellen und führen vordefinierte Vorgänge auf diese Tabellen aus. Da die Resultsetmetadaten für solche Anwendungen definiert werden, bevor die Anwendung überhaupt geschrieben wird, und vom Entwickler gesteuert werden, können sie in die Anwendung hartcodiert werden. Wenn beispielsweise eine OrderID-Spalte in der Datenquelle als 4-Byte-Ganzzahl definiert ist, kann die Anwendung stets eine 4-Byte-Ganzzahl an diese Spalte binden. Wenn Metadaten in der Anwendung hartcodiert sind, bedeutet eine Änderung an den von der Anwendung verwendeten Tabelle im Allgemeinen eine Änderung am Anwendungscode.  
  
 In generischen Anwendungen, vor allem Anwendungen, die Ad-Hoc-Abfragen unterstützen, sind die Metadaten des von ihnen erstellten Resultsets typischerweise bis zur Laufzeit unbekannt.  
  
 Ein Anwendung kann folgende Aufrufe durchführen, um die Eigenschaften eines Resultsets zu bestimmen:  
  
-   [SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) um zu bestimmen, wie viele Spalten von einer Anforderung zurückgegeben.  
  
-   [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) oder [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) um eine Spalte im Resultset zu beschreiben.  
  
 Eine wohlgeformte Anwendung wird ausgehend von der Annahme geschrieben, dass das Resultset unbekannt ist, und verwendet die von diesen Funktionen zurückgegebenen Informationen dazu, die Spalten im Resultset zu binden. Eine Anwendung kann diese Funktionen jederzeit aufrufen, nachdem eine Anweisung vorbereitet oder ausgeführt wurde. Für eine optimale Leistung eine Anwendung sollten jedoch aufrufen **SQLColAttribute**, **SQLDescribeCol**, und **SQLNumResultCols** nachdem eine Anweisung ausgeführt wird.  
  
 Sie können mehrere gleichzeitige Abrufe auf Metadaten durchführen. Die den ODBC-API-Implementierungen zugrunde liegenden Systemkatalogprozeduren können mit dem ODBC-Treiber aufgerufen werden, während dieser statische Servercursor verwendet. So können Anwendungen mehrere Aufrufe an ODBC-Katalogfunktionen gleichzeitig verarbeiten.  
  
 Wenn die Anwendung einen bestimmten Metadatensatz mehr als ein Mal verwendet, ist es möglicherweise von Vorteil, wenn die Informationen beim ersten Abrufen in privaten Variablen zwischengespeichert werden. Dadurch werden spätere Aufrufe an die ODBC-Katalogfunktionen für die gleichen Informationen vermieden, durch die der Treiber zu Roundtrips zum Server gezwungen wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Verarbeitens von Ergebnissen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
