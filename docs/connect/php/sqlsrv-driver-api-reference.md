---
title: SQLSRV-Treiber-API-Referenz | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b55da26-ddeb-4e89-872a-91e0aba57103
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2bd1cf731f49119e54fb9e5a548a8988af1ef9fc
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrv-driver-api-reference"></a>API-Referenz für den SQLSRV-Treiber
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Der Name der API für den SQLSRV-Treiber in der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] ist **sqlsrv**. Alle **Sqlsrv** -Funktionen beginnen mit **Sqlsrv_** , gefolgt von einem Verb oder einem Substantiv. Die Funktionen, auf die ein Verb folgt, das eine Aktion ausführt und die Funktionen, auf die ein Substantiv folgt, geben Metadaten zurück.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
Der SQLSRV-Treiber enthält die folgenden Funktionen:  
  
|Funktion|Description|  
|------------|---------------|  
|[sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md)|beginnt eine Transaktion,|  
|[sqlsrv_cancel](../../connect/php/sqlsrv-cancel.md)|Verwirft eine Aussage; bricht ausstehende Ergebnisse der Aussage ab|  
|[sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)|Stellt Informationen über den Client bereit|  
|[sqlsrv_close](../../connect/php/sqlsrv-close.md)|Schließt eine Verbindung Gibt alle der Verbindung zugeordneten Ressourcen frei|  
|[sqlsrv_commit](../../connect/php/sqlsrv-commit.md)|Führt einen Commit für die Transaktion aus.|  
|[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)|Ändert Fehlerbehandlung und Protokollierungskonfigurationen|  
|[sqlsrv_connect](../../connect/php/sqlsrv-connect.md)|Erstellt und öffnet eine Verbindung|  
|[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)|Gibt Informationen über Fehler und/oder Warnungen für den letzten Vorgang zurück|  
|[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)|Führt eine vorbereitete Anweisung aus|  
|[sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)|Macht die nächste Datenzeile zum Lesen verfügbar.|  
|[sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)|Gibt die nächste Datenzeile als ein numerisch indiziertes Array, ein assoziatives Array oder beides zurück.|  
|[sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)|Ruft die nächste Datenzeile als Objekt ab.|  
|[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)|Gibt Metadaten eines Feldes zurück.|  
|[sqlsrv_free_stmt](../../connect/php/sqlsrv-free-stmt.md)|Schließt eine Anweisung. Gibt alle der Anweisung zugeordneten Ressourcen frei.|  
|[sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)|Gibt den Wert der angegebenen Konfigurationseinstellung zurück.|  
|[sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)|Ruft ein Feld in der aktuellen Zeile nach Index ab. Der PHP-Rückgabetyp kann angegeben werden.|  
|[sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md)|Erkennt, ob ein Resultset eine oder mehrere Zeilen hat.|  
|[sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md)|Stellt das nächste Ergebnis zur Verarbeitung zur Verfügung.|  
|[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)|Berichtet über die Anzahl der Zeilen in einem Resultset.|  
|[sqlsrv_num_fields](../../connect/php/sqlsrv-num-fields.md)|Ruft die Anzahl der Felder in einem aktiven Resultset ab.|  
|[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)|Bereitet eine Transact-SQL-Abfrage vor, ohne sie auszuführen Bindet implizit die Parameter.|  
|[sqlsrv_query](../../connect/php/sqlsrv-query.md)|Bereitet eine Transact-SQL-Abfrage vor und führt sie aus|  
|[sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md)|Führt ein Rollback für eine Transaktion aus|  
|[sqlsrv_rows_affected](../../connect/php/sqlsrv-rows-affected.md)|Gibt die Anzahl der veränderten Zeilen zurück|  
|[sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md)|Übermittelt bis zu acht Kilobyte (8 KB) Daten mit jedem Aufruf der Funktion an den Server|  
|[sqlsrv_server_info](../../connect/php/sqlsrv-server-info.md)|Stellt Informationen zum Server bereit|  
  
## <a name="reference"></a>Verweis  
[PHP-Handbuch](http://go.microsoft.com/fwlink/?LinkId=105500)  
  
## <a name="see-also"></a>Siehe auch  
[Übersicht zum PHP-SQL-Treiber](../../connect/php/overview-of-the-php-sql-driver.md)
[Konstanten &#40; Microsoft Drivers for PHP for SQLServer &#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[Programmierhandbuch für den PHP-SQL-Treiber](../../connect/php/programming-guide-for-php-sql-driver.md)
[Erste Schritte mit dem PHP-SQL-Treiber](../../connect/php/getting-started-with-the-php-sql-driver.md)
  

