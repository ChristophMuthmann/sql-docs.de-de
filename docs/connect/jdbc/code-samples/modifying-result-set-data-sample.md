---
title: "Ändern von Resultsetdaten-Beispiel festlegen | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b5ae54dc-2a79-4664-bb21-cacdb7d745e1
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f97de286718a07ddc1b2595ca3e75a2aba294c73
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="modifying-result-set-data-sample"></a>Ändern von Resultsetdaten - Beispiel
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Dies [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] beispielanwendung veranschaulicht, wie ein aktualisierbarer Datensatz aus Abrufen einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datenbank. Klicken Sie dann mit den Methoden der der [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt, fügt, ändert und löscht dann schließlich eine Zeile mit Daten aus dem Satz von Daten.  
  
 Die Codedatei für dieses Beispiel heißt "updateRS.java" und befindet sich im folgenden Pfad:  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \samples\resultsets  
  
## <a name="requirements"></a>Anforderungen  
 Wenn Sie diese Beispielanwendung ausführen möchten, müssen Sie die Datei sqljdbc.jar oder sqljdbc4.jar in den Klassenpfad aufnehmen. Wenn im Klassenpfad kein Eintrag für sqljdbc.jar oder sqljdbc4.jar vorhanden ist, löst die Beispielanwendung die allgemeine Ausnahme "Klasse nicht gefunden" aus. Sie benötigen auch Zugriff auf die [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] -Beispieldatenbank. Weitere Informationen zum Festlegen des Klassenpfads finden Sie unter [mit dem JDBC-Treiber](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  Die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] enthält "sqljdbc.jar" und "sqljdbc4.jar", je nach Ihren bevorzugten Einstellungen für Java Runtime Environment (JRE) verwendet werden. Weitere Informationen zu der JAR-Datei auswählen, finden Sie unter [Systemanforderungen für JDBC Driver](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Beispiel  
 In der folgende Beispielcode stellt eine Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] -Beispieldatenbank. Klicken Sie dann mithilfe einer SQL-Anweisung mit der [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt, er führt die SQL-Anweisung und die zurückgegebenen Daten, die in ein aktualisierbares SQLServerResultSet-Objekt zurückgegeben.  
  
 Als Nächstes im Beispielcode wird die [MoveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) -Methode verschieben, das Resultset Cursor in die Einfügezeile verwendet eine Reihe von [UpdateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) Methoden zum Einfügen von Daten in die neue Zeile ein und ruft dann die [InsertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) Methode, um die neue Zeile der Daten wieder in der Datenbank persistent zu speichern.  
  
 Nachdem die neue Datenzeile eingefügt wurden, im Beispielcode verwendet eine SQL-Anweisung, die zuvor eingefügte Zeile abzurufen, und verwendet dann die Kombination aus UpdateString und [UpdateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) Methoden, um die Zeile der Daten zu aktualisieren und erneut gespeichert sichern die Datenbank.  
  
 Schließlich der Beispielcode ruft die zuvor aktualisierte Datenzeile ab und löscht sie anschließend aus der Datenbank mithilfe der [DeleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md) Methode.  
  
```java
import java.sql.*;  
  
public class updateRS {  
  
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
  
         // Create and execute an SQL statement, retrieving an updateable result set.  
         String SQL = "SELECT * FROM HumanResources.Department;";  
         stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);  
         rs = stmt.executeQuery(SQL);  
  
         // Insert a row of data.  
         rs.moveToInsertRow();  
         rs.updateString("Name", "Accounting");  
         rs.updateString("GroupName", "Executive General and Administration");  
         rs.updateString("ModifiedDate", "08/01/2006");  
         rs.insertRow();  
  
         // Retrieve the inserted row of data and display it.  
         SQL = "SELECT * FROM HumanResources.Department WHERE Name = 'Accounting';";  
         rs = stmt.executeQuery(SQL);  
         displayRow("ADDED ROW", rs);  
  
         // Update the row of data.  
         rs.first();  
         rs.updateString("GroupName", "Finance");  
         rs.updateRow();  
  
         // Retrieve the updated row of data and display it.  
         rs = stmt.executeQuery(SQL);  
         displayRow("UPDATED ROW", rs);  
  
         // Delete the row of data.  
         rs.first();  
         rs.deleteRow();  
         System.out.println("ROW DELETED");  
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
  
   private static void displayRow(String title, ResultSet rs) {  
      try {  
         System.out.println(title);  
         while (rs.next()) {  
            System.out.println(rs.getString("Name") + " : " + rs.getString("GroupName"));  
            System.out.println();  
         }  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Arbeiten mit Resultsets](../../../connect/jdbc/working-with-result-sets.md)  
  
  
