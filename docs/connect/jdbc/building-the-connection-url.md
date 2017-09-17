---
title: Die Verbindungs-URL erstellen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 44996746-d373-4f59-9863-a8a20bb8024a
caps.latest.revision: 53
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b5707221b51bff301aa5e9214497ba9090750aae
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="building-the-connection-url"></a>Erstellen der Verbindungs-URL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die allgemeine Form der Verbindungs-URL lautet:  
  
 `jdbc:sqlserver://[serverName[\instanceName][:portNumber]][;property=value[;property=value]]`  
  
 Dabei gilt:  
  
-   **SQLServer: / /** (erforderlich) als subprotokoll bezeichnet wird und konstant ist.  
  
-   **ServerName** (Optional) ist die Adresse des Servers für die Verbindung. Dabei kann es sich um eine DNS- oder IP-Adresse bzw. "localhost" oder "127.0.0.1" für den lokalen Computer handeln. Wenn der Servername nicht in der Verbindungs-URL angegeben wird, muss er in der properties-Auflistung angegeben werden.  
  
-   **InstanceName** (Optional) ist die Instanz für die Verbindung auf ServerName. Ohne Angabe wird eine Verbindung zur Standardinstanz erstellt.  
  
-   **PortNumber** (Optional) ist der Port für die Verbindung auf ServerName. Der Standardwert ist "1433". Bei Verwendung des Standardwerts müssen der Port und der vorangestellte Doppelpunkt (":") in der URL nicht angegeben werden.  
  
    > [!NOTE]  
    >  Um eine optimale Leistung der Verbindung zu gewährleisten, sollten Sie "portNumber" festlegen, wenn Sie eine Verbindung zu einer benannten Instanz herstellen. Dadurch werden Roundtrips zum Server vermieden, um die Portnummer zu ermitteln. Wenn "portNumber" und "instanceName" verwendet werden, hat "portNumber" Vorrang und "instanceName" wird ignoriert.  
  
-   **Eigenschaft** (Optional) ist mindestens eine optionale Verbindungseigenschaft. Weitere Informationen finden Sie unter [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md). Sie können eine beliebige Eigenschaft aus der Liste angeben. Mehrere Eigenschaften müssen durch ein Semikolon (';') getrennt werden und dürfen nicht doppelt vorkommen.  
  
> [!CAUTION]  
>  Aus Sicherheitsgründen sollten Sie es vermeiden, die Verbindungs-URLs basierend auf Benutzereingaben zu erstellen. Sie sollten in der URL lediglich Servername und Treiber angeben. Verwenden Sie für Werte von Benutzernamen und Kennwörtern die properties-Auflistungen für Verbindungen. Weitere Informationen zur Sicherheit in JDBC-Anwendungen finden Sie unter [Sichern von JDBC-Treiberanwendungen](../../connect/jdbc/securing-jdbc-driver-applications.md).  
  
## <a name="connection-examples"></a>Verbindungsbeispiele  
 Herstellen einer Verbindung zur Standarddatenbank auf dem lokalen Computer mit Benutzername und Kennwort:  
  
 `jdbc:sqlserver://localhost;user=MyUserName;password=*****;`  
  
> [!NOTE]  
>  Obwohl im vorherigen Beispiel in der Verbindungszeichenfolge ein Benutzername und ein Kennwort verwendet wurden, sollten Sie aufgrund der höheren Sicherheit die integrierte Sicherheit verwenden. Weitere Informationen finden Sie unter der [Herstellen einer Verbindung mit integrierter Authentifizierung](#Connectingintegrated) weiter unten in diesem Thema.  
  
 Die folgende Verbindungszeichenfolge veranschaulicht, Herstellen einer Verbindung mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank über die integrierte Authentifizierung und Kerberos aus einer Anwendung, die auf alle vom unterstützten Betriebssystem ausgeführt wird die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]:  
  
```  
jdbc:sqlserver://;servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos  
```  
  
 Herstellen einer Verbindung zur Standarddatenbank auf dem lokalen Computer mit integrierter Authentifizierung:  
  
 `jdbc:sqlserver://localhost;integratedSecurity=true;`  
  
 Herstellen einer Verbindung zu einer benannten Datenbank auf einem Remoteserver:  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 Herstellen einer Verbindung zum Standardport auf dem Remoteserver:  
  
 `jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 Herstellen einer Verbindung mit Angabe eines angepassten Anwendungsnamens:  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;applicationName=MyApp;`  
  
## <a name="named-and-multiple-sql-server-instances"></a>Benannte und mehrere SQL Server-Instanzen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]lässt die Installation mehrerer Datenbankinstanzen Server. Jede Instanz wird durch einen bestimmten Namen gekennzeichnet. Verbindung mit einer benannten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], können Sie entweder die Portnummer der benannten Instanz (bevorzugt) angeben, oder Sie können den Instanznamen als JDBC-URL-Eigenschaft angeben oder ein **Datasource** Eigenschaft. Wenn keine Eigenschaft für Instanzname oder Portnummer angegeben wurde, wird eine Verbindung zur Standardinstanz erstellt. Vergleichen Sie die folgenden Beispiele:  
  
 Gehen Sie folgendermaßen vor, wenn eine Portnummer verwendet werden soll:  
  
 `jdbc:sqlserver://localhost:1433;integratedSecurity=true;<more properties as required>;`  
  
 Gehen Sie folgendermaßen vor, wenn eine JDBC-URL-Eigenschaft verwendet werden soll:  
  
 `jdbc:sqlserver://localhost;instanceName=instance1;integratedSecurity=true;<more properties as required>;`  
  
## <a name="escaping-values-in-the-connection-url"></a>Maskieren von Werten in der Verbindungs-URL  
 Eventuell müssen Sie bestimmte Teile von Werten der Verbindungs-URL aufgrund enthaltener Sonderzeichen wie Leerzeichen, Semikolons und Anführungszeichen maskieren. Der JDBC-Treiber unterstützt die Maskierung dieser Zeichen, indem sie in geschweifte Klammern gesetzt werden. So maskiert {;} beispielsweise ein Semikolon.  
  
 Maskierte Werte können Sonderzeichen enthalten (insbesondere '=', ';', '[]' und Leerzeichen), dürfen aber keine geschweiften Klammern enthalten. Werte, die maskiert werden müssen und geschweifte Klammern enthalten, müssen zu einer properties-Auflistung hinzugefügt werden.  
  
> [!NOTE]  
>  Leerräume innerhalb der Klammern sind literal und werden nicht gekürzt.  
  
##  <a name="Connectingintegrated"></a>Herstellen einer Verbindung mit integrierter Authentifizierung unter Windows  
 Der JDBC-Treiber unterstützt über die integratedSecurity-Verbindungszeichenfolgeneigenschaft die Verwendung der integrierten Authentifizierung vom Typ 2 auf Windows-Betriebssystemen. Wenn Sie die integrierte Authentifizierung verwenden möchten, müssen Sie die Datei „sqljdbc_auth.dll“ in ein Verzeichnis im Windows-Systempfad des Computers kopieren, auf dem der JDBC-Treiber installiert ist.  
  
 Die „sqljdbc_auth.dll“-Dateien werden im folgenden Pfad installiert:  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \auth\  
  
 Für alle vom unterstützten Betriebssystem die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], finden Sie unter [mithilfe von integrierten Kerberos-Authentifizierung zum Herstellen einer Verbindung mit SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) eine Beschreibung einer eingeführten Funktion [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] , mit dessen Hilfe einer Anwendung für die Verbindung ein die Datenbank mithilfe der integrierten Authentifizierung mit Kerberos-Typ 4.  
  
> [!NOTE]  
>  Wenn Sie eine 32-Bit-JVM (Java Virtual Machine) ausführen, verwenden Sie die Datei „sqljdbc_auth.dll“ im Ordner „x86“, auch wenn es sich bei dem Betriebssystem um die x64-Version handelt. Wenn Sie eine 64-Bit-JVM mit einem x64-Prozessor ausführen, verwenden Sie die Datei „sqljdbc_auth.dll“ im Ordner „x64“.  
  
 Alternativ können Sie mit der java.libary.path-Systemeigenschaft das Verzeichnis von „sqljdbc_auth.dll“ angeben. Wenn der JDBC-Treiber beispielsweise im Standardverzeichnis installiert ist, können Sie den Speicherort der DLL beim Start der Java-Anwendung mit dem folgenden VM-Argument (Virtual Machine) angeben:  
  
 `-Djava.library.path=C:\Microsoft JDBC Driver 4.0 for SQL Server\sqljdbc_<version>\enu\auth\x86`  
  
## <a name="connecting-with-ipv6-addresses"></a>Herstellen von Verbindungen mit IPv6-Adressen  
 Der JDBC-Treiber unterstützt die Verwendung von IPv6-Adressen in der properties-Auflistung der Verbindung und in der serverName-Eigenschaft der Verbindungszeichenfolge. Der ursprüngliche ServerName-Wert, z. B. Jdbc:*Sqlserver*://*ServerName*, wird für IPv6-Adressen in Verbindungszeichenfolgen nicht unterstützt. Verwenden einen Namen für *ServerName* anstatt einer IPv6-Adresse wird in jedem Fall in der Verbindung arbeiten. Die folgenden Beispiele enthalten weitere Informationen.  
  
 **Verwenden Sie die ServerName-Eigenschaft**  
  
 `jdbc:sqlserver://;serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1;integratedSecurity=true;`  
  
 **Verwenden Sie die Properties-Auflistung**  
  
 `Properties pro = new Properties();`  
  
 `pro.setProperty("serverName", "serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1");`  
  
 `Connection con = DriverManager.getConnection("jdbc:sqlserver://;integratedSecurity=true;", pro);`  
  
## <a name="see-also"></a>Siehe auch  
 [Herstellen einer Verbindung mit SQLServer mit der JDBC-Treiber](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
