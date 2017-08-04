---
title: Active Directory-Authentifizierung mit SQLServer on Linux | Microsoft Docs
description: "Die Konfigurationsschritte für das AAD-Authentifizierung für SQL Server on Linux"
author: tmullaney
ms.date: 07/17/2017
ms.author: thmullan;rickbyh
manager: jhubbard
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
helpviewer_keywords:
- Linux, AAD authentication
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9e6d1afdfa7b7d4ef1bfec4461badca746651c44
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="active-directory-authentication-with-sql-server-on-linux"></a>Active Directory-Authentifizierung mit SQLServer on Linux  
[!INCLUDE[tsql-appliesto-sslinx-only_md](../../docs/includes/tsql-appliesto-sslinx-only_md.md)]


Dieses Dokument wird erläutert, wie konfigurieren [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] unter Linux, um Active Directory (AD)-Authentifizierung, auch bekannt als integrierte Authentifizierung zu unterstützen. AD-Authentifizierung ermöglicht Clients unter Windows oder Linux zu authentifizieren, die einer Domäne [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] mit ihren Domänenanmeldeinformationen und das Kerberos-Protokoll. AD-Authentifizierung hat die folgenden Vorteile gegenüber [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] Authentifizierung:  
• Benutzerauthentifizierung über einmaliges Anmelden, ohne ein Kennwort eingeben.   
• Von Anmeldungen für AD-Gruppen erstellen, können Sie den Zugriff und Berechtigungen in verwalten [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] mithilfe von AD-Gruppenmitgliedschaften.  
• Jeder Benutzer verfügt über eine einzelne Identität innerhalb Ihres Unternehmens, daher es nicht zum Nachverfolgen der ist [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] Anmeldungen, welche Personen entsprechen.   
• AD ermöglicht Ihnen, eine zentrale Kennwortrichtlinie in Ihrem Unternehmen zu erzwingen.   

## <a name="prerequisites"></a>Erforderliche Komponenten
Bevor Sie AD-Authentifizierung konfigurieren, müssen Sie:
- Einrichten eines AD-Domänencontrollers (Windows) in Ihrem Netzwerk  
- Installieren[!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]
  - [Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
  - [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
  - [Ubuntu](quickstart-install-connect-ubuntu.md)

>  [!IMPORTANT]  
>   Zu diesem Zeitpunkt ist die einzige Authentifizierungsmethode für Datenbank-Spiegelungsendpunkt unterstützt Zertifikat. WINDOWS-Authentifizierungsmethode wird in einer zukünftigen Version aktiviert

## <a name="step-1-join-includessnoversiondocsincludesssnoversion-mdmd-host-to-ad-domain"></a>Schritt 1: Join [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] Host mit AD-Domäne
Zahlreiche Tools bestehen Sie verknüpfen die [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] Hostcomputer Ihrer AD-Domäne. Diese exemplarische Vorgehensweise verwendet  **[Realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.html)**, ein gängiger open Source-Paket. Wenn Sie nicht bereits geschehen, installieren die Realmd und die Kerberos-Client-Pakete auf dem [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] Hostcomputer mit Ihrem Linux-Distribution-Paket-Manager:  
```bash  
# RHEL
sudo yum install realmd krb5-workstation

# SUSE
sudo zypper install realmd krb5-client

# Ubuntu
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```  

Wenn die Installation des Kerberos-Client-Pakets für einen Bereichsnamen aufgefordert werden, geben Sie Ihren Domänennamen in Großbuchstaben ein.  

>  [!NOTE]  
>  In dieser exemplarischen Vorgehensweise verwendet "contoso.com" und "CONTOSO.COM" als Beispiel Domäne und Bereich Namen. Sie sollten diese durch Ihre eigenen Werte ersetzen. Diese Befehle werden Groß-/Kleinschreibung beachtet, achten Sie darauf, dass Sie verwenden, Großbuchstaben, wo sie in dieser exemplarischen Vorgehensweise verwendet wird.  

Führen Sie den folgenden Befehl zum Überprüfen, ob die [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] Hostcomputer ist so konfiguriert, dass für AD-Domänencontroller als ein DNS-Namenserver verwenden:
```bash  
sudo realm discover contoso.com -v
```  
Wenn Ihre Domäne nicht gefunden wird, müssen Sie zum Konfigurieren Ihrer [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] Hostcomputer Ihrer AD-Domänencontroller IP-Adresse als eine DNS-Namenserver verwenden. Zu diesem Zweck die jeweiligen Schritte hängen davon ab, Ihre Netzwerk-Gerätekonfiguration, die Domänenkonfiguration und die Linux-Distribution. Hier sind einige Beispiel-Ansätze.

### <a name="example-dns-configuration-ubuntu"></a>Beispiel-DNS-Konfiguration: Ubuntu
Bearbeiten der `/etc/network/interfaces` Datei, sodass Ihre AD-Domänencontroller IP-Adresse als eine Dns-Namenserver aufgeführt wird. Beispiel: 
 
```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
iface eth0 inet dhcp
dns-nameservers **<AD domain controller IP address>**
dns-search **<AD domain name>**
```  
>  [!NOTE]  
>  Die Netzwerkschnittstelle (eth0) unterscheiden sich für anderes Computer. Um herauszufinden, welcher Schlüssel, die Sie verwenden, führen Sie Ifconfig, und kopieren Sie die Schnittstelle, die eine IP-Adresse und die gesendeten und empfangenen Bytes hat.

Starten Sie nach der Bearbeitung dieser Datei den Netzwerkdienst neu:
```bash
sudo ifdown eth0 && sudo ifup eth0
```
Nun überprüfen Sie, ob Ihre `/etc/resolv.conf` Datei enthält eine Zeile wie folgt:  
```Code  
nameserver **<AD domain controller IP address>**
```  

### <a name="example-dns-configuration-rhel"></a>Beispiel-DNS-Konfiguration: RHEL
Bearbeiten der `/etc/sysconfig/network-scripts/ifcfg-eth0` -Datei (oder andere Schnittstelle Config-Datei nach Bedarf), damit die IP-Adresse Ihrer AD-Domänencontroller als DNS-Server aufgeführt wird:

 ```/etc/sysconfig/network-scripts/ifcfg-eth0
<...>
PEERDNS=no
DNS1=**<AD domain controller IP address>**
```
Starten Sie nach der Bearbeitung dieser Datei den Netzwerkdienst neu:
```bash
sudo systemctl restart network
```
Nun überprüfen Sie, ob Ihre `/etc/resolv.conf` Datei enthält eine Zeile wie folgt:  
```Code  
nameserver **<AD domain controller IP address>**
```  

### <a name="join-the-domain"></a>Treten Sie zur Domäne bei
Nachdem Sie bestätigt haben, dass DNS ordnungsgemäß konfiguriert ist, treten Sie der Domäne, indem Sie den folgenden Befehl ausführen. Sie müssen die Authentifizierung mit einem AD-Konto, das über ausreichende Berechtigungen in AD, um das Hinzufügen eines neuen Computers zur Domäne verfügt. Insbesondere werden mit diesem Befehl erstellen Sie ein neues Computerkonto in AD, erstellen Sie die `/etc/krb5.keytab` hosten Keytab-Datei, und konfigurieren Sie die Domäne in `/etc/sssd/sssd.conf`:
```bash                                     
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
 * Successfully enrolled machine in realm
```    

>  [!NOTE]  
>   Wenn Sie eine Fehlermeldung angezeigt, "erforderlichen Pakete nicht installiert sind", und installieren Sie diese Pakete mit Ihrem Linux-Distribution-Paket-Manager vor dem Ausführen der `realm join` erneut aus. 
>  
>  Erhalten Sie eine Fehlermeldung, "Unzureichende Berechtigungen für den Domänenbeitritt" müssen Sie mit Domänenadministrator überprüfen Sie, ob Sie über ausreichende Berechtigungen zum Linux-Computer mit Ihrer Domäne zu verknüpfen.

 
Stellen Sie sicher, dass Sie nun Informationen zu einem Benutzer aus der Domäne sammeln können, und ein Kerberos-Ticket als dieser Benutzer erhalten werden können. 

We will use **id**, **[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)** and **[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)** commands for this.

```bash  
id user@contoso.com
uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

kinit user@CONTOSO.COM
Password for user@CONTOSO.COM:

klist
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: user@CONTOSO.COM
<...>
```   

>  [!NOTE]  
>   Wenn `id user@contoso.com` zurückgegeben wird, "Keine solche Benutzer," Stellen Sie sicher, dass der SSSD-Dienst erfolgreich gestartet werden, mithilfe des Befehls `sudo systemctl status sssd`. Wenn der Dienst ausgeführt wird und weiterhin den Fehler "Keine solche Benutzer" angezeigt, versuchen Sie die ausführlichen Protokollierung für SSSD zu aktivieren. Weitere Informationen finden Sie unter Red Hat-Dokumentation für [SSSD Problembehandlung](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting).  
>  
>  Wenn `kinit user@CONTOSO.COM` zurückgegeben wird, "KDC Antwort Erwartungen entsprach nicht beim anfänglichen Anmeldeinformationen abrufen" Stellen Sie sicher, dass Sie den Bereich in Großbuchstaben angegeben haben.

Weitere Informationen finden Sie unter Red Hat-Dokumentation für [Ermitteln von und Verknüpfen von Identität Domänen](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html). 

## <a name="step-2-create-ad-user-for-includessnoversiondocsincludesssnoversion-mdmd-and-set-spn"></a>Schritt 2: Erstellen von AD-Benutzers für [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] und Festlegen des SPN  

>  [!NOTE]  
>  In den nächsten Schritten verwenden wir Ihre [vollständig qualifizierten Domänennamen](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Bei **Azure**, müssen Sie  **[erstellen Sie eine](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/portal-create-fqdn)**  bevor Sie fortfahren. 

Führen Sie auf dem Domänencontroller die [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) PowerShell-Befehl, um einen neuen AD-Benutzer mit einem Kennwort zu erstellen, das nicht abläuft. In diesem Beispiel den Namen des Kontos "Mssql", aber der Kontoname kann alles gewünschte sein. Sie werden aufgefordert, ein neues Kennwort für das Konto einzugeben:  
```PowerShell   
Import-Module ActiveDirectory

New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
```   

>  [!NOTE]  
>  Es ist eine bewährte Sicherheitsmethode, ein dediziertes AD-Konto für SQL Server zu verwenden, sodass SQL Server Anmeldeinformationen sind nicht mit anderen Diensten, die mit dem gleichen Konto gemeinsam verwendet. Jedoch können Sie ein vorhandenes AD-Konto wiederverwenden, wenn Sie dies bevorzugen, wenn Sie wissen, dass das Kennwort des Kontos (erforderlich, um eine Keytab-Datei im nächsten Schritt generieren).

Nun legen Sie den ServicePrincipalName (SPN) für dieses Konto verwenden die `setspn.exe` Tool. Der SPN muss genau wie im folgenden Beispiel angegeben formatiert: finden Sie den vollqualifizierten Domänennamen des der [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] Hostcomputer durch Ausführen `hostname --all-fqdns` auf die [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] Host und den TCP-Port muss 1433, sofern Sie konfiguriert haben [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] auf eine andere Portnummer zu verwenden.  
```PowerShell   
setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
```   

>  [!NOTE]  
>  Wenn Sie einen Fehler "nicht über ausreichende Zugriffsrechte," erhalten müssen Sie mit Domänenadministrator überprüfen Sie, ob Sie über ausreichende Berechtigungen, um einen SPN für dieses Konto festlegen.
>  
>  Wenn Sie den TCP-Port in der Zukunft ändern, müssen Sie den Befehls "Setspn" mit die neue Portnummer erneut ausführen. Sie müssen auch die neuen SPN die Keytab-Datei für SQL Server-Dienst hinzufügen, indem Sie die Schritte im nächsten Abschnitt.

Weitere Informationen finden Sie unter [Registrieren eines Dienstprinzipalnamens für Kerberos-Verbindungen](/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  

## <a name="step-3-configure-includessnoversiondocsincludesssnoversion-mdmd-service-keytab"></a>Schritt 3: Konfigurieren von [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] Dienst Keytab-Datei  
Überprüfen Sie zunächst die Versionsnummer des Schlüssels (Kvno) für das AD-Konto, das im vorherigen Schritt erstellt haben. Sie werden in der Regel 2, aber er kann eine andere ganze Zahl sein, wenn Sie das Kennwort des Kontos mehrmals geändert haben. Auf der [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] Hostcomputer, führen Sie Folgendes aus:

```bash
kinit user@CONTOSO.COM

kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
```

Erstellen Sie jetzt eine Keytab-Datei für den AD-Benutzer, den Sie im vorherigen Schritt erstellt haben. In diesem Fall werden wir verwenden  **[Ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)**. Wenn Sie aufgefordert werden, geben Sie das Kennwort für das AD-Konto ein. 
```bash  
sudo ktutil

ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96

ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac

ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

quit
```  

>  [!NOTE]  
>  Das Tool Ktutil überprüft das Kennwort nicht, achten Sie darauf, dass Sie die eingeben.

Jede Person mit Zugriff auf diese `keytab` Datei kann die Identität [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] in der Domäne, weshalb Sie sicherstellen müssen Sie den Zugriff auf die Datei, nur die `mssql` Konto über Lesezugriff verfügt:  
```bash  
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```  
Als Nächstes konfigurieren [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] dieses `keytab` Datei für die Kerberos-Authentifizierung:  
```bash  
sudo /opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```  

## <a name="step-4-create-ad-based-logins-in-transact-sql"></a>Schritt 4: Erstellen von AD-basierte Anmeldungen in Transact-SQL  
Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] und erstellen Sie eine neue, auf AD basierende Anmeldung:  
```Transact-SQL  
CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
```   

Stellen Sie sicher, dass die Anmeldung jetzt im aufgeführt ist die [Sys. server_principals](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql.mc) Systemkatalogsicht:  
```Transact-SQL  
SELECT name FROM sys.server_principals;
```  

## <a name="step-5-connect-to-includessnoversiondocsincludesssnoversion-mdmd-using-ad-authentication"></a>Schritt 5: Verbinden mit [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] mithilfe der AD-Authentifizierung  
Melden Sie sich auf einen Clientcomputer über Ihre Domänenanmeldeinformationen an. Nachdem Sie eine Verbindung herstellen können [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] ohne Ihr Kennwort mithilfe der AD-Authentifizierung her. Wenn Sie eine Anmeldung für eine AD-Gruppe erstellen, kann alle AD-Benutzer, die Mitglied dieser Gruppe ist auf die gleiche Weise verbinden.  
Die spezifische Verbindungszeichenfolgenparameter für Clients, die AD-Authentifizierung verwenden hängt ab, auf welcher Treiber verwenden. Einige Beispiele sind unten aufgeführt.  

## <a name="examples"></a>Beispiele  
### <a name="example-1-sqlcmd-on-a-domain-joined-linux-client"></a>Beispiel 1: `sqlcmd` auf einem Linux-Client Domäne  
Melden Sie sich einer Domäne Linux-Client mit `ssh` und Anmeldeinformationen für die Domäne:  
```bash  
ssh -l user@contoso.com client.contoso.com
```  

Stellen Sie sicher, dass Sie installiert haben die [Mssql-Tools](sql-server-linux-setup-tools.md) Verpacken und dann eine Verbindung über `sqlcmd` ohne Angabe von Anmeldeinformationen:  
```bash  
sqlcmd -S mssql.contoso.com
```  

### <a name="example-2-ssms-on-a-domain-joined-windows-client"></a>Beispiel 2: SSMS auf eine Domäne eingebundenen Windows-client  
Melden Sie sich eine Domäne eingebundenen Windows-Client über Ihre Domänenanmeldeinformationen an. Stellen Sie sicher, dass [!INCLUDE[ssmanstudiofull-md](../../docs/includes/ssmanstudiofull-md.md)] installiert ist, wird eine Verbindung herstellen, um Ihre [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] Instanz durch Angabe **Windows-Authentifizierung** in der **Verbindung mit Server herstellen** Dialogfeld.  

### <a name="ad-authentication-using-other-client-drivers"></a>AD-Authentifizierung, die mit anderen Clienttreibern  
• JDBC: [mithilfe von Kerberos die integrierte Authentifizierung, um SQLServer herstellen](https://docs.microsoft.com/sql/connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server])  
• ODBC: [mithilfe der integrierten Authentifizierung](https://docs.microsoft.com/sql/connect/odbc/linux/using-integrated-authentication)  
• ADO.NET: [Verbindungszeichenfolgensyntax](https://msdn.microsoft.com/library/ms254500.aspx)   


