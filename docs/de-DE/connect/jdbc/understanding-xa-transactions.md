---
title: Grundlegendes zu XA-Transaktionen | Microsoft Docs
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
ms.assetid: 574e326f-0520-4003-bdf1-62d92c3db457
caps.latest.revision: 80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8374e1fdf20194bad254857b5efacdca13da4dd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-xa-transactions"></a>Grundlegendes zu XA-Transaktionen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] bietet Unterstützung für Java-Plattform, Enterprise Edition/JDBC 2.0 optional verteilte Transaktionen. JDBC-Verbindungen abgerufen werden, aus der [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) Klasse normaler verteilter transaktionsverarbeitungsumgebungen wie Java-Plattform, Enterprise Edition (Java EE)-Anwendungsservern teilnehmen kann.  
  
> [!WARNING]  
>  Microsoft JDBC Driver 4.2 (und höher) für SQL neue Timeoutoptionen für die vorhandene Funktion für den automatischen Rollback nicht vorbereiteter Transaktionen enthält. Finden Sie unter [Konfigurieren von serverseitigen Timeouteinstellungen für den automatischen Rollback nicht vorbereiteter Transaktionen](../../connect/jdbc/understanding-xa-transactions.md#BKMK_ServerSide) weiter unten in diesem Thema ausführlicher.  
  
## <a name="remarks"></a>Hinweise  
 Für die Implementierung verteilter Transaktionen stehen die folgenden Klassen zur Verfügung:  
  
|Klasse|Implementiert|Description|  
|-----------|----------------|-----------------|  
|com.microsoft.sqlserver.jdbc.SQLServerXADataSource|javax.sql.XADataSource|Das Klassenfactory für verteilte Verbindungen.|  
|com.microsoft.sqlserver.jdbc.SQLServerXAResource|javax.transaction.xa.XAResource|Der Ressourcenadapter für den Transaktions-Manager.|  
  
> [!NOTE]  
>  Verbindungen für verteilte XA-Transaktionen verwenden standardmäßig die Isolationsstufe "Lesen mit Commit".  
  
## <a name="guidelines-and-limitations-when-using-xa-transactions"></a>Richtlinien und Einschränkungen für die Verwendung von XA-Transaktionen  
 Die folgenden zusätzlichen Richtlinien gelten für eng verkoppelte Transaktionen:  
  
-   Wenn Sie XA-Transaktionen zusammen mit MS DTC (Microsoft Distributed Transaction Coordinator) verwenden, stellen Sie möglicherweise fest, dass die aktuelle Version von MS DTC eng verkoppeltes XA-Verzweigungsverhalten nicht unterstützt. MS DTC verfügt beispielsweise über eine 1:1-Zuordnung zwischen einer Transaktions-ID für eine XA-Verzweigung (XID) und einer MS DTC-Transaktions-ID, und die von lose verbundenen XA-Verzweigungen ausgeführten Aktionen sind voneinander isoliert.  
  
     An bereitgestellte Hotfix [MSDTC und eng verkoppelte Transaktionen](http://support.microsoft.com/kb/938653) ermöglicht die Unterstützung von eng verkoppelte XA-Verzweigungen, wobei mehrere XA-mit derselben globalen Transaktions-ID (GTRID Verzweigungen) einer einzelnen MS DTC-Transaktions-ID zugeordnet sind Diese Unterstützung können mehrere eng verkoppelte XA-Verzweigungen die jeweiligen Änderungen im Ressourcen-Manager, wie etwa [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Ein [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) Flag ermöglicht, dass die Anwendungen die eng verkoppelte XA-Transaktionen verwenden, die verschiedene XA-verzweigungstransaktions-IDs (BQUAL) aufweisen, jedoch haben die gleiche globale Transaktions-ID (GTRID) und format-ID (FormatID verfügen). Um diese Funktion verwenden zu können, müssen Sie festlegen der [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) für den Flagsparameter der Methode XAResource.start:  
  
    ```  
    xaRes.start(xid, SQLServerXAResource.SSTRANSTIGHTLYCPLD);  
    ```  
  
## <a name="configuration-instructions"></a>Konfigurationsanweisungen  
 Die folgenden Schritte sind erforderlich, wenn Sie XA-Datenquellen zusammen mit Microsoft Distributed Transaction Coordinator (MS DTC) verwenden möchten.  
  
> [!NOTE]  
>  Die JDBC-Komponenten für verteilte Transaktionen sind im Verzeichnis "xa" der JDBC-Treiberinstallation enthalten. Zu diesen Komponenten zählen die Dateien "xa_install.sql" und "sqljdbc_xa.dll".  
  
### <a name="running-the-ms-dtc-service"></a>Ausführen des MS DTC-Diensts  
 Der MS DTC-Dienst sollte markiert **automatische** in Service Manager, um sicherzustellen, dass er, wenn ausgeführt wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Dienst wird gestartet. Führen Sie die folgenden Schritte aus, um MS DTC für XA-Transaktionen zu aktivieren:  
  
 Unter Windows Vista und höher:  
  
1.  Klicken Sie auf die **starten** , geben **Dcomcnfg** am Anfang **Suche** Feld, und drücken Sie dann die EINGABETASTE, um öffnen **Komponentendienste**. Sie können auch in %windir%\system32\comexp.msc eingeben der **Suche** um öffnen **Komponentendienste**.  
  
2.  Erweitern Sie „Komponentendienste“, „Computer“, „Arbeitsplatz“ und dann „Distributed Transaction Coordinator“.  
  
3.  Mit der rechten Maustaste **Lokaler DTC** und wählen Sie dann **Eigenschaften**.  
  
4.  Klicken Sie auf die **Sicherheit** Registerkarte auf die **Eigenschaften von Lokaler DTC** (Dialogfeld).  
  
5.  Wählen Sie die **XA-Transaktionen ermöglichen** Kontrollkästchen, und klicken Sie dann auf **OK**. Daraufhin muss der MS DTC-Dienst neu gestartet werden.  
  
6.  Klicken Sie auf **OK** zu schließen die **Eigenschaften** (Dialogfeld), und schließen Sie **Komponentendienste**.  
  
7.  Beenden und anschließenden Neustarten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] um sicherzustellen, dass sie die MS DTC-Änderungen synchronisiert.  
  
### <a name="configuring-the-jdbc-distributed-transaction-components"></a>Konfigurieren der JDBC-Komponenten für verteilte Transaktionen  
 Führen Sie die folgenden Schritte aus, um die Komponenten des JDBC-Treibers für verteilte Transaktionen zu konfigurieren:  
  
1.  Kopieren Sie die neue "sqljdbc_xa.dll" aus dem Installationsverzeichnis des JDBC-Treiber in das Verzeichnis "BINN" der jeder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Computers, der in an verteilten Transaktionen.  
  
    > [!NOTE]  
    >  Bei Verwendung von XA-Transaktionen mit einem 32-Bit- [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], verwenden Sie die Datei "sqljdbc_xa.dll" in der X86 Ordner, auch wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] installiert ist, auf eine X64 Prozessor. Bei Verwendung von XA-Transaktionen mit einem 64-Bit- [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] auf die X64 Prozessor, verwenden Sie die Datei "sqljdbc_xa.dll" in der X64 Ordner.  
  
2.  Führen Sie das Datenbankskript xa_install.SQL aus, für jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Instanz, die in einbezogen werden verteilte Transaktionen. Mit diesem Skript werden die erweiterten gespeicherten Prozeduren installiert, die von „sqljdbc_xa.dll“ aufgerufen werden. Diese erweiterten gespeicherten Prozeduren implementieren verteilte Transaktionen und XA-Unterstützung für die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]. Sie müssen dieses Skript als Administrator Ausführen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Instanz.  
  
3.  Um einem bestimmten Benutzer die Berechtigungen für die Teilnahme an verteilten Transaktionen mit dem JDBC-Treiber zu gewähren, fügen Sie den Benutzer der Rolle "SqlJDBCXAUser" hinzu.  
  
 Sie können nur eine Version der Assembly "sqljdbc_xa.dll" auf jedem konfigurieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Instanz zu einem Zeitpunkt. Anwendungen müssen möglicherweise unterschiedliche Versionen des JDBC-Treibers verwenden, für die Verbindung mit derselben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Instanz mithilfe der XA-Verbindungs. In diesem Fall muss "sqljdbc_xa.dll", die mit den neuesten JDBC-Treibers stammt, installiert werden, auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Instanz.  
  
 Es gibt drei Möglichkeiten, um zu überprüfen, ob derzeit installierte Version von "sqljdbc_xa.dll" auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Instanz:  
  
1.  Öffnen Sie das Verzeichnis LOG des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Computers, der in an verteilten Transaktionen. Wählen Sie aus, und öffnen Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datei "ERRORLOG". Suchen Sie in der Datei "ERRORLOG" nach "Version ... von 'SQLJDBC_XA.dll' wird verwendet".  
  
2.  Öffnen Sie das Verzeichnis "BINN" der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Computers, der in an verteilten Transaktionen. Wählen Sie die Assembly "sqljdbc_xa.dll".  
  
    -   Unter Windows Vista oder höheren Versionen: Klicken Sie mit der rechten Maustaste auf "sqljdbc_xa.dll", und klicken Sie anschließend auf "Eigenschaften". Klicken Sie dann auf die **Details** Registerkarte. Die **Dateiversion** Feld zeigt die Version von "sqljdbc_xa.dll", die derzeit auf installiert ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Instanz.  
  
3.  Legen Sie die Protokollfunktion wie im Codebeispiel im nächsten Abschnitt fest. Suchen Sie in der Ausgabeprotokolldatei nach "Server-XA-DLL-Version ...".  
  
###  <a name="BKMK_ServerSide"></a> Konfigurieren von serverseitigen Timeouteinstellungen für den automatischen Rollback nicht vorbereiteter Transaktionen  
  
> [!WARNING]  
>  Diese serverseitige Option ist neu in Microsoft JDBC Driver 4.2 (und höher) für SQL Server. Um das aktualisierte Verhalten nutzen zu können, stellen Sie sicher, dass ein Update von „sqljdbc_xa.dll“ auf dem Server ausgeführt wird. Weitere Informationen zum Festlegen von clientseitigen Timeouts finden Sie unter [XAResource.setTransactionTimeout()](http://docs.oracle.com/javase/8/docs/api/javax/transaction/xa/XAResource.html).  
  
 Das Timeoutverhalten von verteilten Transaktionen wird mithilfe von zwei Registrierungseinstellungen (DWORD-Werten) gesteuert:  
  
-   **XADefaultTimeout** (in Sekunden): das Standard-Timeoutwert verwendet werden, wenn der Benutzer kein Timeout festgelegt wird. Die Standardeinstellung ist 0.  
  
-   **XAMaxTimeout** (in Sekunden): der maximale Wert des Timeouts, die ein Benutzer festlegen können. Die Standardeinstellung ist 0.  
  
 Diese Einstellungen sind für die jeweilige SQL Server-Instanz spezifisch und sollten unter diesem Registrierungsschlüssel erstellt werden:  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL\<**Version**>.\< *Instance_name*> \XATimeout  
  
> [!NOTE]  
>  Für 32-Bit SQL Server auf 64-Bit-Computern ausgeführt, die Registrierungseinträge erstellt werden soll, unter dem folgenden Schlüssel: HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Microsoft SQL Server\MSSQL\<Version >. < Instanzname > \ XATimeout  
  
 Ein Timeoutwert wird für jede Transaktion bei deren Start festgelegt, und es erfolgt ein Rollback der Transaktion durch SQL Server, wenn der Timeout abläuft. Das Timeout wird auf der Grundlage dieser Registrierungseinstellungen und der Angaben des Benutzers in „XAResource.setTransactionTimeout()“ festgelegt. Hier einige Beispiele zur Interpretation dieser Timeoutwerte:  
  
-   XADefaultTimeout = 0, XAMaxTimeout = 0  
  
     Bedeutet, dass kein Standardtimeout verwendet wird, und kein maximales Timeout für Clients durchgesetzt wird. In diesem Fall tritt ein Timeout für Transaktionen nur dann auf, wenn der Client ein Timeout mithilfe von „XAResource.setTransactionTimeout“ festlegt.  
  
-   XADefaultTimeout = 60, XAMaxTimeout = 0  
  
     Bedeutet, dass alle Transaktionen ein Timeout von 60 Sekunden aufweisen, wenn vom Client kein Timeout festgelegt wird. Wenn der Client ein Timeout angibt, wird dieser Timeoutwert verwendet. Es wird kein maximaler Wert für das Timeout durchgesetzt.  
  
-   XADefaultTimeout = 30, XAMaxTimeout = 60  
  
     Bedeutet, dass alle Transaktionen ein Timeout von 30 Sekunden aufweisen, wenn vom Client kein Timeout festgelegt wird. Wenn der Client ein Timeout angibt, wird das Timeout des Clients verwendet, sofern es weniger als 60 Sekunden (den Maximalwert) beträgt.  
  
-   XADefaultTimeout = 0, XAMaxTimeout = 30  
  
     Bedeutet, dass alle Transaktionen ein Timeout von 30 Sekunden (den Maximalwert) aufweisen, wenn vom Client kein Timeout festgelegt wird. Wenn der Client ein Timeout angibt, wird das Timeout des Clients verwendet, sofern es weniger als 30 Sekunden (den Maximalwert) beträgt.  
  
### <a name="upgrading-sqljdbcxadll"></a>Aktualisieren von "sqljdbc_xa.dll"  
 Wenn Sie eine neue Version des JDBC-Treibers installieren, sollten Sie auch „sqljdbc_xa.dll“ aus der neuen Version verwenden, um „sqljdbc_xa.dll“ auf dem Server zu aktualisieren.  
  
> [!IMPORTANT]  
>  Sie sollten das Upgrade von „sqljdbc_xa.dll“ im Rahmen einer Wartung oder zu einem Zeitpunkt ausführen, zu dem keine MS DTC-Transaktionen MS DTC in Bearbeitung sind.  
  
1.  Entladen von "sqljdbc_xa.dll" mit der [!INCLUDE[tsql](../../includes/tsql_md.md)] Befehl **DBCC Sqljdbc_xa (FREE)**.  
  
2.  Kopieren Sie die neue "sqljdbc_xa.dll" aus dem Installationsverzeichnis des JDBC-Treiber in das Verzeichnis "BINN" der jeder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Computers, der in an verteilten Transaktionen.  
  
     Die neue DLL wird geladen, wenn eine erweiterte Prozedur in „sqljdbc_xa.dll“ aufgerufen wird. Sie müssen nicht neu starten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] erforderlichen neuen Definitionen zu laden.  
  
### <a name="configuring-the-user-defined-roles"></a>Konfigurieren der benutzerdefinierten Rollen  
 Um einem bestimmten Benutzer die Berechtigungen für die Teilnahme an verteilten Transaktionen mit dem JDBC-Treiber zu gewähren, fügen Sie den Benutzer der Rolle "SqlJDBCXAUser" hinzu. Verwenden Sie z. B. die folgende [!INCLUDE[tsql](../../includes/tsql_md.md)] Code die Rolle "SqlJDBCXAUser" einen Benutzer mit dem Namen 'Shelby' (SQL-Standardanmeldename-Benutzer mit dem Namen 'Shelby') hinzu:  
  
```  
USE master  
GO  
EXEC sp_grantdbaccess 'shelby', 'shelby'  
GO  
EXEC sp_addrolemember [SqlJDBCXAUser], 'shelby'  
```  
  
 Benutzerdefinierte SQL-Rollen werden jeweils für eine Datenbank definiert. Wenn Sie aus Sicherheitsgründen eigene Rollen erstellen möchten, müssen Sie die Rolle in jeder Datenbank definieren und die Benutzer den jeweiligen Datenbanken hinzufügen. Die Rolle "SqlJDBCXAUser" ist ausschließlich in der Masterdatenbank definiert, da damit Zugriff auf die erweiterten gespeicherten SQL JDBC-Prozeduren gewährt wird, die sich in der Masterdatenbank befinden. Sie müssen den einzelnen Benutzern zuerst Zugriff auf die Masterdatenbank und dann auf die Rolle "SqlJDBCXAUser" gewähren. Dazu müssen Sie bei der Masterdatenbank angemeldet sein.  
  
## <a name="example"></a>Beispiel  
  
```  
import java.net.Inet4Address;  
import java.sql.*;  
import java.util.Random;  
import javax.transaction.xa.*;  
import javax.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  
  
public class testXA {  
  
   public static void main(String[] args) throws Exception {  
  
      // Create variables for the connection string.  
      String prefix = "jdbc:sqlserver://";  
      String serverName = "localhost";  
      int portNumber = 1433;  
      String databaseName = "AdventureWorks";   
      String user = "UserName";   
      String password = "*****";  
      String connectionUrl = prefix + serverName + ":" + portNumber  
         + ";databaseName=" + databaseName + ";user=" + user + ";password=" + password;  
  
      try {  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         Connection con = DriverManager.getConnection(connectionUrl);  
  
         // Create a test table.  
         Statement stmt = con.createStatement();  
         try {  
            stmt.executeUpdate("DROP TABLE XAMin");   
         }  
         catch (Exception e) {  
         }  
         stmt.executeUpdate("CREATE TABLE XAMin (f1 int, f2 varchar(max))");  
         stmt.close();  
         con.close();  
  
         // Create the XA data source and XA ready connection.  
         SQLServerXADataSource ds = new SQLServerXADataSource();  
         ds.setUser(user);  
         ds.setPassword(password);  
         ds.setServerName(serverName);  
         ds.setPortNumber(portNumber);  
         ds.setDatabaseName(databaseName);  
         XAConnection xaCon = ds.getXAConnection();  
         con = xaCon.getConnection();  
  
         // Get a unique Xid object for testing.  
         XAResource xaRes = null;  
         Xid xid = null;  
         xid = XidImpl.getUniqueXid(1);  
  
         // Get the XAResource object and set the timeout value.  
         xaRes = xaCon.getXAResource();  
         xaRes.setTransactionTimeout(0);  
  
         // Perform the XA transaction.  
         System.out.println("Write -> xid = " + xid.toString());  
         xaRes.start(xid,XAResource.TMNOFLAGS);  
         PreparedStatement pstmt =   
         con.prepareStatement("INSERT INTO XAMin (f1,f2) VALUES (?, ?)");  
         pstmt.setInt(1,1);  
         pstmt.setString(2,xid.toString());  
         pstmt.executeUpdate();  
  
         // Commit the transaction.  
         xaRes.end(xid,XAResource.TMSUCCESS);  
         xaRes.commit(xid,true);  
  
         // Cleanup.  
         con.close();  
         xaCon.close();  
  
         // Open a new connection and read back the record to verify that it worked.  
         con = DriverManager.getConnection(connectionUrl);  
         ResultSet rs = con.createStatement().executeQuery("SELECT * FROM XAMin");  
         rs.next();  
         System.out.println("Read -> xid = " + rs.getString(2));  
         rs.close();  
         con.close();  
      }   
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
  
class XidImpl implements Xid {  
  
   public int formatId;  
   public byte[] gtrid;  
   public byte[] bqual;  
   public byte[] getGlobalTransactionId() {return gtrid;}  
   public byte[] getBranchQualifier() {return bqual;}  
   public int getFormatId() {return formatId;}  
  
   XidImpl(int formatId, byte[] gtrid, byte[] bqual) {  
      this.formatId = formatId;  
      this.gtrid = gtrid;  
      this.bqual = bqual;  
   }  
  
   public String toString() {  
      int hexVal;  
      StringBuffer sb = new StringBuffer(512);  
      sb.append("formatId=" + formatId);  
      sb.append(" gtrid(" + gtrid.length + ")={0x");  
      for (int i=0; i<gtrid.length; i++) {  
         hexVal = gtrid[i]&0xFF;  
         if ( hexVal < 0x10 )  
            sb.append("0" + Integer.toHexString(gtrid[i]&0xFF));  
         else  
            sb.append(Integer.toHexString(gtrid[i]&0xFF));  
         }  
         sb.append("} bqual(" + bqual.length + ")={0x");  
         for (int i=0; i<bqual.length; i++) {  
            hexVal = bqual[i]&0xFF;  
            if ( hexVal < 0x10 )  
               sb.append("0" + Integer.toHexString(bqual[i]&0xFF));  
            else  
               sb.append(Integer.toHexString(bqual[i]&0xFF));  
         }  
         sb.append("}");  
         return sb.toString();  
      }  
  
      // Returns a globally unique transaction id.  
      static byte [] localIP = null;  
      static int txnUniqueID = 0;  
      static Xid getUniqueXid(int tid) {  
  
      Random rnd = new Random(System.currentTimeMillis());  
      txnUniqueID++;  
      int txnUID = txnUniqueID;  
      int tidID = tid;  
      int randID = rnd.nextInt();  
      byte[] gtrid = new byte[64];  
      byte[] bqual = new byte[64];  
      if ( null == localIP) {  
         try {  
            localIP = Inet4Address.getLocalHost().getAddress();  
         }  
         catch ( Exception ex ) {  
            localIP =  new byte[] { 0x01,0x02,0x03,0x04 };  
         }  
      }  
      System.arraycopy(localIP,0,gtrid,0,4);  
      System.arraycopy(localIP,0,bqual,0,4);  
  
      // Bytes 4 -> 7 - unique transaction id.  
      // Bytes 8 ->11 - thread id.  
      // Bytes 12->15 - random number generated by using seed from current time in milliseconds.  
      for (int i=0; i<=3; i++) {  
         gtrid[i+4] = (byte)(txnUID%0x100);  
         bqual[i+4] = (byte)(txnUID%0x100);  
         txnUID >>= 8;  
         gtrid[i+8] = (byte)(tidID%0x100);  
         bqual[i+8] = (byte)(tidID%0x100);  
         tidID >>= 8;  
         gtrid[i+12] = (byte)(randID%0x100);  
         bqual[i+12] = (byte)(randID%0x100);  
         randID >>= 8;  
      }  
      return new XidImpl(0x1234, gtrid, bqual);  
   }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Transaktionen mit dem JDBC-Treiber](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
