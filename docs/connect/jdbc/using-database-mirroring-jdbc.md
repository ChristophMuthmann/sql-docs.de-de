---
title: Verwenden der Datenbankspiegelung (JDBC) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4ff59218-0d3b-4274-b647-9839c4955865
caps.latest.revision: "25"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 39ff223c82ad0eb521fc0c220a510bc8eb2e546a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="using-database-mirroring-jdbc"></a>Verwenden der Datenbankspiegelung (JDBC)
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Bei der Datenbankspiegelung handelt es sich im Wesentlichen um eine Softwarelösung, um Datenbankverfügbarkeit und Datenredundanz zu verbessern. Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] beinhaltet eine implizite Unterstützung für die datenbankspiegelung, sodass der Entwickler nicht notwendigerweise Code schreiben oder andere Aktionen ausführen, wenn er für die Datenbank konfiguriert wurde.  
  
 Datenbankspiegelung, die für eine Datenbanken einzeln implementiert wird, befindet sich eine Kopie einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Produktionsdatenbank auf einem Standbyserver. Bei dem Server handelt es sich je nach Konfiguration und Status der Datenbankspiegelungs-Sitzung um einen unmittelbar betriebsbereiten oder einfach betriebsbereiten Standbyserver. Ein unmittelbar betriebsbereiter Standbyserver unterstützt einen schnellen Failover ohne Verlust von Transaktionen, für die ein Commit ausgeführt wurde. Ein betriebsbereiter Standbyserver sorgt lediglich dafür, dass der Dienst bereitgestellt wird (mit möglichem Datenverlust).  
  
 Die Produktionsdatenbank wird aufgerufen, die *principal* Datenbank und die Standbykopie wird aufgerufen, die *Spiegel* Datenbank. Die Prinzipaldatenbank und Spiegeldatenbank müssen, befinden sich auf separaten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] (Serverinstanzen), und sie sollten auf separaten Computern befinden, ist es möglich.  
  
 Die Produktionsserverinstanz (Prinzipalserver) kommuniziert mit der Standbyserverinstanz (Spiegelserver). Der Prinzipal- und der Spiegelserver agieren in einer Datenbankspiegelungs-Sitzung als Partner. Wenn der Prinzipalserver ausfällt, kann der Spiegelserver seine Datenbank vornehmen, in der Prinzipaldatenbank mithilfe des so genannten *Failover*. Beispiel: Partner_A und Partner_B sind zwei Partnerserver. Die Prinzipaldatenbank befindet sich anfänglich auf dem Prinzipalserver Partner_A und die Spiegeldatenbank auf dem Spiegelserver Partner_B. Wenn Partner_A offline geht, kann die Datenbank auf Partner_B ein Failover ausführen, um zur aktuellen Prinzipaldatenbank zu werden. Sobald Partner_A wieder mit der Sitzung verbunden ist, übernimmt er wieder die Rolle des Spiegelservers und seine Datenbank wird zur Spiegeldatenbank.  
  
 Falls der Server Partner_A irreparabel beschädigt wird, kann der Server Partner_C in den Onlinemodus versetzt werden und als Spiegelserver für Partner_B fungieren, der jetzt der Prinzipalserver ist. In diesem Szenario muss die Clientanwendung jedoch eine Programmlogik enthalten, die sicherstellt, dass die Verbindungszeichenfolgeneigenschaften mit den neuen Servernamen aktualisiert werden, die in der Datenbankspiegelungskonfiguration verwendet werden, da andernfalls keine Verbindung zu den Servern hergestellt werden kann.  
  
 Alternative Konfigurationen für die Datenbankspiegelung bieten unterschiedliche Leistungs- und Datensicherheitsstufen und unterstützen unterschiedliche Formen des Failover. Weitere Informationen finden Sie unter "Übersicht über die Datenbankspiegelung" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="programming-considerations"></a>Überlegungen zur Programmierung  
 Wenn auf dem Prinzipaldatenbankserver ein Fehler auftritt, empfängt die Clientanwendung als Antwort auf API-Aufrufe Fehlermeldungen. Dadurch wird angezeigt, dass die Verbindung zur Datenbank unterbrochen ist. In diesem Fall gehen Änderungen verloren, für die kein Commit ausgeführt wurde, und für die aktuelle Transaktion wird ein Rollback ausgeführt. Die Anwendung muss dann die Verbindung schließen (oder das Datenquellenobjekt freigeben) und versuchen, eine neue Verbindung zu öffnen. Nachdem die Verbindung hergestellt wurde, wird die neue Verbindung transparent an die Spiegeldatenbank umgeleitet, die jetzt als Prinzipalserver fungiert, ohne dass der Client die Verbindungszeichenfolge oder das Datenquellenobjekt ändern muss.  
  
 Wenn die erste Verbindung hergestellt wird, sendet der Prinzipalserver die Identität seines Failoverpartners, der bei einem Failover verwendet wird, an den Client. Wenn eine Anwendung versucht, die erste Verbindung zu einem ausgefallenen Prinzipalserver herzustellen, kennt der Client die Identität des Failoverpartners nicht. Damit Clients die Möglichkeit, die in dieser Situation, die die FailoverPartner-Verbindungszeichenfolgeneigenschaft Abhilfe können und optional die [SetFailoverPartner](../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) datenquellmethode, kann der Client die Identität des Failovers angeben Partner selbst. Die Clienteigenschaft wird nur in diesem Szenario verwendet. Sie wird nicht verwendet, wenn der Prinzipalserver verfügbar ist.  
  
> [!NOTE]  
>  Wenn in der Verbindungszeichenfolge oder mit einem Datenquellenobjekt ein Failoverpartner angegeben wird, muss auch die databaseName-Eigenschaft festgelegt werden, da sonst eine Ausnahme ausgegeben wird. Wenn failoverPartner und databaseName nicht explizit angegeben werden, versucht die Anwendung kein Failover, wenn beim Prinzipaldatenbankserver ein Fehler auftritt. Anders ausgedrückt funktioniert die transparente Umleitung nur bei Verbindungen, bei denen failoverPartner und databaseName explizit angegeben werden. Weitere Informationen zu FailoverPartner und anderen verbindungszeichenfolgeeigenschaften finden Sie unter [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Wenn der vom Client angegebene Failoverpartnerserver kein Server ist, der als Failoverpartner für die angegebene Datenbank fungiert und der Server bzw. die Datenbank, auf den bzw. die verwiesen wird, für die Spiegelung konfiguriert wurde, wird die Verbindung vom Server abgelehnt. Obwohl die [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) -Klasse stellt die [GetFailoverPartner](../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md) -Methode, gibt diese Methode nur den Namen des Failoverpartners in der Verbindungszeichenfolge angegeben oder die SetFailoverPartner-Methode. Um den Namen des tatsächlichen Failoverpartners abrufen, die derzeit verwendet wird, verwenden Sie die folgenden [!INCLUDE[tsql](../../includes/tsql_md.md)] Anweisung:  
  
```  
SELECT m.mirroring_role_DESC, m.mirroring_state_DESC,  
m.mirroring_partner_instance FROM sys.databases as db,  
sys.database_mirroring AS m WHERE db.name = 'MirroringDBName'  
AND db.database_id = m.database_id  
```  
  
> [!NOTE]  
>  Sie müssen diese Anweisung so ändern, dass der Name der jeweiligen Spiegeldatenbank verwendet wird.  
  
 Sie sollten erwägen, die Partnerinformationen zwischenzuspeichern, um die Verbindungszeichenfolge zu aktualisieren, oder eine Wiederholungsstrategie entwickeln, falls der erste Versuch, eine Verbindung herzustellen, fehlschlägt.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird versucht, zuerst eine Verbindung zum Prinzipalserver herzustellen. Wenn keine Verbindung hergestellt werden kann und eine Ausnahme ausgegeben wird, wird versucht, eine Verbindung zum Spiegelserver herzustellen, der zum neuen Prinzipalserver heraufgestuft wurde. Achten Sie auf die Verwendung der failoverPartner-Eigenschaft in der Verbindungszeichenfolge.  
  
```  
import java.sql.*;  
  
public class clientFailover {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://serverA:1433;" +  
         "databaseName=AdventureWorks;integratedSecurity=true;" +  
         "failoverPartner=serverB";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
  
      try {  
         // Establish the connection to the principal server.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
         System.out.println("Connected to the principal server.");  
  
         // Note that if a failover of serverA occurs here, then an  
         // exception will be thrown and the failover partner will  
         // be used in the first catch block below.  
  
         // Create and execute an SQL statement that inserts some data.  
         stmt = con.createStatement();  
  
         // Note that the following statement assumes that the   
         // TestTable table has been created in the AdventureWorks  
         // sample database.  
         stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");  
      }  
  
      // Handle any errors that may have occurred.  
      catch (SQLException se) {  
         try {  
            // The connection to the principal server failed,  
            // try the mirror server which may now be the new  
            // principal server.  
            System.out.println("Connection to principal server failed, " +  
            "trying the mirror server.");  
            con = DriverManager.getConnection(connectionUrl);  
            System.out.println("Connected to the new principal server.");  
            stmt = con.createStatement();  
            stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");  
         }  
         catch (Exception e) {  
            e.printStackTrace();  
         }  
      }  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
      // Close the JDBC objects.  
      finally {  
         if (stmt != null) try { stmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verbinden von SQL Server mit dem JDBC-Treiber](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
