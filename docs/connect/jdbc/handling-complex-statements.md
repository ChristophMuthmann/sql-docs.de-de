---
title: Verarbeiten komplexer Anweisungen | Microsoft Docs
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
ms.assetid: 6b807a45-a8b5-4b1c-8b7b-d8175c710ce0
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7eb061374707182a9ccc2cd26e223387c580d72a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="handling-complex-statements"></a>Verarbeiten komplexer Anweisungen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Bei Verwendung der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], möglicherweise müssen Sie komplexe Anweisungen verarbeiten, z. B. Anweisungen, die zur Laufzeit dynamisch generiert werden. Komplexe Anweisungen führen oftmals eine Vielzahl von Tasks aus, wie z. B. Update-, Insert- und Delete-Operationen. Diese Anweisungstypen können auch mehrere Resultsets und Ausgabeparameter zurückgeben. In diesen Situationen kann es vorkommen, dass der Java-Code, der die Anweisungen ausführt, die Typen und die Anzahl der zurückgegebenen Objekte und Daten zunächst nicht kennt.  
  
 Um komplexe Anweisungen effizient auszuführen, umfasst der JDBC-Treiber eine Reihe von Methoden, um die zurückgegebenen Objekte und Daten abzufragen, damit sie in der Anwendung ordnungsgemäß verarbeitet werden können. Der Schlüssel für die Verarbeitung komplexer Anweisungen ist die [ausführen](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) Methode der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse. Diese Methode gibt ein **booleschen** Wert. Ist der Wert "true", handelt es sich bei dem ersten zurückgegebenen Ergebnis der Anweisungen um ein Resultset. Ist der Wert "false", handelt es sich bei dem ersten zurückgegebenen Ergebnis um eine Updatezählung.  
  
 Wenn Sie, den Typ der Objekte oder Daten, die zurückgegeben wurde wissen, können Sie entweder die [GetResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) oder [GetUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) Methode, um diese Daten verarbeiten. Um den Vorgang fortzusetzen, um die nächsten Objekte oder Daten, die von der komplexen Anweisung zurückgegeben wird, rufen Sie die [GetMoreResults](../../connect/jdbc/reference/getmoreresults-method.md) Methode.  
  
 Im folgenden Beispiel wird eine offene Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben, eine komplexe Anweisung erstellt, die den Aufruf einer gespeicherten Prozedur mit einer SQL­Anweisung kombiniert, die Anweisungen ausgeführt werden, und klicken Sie dann eine `do` Schleife ist verwendet, um alle zu verarbeiten, die Resultsets und updatezählungen, die zurückgegeben werden.  
  
 [!code[JDBC#HandlingComplexStatements1](../../connect/jdbc/codesnippet/Java/handling-complex-statements_1.java)]  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit dem JDBC-Treiber](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
