---
title: Verbindungs-URL-Beispiel | Microsoft Docs
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
ms.assetid: 96fabc42-59d1-4cc0-93c5-db00cbe55e95
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0de7532072829348ad1beac67137e8674260807c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="connection-url-sample"></a>Verbindungs-URL - Beispiel
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Dies [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] beispielanwendung veranschaulicht die Vorgehensweise beim Herstellen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] her, indem Sie einen Verbindungs-URL. Außerdem wird veranschaulicht, wie zum Abrufen von Daten aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank mithilfe einer SQL­Anweisung.  
  
 Die Codedatei für dieses Beispiel heißt "connectURL.java" und befindet sich im folgenden Pfad:  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \samples\connections  
  
## <a name="requirements"></a>Anforderungen  
 Um diese beispielanwendung ausführen möchten, müssen Sie den Klassenpfad zu der Datei "sqljdbc.jar" oder die Datei "sqljdbc4.jar" enthalten festlegen. Wenn im Klassenpfad kein Eintrag für sqljdbc.jar oder sqljdbc4.jar vorhanden ist, löst die Beispielanwendung die allgemeine Ausnahme "Klasse nicht gefunden" aus. Sie benötigen auch Zugriff auf die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank. Weitere Informationen zum Festlegen des Klassenpfads finden Sie unter [mit dem JDBC-Treiber](../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] enthält "sqljdbc.jar" und "sqljdbc4.jar", je nach Ihren bevorzugten Einstellungen für Java Runtime Environment (JRE) verwendet werden. Weitere Informationen zu der JAR-Datei auswählen, finden Sie unter [Systemanforderungen für JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel der Beispielcode legt in der Verbindungs-URL verschiedene Verbindungseigenschaften fest und ruft anschließend die GetConnection-Methode der zurückzugebenden DriverManager-Klasse eine [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.  
  
 Als Nächstes im Beispielcode wird die [CreateStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) Methode der SQLServerConnection-Objekt zum Erstellen einer [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, und klicken Sie dann die [ExecuteQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) Methode wird aufgerufen, um die SQL-Anweisung auszuführen.  
  
 Zum Schluss das Beispiel verwendet die [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt aus der ExecuteQuery-Methode zum Durchlaufen der von der SQL-Anweisung zurückgegebenen Ergebnisse zurückgegeben.  
  
```java  
import java.sql.*;  
  
public class connectURL {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
         "databaseName=AdventureWorks;user=UserName;password=*****";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
  
         // Create and execute an SQL statement that returns some data.  
         String SQL = "SELECT TOP 10 * FROM Person.Contact";  
         stmt = con.createStatement();  
         rs = stmt.executeQuery(SQL);  
  
         // Iterate through the data in the result set and display it.  
         while (rs.next()) {  
            System.out.println(rs.getString(4) + " " + rs.getString(6));  
         }  
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
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verbinden und Abrufen von Daten](../../connect/jdbc/connecting-and-retrieving-data.md)  
  
  
