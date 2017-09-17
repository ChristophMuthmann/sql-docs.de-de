---
title: Verbindung mit SQLServer-Authentifizierung mit Kerberos integriert | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f26a429563aaf5c079c45b064b4723cb19cada90
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>Verwenden der integrierten Kerberos-Authentifizierung für Verbindungen mit SQL Server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ab [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], eine Anwendung kann mithilfe der **AuthenticationScheme** Connection-Eigenschaft, um anzugeben, dass es mit einer Datenbank mithilfe der integrierten Kerberos-Authentifizierung Typ 4 eine Verbindung herstellen möchte. Finden Sie unter [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md) für Weitere Informationen zu Verbindungseigenschaften. Weitere Informationen zu Kerberos finden Sie unter [Microsoft Kerberos](http://go.microsoft.com/fwlink/?LinkID=100758).  
  
 Bei Verwendung der integrierten Authentifizierung mit dem Java- **Krb5LoginModule**, können Sie konfigurieren Sie das Modul mit [Krb5LoginModule-Klasse](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html).  
  
 Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] für Java-VMs von IBM die folgenden Eigenschaften festgelegt:  
  
-   **UseDefaultCcache = "true"**  
  
-   **ModuleBanner = "false"**  
  
 Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] für alle anderen Java-VMs die folgenden Eigenschaften festgelegt:  
  
-   **UseTicketCache = "true"**  
  
-   **DoNotPrompt = "true"**  
  
## <a name="remarks"></a>Hinweise  
 Vor [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], Anwendungen können die integrierte Authentifizierung (Kerberos oder NTLM, je nach Verfügbarkeit) angeben mithilfe der **"IntegratedSecurity"** -Verbindungseigenschaft und durch Verweisen auf ** "sqljdbc_auth.dll"**, wie in beschrieben [Erstellen der Verbindungs-URL](../../connect/jdbc/building-the-connection-url.md).  
  
 Ab [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], eine Anwendung kann mithilfe der **AuthenticationScheme** Connection-Eigenschaft, um anzugeben, dass es mit einer Datenbank mithilfe von Kerberos eine Verbindung herstellen möchte integrierte mit der reinen Java-Kerberos-Authentifizierung Implementierung:  
  
-   Wenn Sie die integrierte Authentifizierung verwenden möchten **Krb5LoginModule**, müssen Sie noch angeben der **"IntegratedSecurity" = "true"** Connection-Eigenschaft. Anschließend würden Sie auch angeben der **AuthenticationScheme = Java Kerberos** Connection-Eigenschaft.  
  
-   Um den Vorgang fortzusetzen, integrierte Authentifizierung mit **"sqljdbc_auth.dll"**, geben Sie einfach **"IntegratedSecurity" = "true"** -Verbindungseigenschaft (und optional **AuthenticationScheme = NativeAuthentication**).  
  
-   Bei Angabe von **AuthenticationScheme = Java Kerberos** jedoch nicht gleichzeitig angeben **"IntegratedSecurity" = "true"**, ignoriert der Treiber die **AuthenticationScheme** Verbindungseigenschaft, und es werden davon ausgegangen, dass Benutzer und Kennwort-Anmeldeinformationen in der Verbindungszeichenfolge angegeben.  
  
 Mit einer Datenquelle, um Verbindungen zu erstellen, können Sie legen Sie das Authentifizierungsschema mit "setauthenticationscheme" programmgesteuert fest und (optional) legen Sie den SPN für Kerberos-Verbindungen mit dem **SetServerSpn**.  
  
 Zur Unterstützung der Kerberos-Authentifizierung wurde eine neue Protokollierung eingeführt: com.microsoft.sqlserver.jdbc.internals.KerbAuthentication. Weitere Informationen finden Sie unter [Ablaufverfolgung für Treibervorgänge](../../connect/jdbc/tracing-driver-operation.md).  
  
 Befolgen Sie beim Konfigurieren von Kerberos die folgenden Richtlinien:  
  
1.  Legen Sie **AllowTgtSessionKey** in der Registrierung für Windows auf 1. Weitere Informationen finden Sie unter [Kerberos-Protokoll-Registrierungseinträge und KDC-Konfigurationsschlüssel in Windows Server 2003](http://support.microsoft.com/kb/837361).  
  
2.  Stellen Sie sicher, dass die Kerberos-Konfiguration (krb5.conf in UNIX-Umgebungen) auf den richtigen Bereich und KDC für Ihre Umgebung zeigt.  
  
3.  Initialisieren Sie den TGT-Cache mit "kinit" oder indem Sie sich bei der Domäne anmelden.  
  
4.  Wenn eine Anwendung, **AuthenticationScheme = Java Kerberos** Betriebssysteme auf dem Windows Vista oder Windows 7 ausgeführt wird, sollten Sie ein Standardbenutzerkonto verwenden. Wenn Sie jedoch die Anwendung unter einem Administratorkonto ausführen, muss sie mit Administratorberechtigungen ausgeführt werden.  
  
> [!NOTE]  
>  Das ServerSpn-Verbindungsattribut wird nur von Microsoft JDBC Drivers 4.2 und höher unterstützt.  
  
## <a name="service-principal-names"></a>Dienstprinzipalnamen  
 Ein Dienstprinzipalname (SPN, Service Principal Name) ist der Name, über den ein Client eine Instanz eines Diensts eindeutig identifiziert.  
  
 Sie können angeben, den SPN mithilfe der **ServerSpn** Connection-Eigenschaft oder einfach den Treiber, die für Sie (Standard) zu erstellen.  Diese Eigenschaft ist in der Form: "MSSQLSvc/fqdn:port@REALM", in dem Fqdn ist der vollständig qualifizierte Domänenname, Port ist die Portnummer und Bereich ist die Kerberos-Bereich des SQL-Servers in Großbuchstaben.  Der Bereichsteil dieser Eigenschaft ist optional, wenn der Standardbereich Ihrer Kerberos-Konfiguration der gleiche Bereich wie der des Servers ist, und wird standardmäßig nicht angegeben.  Wenn Sie ein bereichsübergreifendes Authentifizierungsszenario unterstützen möchten, in dem sich der Standardbereich der Kerberos-Konfiguration vom Bereich des Servers unterscheidet, müssen Sie den SPN mithilfe der Eigenschaft „serverSpn“ angeben.  
  
 Angenommen, Ihr SPN kann folgendermaßen aussehen: "MSSQLSvc/some-server.zzz.corp.contoso.com:1433@ZZZZ.CORP.CONTOSO.COM"  
  
 Weitere Informationen zu Dienstprinzipalnamen (SPNs) finden Sie in folgendem Thema:  
  
-   [Gewusst wie: Verwenden der Kerberos-Authentifizierung in SQL Server](http://support.microsoft.com/kb/319723)  
  
-   [Verwenden Kerberos mit SQLServer](http://go.microsoft.com/fwlink/?LinkId=207814)  

> [!NOTE]  
> Bevor 6.2.0 des JDBC-Treibers für die richtige Verwendung von Cross Realm Kerberos, Version müssen Sie explizit festlegen der **ServerSpn**.
>
> Zum Zeitpunkt der 6.2.0 Version der Treiber werden zum Erstellen der **ServerSpn** in der Standardeinstellung, selbst wenn Cross Realm Kerberos verwendet. Obwohl eine verwenden können **ServerSpn** explizit zu. 
  
## <a name="creating-a-login-module-configuration-file"></a>Erstellen einer Anmeldemodul-Konfigurationsdatei  
 Sie können optional eine Kerberos-Konfigurationsdatei angeben. Wenn keine Konfigurationsdatei angegeben wird, gelten die folgenden Einstellungen:  
  
 Sun-JVM  
 com.sun.security.auth.module.Krb5LoginModule erforderlich UseTicketCache = True;  
  
 IBM-JVM  
 com.ibm.security.auth.module.Krb5LoginModule erforderlich UseDefaultCcache = True;  
  
 Wenn Sie selbstständig eine Anmeldemodul-Konfigurationsdatei erstellen, muss die Datei das folgende Format aufweisen:  
  
```  
<name> {  
    <LoginModule> <flag> <LoginModule options>;  
    <optional_additional_LoginModules, flags_and_options>;  
};  
```  
  
 Eine Anmeldemodul-Konfigurationsdatei enthält einen oder mehrere Einträge, die jeweils angeben, welche zugrunde liegende Authentifizierungstechnologie für eine bestimmte Anwendung bzw. für bestimmte Anwendungen verwendet werden soll. Beispiel:  
  
```  
SQLJDBCDriver {  
   com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;  
};  
```  
  
 Jeder Eintrag der Anmeldemodul-Konfigurationsdatei besteht aus einem Namen, auf den ein oder mehrere LoginModule-spezifische Einträge folgen. Jeder LoginModule-spezifische Eintrag wird jeweils durch ein Semikolon abgeschlossen, und die gesamte Gruppe von LoginModule-spezifischen Einträgen wird von geschweiften Klammern umschlossen. Jeder Konfigurationsdateieintrag wird durch ein Semikolon abgeschlossen.  
  
 Für den Treiber kann nicht nur festgelegt werden, dass Kerberos-Anmeldeinformationen mit den Einstellungen in der Anmeldemodul-Konfigurationsdatei erhalten werden können. Stattdessen kann der Treiber auch vorhandene Anmeldeinformationen verwenden. Dies kann hilfreich sein, wenn die Anwendung Verbindungen mit den Anmeldeinformationen mehrerer Benutzer herstellen muss.  
  
 Der Treiber versucht zunächst vorhandene Anmeldeinformationen zu verwenden (sofern diese verfügbar sind), bevor er die Anmeldung mit dem angegebenen Anmeldemodul ausführt. Bei Ausführung von Code unter einem bestimmten Kontext mithilfe der Subject.doAs-Methode wird daher eine Verbindung mit den Anmeldeinformationen erstellt, die an den Aufruf von Subject.doAs übergeben werden.  
  
 Weitere Informationen finden Sie unter [JAAS Login Configuration File](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html) und [Krb5LoginModule-Klasse](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html).  

 Ab Microsoft JDBC Driver 6.2, Name der Anmeldemodul-Konfigurationsdatei kann optional mit Verbindung Eigenschaft JaasConfigurationName übergeben werden, dadurch wird jede Verbindung, über einen eigenen Anmeldekonfiguration haben.
 
## <a name="creating-a-kerberos-configuration-file"></a>Erstellen einer Kerberos-Konfigurationsdatei  
 Weitere Informationen zu Kerberos-Konfigurationsdateien finden Sie unter [Kerberos Requirements](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html).  
  
 Dies ist eine Konfiguration für eine Beispieldomäne. YYYY und ZZZZ sind durch die Domänennamen an Ihrem Standort zu ersetzen.  
  
```  
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  
  
[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  
  
[realms]  
        YYYY.CORP.CONTOSO.COM = {  
  kdc = krbtgt/YYYY.CORP. CONTOSO.COM @ YYYY.CORP. CONTOSO.COM  
  default_domain = YYYY.CORP. CONTOSO.COM  
}  
  
        ZZZZ.CORP. CONTOSO.COM = {  
  kdc = krbtgt/ZZZZ.CORP. CONTOSO.COM @ ZZZZ.CORP. CONTOSO.COM  
  default_domain = ZZZZ.CORP. CONTOSO.COM  
}  
  
```  
  
## <a name="enabling-the-domain-configuration-file-and-the-login-module-configuration-file"></a>Aktivieren der Domänenkonfigurationsdatei und der Anmeldemodul-Konfigurationsdatei  
 Sie können eine Domänenkonfigurationsdatei mit -Djava.security.krb5.conf aktivieren. Sie können eine Anmeldemodul-Konfigurationsdatei mit aktivieren **-Djava.security.auth.login.config**.  
  
 Sie können beispielsweise beim Starten der Anwendung Folgendes an der Befehlszeile eingeben:  
  
```  
Java.exe -Djava.security.auth.login.config=SQLJDBCDriver.conf -Djava.security.krb5.conf=krb5.ini <APPLICATION_NAME>  
  
```  
  
## <a name="verifying-that-sql-server-can-be-accessed-via-kerberos"></a>Überprüfen des Zugriffs auf SQL Server über Kerberos  
 Führen Sie in SQL Server Management Studio die folgende Abfrage aus:  
  
 **Wählen Sie Auth_scheme aus sys. dm_exec_connections, in denen Session_id = @@spid**  
  
 Vergewissern Sie sich, dass Sie über die erforderliche Berechtigung zum Ausführen dieser Abfrage verfügen.  

## <a name="constrained-delegation"></a>Eingeschränkte Delegierung
Ab Microsoft JDBC Driver 6.2, unterstützt der Treiber die eingeschränkte Kerberos-Delegierung. Die delegierte Anmeldeinformationen als org.ietf.jgss.GSSCredential-Objekt übergeben werden kann, diese Anmeldeinformationen werden vom Treiber verwendet, um die Verbindung herzustellen. 

```
Properties driverProperties = new Properties();
GSSCredential impersonatedUserCredential = [userCredential]
driverProperties.setProperty("integratedSecurity", "true");
driverProperties.setProperty("authenticationScheme", "JavaKerberos");
driverProperties.put("gsscredential", impersonatedUserCredential);
Connection conn = DriverManager.getConnection(CONNECTION_URI, driverProperties);
```

## <a name="kerberos-connection-using-principal-names-and-password"></a>Kerberos-Verbindung mit, Dienstprinzipalnamen und das Kennwort
Ab Microsoft JDBC Driver 6.2, kann der Treiber herstellen Kerberos, die Verbindung mit dem Prinzipalnamen und Kennwort übergeben in der Verbindungszeichenfolge angegeben. 
```
jdbc:sqlserver://servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos;userName=user@REALM;password=****
```
Die Username-Eigenschaft ist kein Bereich erforderlich, wenn Benutzer die Default_realm legen Sie in der Datei krb5.conf gehört. Wenn `userName` und `password` festgelegt ist, zusammen mit `integratedSecurity=true;` und `authenticationScheme=JavaKerberos;` -Eigenschaft, die Verbindung wird hergestellt mit dem Wert des Benutzernamens als Kerberos-Prinzipal zusammen mit dem angegebenen Kennwort.
 
## <a name="see-also"></a>Siehe auch  
 [Herstellen einer Verbindung mit SQLServer mit der JDBC-Treiber](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  

