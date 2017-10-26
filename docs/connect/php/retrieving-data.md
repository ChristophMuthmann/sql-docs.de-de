---
title: Abrufen von Daten | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3414992c-61c0-4e7d-b509-72517e52c1bb
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce6cee44ce2e24055285b56b7889902166d460f1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-data"></a>Abrufen von Daten
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Dieses Thema und die anderen Themen in diesem Abschnitt erläutern, wie Sie Daten abrufen können.  
  
## <a name="sqlsrv-driver"></a>SQLSRV-Treiber  
Der SQLSRV-Treiber des [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] bietet die folgenden Optionen zum Abrufen von Daten aus einem Resultset:  
  
-   [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)  
  
-   [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)  
  
-   [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)/[sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)  
  
> [!NOTE]  
> Legen Sie bei Verwendung einer der oben genannten Funktionen keine Null-Vergleiche als Kriterium für das Beenden von Schleifen fest. Da **sqlsrv** -Funktionen „false“ zurückgeben, wenn ein Fehler auftritt, kann folgender Code nach einem Fehler in [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)zu einer Endlosschleife führen:  
>   
> `/*``This code could result in an infinite loop. It is recommended that`  
>   
> `you do NOT use null comparisons as the criterion for exiting loops,`  
>   
> `as is done here. */`  
>   
> `do{`  
>   
> `$result = sqlsrv_fetch_array($stmt);`  
>   
> `} while( !is_null($result));`  
  
Wenn Ihre Abfrage mehr als ein Resultset abruft, können Sie das nächste Resultset mit [sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md)anzeigen.  
  
Ab Version 1.1 von der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], können Sie [zu Sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md) um festzustellen, ob ein Resultset Zeilen enthält.  
  
## <a name="pdosqlsrv-driver"></a>PDO_SQLSRV-Treiber  
Der PDO_SQLSRV-Treiber von der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] bietet die folgenden Optionen zum Abrufen von Daten aus einem Resultset:  
  
-   [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md)  
  
-   [PDOStatement::fetchAll](../../connect/php/pdostatement-fetchall.md)  
  
-   [PDOStatement::fetchColumn](../../connect/php/pdostatement-fetchcolumn.md)  
  
-   [PDOStatement::fetchObject](../../connect/php/pdostatement-fetchobject.md)  
  
Wenn Ihre Abfrage mehr als ein Resultset abruft, können Sie das nächste Resultset mit [PDOStatement::nextRowset](../../connect/php/pdostatement-nextrowset.md)anzeigen.  
  
Sie können sehen, wie viele Zeilen ein Resultset aufweist, indem Sie einen bildlauffähigen Cursor verwenden und anschließend [PDOStatement::rowCount](../../connect/php/pdostatement-rowcount.md)aufrufen.  
  
[PDO::prepare](../../connect/php/pdo-prepare.md) ermöglicht die Angabe ein Cursortyps. Anschließend können Sie mit [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md) eine Zeile auswählen. Unter [PDO::prepare](../../connect/php/pdo-prepare.md) finden Sie ein Beispiel und weitere Informationen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Beschreibung|  
|---------|---------------|  
|[Abrufen von Daten als Stream](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)|Bietet einen Überblick über das Streamen von Daten vom Server und stellt Links für spezifische Anwendungsszenarien bereit.|  
|[Verwenden direktionaler Parameter](../../connect/php/using-directional-parameters.md)|Beschreibt die Verwendung direktionaler Parameter beim Aufrufen einer gespeicherten Prozedur.|  
|[Festlegen eines Cursortyps und Zeilenauswahl](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)|Veranschaulicht, wie bei Verwendung des SSQLSRV-Treibers ein Resultset mit Zeilen erstellen, auf die Sie in beliebiger Reihenfolge zugreifen können.|  
|[Vorgehensweise: Datums- und Uhrzeittypen mittels des SQLSRV-Treibers als Zeichenfolgen abrufen](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)|Beschreibt, wie Sie Datums- und Uhrzeittypen als Zeichenfolgen abrufen|  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
[Vorgehensweise: PHP-Datentypen festlegen](../../connect/php/how-to-specify-php-data-types.md)  
  
## <a name="see-also"></a>Siehe auch  
[Programmierhandbuch für den PHP-SQL-Treiber](../../connect/php/programming-guide-for-php-sql-driver.md)
[Abrufen von Daten](../../connect/php/retrieving-data.md)  
  

