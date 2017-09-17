---
title: Verwenden einer SQL-Anweisung ohne Parameter | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b0728bd-059b-4b71-895c-999335bc7427
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1e7e97fa030c2efd499aebfa054c0e4827d590dc
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-an-sql-statement-with-no-parameters"></a>Verwenden von SQL-Anweisungen ohne Parameter
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Zum Arbeiten mit Daten in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank mithilfe einer SQL-Anweisung, die keine Parameter enthält, können Sie die [ExecuteQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) Methode der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse die Rückgabe eine [ SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) , der die angeforderten Daten enthält. Zu diesem Zweck müssen Sie zuerst ein SQLServerStatement-Objekt erstellen, mit der [CreateStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse.  
  
 Im folgenden Beispiel wird eine offene Verbindung mit dem [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben, eine SQL-Anweisung erstellt und ausgeführt wird, und klicken Sie dann die Ergebnisse aus dem Resultset gelesen.  
  
 [!code[JDBC#UsingSQLWithNoParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_0_1.java)]  
  
 Weitere Informationen zur Verwendung von Resultsets finden Sie unter [Verwalten von Resultsets mit dem JDBC-Treiber](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit SQL](../../connect/jdbc/using-statements-with-sql.md)  
  
  
