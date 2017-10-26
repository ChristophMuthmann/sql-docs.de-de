---
title: Arbeiten mit einer Verbindung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf8ee392-8a10-40a3-ae32-31c7b1efdd04
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 03921ad2e09bb1da941c3570fac0b3d9c6a1ba31
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="working-with-a-connection"></a>Arbeiten mit einer Verbindung
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die folgenden Abschnitte enthalten Beispiele für die verschiedenen Möglichkeiten zum Herstellen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] her, indem die [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse von der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
> [!NOTE]  
>  Wenn Probleme beim Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC-Treiber verwenden, finden Sie unter [Behandlung von Verbindungsproblemen](../../connect/jdbc/troubleshooting-connectivity.md) Vorschläge zum beheben.  
  
## <a name="creating-a-connection-by-using-the-drivermanager-class"></a>Erstellen einer Verbindung mit der DriverManager-Klasse  
 Die einfachste Vorgehensweise zum Erstellen einer Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank ist das Laden des JDBC-Treibers und rufen Sie die GetConnection-Methode der DriverManager-Klasse, wie im folgenden:  
  
```  
Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = DriverManager.getConnection(connectionUrl);  
```  
  
 Bei diesem Verfahren wird eine Datenbankverbindung mit dem ersten verfügbaren Treiber in der Liste der Treiber erstellt, der erfolgreich eine Verbindung mit der angegebenen URL herstellen kann.  
  
> [!NOTE]  
>  Wenn Sie die Klassenbibliothek "sqljdbc4.jar" verwenden zu können, müssen Anwendungen nicht explizit registriert oder Laden Sie den Treiber mit der Class.forName-Methode. Wenn die GetConnection-Methode der DriverManager-Klasse aufgerufen wird, ist ein geeigneter Treiber aus der Gruppe der registrierten JDBC-Treiber. Weitere Informationen finden Sie unter "Verwenden des JDBC-Treibers".  
  
## <a name="creating-a-connection-by-using-the-sqlserverdriver-class"></a>Erstellen einer Verbindung mit der SQLServerDriver-Klasse  
 Wenn Sie einen bestimmten Treiber in der Liste der Treiber für DriverManager angeben müssen, können Sie eine Verbindung mit Datenbank erstellen, indem Sie mit der [verbinden](../../connect/jdbc/reference/connect-method-sqlserverdriver.md) Methode der [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) -Klasse, wie im folgenden:  
  
```  
Driver d = (Driver) Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver").newInstance();  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = d.connect(connectionUrl, new Properties());  
```  
  
## <a name="creating-a-connection-by-using-the-sqlserverdatasource-class"></a>Erstellen einer Verbindung mit der SQLServerDataSource-Klasse  
 Haben, erstellen Sie eine Verbindung mithilfe der [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) -Klasse, können Sie verschiedene festlegungsmethoden der Klasse vor dem Aufrufen der [GetConnection](../../connect/jdbc/reference/getconnection-method.md) Methode, wie im folgenden:  
  
```  
SQLServerDataSource ds = new SQLServerDataSource();  
ds.setUser("MyUserName");  
ds.setPassword("*****");  
ds.setServerName("localhost");  
ds.setPortNumber(1433);   
ds.setDatabaseName("AdventureWorks");  
Connection con = ds.getConnection();  
```  
  
## <a name="creating-a-connection-that-targets-a-very-specific-data-source"></a>Erstellen einer Verbindung mit eine sehr speziellen Datenquelle als Ziel  
 Wenn Sie eine Datenbankverbindung mit einer sehr speziellen Datenquelle herstellen müssen, können Sie mehrere Verfahren verwenden. Das jeweilige Verfahren hängt von den Eigenschaften ab, die Sie mit der Verbindungs-URL festlegen.  
  
 Um eine Verbindung zur Standardinstanz auf einem Remoteserver herzustellen, verwenden Sie die folgende URL:  
  
 `String url = "jdbc:sqlserver://MyServer;integratedSecurity=true;"`  
  
 Um eine Verbindung zu einem bestimmten Port eines Servers herzustellen, verwenden Sie die folgende URL:  
  
 `String url = "jdbc:sqlserver://MyServer:1533;integratedSecurity=true;"`  
  
 Um eine Verbindung zu einer benannten Instanz eines Servers herzustellen, verwenden Sie die folgende URL:  
  
 `String url = "jdbc:sqlserver://209.196.43.19;instanceName=INSTANCE1;integratedSecurity=true;"`  
  
 Um eine Verbindung zu einer bestimmten Datenbank eines Servers herzustellen, verwenden Sie die folgende URL:  
  
 `String url = "jdbc:sqlserver://172.31.255.255;database=AdventureWorks;integratedSecurity=true;"`  
  
 Weitere Beispiele für Verbindungs-URL finden Sie unter [Erstellen der Verbindungs-URL](../../connect/jdbc/building-the-connection-url.md).  
  
## <a name="creating-a-connection-with-a-custom-login-time-out"></a>Erstellen einer Verbindung mit einem benutzerdefinierten Anmeldetimeout  
 Wenn Sie Serverlast oder Netzwerkverkehr berücksichtigen müssen, können Sie eine Verbindung mit einem bestimmten Timeoutwert für die Anmeldung in Sekunden erstellen, wie z. B.:  
  
 `String url = "jdbc:sqlserver://MyServer;loginTimeout=90;integratedSecurity=true;"`  
  
## <a name="create-a-connection-with-application-level-identity"></a>Erstellen einer Verbindung mit Identität auf Anwendungsebene  
 Wenn Sie Protokollierung und Profilerstellung verwenden, müssen Sie die Verbindung mit einer bestimmten Anwendung als Ursprung kennzeichnen, wie z. B.:  
  
 `String url = "jdbc:sqlserver://MyServer;applicationName=MYAPP.EXE;integratedSecurity=true;"`  
  
## <a name="closing-a-connection"></a>Trennen einer Verbindung  
 Sie können eine datenbankverbindung explizit schließen, durch Aufrufen der [schließen](../../connect/jdbc/reference/close-method-sqlserverconnection.md) Methode der SQLServerConnection-Klasse, wie im folgenden:  
  
 `con.close();`  
  
 Dies wird die Datenbankressourcen frei, die das SQLServerConnection-Objekt verwendet wird oder die Verbindung an den Verbindungspool in poolszenarien zurückgegeben.  
  
> [!NOTE]  
>  Aufrufen der close-Methode wird auch alle ausstehenden Transaktionen ein Rollback.  
  
## <a name="see-also"></a>Siehe auch  
 [Herstellen einer Verbindung mit SQLServer mit der JDBC-Treiber](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  

