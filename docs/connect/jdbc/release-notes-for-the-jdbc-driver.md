---
title: "Versionshinweise für den JDBC-Treiber | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
caps.latest.revision: 206
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd65725237fd625c40f8755e636bb4f6fa2c55ea
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="release-notes-for-the-jdbc-driver"></a>Anmerkungen zu dieser Version für den JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Updates in Microsoft JDBC Driver 6.2 für SQLServer
Die Microsoft JDBC Driver 6.2 für SQL Server ist vollständig kompatibel mit den JDBC-Spezifikationen 4.1 und 4.2. Der Support in 6.0-Paket enthalten sind, werden gemäß Java-Versionskompatibilität benannt. Beispielsweise wird die Mssql-Jdbc-6.2.1.jre8.jar-Datei aus dem Paket 6.2 empfohlen, mit Java 8 verwendet werden soll. 

**Hinweis:** wurde ein Problem mit den Metadaten, die zur Verbesserung der Zwischenspeicherung in der JDBC-6.2 RTW auf 29 Juni 2017 freigegeben gefunden. Wurde ein Rollback für die Verbesserung und neue Support (Version 6.2.1) auf 17 Juli 2017 veröffentlicht wurden, auf die [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460), [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1), und [Maven zentralen](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22). Aktualisieren Sie auf der Projekte zur Verwendung der 6.2.1 Support freizugeben. Lesen Sie bitte die [Anmerkungen zu dieser Version](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) Weitere Details.

**Azure Active Directory (AAD)-Unterstützung für Linux**

Verbinden Sie Ihre Linux-Anwendungen für Azure SQL-Datenbank mithilfe der AAD-Authentifizierung über Benutzername/Kennwort und Sicherheitstoken Zugriffsmethoden.

**Federal Information Processing Standard (FIPS) aktiviert JVMs**

Der JDBC-Treiber kann jetzt auf JVMs verwendet werden, die Ausführung im FIPS 140-Kompatibilitätsmodus federal Standards und Kompatibilität zu erfüllen. 

**Verbesserungen der Kerberos-Authentifizierung** 

Der JDBC-Treiber bietet jetzt Unterstützung für: 
* Prinzipal/Kennwort-Methode für Anwendungen, in denen die Kerberos-Konfiguration geändert oder kann nicht auf ein neues Token oder eine keytab-Datei abgerufen werden kann. Diese Methode kann verwendet werden, für die Authentifizierung mit einem SQL-Server, die nur die Kerberos-Authentifizierung zulässt. 
* Bereichsübergreifende Authentifizierung mithilfe der integrierten Kerberos-Authentifizierung ohne explizit festlegen, dass der Server-SPN. Der Treiber berechnet jetzt automatisch den Bereich, selbst wenn er nicht bereitgestellt wurde.
* Eingeschränkte Kerberos-Delegierung durch das abweisen angenommen Anmeldeinformationen des Benutzers als Anmeldeinformationen GSS-Objekt über die Datenquelle an. Dieser Identitätswechsel-Anmeldeinformationen wird dann zum Herstellen einer Verbindung Kerberos verwendet. 

**Hinzugefügte Timeouts**

Der JDBC-Treiber unterstützt nun die folgenden konfigurierbare Timeouts, die Sie ändern können basierend auf den Anforderungen Ihrer Anwendung: 
* Abfragetimeout zum Steuern der Anzahl von Sekunden wartet, bevor ein Timeout tritt auf, wenn eine Abfrage ausgeführt wird. 
* Sockettimeout, geben Sie die Anzahl der Millisekunden, die gewartet wird, bevor ein Timeout, auf ein Socket auftritt Lese- oder akzeptieren. 

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>Updates in Microsoft JDBC Driver 6.1 für SQLServer

Die Microsoft JDBC Driver 6.1 für SQL Server ist vollständig kompatibel mit den JDBC-Spezifikationen 4.1 und 4.2. Dies ist die erste open-Source-Version des JDBC-Treibers und enthält die Mssql-Jdbc-6.1.0.jre8.jar Mssql-Jdbc-6.1.0.jre7.jar-Dateien, die die Kompatibilität der Java-Version entsprechen. 

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>Updates in Microsoft JDBC Driver 6.0 für SQLServer

Microsoft JDBC Driver 6.0 für SQL Server ist vollständig kompatibel mit den JDBC-Spezifikationen 4.1 und 4.2. Der Support im 6.0 Paket enthaltenen werden nach deren Einhaltung der JDBC-API-Version benannt. Beispielsweise ist die Datei "sqljdbc42.jar" aus dem Paket 6.0 JDBC-API 4.2-kompatibler. Ebenso ist die Datei "sqljdbc41.jar" JDBC-API 4.1 einhalten.

Um sicherzustellen, dass Sie die Rechte "sqljdbc42.jar" oder "sqljdbc41.jar" haben, führen Sie die folgenden Codezeilen. Wenn die Ausgabe "Driver, Version: 6.0.7507.100", Sie verfügen über die JDBC Driver 6.0-Paket.
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```  
 **Always Encrypted**  
  
 Unterstützung für das zuletzt veröffentlichte Always Encrypted-Feature in SQL Server 2016, eine neue Sicherheitsfunktion, die sicherstellt, dass sensible Daten nie als nur-Text in einer SQL Server-Instanz angezeigt werden. Always Encrypted arbeitet mit transparenter Verschlüsselung der Daten in der Anwendung, sodass SQL Server nur die verschlüsselten Daten verarbeitet, aber keine Klartextwerte. Auch wenn die SQL-Instanz oder des Hostcomputers gefährdet ist, erhalten Angreifer lediglich Chiffretext sensibler Daten. Weitere Informationen finden Sie [Using Always Encrypted mit dem JDBC-Treiber](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).  
  
 **Internationaler Domänenname (IDN)**  
  
 Unterstützung für internationale Domänennamen (IDNs) bei Servernamen. Details finden Sie unter Verwendung von internationalen Domänennamen auf die [internationale Features des JDBC-Treibers](../../connect/jdbc/international-features-of-the-jdbc-driver.md) Seite.  
  
 **Parametrisierte Abfrage**  
  
 Jetzt wird das Abrufen von Parametermetadaten mit vorbereiteten Anweisungen für komplexe Abfragen unterstützt, wie etwa Teilabfragen und/oder Joins. Beachten Sie, dass diese Verbesserung nur bei Verwendung von SQL Server 2012 und neueren Versionen verfügbar ist.  
  
 **Azure Active Directory (AAD)**  
  
 AAD-Authentifizierung ist ein Mechanismus für das Herstellen einer Verbindung mit Azure SQL-Datenbank v12 mithilfe von Identitäten in AAD. AAD-Authentifizierung zur zentralen Verwaltung von Identitäten von Datenbankbenutzern und als Alternative zu SQL Server-Authentifizierung verwenden. JDBC Driver 6.0 können Sie Ihre AAD-Anmeldeinformationen in der JDBC-Verbindungszeichenfolge zur Verbindung mit Azure SQL-Datenbank angeben.  Details finden Sie unter der Authentifizierungseigenschaft auf die [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md) Seite.  
  
 **Tabellenwertparameter**  
  
 Tabellenwertparameter bieten eine einfache Möglichkeit, mehrere Datenzeilen aus einer Clientanwendung mit SQL Server zu marshallen, ohne dass mehrere Roundtrips oder spezielle serverseitige Logik für die Verarbeitung der Daten. Tabellenwertparameter können Sie Datenzeilen in einer Clientanwendung zu kapseln und die Daten in einem einzelnen parametrisierten Befehl an den Server gesendet. Die eingehenden Datenzeilen werden in einer Tabellenvariablen gespeichert, die Sie dann auf mithilfe von Transact-SQL bearbeitet werden können. Weitere Informationen finden Sie [Using Table-Valued Parameter](../../connect/jdbc/using-table-valued-parameters.md).  
  
 **AlwaysOn-Verfügbarkeitsgruppen (VG)**  
  
 Der Treiber unterstützt jetzt transparente Verbindungen mit AlwaysOn-Verfügbarkeitsgruppen. Der Treiber ermittelt die aktuellen AlwaysOn-Topologie Ihrer Serverinfrastruktur schnell und transparent eine Verbindung mit dem derzeit aktiven Server her.  
  
## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>Updates in Microsoft JDBC Driver 4.2 für SQL Server und höheren Versionen  
Der Microsoft JDBC Driver 4.2 für SQL Server ist vollständig kompatibel mit den JDBC-Spezifikationen 4.1 und 4.2. Der Support im 4.2 Paket enthaltenen heißen gemäß deren Einhaltung der JDBC-API-Version. Beispielsweise ist die Datei "sqljdbc42.jar" aus dem 4.2-Paket JDBC-API 4.2-kompatibel. Ebenso ist die Datei "sqljdbc41.jar" JDBC-API 4.1 einhalten.

Um sicherzustellen, dass Sie die Rechte "sqljdbc42.jar" oder "sqljdbc41.jar" haben, führen Sie die folgenden Codezeilen. Wenn die Ausgabe "Driver, Version: 4.2.6420.100", Sie verfügen über die JDBC Driver 4.2-Paket.
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```
 **Unterstützung für JDK 8**  
  
 Unterstützung für Java Development Kit (JDK) Version 8.0, zusätzlich zu JDK 7.0, 6.0 und 5.0.  
  
 **JDBC 4.1 und 4.2-Kompatibilität**  
  
 Unterstützung für die Java Database Connectivity-API-Spezifikationen 4.1 und 4.2, zusätzlich zu 4.0. Weitere Informationen finden Sie [JDBC 4.1-Kompatibilität für JDBC Driver](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) und [JDBC 4.2-Kompatibilität für JDBC Driver](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).  
  
 **Massenkopieren**  
  
 Die Massenkopierfunktion wird verwendet, um schnell große Datenmengen in Tabellen oder Ansichten in SQL Server-Datenbanken zu kopieren. Weitere Informationen finden Sie [Verwenden von Massenkopieren mit dem JDBC-Treiber](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).  
  
 **Rollbackoption für XA-Transaktion**  
  
 Es wurden neue Timeoutoptionen für das vorhandene automatische Rollback nicht vorbereiteter Transaktionen hinzugefügt. Einzelheiten finden Sie in [XA-Transaktionen](../../connect/jdbc/understanding-xa-transactions.md).  
  
 **Neue Kerberos-Prinzipalverbindungseigenschaft**  
  
 Es wurde eine neue Verbindungseigenschaft hinzugefügt, um mehr Flexibilität für Kerberos-Verbindungen zu ermöglichen. Einzelheiten finden Sie in [mithilfe von integrierten Kerberos-Authentifizierung zum Herstellen einer Verbindung mit SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md).  
  
## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>Updates in Microsoft JDBC Driver 4.1 für SQL Server und höheren Versionen  
 **Unterstützung für JDK 7**  
  
 Unterstützung für Java Development Kit (JDK), Version 7.0, zusätzlich zu JDK 6.0 und 5.0.  
  
## <a name="updates-in-microsoft-jdbc-driver-40-for-sql-server-and-later"></a>Updates in Microsoft JDBC Driver 4.0 für SQL Server und höheren Versionen  
 **Informationen zum Herstellen einer Verbindung mit einer Azure SQL-Datenbank**  
  
 Es gibt ein neues Thema mit Informationen zum Herstellen von Verbindungen mit einer Azure SQL-Datenbank. Finden Sie unter [Herstellen einer Verbindung mit einer Azure SQL-Datenbank](../../connect/jdbc/connecting-to-an-azure-sql-database.md) für Weitere Informationen.  
  
 **Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall**  
  
 Unterstützung für hohe Verfügbarkeit und Verbindungen zur notfallwiederherstellung bei AlwaysOn-Verfügbarkeitsgruppen in [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]. Finden Sie unter [JDBC Driver-Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md) für Weitere Informationen.  
  
 **Verwenden integrierte Kerberos-Authentifizierung zum Verbinden mit SQLServer**  
  
 Unterstützung für integrierte Typ 4 Kerberos-Authentifizierung für Verbindungen von Anwendungen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank. Weitere Informationen finden Sie unter [mithilfe von integrierten Kerberos-Authentifizierung zum Herstellen einer Verbindung mit SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md). (Geben Sie die integrierte Authentifizierung in steht 2-Kerberos [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] -Versionen vor 4.0.)  
  
 **Zugreifen auf Diagnoseinformationen im Protokoll für erweiterte Ereignisse**  
  
 Sie können auf die Informationen in den erweiterten Ereignisprotokollen des Servers zugreifen, um die Ursachen von Verbindungsfehlern zu bestimmen. Weitere Informationen finden Sie unter [Zugriff auf Diagnoseinformationen im Protokoll für erweiterte Ereignisse](../../connect/jdbc/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
 **Zusätzliche Unterstützung für Spalten mit geringer Dichte**  
  
 Wenn Ihre Anwendung bereits auf Daten in einer Tabelle zugreift, die Daten mit geringer Dichte verwendet, sollten Sie einen Leistungszuwachs feststellen können. Sie erhalten Informationen über Spalten (einschließlich Informationen zu Spalten mit geringer Dichte) mit [GetColumns-Methode &#40; SQLServerDatabaseMetaData &#41; ](../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md). Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Spalten mit geringer Dichte, finden Sie unter [Spalten mit geringer Dichte verwenden](http://go.microsoft.com/fwlink/?LinkId=224244).  
  
 **Xid.getFormatId**  
  
 Ab [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], übergibt der JDBC-Treiber die Format-ID aus der Anwendung mit dem Datenbankserver her. Um das aktualisierte Verhalten nutzen zu können, stellen Sie sicher, dass ein Update von „sqljdbc_xa.dll“ auf dem Server ausgeführt wird. Weitere Informationen zum Kopieren von einer aktualisierten Version von "sqljdbc_xa.dll" auf dem Server finden Sie unter [XA-Transaktionen](../../connect/jdbc/understanding-xa-transactions.md).  
  
## <a name="itanium-not-supported-for-jdbc-driver-60-42-41-and-40-applications"></a>Keine Itanium-Unterstützung für JDBC Driver 6.0, 4.2, 4.1 und 4.0-Anwendungen  
  
 Microsoft JDBC Drivers 6.0, 4.2, 4.1 und 4.0 für SQL Server-Anwendungen werden nicht unterstützt, um auf einem Itanium-Computer ausführen.  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über die JDBC-Treiber](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

