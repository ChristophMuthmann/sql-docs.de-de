---
title: Datenquellen-Beispiel | Microsoft Docs
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
ms.topic: conceptual
ms.assetid: b4a933ee-f2c6-4e0d-a96d-6dd061abf759
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f900b1b91bb3d9114c4f7da2e4450da45fd9ec21
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-sample"></a>Beispiel für Datenquellen
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Dies [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] beispielanwendung veranschaulicht die Vorgehensweise beim Herstellen einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] her, indem Sie ein Datenquellenobjekt. Außerdem wird veranschaulicht, wie zum Abrufen von Daten aus einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datenbank mithilfe einer gespeicherten Prozedur.  
  
 Die Codedatei für dieses Beispiel heißt "connectDS.java" und befindet sich im folgenden Pfad:  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \samples\connections  
  
## <a name="requirements"></a>Anforderungen  
 Um diese beispielanwendung ausführen möchten, müssen Sie den Klassenpfad zu der Datei "sqljdbc.jar" oder die Datei "sqljdbc4.jar" enthalten festlegen. Wenn im Klassenpfad kein Eintrag für sqljdbc.jar oder sqljdbc4.jar vorhanden ist, löst die Beispielanwendung die allgemeine Ausnahme "Klasse nicht gefunden" aus. Sie benötigen auch Zugriff auf die [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] -Beispieldatenbank. Weitere Informationen zum Festlegen des Klassenpfads finden Sie unter [mit dem JDBC-Treiber](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  Die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] enthält "sqljdbc.jar" und "sqljdbc4.jar", je nach Ihren bevorzugten Einstellungen für Java Runtime Environment (JRE) verwendet werden. Weitere Informationen zu der JAR-Datei auswählen, finden Sie unter [Systemanforderungen für JDBC Driver](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel legt der Beispielcode verschiedene Verbindungseigenschaften festlegungsmethoden der mit der [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) -Objekt, und ruft dann die [GetConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) Methode der SQLServerDataSource-Objekt, das Zurückgeben einer [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.  
  
 Als Nächstes im Beispielcode wird die [PrepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) Methode der SQLServerConnection-Objekt zum Erstellen einer [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) -Objekt, und klicken Sie dann die [ExecuteQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) Methode wird aufgerufen, um die gespeicherte Prozedur auszuführen.  
  
 Zum Schluss das Beispiel verwendet die [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt aus der ExecuteQuery-Methode zum Durchlaufen der von der gespeicherten Prozedur zurückgegebenen Ergebnisse zurückgegeben.  
  
```java
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  
  
public class connectDS {  
  
   public static void main(String[] args) {  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      CallableStatement cstmt = null;  
      ResultSet rs = null;  
  
      try {  
         // Establish the connection.   
         SQLServerDataSource ds = new SQLServerDataSource();  
         ds.setUser("UserName");  
         ds.setPassword("*****");  
         ds.setServerName("localhost");  
         ds.setPortNumber(1433);   
         ds.setDatabaseName("AdventureWorks");  
         con = ds.getConnection();  
  
         // Execute a stored procedure that returns some data.  
         cstmt = con.prepareCall("{call dbo.uspGetEmployeeManagers(?)}");  
         cstmt.setInt(1, 50);  
         rs = cstmt.executeQuery();  
  
         // Iterate through the data in the result set and display it.  
         while (rs.next()) {  
            System.out.println("EMPLOYEE: " + rs.getString("LastName") +   
               ", " + rs.getString("FirstName"));  
            System.out.println("MANAGER: " + rs.getString("ManagerLastName") +   
               ", " + rs.getString("ManagerFirstName"));  
            System.out.println();  
         }  
      }  
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
      finally {  
         if (rs != null) try { rs.close(); } catch(Exception e) {}  
         if (cstmt != null) try { cstmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
         System.exit(1);  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verbinden und Abrufen von Daten](../../../connect/jdbc/connecting-and-retrieving-data.md)  
  
  
