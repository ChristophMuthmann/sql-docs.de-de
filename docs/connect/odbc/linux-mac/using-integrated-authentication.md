---
title: Mithilfe der integrierten Authentifizierung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- integrated authentication
ms.assetid: 9499ffdf-e0ee-4d3c-8bca-605371eb52d9
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8e2c2a07d94fce76b37970cc998ae6a0959a0080
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-integrated-authentication"></a>Nutzung der Integrierten Authentifizierung
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Die [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] auf Linux- und MacOS unterstützt Verbindungen mit Kerberos die integrierte Authentifizierung. Es unterstützt MIT Kerberos Key Distribution Center (KDC), und arbeitet mit der Generic Security Services Anwendung Programm-Schnittstelle (GSSAPI) und Kerberos v5-Bibliotheken.
  
## <a name="using-integrated-authentication-to-connect-to-includessnoversionincludesssnoversionmdmd-from-an-odbc-application"></a>Mithilfe der integrierten Authentifizierung für die Verbindung [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] aus einer ODBC-Anwendung  

Sie können die integrierte Kerberos-Authentifizierung aktivieren, indem **Trusted_Connection = Yes** in der Verbindungszeichenfolge des **SQLDriverConnect** oder **SQLConnect**. Beispiel:  

```
Driver='ODBC Driver 13 for SQL Server';Server=your_server;Trusted_Connection=yes  
```
  
Bei der Verbindung mit einem DSN, können Sie auch hinzufügen **Trusted_Connection = Yes** auf den DSN-Eintrag im `odbc.ini`.
  
Die `-E` -Option von `sqlcmd` und `-T` Option `bcp` auch an die integrierte Authentifizierung verwendet werden kann, finden Sie unter [Herstellen einer Verbindung mit **Sqlcmd** ](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md) und [ Herstellen einer Verbindung mit **Bcp** ](../../../connect/odbc/linux-mac/connecting-with-bcp.md) für Weitere Informationen.

Stellen Sie sicher, dass den clientprinzipal, auf die Verbindung mit dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] ist bereits beim Kerberos KDC authentifiziert.
  
**ServerSPN** und **FailoverPartnerSPN** werden nicht unterstützt.  
  
## <a name="deploying-a-linux-or-macos-odbc-driver-application-designed-to-run-as-a-service"></a>Bereitstellen von einem Linux- oder MacOS ODBC-Treiber-Anwendung entwickelt zum Ausführen als Dienst

Ein Systemadministrator kann eine Anwendung als Dienst ausgeführt wird, die Kerberos-Authentifizierung verwendet wird, für die Verbindung bereitstellen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
Sie müssen zuerst Kerberos auf dem Client zu konfigurieren und stellen Sie sicher, dass die Anwendung die Kerberos-Anmeldeinformationen des standardprinzipals verwenden kann.

Stellen Sie sicher, dass die Verwendung von `kinit` oder PAM (Pluggable Authentication Module) zum Abrufen und Zwischenspeichern TGT für den Prinzipal, der die Verbindung verwendet wird, über eine der folgenden Methoden:  
  
-   Führen Sie `kinit`, und übergeben Sie einen Prinzipalnamen und ein Kennwort.  
  
-   Führen Sie `kinit`, und übergeben Sie einen Prinzipalnamen und den Speicherort einer schlüsseltabellendatei, die den prinzipalschlüssel erstellt, indem enthält `ktutil`.  
  
-   Stellen Sie sicher, dass die Anmeldung am System vorgenommen wurde mithilfe von Kerberos PAM (Pluggable Authentication Module).

Wenn eine Anwendung als Dienst wird ausgeführt, da Kerberos-Anmeldeinformationen programmbedingt ablaufen, erneuern Sie die Anmeldeinformationen, um kontinuierliche Verfügbarkeit des Diensts sicherzustellen. Der ODBC-Treiber erneuert nicht Anmeldeinformationen selbst; Stellen Sie sicher, dass es ist ein `cron` Job oder ein Skript, die regelmäßig ausgeführt wird, um die Anmeldeinformationen vor deren Ablauf zu erneuern. Um zu vermeiden, dass das Kennwort bei jeder Verlängerung, können Sie eine Keytab-Datei verwenden.  
  
[Kerberos-Konfiguration und Verwendung](http://commons.oreilly.com/wiki/index.php/Linux_in_a_Windows_World/Centralized_Authentication_Tools/Kerberos_Configuration_and_Use) bietet ausführliche Informationen zu Methoden zum kerberisieren von Diensten unter Linux.
  
## <a name="tracking-access-to-a-database"></a>Nachverfolgen von Zugriffen auf eine Datenbank

Ein Datenbankadministrator kann einen Audit-Trail des Zugriffs auf eine Datenbank erstellen, wenn Systemkonten genutzt wird, den Zugriff auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] mithilfe der integrierten Authentifizierung.  
  
Anmelden an [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] wird das Systemkonto verwendet und ist keine Funktionalität für Linux, um den Sicherheitskontext imitieren. Aus diesem Grund muss der Benutzer genauer bestimmt werden.
  
Überwachen der Aktivitäten in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] im Auftrag von Benutzern als das Systemkonto, muss die Anwendung verwenden [!INCLUDE[tsql](../../../includes/tsql_md.md)] **EXECUTE AS**.  
  
Zum Verbessern der Anwendungsleistung kann eine Anwendung Verbindungspooling mit integrierten Authentifizierung und Überwachung verwenden. Allerdings erstellt die Kombinieren von Verbindungspooling, integrierter Authentifizierung und Überwachung ein Sicherheitsrisiko, da der UnixODBC-Treiber-Manager mit andere Benutzern, gepoolte Verbindungen wiederzuverwenden erlaubt. Weitere Informationen finden Sie unter [ODBC-Verbindungspooling](http://www.unixodbc.org/doc/conn_pool.html).  

Vor der Wiederverwendung muss eine Anwendung gepoolte Verbindungen durch Ausführen zurückgesetzt `sp_reset_connection`.  

## <a name="using-active-directory-to-manage-user-identities"></a>Verwalten von Benutzeridentitäten mithilfe von Active Directory

Ein anwendungssystemadministrator muss keine separate Sätze von Anmeldeinformationen verwalten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Es ist möglich, Active Directory als ein Schlüsselverteilungscenter (KDC) für die integrierte Authentifizierung zu konfigurieren. Finden Sie unter [Microsoft Kerberos](https://msdn.microsoft.com/en-us/library/windows/desktop/aa378747(v=vs.85).aspx) für Weitere Informationen.

## <a name="using-linked-server-and-distributed-queries"></a>Verbindungsserver und verteilte Abfragen nutzen

Entwickler können eine Anwendung bereitstellen, die einen Verbindungsserver oder verteilte Abfragen nutzt. Dies geschieht ohne einen Datenbankadministrator, der separate Sätze von SQL-Anmeldeinformationen verwaltet. In diesem Fall muss ein Entwickler eine Anwendung auf die Verwendung der integrierten Authentifizierung konfigurieren:  
  
-   Der Benutzer meldet sich bei einem Clientcomputer an und authentifiziert sich beim Anwendungsserver.  
  
-   Die Anwendungsserver als eine andere Datenbank authentifiziert und eine Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]als Datenbankbenutzer in eine andere Datenbank authentifiziert ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
Nachdem die integrierte Authentifizierung konfiguriert ist, werden Anmeldeinformationen für den Verbindungsserver übergeben.  
  
## <a name="integrated-authentication-and-sqlcmd"></a>Integrierte Authentifizierung und sqlcmd
Für den Zugriff auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] mithilfe der integrierten Authentifizierung, verwenden Sie die `-E` -Option von `sqlcmd`. Stellen Sie sicher, dass das Konto, das führt `sqlcmd` der Standard-Kerberos-Client-Prinzipal zugeordnet ist.

## <a name="integrated-authentication-and-bcp"></a>Integrierte Authentifizierung und bcp
Für den Zugriff auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] mithilfe der integrierten Authentifizierung, verwenden Sie die `-T` -Option von `bcp`. Stellen Sie sicher, dass das Konto, das führt `bcp` der Standard-Kerberos-Client-Prinzipal zugeordnet ist. 
  
Es ist ein Fehler mit `-T` mit der `-U` oder `-P` Option.
  
## <a name="supported-syntax-for-an-spn-registered-by-includessnoversionincludesssnoversionmdmd"></a>Unterstützte Syntax für einen SPN registriert von[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]

Die Syntax, die SPNs in der Verbindungszeichenfolge oder Verbindungsattribute verwenden lautet wie folgt:  

|Syntax|Beschreibung|  
|----------|---------------|  
|MSSQLSvc/*fqdn*:*port*|Der vom Anbieter erstellte Standard-SPN, wenn TCP verwendet wird. *port* ist eine TCP-Portnummer. *fqdn* ist ein vollqualifizierter Domänenname.|  
  
## <a name="authenticating-a-linux-or-macos-computer-with-active-directory"></a>Authentifizieren einen Linux- oder MacOS Computer mit Active Directory

Geben Sie zum Konfigurieren von Kerberos, Daten in die `krb5.conf` Datei. `krb5.conf`befindet sich im `/etc/` aber erhalten Sie in eine andere Datei, die mit der Syntax, z. B. `export KRB5_CONFIG=/home/dbapp/etc/krb5.conf`. Im folgenden ist ein Beispiel für `krb5.conf` Datei:  
  
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
```  
  
Wenn Ihre Linux- oder MacOS-Computer konfiguriert ist, um das Dynamic Host Configuration Protocol (DHCP) mit einem Windows-DHCP-Server bietet der DNS-Server zu verwenden, verwenden, können Sie **Dns_lookup_kdc = "true"**. Jetzt können Sie Kerberos verwenden, mit der Domäne anmelden, indem er den Befehl `kinit alias@YYYY.CORP.CONTOSO.COM`. Parameter übergeben wird, um `kinit` Groß-/Kleinschreibung beachtet und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Computer so konfiguriert, dass in der Domäne befinden, muss dieser Benutzer haben `alias@YYYY.CORP.CONTOSO.COM` Anmeldenamen hinzugefügt. Sie können nun vertrauenswürdige Verbindungen (**Trusted_Connection = YES** in einer Verbindungszeichenfolge **Bcp -T**, oder **Sqlcmd-e**).  
  
Die Zeit auf dem Linux oder MacOS Computer und die Zeit auf Kerberos Key Distribution Center (KDC) müssen möglichst übereinstimmen. Stellen Sie sicher, dass die Systemzeit richtig, z. B. mithilfe der Netzwerkzeitprotokoll (NTP) festgelegt ist.  

Wenn Kerberos-Authentifizierung fehlschlägt, wird der ODBC-Treiber unter Linux oder MacOS NTLM-Authentifizierung nicht verwendet.  

Weitere Informationen zum Authentifizieren von Linux oder MacOS Computer mit Active Directory finden Sie unter [Linux-Clients mit Active Directory authentifizieren](http://technet.microsoft.com/magazine/2008.12.linux.aspx#id0060048) und [bewährte Methoden für die Integration von OS X mit Active Directory](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf). Weitere Informationen zum Konfigurieren von Kerberos finden Sie unter der [MIT Kerberos-Dokumentation](https://web.mit.edu/kerberos/krb5-1.12/doc/index.html).

## <a name="see-also"></a>Siehe auch  
[Programmierrichtlinien](../../../connect/odbc/linux-mac/programming-guidelines.md)

[Versionsanmerkungen](../../../connect/odbc/linux-mac/release-notes.md)

[Mithilfe von Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md)

