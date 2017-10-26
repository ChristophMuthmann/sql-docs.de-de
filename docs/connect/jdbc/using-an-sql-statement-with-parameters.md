---
title: Verwenden eine SQL-Anweisung mit Parametern | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3202b88f-ce13-44dd-982c-c6a3b0260378
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8475ea4917ffcc0d9226933b29e81b99f89345c2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-an-sql-statement-with-parameters"></a>Verwenden von SQL-Anweisungen mit Parametern
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Zum Arbeiten mit Daten in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank mithilfe einer SQL-Anweisung, die IN-Parameter enthält, können Sie die [ExecuteQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) Methode der [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) Klasse, um eine zurückgeben[ SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) , der die angeforderten Daten enthält. Zu diesem Zweck müssen Sie zuerst ein SQLServerPreparedStatement-Objekt erstellen, mit der [PrepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse.  
  
 Beim Erstellen der SQL-Anweisung werden die IN-Parameter mit dem ? (Fragezeichen) angegeben, das als Platzhalter für die Parameterwerte fungiert, die später an die SQL-Anweisung übergeben werden. Um einen Wert für einen Parameter angeben, können Sie eine der Methoden Setter-Methode der SQLServerPreparedStatement-Klasse. Die verwendete Festlegungsmethode hängt vom Datentyp des Werts ab, der an die SQL-Anweisung übergeben werden soll.  
  
 Wenn Sie einen Wert an die Festlegungsmethode übergeben, müssen Sie nicht nur den Wert angeben, der in der SQL-Anweisung verwendet werden soll, sondern auch die ordinale Position des Parameters in der SQL-Anweisung. Wenn die SQL-Anweisung einen einzelnen Parameter enthält, wird z. B. ihres Ordinalwerts 1 sein. Wenn die Anweisung zwei Parameter enthält, wird der erste Ordinalwert 1, werden während der zweite Ordinalwert 2 ist.  
  
 Im folgenden Beispiel wird eine offene Verbindung mit dem [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben, eine vorbereitete SQL-Anweisung erstellt und mit einem einzigen String-Parameterwert ausgeführt, und klicken Sie dann die Ergebnisse aus dem Resultset gelesen.  
  
 [!code[JDBC#UsingSQLWithParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_1_1.java)]  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit SQL](../../connect/jdbc/using-statements-with-sql.md)  
  
  

