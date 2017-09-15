---
title: Verwalten von Resultsets mit dem JDBC-Treiber legt | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9ed5ad41-22e0-4e4a-8a79-10512db60d50
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e17e39f8a83313a60b269fed82631b80f07ffed5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
 [Übersicht über die JDBC-Treiber](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
