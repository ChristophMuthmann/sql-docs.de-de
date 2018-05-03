---
title: Verwalten von Resultsets mit dem JDBC-Treiber legt | Microsoft Docs
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
ms.topic: conceptual
ms.assetid: 9ed5ad41-22e0-4e4a-8a79-10512db60d50
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70998fad7f3fa628b952e54a5d5dbb6cb90afde9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="managing-result-sets-with-the-jdbc-driver"></a>Verwalten von Resultsets mit dem JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Beim Resultset handelt es sich um ein Objekt, das die von einer Datenquelle zurückgegebenen Daten darstellt (normalerweise als Ergebnis einer Abfrage). Das Resultset enthält Zeilen und Spalten, die die angeforderten Datenelemente enthalten. Die Navigation erfolgt über einen Cursor. Ein Resultset kann aktualisiert werden, d. h., es besteht die Möglichkeit das Resultset zu ändern und diese Änderungen an die ursprüngliche Datenquelle zu übergeben. Ein Resultset kann auch unterschiedlich sensitiv gegenüber Änderungen in der zugrunde liegenden Datenquelle sein.  
  
 Der Typ des Resultset wird festgelegt, wenn eine Anweisung erstellt wird, also wenn bei einem Aufruf der [CreateStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) -Klasse aufgerufen wird. Die grundlegende Aufgabe eines Resultsets besteht darin, Java-Anwendungen eine nutzbare Darstellung der Datenbankdaten bereitzustellen. Dies erfolgt normalerweise mit den typisierten Abruf- und Festlegungsmethoden der Datenelemente des Resultset.  
  
 Im folgenden Beispiel wird die basierend auf der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank, ein Resultset wird erstellt, durch Aufrufen der [ExecuteQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) Methode der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse. Daten aus dem Resultset werden dann angezeigt, mit der [GetString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Klasse.  
  
 [!code[JDBC#ManagingResultSets1](../../connect/jdbc/codesnippet/Java/managing-result-sets-with-t_1.java)]  
  
 Die Themen in diesem Abschnitt beschreiben verschiedene Aspekte der Verwendung von Resultsets wie Cursortypen, Gleichzeitigkeit und Zeilensperren.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Grundlegendes zu Cursortypen](../../connect/jdbc/understanding-cursor-types.md)|Beschreibt die verschiedenen Cursortypen, die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] unterstützt.|  
|[Grundlegendes zur Parallelitätssteuerung](../../connect/jdbc/understanding-concurrency-control.md)|Beschreibt, wie der JDBC-Treiber die Parallelitätssteuerung unterstützt.|  
|[Grundlegendes zu Zeilensperren](../../connect/jdbc/understanding-row-locking.md)|Beschreibt, wie der JDBC-Treiber Zeilensperren unterstützt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Overview of the JDBC Driver (Übersicht über den JDBC-Treiber)](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
