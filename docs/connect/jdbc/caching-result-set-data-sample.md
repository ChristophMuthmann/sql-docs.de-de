---
title: Zwischenspeichern von Ergebnis Datenbeispiel festlegen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13a95ebb-996c-4713-a1bd-5834fe22a334
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9061548b946d631f20a9b48ed49d56aac4a4f0fd
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="caching-result-set-data-sample"></a>Zwischenspeichern von Resultsetdaten - Beispiel
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Dies [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] beispielanwendung veranschaulicht, wie umfangreiche Daten aus einer Datenbank abgerufen und dann steuern die Anzahl von Zeilen mit Daten, die auf dem Client, mithilfe zwischengespeichert werden der [SetFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) Methode der [ SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
> [!NOTE]  
>  Die Einschränkung der im Client zwischengespeicherten Zeilen ist nicht mit der Einschränkung der Gesamtanzahl von Zeilen identisch, die ein Resultset enthalten kann. Verwenden, um die Gesamtzahl der Zeilen zu steuern, die in einem Resultset enthalten sind, die [SetMaxRows](../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) Methode der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, das von beiden geerbt wird die [ SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) und [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Objekte.  
  
 Um eine Grenze für die Anzahl der Zeilen, die auf dem Client zwischengespeicherten festzulegen, müssen Sie zuerst einen serverseitigen Cursor verwenden, wenn Sie eines der Statement-Objekte erstellen, indem Sie ausdrücklich den Cursortyp angeben zu verwenden, wenn das Statement-Objekt zu erstellen. Der JDBC-Treiber enthält beispielsweise den Cursortyp TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, d. h. eine schnelle Vorwärtscursor, schreibgeschützte serverseitige Cursor für die Verwendung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken.  
  
> [!NOTE]  
>  Alternativ zum SQL Server-spezifischen Cursortyp kann die selectMethod-Verbindungszeichenfolgeneigenschaft verwendet werden, indem deren Wert auf "cursor" festgelegt wird. Weitere Informationen zu den vom JDBC-Treiber unterstützten Cursortypen finden Sie unter [Grundlegendes zu Cursortypen](../../connect/jdbc/understanding-cursor-types.md).  
  
 Nachdem Sie die Abfrage in das Statement-Objekt enthaltenen ausgeführt haben, und die Daten ist an den Client als Resultset zurückgegebenen, können Sie durch Aufrufen die SetFetchSize-Methode, um zu steuern, wie viele Daten gleichzeitig aus der Datenbank abgerufen werden. Wenn eine Tabelle beispielsweise 100 Datenzeilen enthält und die Abrufgröße auf 10 festgelegt wird, werden im Client jeweils nur immer 10 Datenzeilen zwischengespeichert. Obwohl dadurch die Verarbeitungsgeschwindigkeit der Daten sinkt, ist auf dem Client weniger Speicher erforderlich, was insbesondere dann von Nutzen sein kann, wenn umfangreiche Daten verarbeitet werden müssen.  
  
 Die Codedatei für dieses Beispiel heißt "cacheRS.java" und befindet sich im folgenden Pfad:  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \samples\resultsets  
  
## <a name="requirements"></a>Anforderungen  
 Wenn Sie diese Beispielanwendung ausführen möchten, müssen Sie die Datei sqljdbc.jar oder sqljdbc4.jar in den Klassenpfad aufnehmen. Wenn im Klassenpfad kein Eintrag für sqljdbc.jar oder sqljdbc4.jar vorhanden ist, löst die Beispielanwendung die allgemeine Ausnahme "Klasse nicht gefunden" aus. Sie benötigen auch Zugriff auf die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank. Weitere Informationen zum Festlegen des Klassenpfads finden Sie unter [mit dem JDBC-Treiber](../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] enthält "sqljdbc.jar" und "sqljdbc4.jar", je nach Ihren bevorzugten Einstellungen für Java Runtime Environment (JRE) verwendet werden. Weitere Informationen zu der JAR-Datei auswählen, finden Sie unter [Systemanforderungen für JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Beispiel  
 In der folgende Beispielcode stellt eine Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank. Anschließend wird eine SQL-Anweisung mit der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, gibt den serverseitige Cursortyp, und klicken Sie dann führt die SQL-Anweisung und die zurückgegebenen Daten, die in ein SQLServerResultSet-Objekt zurückgegeben.  
  
 Als Nächstes ruft der Beispielcode die benutzerdefinierten TimerTest-Methode und übergeben die Abrufgröße als Argumente aus, und das Resultset. Die TimerTest-Methode legt die Abrufgröße des Resultsets mithilfe der SetFetchSize-Methode, die Startzeit des Tests fest und iteriert dann durch das Resultset mit einer `While` Schleife. Sobald die `While` Schleife beendet wird, der Code die Beendigungszeit des Tests und anschließend das Testergebnis einschließlich Abrufgröße, die Anzahl der Zeilen verarbeitet, wird angezeigt, und die Zeit zum Ausführen des Tests.  
  
```java
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.SQLServerResultSet;  
  
public class cacheRS {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
            "databaseName=AdventureWorks;integratedSecurity=true;";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
  
         // Create and execute an SQL statement that returns a large  
         // set of data and then display it.  
         String SQL = "SELECT * FROM Sales.SalesOrderDetail;";  
         stmt = con.createStatement(SQLServerResultSet.TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, +  
               SQLServerResultSet.CONCUR_READ_ONLY);  
  
         // Perform a fetch for every row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(1, rs);  
         rs.close();  
  
         // Perform a fetch for every tenth row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(10, rs);  
         rs.close();  
  
         // Perform a fetch for every 100th row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(100, rs);  
         rs.close();  
  
         // Perform a fetch for every 1000th row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(1000, rs);  
         rs.close();  
  
         // Perform a fetch for every 128th row (the default) in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(0, rs);  
         rs.close();  
      }  
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
  
      finally {  
         if (rs != null) try { rs.close(); } catch(Exception e) {}  
         if (stmt != null) try { stmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
      }  
   }  
  
   private static void timerTest(int fetchSize, ResultSet rs) {  
      try {  
  
         // Declare the variables for tracking the row count and elapsed time.  
         int rowCount = 0;  
         long startTime = 0;  
         long stopTime = 0;  
         long runTime = 0;  
  
         // Set the fetch size then iterate through the result set to  
         // cache the data locally.  
         rs.setFetchSize(fetchSize);  
         startTime = System.currentTimeMillis();  
         while (rs.next()) {  
            rowCount++;  
         }  
         stopTime = System.currentTimeMillis();  
         runTime = stopTime - startTime;  
  
         // Display the results of the timer test.  
         System.out.println("FETCH SIZE: " + rs.getFetchSize());  
         System.out.println("ROWS PROCESSED: " + rowCount);  
         System.out.println("TIME TO EXECUTE: " + runTime);  
         System.out.println();  
  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Arbeiten mit Resultsets](../../connect/jdbc/working-with-result-sets.md)  
  
  
