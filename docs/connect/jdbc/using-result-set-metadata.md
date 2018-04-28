---
title: Verwenden von Resultsetmetadaten | Microsoft Docs
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
ms.topic: article
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 03e6d7d247474c5c5c216ce744591e58f1c0eec8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="using-result-set-metadata"></a>Verwenden von Resultsetmetadaten
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Zum Abfragen eines Resultsets nach Informationen zu den Spalten, die es enthält, die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] implementiert die [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) Klasse. Diese Klasse enthält eine Vielzahl von Methoden, die Informationen in der Form eines einzelnen Werts zurückgeben.  
  
 Um ein SQLServerResultSetMetaData-Objekt zu erstellen, können Sie die [GetMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Klasse.  
  
 Im folgenden Beispiel wird eine offene Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben, die GetMetaData-Methode der SQLServerResultSet-Klasse wird verwendet, um ein SQLServerResultSetMetaData-Objekt, und klicken Sie dann den verschiedenen Methoden des Zurückgeben der SQLServerResultSetMetaData-Objekt werden verwendet, um Informationen zu den Namen und den Datentyp der im Resultset enthaltenen Spalten anzuzeigen.  
  
 [!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]  
  
## <a name="see-also"></a>Siehe auch  
 [Verarbeiten von Metadaten mit dem JDBC-Treiber](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  
