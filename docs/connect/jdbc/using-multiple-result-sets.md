---
title: Verwenden mehrerer Resultsets | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab6a3cfa-073b-44e9-afca-a8675cfe5fd1
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e4796d369ed9eb5567cb026d1892399c86479897
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-multiple-result-sets"></a>Verwenden von mehreren Resultsets
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Bei der Arbeit mit Inline-SQL oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gespeicherte Prozeduren, die mehrere Resultsets zurückgeben der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] bietet die [GetResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) Methode in der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) für Klasse Abrufen jedes Dataset zurückgegeben. Darüber hinaus beim Ausführen einer Anweisung, die mehr als ein Resultset zurückgibt, können Sie die [ausführen](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) -Methode der SQLServerStatement-Klasse, da es zurück eine **booleschen** -Wert, der gibt an, wenn die zurückgegebene Wert ist ein Resultset oder eine updatezählung.  
  
 Wenn die Execute-Methode gibt **"true"**, die ausgeführte Anweisung verfügt über eine oder mehrere Resultsets zurückgegeben. Sie können das erste Resultset durch Aufrufen der GetResultSet-Methode zugreifen. Um zu ermitteln, falls weitere Resultsets verfügbar sind, können Sie Aufrufen der [GetMoreResults](../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md) Methode, die zurückgibt eine **booleschen** Wert **"true"** Falls weitere Resultsets verfügbar sind. Falls weitere Resultsets verfügbar sind, können Sie rufen die GetResultSet-Methode erneut aus, um darauf zuzugreifen, und den Prozess fortsetzen, bis alle Resultsets verarbeitet wurden. Wenn Sie die GetMoreResults-Methode gibt **"false"**, es sind keine weiteren Resultsets zu verarbeiten.  
  
 Wenn die Execute-Methode gibt **"false"**, die ausgeführte Anweisung hat ein updatezählwert, die Sie, durch den Aufruf abrufen können der [GetUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) Methode.  
  
> [!NOTE]  
>  Weitere Informationen zu updatezählungen finden Sie unter [mithilfe einer gespeicherten Prozedur mit einer Anzahl aktualisieren](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md).  
  
 Im folgenden Beispiel wird eine offene Verbindung mit dem [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben und eine SQL­Anweisung erstellt, die bei Ausführung zwei Resultsets zurückgibt:  
  
 [!code[JDBC#UsingMultipleResultSets1](../../connect/jdbc/codesnippet/Java/using-multiple-result-sets_1.java)]  
  
 In diesem Fall ist bekannt, dass zwei Resultsets zurückgegeben werden. Der Code ist jedoch so geschrieben, dass alle Resultsets verarbeitet werden, wenn die Anzahl der zurückgegebenen Resultsets unbekannt ist, wie z. B. beim Aufrufen einer gespeicherten Prozedur. Ein Beispiel für das Aufrufen einer gespeicherten Prozedur, die mehrere Resultsets sowie updatewerte zurückgibt, finden Sie unter [Behandlung von komplexen Anweisungen](../../connect/jdbc/handling-complex-statements.md).  
  
> [!NOTE]  
>  Wenn Sie die GetMoreResults-Methode der SQLServerStatement-Klasse aufrufen, wird das zuvor zurückgegebene Resultset implizit geschlossen.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit der JDBC-Treiber](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  

