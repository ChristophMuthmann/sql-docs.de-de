---
title: Abrufen von Daten als Stream mit dem SQLSRV-Treiber | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 17dc9129-04cd-430c-b5b3-82824116425d
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8fa189273eeb236d30f7f9ed9f01f00f14c6f70d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-data-as-a-stream-using-the-sqlsrv-driver"></a>Abrufen von Daten als Stream mit dem SQLSRV-Treiber
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Abrufen von Daten als Stream ist nur verfügbar im SQLSRV-Treiber von der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], und ist nicht im PDO_SQLSRV-Treiber verfügbar.  
  
Die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] nutzen Streams zum Abrufen großer Datenmengen. Die Themen in diesem Abschnitt enthalten ausführliche Informationen zum Abrufen von Daten als Stream.  
  
Die folgenden Schritte fassen zusammen, wie Daten als Stream abgerufen werden können:  
  
1.  Vorbereiten und Ausführen eine Transact-SQL-Abfrage mit [Sqlsrv_query](../../connect/php/sqlsrv-query.md) oder eine Kombination von [Sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[Sqlsrv_execute](../../connect/php/sqlsrv-execute.md).  
  
2.  Verwenden Sie [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) , um in die nächste Zeile im Resultset zu wechseln.  
  
3.  Verwenden Sie [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) , um ein Feld aus der Zeile abzurufen. Geben Sie, dass die Daten als Stream abgerufen werden, mithilfe von **SQLSRV_PHPTYPE_STREAM (<encoding>)** als dritten Parameter im Funktionsaufruf. Diese Tabelle enthält die Konstanten, mit denen die Codierungen und ihre Beschreibungen angegeben werden:  
  
    |SQLSRV-Konstante|Description|  
    |-------------------|---------------|  
    |SQLSRV_ENC_BINARY|Die Daten werden als uncodierter und nicht übersetzter Strom aus unbearbeiteten Bytes vom Server zurückgegeben.|  
    |SQLSRV_ENC_CHAR|Daten werden in 8-Bit-Zeichen gemäß der Codepage des im System eingestellten Windows-Gebietsschemas zurückgegeben. Alle Multi-Byte-Zeichen oder Zeichen, die nicht in dieser Codepage abgebildet sind, werden durch ein aus einem einzelnen Byte bestehendes Fragezeichen (?) ersetzt.|  
  
> [!NOTE]  
> Einige Datentypen werden standardmäßig als Stream zurückgegeben. Weitere Informationen finden Sie unter [Default PHP Data Types](../../connect/php/default-php-data-types.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Beschreibung|  
|---------|---------------|  
|[Datentypen mit Stream-Unterstützung, die den SQLSRV-Treiber nutzen](../../connect/php/data-types-with-stream-support-using-the-sqlsrv-driver.md)|Listet die SQL Server-Datentypen auf, die als Streams abgerufen werden können.|  
|[Vorgehensweise: Abrufen von Zeichendaten als Stream mit dem SQLSRV-Treiber](../../connect/php/how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver.md)|Veranschaulicht, wie Zeichendaten als Stream abgerufen werden können.|  
|[Vorgehensweise: Abrufen von Binärdaten als Stream mithilfe des SQLSRV-Treibers](../../connect/php/how-to-retrieve-binary-data-as-a-stream-using-the-sqlsrv-driver.md)|Veranschaulicht, wie Binärdaten als Stream abgerufen werden können.|  
  
## <a name="see-also"></a>Siehe auch  
[Abrufen von Daten](../../connect/php/retrieving-data.md)  
[Konstanten &#40;Microsoft-Treiber für PHP für SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
  

