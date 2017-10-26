---
title: Mit dem JDBC-Treiber | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6faaf05b-8b70-4ed2-9b44-eee5897f1cd0
caps.latest.revision: 54
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1a067e98988c59de27e2c6a65775a337d58b23f9
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-the-jdbc-driver"></a>Verwenden des JDBC-Treibers
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Dieser Abschnitt enthält die Schnellstart-Anweisungen zum Herstellen einer einfachen Verbindung mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank mithilfe der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]. Vor dem Verbinden mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] müssen auf dem lokalen Computer oder einem Server installiert werden und der JDBC-Treiber muss auf dem lokalen Computer installiert sein.  
  
## <a name="choosing-the-right-jar-file"></a>Auswählen der richtigen JAR-Datei  
 Die Microsoft JDBC Driver 6.2 für SQL Server bietet **Mssql-Jdbc-6.2.1.jre7.jar**, und **Mssql-Jdbc-6.2.1.jre8.jar** Klassenbibliotheksdateien je nach Ihrer bevorzugten Java-Laufzeit verwendet werden Environment (JRE)-Einstellungen.  
  
  Geben Sie die Microsoft JDBC Driver 6.0 und 4.2 für SQL Server **"sqljdbc41.jar"**, und **"sqljdbc42.jar"** Klassenbibliotheksdateien abhängig von Ihren bevorzugten Einstellungen für Java Runtime Environment (JRE) verwendet werden.  
  
 Der Microsoft JDBC Driver 4.1 für SQL Server bietet die **"sqljdbc41.jar"** klassenbibliothekdatei abhängig von Ihren bevorzugten Einstellungen für Java Runtime Environment (JRE) verwendet werden.  
  
 Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 4.0 bietet **"sqljdbc.jar"** und **"sqljdbc4.jar"** Klassenbibliotheksdateien abhängig von Ihren bevorzugten Einstellungen für Java Runtime Environment (JRE) verwendet werden.  
  
 Ihre Auswahl entscheidet auch über die verfügbaren Funktionen. Weitere Informationen zu der JAR-Datei auswählen, finden Sie unter [Systemanforderungen für JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="setting-the-classpath"></a>Festlegen des Klassenpfads  
 Der JDBC-Treiber ist kein Bestandteil des Java SDK. Wenn Sie sie verwenden möchten, müssen Sie den Klassenpfad eingeschlossen Festlegen der **"sqljdbc.jar"** Datei **"sqljdbc4.jar"** Datei, die **"sqljdbc41.jar"** Datei, oder die ** "sqljdbc42.jar"** Datei. Wenn mit der JDBC-Treiber 6.2, den Klassenpfad so festlegen enthalten die **Mssql-Jdbc-6.2.1.jre7.jar** oder **Mssql-Jdbc-6.2.1.jre8.jar**. Wenn die Angabe des Klassenpfads fehlt, gibt die Anwendung die allgemeine Ausnahme „Klasse nicht gefunden“ aus.  
  
### <a name="for-microsoft-jdbc-driver-62"></a>Für Microsoft JDBC Driver 6.2
 Die **Mssql-Jdbc-6.2.1.jre7.jar** oder **Mssql-Jdbc-6.2.1.jre8.jar** Dateien werden an folgendem Speicherort installiert:  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \mssql-jdbc-6.2.1.jre7.jar 
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \mssql-jdbc-6.2.1.jre8.jar
  
 Für eine Windows-Anwendung wird beispielsweise die folgende CLASSPATH-Anweisung verwendet:  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.2 for SQL Server\sqljdbc_6.2\enu\mssql-jdbc-6.2.1.jre8.jar`  
  
 Für eine Unix-/Linux-Anwendung wird beispielsweise die folgende CLASSPATH-Anweisung verwendet:  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.2/enu/mssql-jdbc-6.2.1.jre8.jar`  
  
 Sie müssen sicherstellen, dass die CLASSPATH-Anweisung nur einen enthält [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], z. B. Mssql-Jdbc-6.2.1.jre7.jar oder Mssql-Jdbc-6.2.1.jre8.jar.  

### <a name="for-microsoft-jdbc-driver-40-41-42-and-60"></a>Für Microsoft JDBC Driver 4.0, 4.1, 4.2 und 6.0
 Die JAR-Datei sqljdbc.jar file, sqljdbc4.jar file, sqljdbc41.jar oder sqljdbc42.jar wird an folgendem Speicherorten installiert.  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \sqljdbc.jar  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \sqljdbc4.jar  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \sqljdbc41.jar  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \sqljdbc42.jar  
  
 Für eine Windows-Anwendung wird beispielsweise die folgende CLASSPATH-Anweisung verwendet:  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.0 for SQL Server\sqljdbc_4.2\enu\sqljdbc42.jar`  
  
 Für eine Unix-/Linux-Anwendung wird beispielsweise die folgende CLASSPATH-Anweisung verwendet:  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_4.2/enu/sqljdbc42.jar`  
  
 Sie müssen sicherstellen, dass die CLASSPATH-Anweisung nur einen enthält [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], z. B. entweder "sqljdbc.jar", "sqljdbc4.jar", "sqljdbc41.jar" oder "sqljdbc42.jar".  
  
> [!NOTE]  
>  Auf Windows-Systemen können Verzeichnisnamen, die länger als die 8.3-Namenskonvention sind, oder Ordnernamen mit Leerzeichen zu Problemen bei Klassenpfaden führen. Wenn Sie ein derartiges Problem vermuten, Sie sollten vorübergehend Verschieben der Datei "sqljdbc.jar", Datei "sqljdbc4.jar" oder "sqljdbc41.jar"-Datei in einem einfachen Namen wie z. B. `C:\Temp`, den Klassenpfad ändern und zu bestimmen, ob das Problem behoben.  
  
### <a name="applications-that-are-run-directly-at-the-command-prompt"></a>Anwendungen, die direkt an der Eingabeaufforderung ausgeführt werden  
 Der Klassenpfad wird im Betriebssystem konfiguriert. Hängen Sie "sqljdbc.jar", "sqljdbc4.jar" oder "sqljdbc41.jar" an den Klassenpfad des Systems an. Alternativ können Sie den Klassenpfad angeben, in der Java-Befehlszeile, die die Anwendung ausgeführt, mithilfe wird der `java -classpath` Option.  
  
### <a name="applications-that-run-in-an-ide"></a>Anwendungen, die in einer IDE ausgeführt werden  
 Jeder IDE-Hersteller verwendet eine andere Methode, um den Klassenpfad in der IDE festzulegen. Es reicht nicht aus, den Klassenpfad lediglich im Betriebssystem festzulegen. Sie müssen "sqljdbc.jar", "sqljdbc4.jar" oder "sqljdbc41.jar" an den IDE-Klassenpfad anhängen.  
  
### <a name="servlets-and-jsps"></a>Servlets und JSPs  
 Servlets und JSPs werden in einem Servlet-/JSP-Modul wie Tomcat ausgeführt. Der Klassenpfad muss wie in der Dokumentation für das Servlet-/JSP-Modul angegeben festgelegt werden. Es reicht nicht aus, den Klassenpfad lediglich im Betriebssystem festzulegen. Einige Servlet-/JSP-Module verfügen über Setupfenster, in denen Sie den Klassenpfad des Moduls festlegen können. In dieser Situation müssen Sie die richtige JAR-Datei für den JDBC-Treiber an den vorhandenen Klassenpfad des Moduls anhängen und das Modul neu starten. In anderen Situationen können Sie den Treiber bereitstellen, indem Sie "sqljdbc.jar", "sqljdbc4.jar" oder "sqljdbc41.jar" bei der Modulinstallation in ein bestimmtes Verzeichnis kopieren, z. B. "lib". Der Klassenpfad für den Modultreiber kann auch in einer modulspezifischen Konfigurationsdatei angegeben werden.  
  
### <a name="enterprise-java-beans"></a>Enterprise Java Beans  
 Enterprise Java Beans (EJB) werden in einem EJB-Container ausgeführt. EJB-Container sind von verschiedenen Herstellern erhältlich. Java-Applets werden in einem Browser ausgeführt, aber von einem Webserver heruntergeladen. Kopieren Sie "sqljdbc.jar", "sqljdbc4.jar" oder "sqljdbc41.jar" in das Stammverzeichnis des Webservers, und geben Sie den Namen der JAR-Datei in das HTML-archivregisterkarte des Applets an, z. B. `<applet ... archive=sqljdbc.jar>`.  
  
## <a name="making-a-simple-connection-to-a-database"></a>Herstellen einer einfachen Verbindung mit einer Datenbank  
 Mithilfe der sqljdbc.jar-Klassenbibliothek müssen Anwendungen zuerst den Treiber wie folgt zu registrieren:  
  
 `Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");`  
  
 Wenn der Treiber geladen wurde, können Sie eine Verbindung herstellen, unter Verwendung einer Verbindungs-URL und die GetConnection-Methode der DriverManager-Klasse:  
  
```  
String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
   "databaseName=AdventureWorks;user=MyUserName;password=*****;";  
Connection con = DriverManager.getConnection(connectionUrl);  
```  
  
 In der JDBC API 4.0 wurde die DriverManager.getConnection Methode verbessert, um die JDBC-Treiber automatisch geladen. Daher müssen Anwendungen nicht, rufen Sie die Class.forName-Methode, um zu registrieren, oder Laden Sie den Treiber, bei Verwendung der "sqljdbc4.jar", "sqljdbc41.jar" oder "sqljdbc42.jar"-Klassenbibliothek.  
  
 Wenn die GetConnection-Methode der DriverManager-Klasse aufgerufen wird, ist ein geeigneter Treiber aus der Gruppe der registrierten JDBC-Treiber. Datei "sqljdbc4.jar", "sqljdbc41.jar" oder "sqljdbc42.jar" enthält die Datei "META-INF/services/java.sql.Driver" enthält die **com.microsoft.sqlserver.jdbc.SQLServerDriver** als registrierten Treiber. Vorhandenen Anwendungen, die die Treiber derzeit mit der Methode Class.forName zu laden, werden fortgesetzt, ohne Änderungen.  
  
> [!NOTE]  
>  Die Klassenbibliothek „sqljdbc4.jar“, „sqljdbc41.jar“ oder „sqljdbc42.jar“ kann nicht mit älteren Versionen von Java Runtime Environment (JRE) verwendet werden. Finden Sie unter [Systemanforderungen für JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md) für die Liste der vom unterstützten JRE-Versionen der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 Weitere Informationen zum Herstellen einer Verbindung mit Datenquellen und die Verwendung einer Verbindungs-URL finden Sie unter [der Verbindungs-URL erstellen](../../connect/jdbc/building-the-connection-url.md) und [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über die JDBC-Treiber](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

