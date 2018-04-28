---
title: Ausführen von Batchvorgängen | Microsoft Docs
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
ms.assetid: 1a576d95-7da6-4b7b-8b32-59e5b4d354c4
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d7d2354686c312a353766d4af8b0b52d4f63e1e2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="performing-batch-operations"></a>Ausführen von Batchvorgängen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Zur Verbesserung der Leistung bei mehreren updates einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank auftreten, die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] bietet die Möglichkeit, mehrere Updates als einzelne Einheit arbeiten, auch bezeichnet als Batch zu übermitteln.  
  
 Die [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), und [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klassen können alle zum Übermitteln von BatchUpdates verwendet werden. Die [AddBatch](../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md) Methode wird verwendet, um einen Befehl hinzufügen. Die [ClearBatch](../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md) Methode wird verwendet, um die Liste der Befehle löschen. Die [ExecuteBatch](../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md) Methode wird verwendet, um alle zu verarbeitenden Befehle übermitteln. In einem Batch können nur DDL- (Data Definition Language) und DML-Anweisungen (Data Manipulation Language) ausgeführt werden, die eine einfache Updatezählung zurückgeben.  
  
 ExecuteBatch-Methode gibt ein Array von **Int** Werte, die der updatezählung der einzelnen Befehle entsprechen. Wenn einer der Befehle fehlschlägt, eine BatchUpdateException wird ausgelöst, und Sie sollten die GetUpdateCounts-Methode der Klasse BatchUpdateException verwenden, das Update Array mit updatezählungen abrufen. Wenn ein Befehl fehlschlägt, wird die Verarbeitung der restlichen Befehle vom Treiber fortgesetzt. Wenn ein Befehl einen Syntaxfehler enthält, schlagen die Anweisungen im Batch allerdings fehl.  
  
> [!NOTE]  
>  Wenn Sie keine updatezählungen verwendet, können Sie zuerst eine SET NOCOUNT ON-Anweisung an ausgeben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Dadurch wird das Verkehrsaufkommen im Netzwerk verringert und zusätzlich die Leistung der Anwendung verbessert.  
  
 Erstellen Sie beispielsweise die folgende Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank:  
  
```  
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
```  
  
 Im folgenden Beispiel wird eine offene Verbindung mit dem [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben, die AddBatch-Methode wird verwendet, um die auszuführenden Anweisungen erstellen und die ExecuteBatch-Methode wird aufgerufen, um den Stapel an die Datenbank zu übermitteln.  
  
```  
public static void executeBatchUpdate(Connection con) {  
   try {  
      Statement stmt = con.createStatement();  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('X', 100)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Y', 200)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Z', 300)");  
      int[] updateCounts = stmt.executeBatch();  
      stmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit dem JDBC-Treiber](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
