---
title: Abrufen von Resultsetdaten-Beispiel festgelegt | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1b190c36-3d38-49a2-8599-612329675851
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a2399dd259a9b06e2410c88c07991feb400b9080
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-result-set-data-sample"></a>Abrufen von Resultsetdaten - Beispiel
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Dies [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] beispielanwendung veranschaulicht das Abrufen von eines Satz von Daten aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, und klicken Sie dann Daten angezeigt werden.  
  
 Die Codedatei für dieses Beispiel heißt "retrieveRS.java" und befindet sich im folgenden Pfad:  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \samples\resultsets  
  
## <a name="requirements"></a>Anforderungen  
 Wenn Sie diese Beispielanwendung ausführen möchten, müssen Sie die Datei sqljdbc.jar oder sqljdbc4.jar in den Klassenpfad aufnehmen. Wenn im Klassenpfad kein Eintrag für sqljdbc.jar oder sqljdbc4.jar vorhanden ist, löst die Beispielanwendung die allgemeine Ausnahme "Klasse nicht gefunden" aus. Sie benötigen auch Zugriff auf die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank. Weitere Informationen zum Festlegen des Klassenpfads finden Sie unter [mit dem JDBC-Treiber](../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] enthält "sqljdbc.jar" und "sqljdbc4.jar", je nach Ihren bevorzugten Einstellungen für Java Runtime Environment (JRE) verwendet werden. Weitere Informationen zu der JAR-Datei auswählen, finden Sie unter [Systemanforderungen für JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Beispiel  
 In der folgende Beispielcode stellt eine Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank. Klicken Sie dann mithilfe einer SQL-Anweisung mit der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekts können sie führt die SQL-Anweisung und fügt die Daten werden in eine [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
 Als Nächstes der Beispielcode ruft die benutzerdefinierten DisplayRow-Methode, die die Datenzeilen durchlaufen, die im Resultset enthalten sind, und verwendet die [GetString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) Methode, um einige der Daten anzuzeigen, die es enthält.  
  
```java
import java.sql.*;  
  
public class retrieveRS {  
  
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
  
         // Create and execute an SQL statement that returns a  
         // set of data and then display it.  
         String SQL = "SELECT * FROM Production.Product;";  
         stmt = con.createStatement();  
         rs = stmt.executeQuery(SQL);  
         displayRow("PRODUCTS", rs);  
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
            System.out.println(rs.getString("ProductNumber") + " : " + rs.getString("Name"));  
         }  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Arbeiten mit Resultsets](../../connect/jdbc/working-with-result-sets.md)  
  
  

