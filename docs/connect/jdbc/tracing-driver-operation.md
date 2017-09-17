---
title: "Ablaufverfolgung für Treibervorgänge | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 723aeae7-6504-4585-ba8b-3525115bea8b
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e364f990cc2428d771f3bc57015df0636e23fbfb
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="tracing-driver-operation"></a>Ablaufverfolgung für Treibervorgänge
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] unterstützt die Verwendung der Ablaufverfolgung (oder Protokollierung), um Informationen zum Beheben von Problemen mit der JDBC-Treiber, wenn er in der Anwendung verwendet wird. Um die Verwendung der Ablaufverfolgung zu aktivieren, verwendet der JDBC-Treiber die protokollierungs-APIs in "java.util.Logging", die eine Reihe von Klassen zum Erstellen von Objekten für Protokollierung und LogRecord bereitstellt.  
  
> [!NOTE]  
>  Für die im JDBC-Treiber enthaltene systemeigene Komponente ("sqljdbc_xa.dll") wird die Ablaufverfolgung durch das BID-Framework (Built-In Diagnostics) ermöglicht. Informationen zu BID finden Sie unter [Data Access Tracing in SQL Server](http://go.microsoft.com/fwlink/?LinkId=70042).  
  
 Wenn Sie Ihre Anwendung entwickeln, können Sie Protokollierung-Objekte aufrufen, machen wiederum erstellen LogRecord-Objekte, die dann für von ereignishandlerobjekten für übergeben werden verarbeitet. Protokollierung und Handler Objekten beide Protokollierungsstufen, und optional Protokollierungsfilter, um zu bestimmen, welche LogRecords verarbeitet werden. Wenn die Protokollierung Vorgänge abgeschlossen sind, können Handlerobjekte Formatierer Objekte optional verwenden, um die Protokollinformationen zu veröffentlichen.  
  
 Standardmäßig erfolgt die Ausgabe des java.util.logging-Frameworks in eine Datei. Diese Ausgabeprotokolldatei muss Schreibberechtigungen für den Kontext aufweisen, unter dem der JDBC-Treiber ausgeführt wird.  
  
> [!NOTE]  
>  Weitere Informationen zur Verwendung der verschiedenen Protokollierungsobjekte für die Programmablaufverfolgung finden Sie unter Java Logging APIs auf der Sun Microsystems-Website.  
  
 Die folgenden Abschnitte beschreiben die Protokolliergrade sowie die protokollierbaren Kategorien und enthalten Informationen darüber, wie die Ablaufverfolgung in der Anwendung aktiviert werden kann.  
  
## <a name="logging-levels"></a>Protokolliergrade  
 Jeder erstellten Protokollmeldung ist ein Protokolliergrad zugeordnet. Der Protokolliergrad bestimmt die Wichtigkeit der protokollmeldung, die durch festgelegt sind die **Ebene** Klasse in "java.util.Logging". Durch Aktivieren der Protokollierung für einen bestimmten Grad wird auch das Protokollieren für alle höheren Grade aktiviert. In diesem Abschnitt werden die Protokolliergrade für öffentliche und interne Protokollierungskategorien beschrieben. Weitere Informationen zu den Protokollierungskategorien finden Sie in diesem Thema im Abschnitt "Protokollierungskategorien".  
  
 Die verfügbaren Protokolliergrade für öffentliche Protokollierungskategorien werden in der folgenden Tabelle beschrieben:  
  
|Name|Description|  
|----------|-----------------|  
|SEVERE|Der höchste Protokolliergrad, der schwerwiegende Fehler kennzeichnet. Im JDBC-Treiber wird dieser Grad für Fehler und Ausnahmen verwendet.|  
|WARNING|Kennzeichnet ein mögliches Problem.|  
|INFO|Stellt informative Meldungen bereit.|  
|CONFIG|Stellt Konfigurationsmeldungen bereit. Beachten Sie, dass der JDBC-Treiber derzeit keine Konfigurationsmeldungen bereitstellt.|  
|FINE|Stellt grundlegende Ablaufverfolgungsinformationen einschließlich aller von den öffentlichen Methoden ausgelösten Ausnahmen bereit.|  
|FINER|Stellt ausführliche Ablaufverfolgungsinformationen einschließlich aller Ein- und Ausstiegspunkte von öffentlichen Methoden mit den zugeordneten Parameterdatentypen und allen öffentlichen Eigenschaften für öffentliche Klassen bereit. Darüber hinaus geben Sie Parameter, Ausgabeparameter und Methodenrückgabewerte mit Ausnahme von CLOB, BLOB, NCLOB, Reader \<Stream > Werttypen zurück.|  
|FINEST|Stellt sehr ausführliche Ablaufverfolgungsinformationen bereit. Dieser Grad ist der niedrigste Protokolliergrad.|  
|OFF|Schaltet die Protokollierung aus.|  
|ALL|Aktiviert die Protokollierung aller Meldungen.|  
  
 Die verfügbaren Protokolliergrade für interne Protokollierungskategorien werden in der folgenden Tabelle beschrieben:  
  
|Name|Description|  
|----------|-----------------|  
|SEVERE|Der höchste Protokolliergrad, der schwerwiegende Fehler kennzeichnet. Im JDBC-Treiber wird dieser Grad für Fehler und Ausnahmen verwendet.|  
|WARNING|Kennzeichnet ein mögliches Problem.|  
|INFO|Stellt informative Meldungen bereit.|  
|FINE|Stellt Ablaufverfolgungsinformationen einschließlich grundlegender Informationen zum Erstellen und Löschen von Objekten. Außerdem alle von den öffentlichen Methoden ausgelösten Ausnahmen.|  
|FINER|Stellt ausführliche Ablaufverfolgungsinformationen einschließlich aller Ein- und Ausstiegspunkte von öffentlichen Methoden mit den zugeordneten Parameterdatentypen und allen öffentlichen Eigenschaften für öffentliche Klassen bereit. Darüber hinaus geben Sie Parameter, Ausgabeparameter und Methodenrückgabewerte mit Ausnahme von CLOB, BLOB, NCLOB, Reader \<Stream > Werttypen zurück.<br /><br /> Die folgenden Protokollierungskategorien vorhanden, die in Version 1.2 von JDBC Driver war und hatte den Protokolliergrad Fine aufweisen: [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md), [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), XA und [SQLServerDataSource ](../../connect/jdbc/reference/sqlserverdatasource-class.md). Diese wurden ab Version 2.0 auf den Grad FINER hochgestuft.|  
|FINEST|Stellt sehr ausführliche Ablaufverfolgungsinformationen bereit. Dieser Grad ist der niedrigste Protokolliergrad.<br /><br /> In Version 1.2 von JDBC Driver waren die folgenden Protokollierungskategorien vorhanden, die auch den Protokolliergrad FINEST aufweisen: TDS.DATA und TDS.TOKEN. Diese behalten ab Version 2.0 den Protokolliergrad FINEST bei.|  
|OFF|Schaltet die Protokollierung aus.|  
|ALL|Aktiviert die Protokollierung aller Meldungen.|  
  
## <a name="logging-categories"></a>Protokollierungskategorien  
 Wenn Sie ein Protokollierungsobjekt erstellen, müssen Sie dem Objekt anweisen, die benannte Entität oder Kategorie an, die Sie Protokollinformationen aus einer interessiert sind. Der JDBC-Treiber unterstützt die folgenden öffentlichen Protokollierungskategorien, die alle im com.microsoft.sqlserver.jdbc-Treiberpaket definiert sind.  
  
|Name|Description|  
|----------|-----------------|  
|Verbindung|Protokolliert Meldungen in die [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINER festlegen.|  
|-Anweisung.|Protokolliert Meldungen in die [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINER festlegen.|  
|DataSource|Protokolliert Meldungen in die [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINE festlegen.|  
|ResultSet|Protokolliert Meldungen in die [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINER festlegen.|  
|Treiber|Protokolliert Meldungen in die [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINER festlegen.|  
  
 Ab Version 2.0 von Microsoft JDBC Driver stellt der Treiber auch das com.microsoft.sqlserver.jdbc.internals-Paket bereit, das die Protokollierungsunterstützung für die folgenden internen Protokollierungskategorien enthält.  
  
|Name|Description|  
|----------|-----------------|  
|AuthenticationJNI|Protokolliert Meldungen zu den Windows-integriert Authentifizierungsprobleme (wenn die **AuthenticationScheme** -Verbindungseigenschaft implizit oder explizit festgelegt ist **NativeAuthentication**).<br /><br /> Die Anwendungen können den Protokolliergrad auf FINER und FINE festlegen.|  
|SQLServerConnection|Protokolliert Meldungen in die [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINE und FINER festlegen.|  
|SQLServerDataSource|Protokolliert Meldungen in die [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md), [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md), und [SQLServerPooledConnection](../../connect/jdbc/reference/sqlserverpooledconnection-class.md) Klassen.<br /><br /> Die Anwendungen können den Protokolliergrad auf FINER festlegen.|  
|InputStream|Protokolliert Meldungen zu den folgenden Datentypen: java.io.InputStream, java.io.Reader und Datentypen mit einem max-Spezifizierer wie die Datentypen varchar, nvarchar und varbinary.<br /><br /> Die Anwendungen können den Protokolliergrad auf FINER festlegen.|  
|SQLServerException|Protokolliert Meldungen in die [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINE festlegen.|  
|SQLServerResultSet|Protokolliert Meldungen in die [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINE, FINER und FINEST festlegen.|  
|SQLServerStatement|Protokolliert Meldungen in die [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINE, FINER und FINEST festlegen.|  
|XA|Protokolliert Meldungen für alle XA-Transaktionen in der [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINE und FINER festlegen.|  
|KerbAuthentication|Protokolliert Meldungen zur Kerberos-Authentifizierung Typ 4 (wenn die **AuthenticationScheme** Connection-Eigenschaft wird festgelegt, um **Java Kerberos**). Für die Anwendung kann der Protokolliergrad auf FINE oder FINER festgelegt werden.|  
|TDS.DATA|Protokolliert Meldungen, die Konversationen auf TDS-Protokollebene zwischen Treiber und SQL Server enthalten. Die ausführlichen Inhalte jedes gesendeten und empfangenen TDS-Pakets werden in ASCII und hexadezimal protokolliert. Die Anmeldeinformationen (Benutzernamen und Kennwörter) werden nicht protokolliert. Alle sonstigen Daten werden protokolliert.<br /><br /> Diese Kategorie erstellt sehr ausführliche Meldungen. Sie kann nur aktiviert werden, indem der Protokolliergrad auf FINEST festgelegt wird.|  
|TDS.Channel|Diese Kategorie verfolgt Aktionen der TCP-Kommunikationskanäle mit SQL Server. Die protokollierten Meldungen umfassen das Öffnen und Schließen von Sockets sowie Lese- und Schreibvorgänge. Außerdem werden Meldungen zum Herstellen einer SSL (Secure Sockets Layer)-Verbindung mit SQL Server verfolgt.<br /><br /> Diese Kategorie kann nur aktiviert werden, indem der Protokolliergrad auf FINE, FINER oder FINEST festgelegt wird.|  
|TDS.Writer|Diese Kategorie verfolgt Schreibvorgänge für den TDS-Kanal. Beachten Sie, dass nur die Länge der Schreibvorgänge verfolgt wird, nicht deren Inhalt. Diese Kategorie verfolgt außerdem Probleme, wenn zum Abbrechen der Ausführung einer Anweisung ein Achtungssignal gesendet wird.<br /><br /> Diese Kategorie kann nur aktiviert werden, indem der Protokolliergrad auf FINEST festgelegt wird.|  
|TDS.Reader|Diese Kategorie verfolgt bestimmte Lesevorgänge für den TDS-Kanal mit dem Grad FINEST. Die Nachverfolgung mit dem Grad FINEST ist möglicherweise sehr ausführlich. Mit den Graden WARNING und SEVERE wird in dieser Kategorie verfolgt, wenn der Treiber ein ungültiges TDS-Protokoll von SQL Server empfängt, bevor der Treiber die Verbindung trennt.<br /><br /> Diese Kategorie kann nur aktiviert werden, indem der Protokolliergrad auf FINER und FINEST festgelegt wird.|  
|TDS.Command|Diese Kategorie verfolgt Zustandsübergänge auf niedriger Ebene und sonstige Informationen zur Ausführung von TDS-Befehlen, wie z. B. [!INCLUDE[tsql](../../includes/tsql_md.md)] anweisungsausführungen, ResultSet-Cursorn, Commits und So weiter.<br /><br /> Diese Kategorie kann nur aktiviert werden, indem der Protokolliergrad auf FINEST festgelegt wird.|  
|TDS.TOKEN|Diese Kategorie protokolliert nur die Token im TDS-Paket und ist weniger ausführlich als die TDS.DATA-Kategorie. Sie kann nur aktiviert werden, indem der Protokolliergrad auf FINEST festgelegt wird.<br /><br /> Mit dem Grad FINEST verfolgt diese Kategorie TDS-Token bei der Verarbeitung in der Antwort. Mit dem Grad SEVERE verfolgt diese Kategorie das Auftreten ungültiger TDS-Token.|  
|SQLServerDatabaseMetaData|Protokolliert Meldungen in die [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINE festlegen.|  
|SQLServerResultSetMetaData|Protokolliert Meldungen in die [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINE festlegen.|  
|SQLServerParameterMetaData|Protokolliert Meldungen in die [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINE festlegen.|  
|SQLServerBlob|Protokolliert Meldungen in die [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINE festlegen.|  
|SQLServerClob|Protokolliert Meldungen in die [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINE festlegen.|  
|SQLServerSQLXML|Protokolliert Meldungen in der internen SQLServerSQLXML-Klasse. Die Anwendungen können den Protokolliergrad auf FINE festlegen.|  
|SQLServerDriver|Protokolliert Meldungen in die [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINE festlegen.|  
|SQLServerNClob|Protokolliert Meldungen in die [SQLServerNClob](../../connect/jdbc/reference/sqlservernclob-class.md) Klasse. Die Anwendungen können den Protokolliergrad auf FINE festlegen.|  
  
## <a name="enabling-tracing-programmatically"></a>Programmgesteuerte Aktivierung der Ablaufverfolgung  
 Ablaufverfolgung kann programmgesteuert aktiviert werden, indem ein Protokollierungsobjekt erstellen und angeben, der Kategorie protokolliert werden. Der folgende Code veranschaulicht beispielsweise, wie die Protokollierung für SQL-Anweisungen aktiviert wird:  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.FINER);  
```  
  
 Die Protokollierung können Sie im Code folgendermaßen deaktivieren:  
  
```  
logger.setLevel(Level.OFF);  
```  
  
 Mit dem folgenden Code können Sie alle verfügbaren Kategorien protokollieren:  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc");  
logger.setLevel(Level.FINE);  
```  
  
 Mit dem folgenden Code können Sie die Protokollierung einer bestimmten Kategorie deaktivieren:  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.OFF);  
```  
  
## <a name="enabling-tracing-by-using-the-loggingproperties-file"></a>Aktivieren der Ablaufverfolgung mit der Datei "Logging.Properties"  
 Können Sie auch die Ablaufverfolgung aktivieren, mit der `logging.properties` Datei, die sich in der `lib` Verzeichnis der Java Runtime Environment (JRE)-Installation. In dieser Datei können Sie die Standardwerte für die Protokollierungund Handler festlegen, die bei Aktivierung der Ablaufverfolgung verwendet werden sollen.  
  
 Im folgenden ist ein Beispiel für die Einstellungen, die Sie in vornehmen können die `logging.properties` Dateien:  
  
```  
# Specify the handler, the handlers will be installed during VM startup.  
handlers= java.util.logging.FileHandler  
  
# Default global logging level.  
.level= OFF  
  
# default file output is in user's home directory.  
java.util.logging.FileHandler.pattern = %h/java%u.log  
java.util.logging.FileHandler.limit = 5000000  
java.util.logging.FileHandler.count = 20  
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter  
java.util.logging.FileHandler.level = FINEST  
  
# Facility specific properties.  
com.microsoft.sqlserver.jdbc.level=FINEST  
  
```  
  
> [!NOTE]  
>  Sie können die Eigenschaften festlegen, der `logging.properties` Datei mithilfe des LogManager-Objekts, das Bestandteil von "java.util.Logging" ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Diagnostizieren von Problemen mit dem JDBC-Treiber](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
