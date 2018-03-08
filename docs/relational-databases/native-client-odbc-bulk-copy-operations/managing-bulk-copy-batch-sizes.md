---
title: "Verwalten von Batchgrößen für das Massenkopieren | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- ODBC, bulk copy operations
- batches [ODBC]
- bulk copy [ODBC], batch sizes
ms.assetid: 4b24139f-788b-45a6-86dc-ae835435d737
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff6ef76f4cd59d845f95f17e8b072dc1311052f4
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="managing-bulk-copy-batch-sizes"></a>Verwalten von Batchgrößen für das Massenkopieren
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Der Hauptzweck eines Batches in Massenkopiervorgängen besteht darin, den Umfang einer Transaktion zu definieren. Wenn keine Batchgröße festgelegt ist, wird der gesamte Massenkopiervorgang von den Massenkopierfunktionen als eine einzige Transaktion behandelt. Ist eine Batchgröße festgelegt, stellt jeder Batch eine Transaktion dar, für die nach Beendigung des Batches ein Commit ausgeführt wird.  
  
 Wenn ein Massenkopiervorgang ohne festgelegte Batchgröße ausgeführt wird und ein Fehler auftritt, wird für den gesamten Massenkopiervorgang ein Rollback durchgeführt. Das Wiederherstellen eines Massenkopiervorgangs mit langer Laufzeit kann einige Zeit in Anspruch nehmen. Wenn eine Batchgröße festgelegt wird, wird jeder Batch als Transaktion betrachtet und ein Commit für jeden Batch ausgeführt. Wenn ein Fehler auftritt, muss nur für den letzten ausstehenden Batch ein Rollback ausgeführt werden.  
  
 Die Batchgröße kann auch den Sperrenaufwand beeinflussen. Beim Durchführen eines Massenkopiervorgangs für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], der TABLOCK-Hinweis kann angegeben werden, mithilfe von [Bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) , eine Tabellensperre statt Zeilensperren abzurufen. Die einzelne Tabellensperre kann mit minimalem Aufwand für einen ganzen Massenkopiervorgang aufrechterhalten werden. Wird TABLOCK nicht festgelegt, werden Sperren für einzelne Zeilen errichtet und der Aufwand zur Aufrechterhaltung aller Sperren für die Dauer des Massenkopiervorgangs kann die Leistung beeinträchtigen. Da die Sperren nur für die Dauer der Transaktion aufrechterhalten werden, wird dieses Problem durch Angabe einer Batchgröße behoben, indem ein Commit ausgeführt wird, mit dem die aktuellen Sperren freigegeben werden.  
  
 Die Anzahl der Zeilen, die zu einem Batch gehören, kann sich erheblich auf die Leistung auswirken, wenn die Zeilenzahl für das Massenkopieren groß ist. Die Empfehlungen für die Batchgröße hängen vom Typ des auszuführenden Massenkopiervorgangs ab.  
  
-   Bei einem Massenkopiervorgang in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geben Sie den TABLOCK-Massenkopierhinweis an und legen eine große Batchgröße fest.  
  
-   Wenn TABLOCK nicht angegeben wird, beschränken Sie Batchgrößen auf unter 1.000 Zeilen.  
  
 Beim Massenkopieren aus einer Datendatei, die Batchgröße wird angegeben, indem **Bcp_control** mit der BCPBATCH-Option vor dem Aufruf [Bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md). Beim Massenkopieren aus Programmvariablen mit [Bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) und [Bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md), wird die Batchgröße durch Aufrufen von gesteuert [Bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) nach dem Aufruf [Bcp_ Sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) *x* Zeiten, Where *x* ist die Anzahl der Zeilen in einem Batch.  
  
 Batches sind nicht nur für das Festlegen der Größe einer Transaktion relevant, sondern wirken sich auch auf den Zeitpunkt aus, an dem Zeilen über das Netzwerk an den Server gesendet werden. Funktionen zum Massenkopieren normalerweise zwischengespeichert, die Zeilen aus **Bcp_sendrow** bis ein Netzwerkpaket gefüllt wird, und klicken Sie dann das volle Paket an den Server senden. Wenn eine Anwendung ruft **Bcp_batch**, allerdings wird das aktuelle Paket gesendet, mit dem Server unabhängig davon, ob es aufgefüllt wurde. Eine sehr niedrige Batchgröße kann die Leistung herabsetzen, wenn dadurch viele teilweise aufgefüllte Pakete an den Server gesendet werden. Beispielsweise Aufrufen **Bcp_batch** nach jedem **Bcp_sendrow** bewirkt, dass jede Zeile in einem einzelnen Paket gesendet werden und, es sei denn, der Zeilen sehr groß sind, verschwendet in jedem Paket Platz. Die Standardgröße von Netzwerkpaketen für SQL Server beträgt 4 KB, obwohl eine Anwendung durch Aufrufen der Größe geändert werden kann [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) angeben des SQL_ATTR_PACKET_SIZE-Attributs.  
  
 Ein anderer Nebeneffekt von Batches ist, dass jeder Batch als ausstehendes Resultset bis zu ihrem Abschluss mit berücksichtigt wird **Bcp_batch**. Wenn keine anderen Vorgänge für ein Verbindungshandle ausgeführt werden, während ein Batch aussteht, ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber gibt einen Fehler mit SQLState = "HY000" und eine Zeichenfolge der Fehlermeldung:  
  
```  
"[Microsoft][SQL Server Native Client] Connection is busy with  
results for another hstmt."  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Massenkopiervorgängen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [Massenimport und -export von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
