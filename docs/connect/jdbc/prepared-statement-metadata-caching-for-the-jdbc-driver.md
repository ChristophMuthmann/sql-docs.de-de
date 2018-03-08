---
title: "Vorbereitete Anweisungsmetadaten für den JDBC-Treiber Zwischenspeichern | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2018
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
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 13d4c0766552d9472038ffe7f2ff7fed6d73584d
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2018
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>Vorbereitete Anweisungsmetadaten Zwischenspeichern für den JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Dieser Artikel enthält Informationen für die zwei Änderungen, die implementiert werden, um die Leistung des Treibers zu optimieren.

## <a name="batching-of-unprepare-for-prepared-statements"></a>Batchverarbeitung von Unprepare für vorbereitete Anweisungen
Seit Version 6.1.6-preview, eine Verbesserung der Leistung durch Minimierung implementiertes Serverroundtrips mit SQL Server. Bisher wurde für jede Abfrage PrepareStatement ein Aufruf von unprepare auch gesendet. Nun wird der Treiber Batchverarbeitung unprepare Abfragen bis zu dem Schwellenwert "ServerPreparedStatementDiscardThreshold" besitzt einen Standardwert von 10.

> [!NOTE]  
>  Benutzer können den Standardwert ändern, mit der folgenden Methode: SetServerPreparedStatementDiscardThreshold (Int-Wert)

Eine weitere Änderung von 6.1.6-preview eingeführt ist, dass vor diesem Treiber immer Sp_prepexec aufrufen. Nun für die erste Ausführung einer vorbereiteten Anweisung Treiber ruft Sp_executesql und für die restlichen Sp_prepexec ausführt und ein Handle zugewiesen. Weitere Informationen finden Sie [hier](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching).

> [!NOTE]  
>  Benutzer können das Standardverhalten ändern, auf die früheren Versionen des Aufrufs immer Sp_prepexec von EnablePrepareOnFirstPreparedStatementCall festlegen, um **"true"** mithilfe des folgenden Verfahrens: SetEnablePrepareOnFirstPreparedStatementCall (boolescher Wert)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>Liste der neuen APIs eingeführt, die durch diese Änderung für die Batchverarbeitung von Unprepare für vorbereitete Anweisungen

 **SQLServerConnection**
 
|Methode „New“|Description|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|Gibt die Anzahl der derzeit ausstehenden vorbereitete Anweisung unprepare Aktionen.|
|void closeUnreferencedPreparedStatementHandles()|Erzwingt, dass die Unprepare-Anforderungen für alle ausstehenden verworfenen vorbereiteten Anweisungen ausgeführt werden.|
|Boolesche getEnablePrepareOnFirstPreparedStatementCall()|Gibt das Verhalten für eine bestimmte Verbindung-Instanz zurück. Wenn "false" Sp_executesql aufruft die erste Ausführung und eine Anweisung nicht vorbereitet werden, sobald die zweite Ausführung Problem tritt auf, ruft er Sp_prepexec und einem vorbereiteten Anweisungshandle tatsächlich einrichten. Folgenden Ausführungen Aufrufe Sp_execute. Dies entlastet die Notwendigkeit Sp_unprepare für vorbereitete Anweisung schließen, wenn die Anweisung nur einmal ausgeführt wird. Der Standardwert für diese Option kann durch Aufrufen von setDefaultEnablePrepareOnFirstPreparedStatementCall() geändert werden.|
|"void" setEnablePrepareOnFirstPreparedStatementCall(boolean value)|Gibt das Verhalten für eine bestimmte Verbindung-Instanz. Falls der Wert "false" Sp_executesql aufruft die erste Ausführung und eine Anweisung nicht vorbereitet werden, sobald die zweite Ausführung Problem tritt auf, ruft er Sp_prepexec und einem vorbereiteten Anweisungshandle tatsächlich einrichten. Folgenden Ausführungen Aufrufe Sp_execute. Dies entlastet die Notwendigkeit Sp_unprepare für vorbereitete Anweisung schließen, wenn die Anweisung nur einmal ausgeführt wird.|
|Int getServerPreparedStatementDiscardThreshold()|Gibt das Verhalten für eine bestimmte Verbindung-Instanz zurück. Diese Einstellung steuert, wie viele ausstehenden verwerfen Anweisung vorbereitet, die Aktionen (Sp_unprepare) Blockierungsvorgang pro Verbindung bleiben können, bevor ein Aufruf zum Bereinigen der ausstehende Handles auf dem Server ausgeführt wird. Wenn die Einstellung < = 1, unprepare Aktionen sofort auf Schließen die vorbereitete Anweisung ausgeführt werden. Wenn sie, um festgelegt ist {@literal >} 1, diese Aufrufe werden einem Batch zusammengefasst Aufwand für die aufrufende Sp_unprepare zu häufig zu vermeiden. Der Standardwert für diese Option kann durch Aufrufen von getDefaultServerPreparedStatementDiscardThreshold() geändert werden.|
|"void" setServerPreparedStatementDiscardThreshold(int value)|Gibt das Verhalten für eine bestimmte Verbindung-Instanz. Diese Einstellung steuert, wie viele ausstehenden verwerfen Anweisung vorbereitet, die Aktionen (Sp_unprepare) Blockierungsvorgang pro Verbindung bleiben können, bevor ein Aufruf zum Bereinigen der ausstehende Handles auf dem Server ausgeführt wird. Wenn die Einstellung < = 1 unprepare Aktionen sofort auf Schließen die vorbereitete Anweisung ausgeführt werden. Wenn sie auf > 1 festgelegt ist werden diese Aufrufe zusammen als Batch ausgeführt um Sp_unprepare zu häufig aufrufen verbundenen Aufwand zu vermeiden.|

 **SQLServerDataSource**
 
|Methode „New“|Description|  
|-----------|-----------------|  
|"void" setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|Wenn diese Konfiguration auf "false" festgelegt ist Sp_executesql aufruft die erste Ausführung einer vorbereiteten Anweisung und eine Anweisung nicht vorbereitet werden, sobald die zweite Ausführung Problem tritt auf, ruft er Sp_prepexec und einem vorbereiteten Anweisungshandle tatsächlich einrichten. Folgenden Ausführungen Aufrufe Sp_execute. Dies entlastet die Notwendigkeit Sp_unprepare für vorbereitete Anweisung schließen, wenn die Anweisung nur einmal ausgeführt wird.|
|Boolesche getEnablePrepareOnFirstPreparedStatementCall()|Wenn diese Konfiguration gibt "false", die erste Ausführung einer vorbereiteten Anweisung Sp_executesql aufruft und eine Anweisung nicht vorbereitet werden, sobald die zweite Ausführung erfolgt, Sp_prepexec aufruft und einem vorbereiteten Anweisungshandle tatsächlich einrichten. Folgenden Ausführungen Aufrufe Sp_execute. Dies entlastet die Notwendigkeit Sp_unprepare für vorbereitete Anweisung schließen, wenn die Anweisung nur einmal ausgeführt wird.|
|"void" setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|Diese Einstellung steuert, wie viele ausstehenden verwerfen Anweisung vorbereitet, die Aktionen (Sp_unprepare) Blockierungsvorgang pro Verbindung bleiben können, bevor ein Aufruf zum Bereinigen der ausstehende Handles auf dem Server ausgeführt wird. Wenn die Einstellung < = 1 unprepare Aktionen sofort auf Schließen die vorbereitete Anweisung ausgeführt werden. Wenn sie, um festgelegt ist {@literal >} 1 diese Aufrufe einem zusammengefasst Batch werden um Sp_unprepare zu häufig aufrufen verbundenen Aufwand zu vermeiden|
|Int getServerPreparedStatementDiscardThreshold()|Diese Einstellung steuert, wie viele ausstehenden verwerfen Anweisung vorbereitet, die Aktionen (Sp_unprepare) Blockierungsvorgang pro Verbindung bleiben können, bevor ein Aufruf zum Bereinigen der ausstehende Handles auf dem Server ausgeführt wird. Wenn die Einstellung < = 1 unprepare Aktionen sofort auf Schließen die vorbereitete Anweisung ausgeführt werden. Wenn sie, um festgelegt ist {@literal >} 1 diese Aufrufe einem zusammengefasst Batch werden um Sp_unprepare zu häufig aufrufen verbundenen Aufwand zu vermeiden.|

## <a name="prepared-statement-metatada-caching"></a>Vorbereitete Anweisung Metadaten Zwischenspeichern
Ab Version 6.3.0-preview Microsoft JDBC Driver für SQL Server das vorbereitete Anweisung Zwischenspeicherung unterstützt. Vor v6.3.0-Vorschau Wenn eine Ausführung einer Abfrage, die bereits vorbereitet und im Cache gespeichert wurden führen erneuten Aufrufen von derselben Abfrage nicht vorbereiten. Nun der Treiber die Abfrage im Cache sucht und suchen Sie das Handle, und führen Sie es mit Sp_execute.
Ist der vorbereiteten Anweisung metadatencaching **deaktiviert** standardmäßig. Um dieses Feature zu aktivieren, müssen Sie die folgende Methode für das Verbindungsobjekt aufrufen:

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

Zum Beispiel: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>Liste der neuen APIs eingeführt, die durch diese Änderung für vorbereitete Anweisung Zwischenspeichern von Metadaten

 **SQLServerConnection**
 
|Methode „New“|Description|  
|-----------|-----------------|  
|"void" setDisableStatementPooling(boolean value)|Legt fest, anweisungspools auf "true" oder "false".|
|boolean getDisableStatementPooling()|Gibt "true" zurück, wenn die Anweisung Verbindungspooling deaktiviert ist.|
|"void" setStatementPoolingCacheSize(int value)|Gibt die Größe des Caches für diese Verbindung vorbereiteten Anweisung. Ein Wert kleiner als 1 bedeutet, dass kein Cache.|
|int getStatementPoolingCacheSize()|Gibt die Größe des Caches vorbereitete Anweisung für diese Verbindung zurück. Ein Wert kleiner als 1 bedeutet, dass kein Cache.|
|int getStatementHandleCacheEntryCount()|Gibt die aktuelle Anzahl der in einem Pool zusammengefasste vorbereiteter Anweisungshandles.|
|boolean isPreparedStatementCachingEnabled()|Ob anweisungspools aktiviert ist oder nicht für diese Verbindung.|

 **SQLServerDataSource**
 
|Methode „New“|Description|  
|-----------|-----------------|  
|"void" setDisableStatementPooling(boolean disableStatementPooling)|Legt die Anweisung pooling auf "true" oder "false"|
|boolean getDisableStatementPooling()|Gibt "true" zurück, wenn die Anweisung Verbindungspooling deaktiviert ist.|
|"void" setStatementPoolingCacheSize(int statementPoolingCacheSize)|Gibt die Größe des Caches für diese Verbindung vorbereiteten Anweisung. Ein Wert kleiner als 1 bedeutet, dass kein Cache.|
|int getStatementPoolingCacheSize()|Gibt die Größe des Caches vorbereitete Anweisung für diese Verbindung zurück. Ein Wert kleiner als 1 bedeutet, dass kein Cache.|

## <a name="see-also"></a>Siehe auch  
 [Verbessern von Leistung und Zuverlässigkeit mit dem JDBC-Treiber](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
