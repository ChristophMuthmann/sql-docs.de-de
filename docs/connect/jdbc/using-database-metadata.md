---
title: Verwenden von Datenbankmetadaten | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 421da278e1a4503a73fb4f4f8a8aba0b3cff672f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-database-metadata"></a>Verwenden von Datenbankmetadaten
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Zum Abfragen einer Datenbank nach Informationen zu den unterstützten Funktionen der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementiert die [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) Klasse. Diese Klasse enthält eine Vielzahl von Methoden, die Informationen in der Form eines einzelnen Werts oder als Resultset zurückgeben.  
  
 Um ein SQLServerDatabaseMetaData-Objekt zu erstellen, können Sie die [GetMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse beim Abrufen von Informationen über die Datenbank, die mit der Sie verbunden ist.  
  
 Im folgenden Beispiel wird eine offene Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben, die GetMetaData-Methode der SQLServerConnection-Klasse wird verwendet, um ein SQLServerDatabaseMetadata-Objekt, und klicken Sie dann den verschiedenen Methoden des Zurückgeben der SQLServerDatabaseMetaData-Objekt werden verwendet, um Informationen zu den Treiber, Treiberversion, Datenbankname und Datenbankversion angezeigt.  
  
 [!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]  
  
## <a name="see-also"></a>Siehe auch  
 [Verarbeiten von Metadaten mit dem JDBC-Treiber](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  
