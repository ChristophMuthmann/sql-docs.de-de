---
title: Active Directory-Authentifizierung-Lernprogramm für SQL Server on Linux | Microsoft Docs
description: Dieses Lernprogramm bietet die Konfigurationsschritte für AAD-Authentifizierung für SQL Server on Linux.
author: meet-bhagdev
ms.date: 02/23/2018
ms.author: meetb
manager: craigg
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 0ff01d10ceb460375df9b3b3ce4a06191b5aaba2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>Lernprogramm: Verwenden Sie Active Directory-Authentifizierung mit SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

In diesem Lernprogramm wird erläutert, wie konfigurieren [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unter Linux, um Active Directory (AD)-Authentifizierung, auch bekannt als integrierte Authentifizierung zu unterstützen. Eine Übersicht finden Sie unter [Active Directory-Authentifizierung für SQL Server on Linux](sql-server-linux-active-directory-auth-overview.md).

Dieses Lernprogramm umfasst die folgenden Aufgaben:

> [!div class="checklist"]
> * Join [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Host mit AD-Domäne
> * Erstellen Sie AD-Benutzer für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] und Festlegen des SPN
> * Konfigurieren Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Dienst Keytab-Datei
> * Erstellen von AD-basierte Anmeldungen in Transact-SQL
> * Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe der AD-Authentifizierung

## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie AD-Authentifizierung konfigurieren, müssen Sie:

* Einrichten eines AD-Domänencontrollers (Windows) in Ihrem Netzwerk  
* Installieren [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> Join [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Host mit AD-Domäne

Verwenden Sie die folgenden Schritte aus, um Verknüpfen einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Host Active Directory-Domäne:

1. Verwendung **[Realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.html)** des Host-Computers mit AD-Domäne zu verknüpfen. Wenn Sie nicht bereits geschehen, installieren die Realmd und die Kerberos-Client-Pakete auf dem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Hostcomputer mit Ihrem Linux-Distribution-Paket-Manager:

   ```bash
   # RHEL
   sudo yum install realmd krb5-workstation

   # SUSE
   sudo zypper install realmd krb5-client

   # Ubuntu
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. Wenn die Installation des Kerberos-Client-Pakets für einen Bereichsnamen aufgefordert werden, geben Sie Ihren Domänennamen in Großbuchstaben ein.

   > [!NOTE]
   > In dieser exemplarischen Vorgehensweise verwendet "contoso.com" und "CONTOSO.COM" als Beispiel Domäne und Bereich Namen. Sie sollten diese durch Ihre eigenen Werte ersetzen. Diese Befehle werden Groß-/Kleinschreibung beachtet, achten Sie darauf, dass Sie verwenden, Großbuchstaben, wo sie in dieser exemplarischen Vorgehensweise verwendet wird.

1. Konfigurieren Sie Ihre [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Hostcomputer Ihrer AD-Domänencontroller IP-Adresse als eine DNS-Namenserver verwenden. 

   - **Ubuntu**:

      Bearbeiten der `/etc/network/interfaces` Datei, sodass Ihre AD-Domänencontroller IP-Adresse als eine Dns-Namenserver aufgeführt wird. Beispiel: 

      ```/etc/network/interfaces
      <...>
      # The primary network interface
      auth eth0
      iface eth0 inet dhcp
      dns-nameservers **<AD domain controller IP address>**
      dns-search **<AD domain name>**
      ```

      > [!NOTE]
      > Die Netzwerkschnittstelle (eth0) unterscheiden sich für die verschiedenen Computern. Um herauszufinden, welcher Schlüssel, die Sie verwenden, führen Sie Ifconfig, und kopieren Sie die Schnittstelle, die eine IP-Adresse und die gesendeten und empfangenen Bytes hat.

      Starten Sie nach der Bearbeitung dieser Datei den Netzwerkdienst neu:

      ```bash
      sudo ifdown eth0 && sudo ifup eth0
      ```

      Nun überprüfen Sie, ob Ihre `/etc/resolv.conf` Datei enthält eine Zeile wie im folgenden Beispiel:  

      ```Code
      nameserver **<AD domain controller IP address>**
      ```

   - **RHEL**:

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

     Nun überprüfen Sie, ob Ihre `/etc/resolv.conf` Datei enthält eine Zeile wie im folgenden Beispiel:  

     ```Code
     nameserver **<AD domain controller IP address>**
     ```

1. Treten Sie zur Domäne bei

   Nachdem Sie bestätigt haben, dass DNS ordnungsgemäß konfiguriert ist, treten Sie der Domäne, indem Sie den folgenden Befehl ausführen. Sie müssen zur Authentifizierung, verwenden ein AD-Konto, das über ausreichende Berechtigungen in AD, um das Hinzufügen eines neuen Computers zur Domäne verfügt.

   Insbesondere dieser Befehl erstellt ein neues Computerkonto in Active Directory, erstellen Sie die `/etc/krb5.keytab` hosten Keytab-Datei, und konfigurieren Sie die Domäne in `/etc/sssd/sssd.conf`:

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   <...>
   * Successfully enrolled machine in realm
   ```

   > [!NOTE]
   > Wenn Sie eine Fehlermeldung angezeigt, "erforderlichen Pakete nicht installiert sind", und installieren Sie diese Pakete mit Ihrem Linux-Distribution-Paket-Manager vor dem Ausführen der `realm join` erneut aus.
   >
   > Erhalten Sie eine Fehlermeldung, "Unzureichende Berechtigungen für den Domänenbeitritt" müssen Sie mit Domänenadministrator überprüfen Sie, ob Sie über ausreichende Berechtigungen zum Linux-Computer mit Ihrer Domäne zu verknüpfen.
   >
   > Wenn Sie eine Fehlermeldung, "KDC Antwort entsprach nicht Erwartungen," dann Sie möglicherweise nicht den richtigen Bereichsnamen für den Benutzer angegeben. Bereichsnamen Groß-/Kleinschreibung beachtet werden, in der Regel in Großbuchstaben und identifiziert werden können, mit dem Befehl `realm discover contoso.com`.
   
   > SQL Server verwendet SSSD und NSS für die Zuordnung von Benutzerkonten und-Gruppen zu Sicherheits-IDs (SID). SSSD muss konfiguriert und wird ausgeführt, damit SQL Server zum erfolgreichen Erstellen von AD-Anmeldungen. Realmd normalerweise der Fall ist dies automatisch als Teil einer Domäne beizutreten, aber in einigen Fällen müssen hierzu Sie separat.
   >
   > Sehen Sie sich die folgenden so konfigurieren Sie [SSSD manuell](https://access.redhat.com/articles/3023951), und [NSS SSSD portzuweisung konfigurieren](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options)

  
5. Stellen Sie sicher, dass Sie nun Informationen zu einem Benutzer aus der Domäne sammeln können, und ein Kerberos-Ticket als dieser Benutzer erhalten werden können.

   Im folgenden Beispiel wird **Id**,  **[Kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)**, und **[Klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)** für diese Befehle.

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

   > [!NOTE]
   > Wenn `id user@contoso.com` zurückgegeben wird, "Keine solche Benutzer," Stellen Sie sicher, dass der SSSD-Dienst erfolgreich gestartet werden, mithilfe des Befehls `sudo systemctl status sssd`. Wenn der Dienst ausgeführt wird und weiterhin den Fehler "Keine solche Benutzer" angezeigt, versuchen Sie die ausführlichen Protokollierung für SSSD zu aktivieren. Weitere Informationen finden Sie unter Red Hat-Dokumentation für [SSSD Problembehandlung](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting).
   >
   > Wenn `kinit user@CONTOSO.COM` zurückgegeben wird, "KDC Antwort Erwartungen entsprach nicht beim anfänglichen Anmeldeinformationen abrufen" Stellen Sie sicher, dass Sie den Bereich in Großbuchstaben angegeben haben.

Weitere Informationen finden Sie unter Red Hat-Dokumentation für [Ermitteln von und Verknüpfen von Identität Domänen](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html). 

## <a id="createuser"></a> Erstellen Sie AD-Benutzer für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] und Festlegen des SPN

  > [!NOTE]
  > Die nächsten Schritte verwenden Ihre [vollständig qualifizierten Domänennamen](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Bei **Azure**, müssen Sie **[erstellen Sie eine](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/portal-create-fqdn)** bevor Sie fortfahren.

1. Führen Sie auf dem Domänencontroller die [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) PowerShell-Befehl, um einen neuen AD-Benutzer mit einem Kennwort zu erstellen, das nicht abläuft. In diesem Beispiel den Namen des Kontos "Mssql", aber der Kontoname kann alles gewünschte sein. Sie werden aufgefordert, ein neues Kennwort für das Konto einzugeben:

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > Es ist eine bewährte Sicherheitsmethode, ein dediziertes AD-Konto für SQL Server zu verwenden, sodass SQL Server Anmeldeinformationen sind nicht mit anderen Diensten, die mit dem gleichen Konto gemeinsam verwendet. Jedoch können Sie ein vorhandenes AD-Konto wiederverwenden, wenn Sie dies bevorzugen, wenn Sie wissen, dass das Kennwort des Kontos (erforderlich, um eine Keytab-Datei im nächsten Schritt generieren).

2. Legen Sie den ServicePrincipalName (SPN) für dieses Konto verwendet die `setspn.exe` Tool. Der SPN muss genau wie im folgenden Beispiel angegeben formatiert werden. Finden Sie den vollqualifizierten Domänennamen des der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Hostcomputer Treiberdienst `hostname --all-fqdns` auf die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Host und den TCP-Port muss 1433, sofern Sie konfiguriert haben [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf eine andere Portnummer zu verwenden.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > Wenn Sie einen Fehler "nicht über ausreichende Zugriffsrechte," erhalten müssen Sie mit Domänenadministrator überprüfen Sie, ob Sie über ausreichende Berechtigungen, um einen SPN für dieses Konto festlegen.
   >
   > Wenn Sie den TCP-Port in der Zukunft ändern, müssen Sie den Befehls "Setspn" erneut ausführen, mit die neue Portnummer. Sie müssen auch die neuen SPN die Keytab-Datei für SQL Server-Dienst hinzufügen, indem Sie die Schritte im nächsten Abschnitt.

3. Weitere Informationen finden Sie unter [Registrieren eines Dienstprinzipalnamens für Kerberos-Verbindungen](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).

## <a id="configurekeytab"></a> Konfigurieren Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Dienst Keytab-Datei

1. Überprüfen Sie die Versionsnummer des Schlüssels (Kvno) für das AD-Konto, das im vorherigen Schritt erstellt haben. Ist in der Regel 2, aber er kann eine andere ganze Zahl sein, wenn Sie das Kennwort des Kontos mehrmals geändert haben. Auf der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Hostcomputer, führen Sie Folgendes aus:

   ```bash
   kinit user@CONTOSO.COM

   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
   ```

2. Erstellen Sie eine Keytab-Datei mit **[Ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)** für AD-Benutzer, die Sie im vorherigen Schritt erstellt haben. Wenn Sie aufgefordert werden, geben Sie das Kennwort für das AD-Konto ein.

   ```bash
   sudo ktutil

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac

   ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

   quit
   ```

   > [!NOTE]
   > Das Tool Ktutil überprüft das Kennwort nicht, achten Sie darauf, dass Sie die eingeben.

3. Jede Person mit Zugriff auf diese `keytab` Datei kann die Identität [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in der Domäne, weshalb Sie sicherstellen müssen Sie den Zugriff auf die Datei, nur die `mssql` Konto über Lesezugriff verfügt:

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
   sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
   ```

4. Konfigurieren Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dieses `keytab` Datei für die Kerberos-Authentifizierung:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
   sudo systemctl restart mssql-server
   ```

## <a id="createsqllogins"></a> Erstellen von AD-basierte Anmeldungen in Transact-SQL

1. Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] und erstellen Sie eine neue, auf AD basierende Anmeldung:

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

2. Stellen Sie sicher, dass die Anmeldung jetzt im aufgeführt ist die [Sys. server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) Systemkatalogsicht:

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe der AD-Authentifizierung

Melden Sie sich auf einen Clientcomputer über Ihre Domänenanmeldeinformationen an. Nachdem Sie eine Verbindung herstellen können [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ohne Ihr Kennwort mithilfe der AD-Authentifizierung her. Wenn Sie eine Anmeldung für eine AD-Gruppe erstellen, kann alle AD-Benutzer, die Mitglied dieser Gruppe ist auf die gleiche Weise verbinden.

Die spezifische Verbindungszeichenfolgenparameter für Clients, die AD-Authentifizierung verwenden hängt ab, auf welcher Treiber verwenden. Betrachten Sie die folgenden Beispiele:

* `sqlcmd` auf einem Linux-Client Domäne

   Melden Sie sich einer Domäne Linux-Client mit `ssh` und Anmeldeinformationen für die Domäne:

   ```bash
   ssh -l user@contoso.com client.contoso.com
   ```

   Stellen Sie sicher, dass Sie installiert haben die [Mssql-Tools](sql-server-linux-setup-tools.md) Verpacken und dann eine Verbindung über `sqlcmd` ohne Angabe von Anmeldeinformationen:

   ```bash
   sqlcmd -S mssql.contoso.com
   ```

* SSMS auf eine Domäne eingebundenen Windows-client

   Melden Sie sich eine Domäne eingebundenen Windows-Client über Ihre Domänenanmeldeinformationen an. Stellen Sie sicher, dass [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] installiert ist, wird eine Verbindung herstellen, um Ihre [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Instanz durch Angabe **Windows-Authentifizierung** in der **Verbindung mit Server herstellen** Dialogfeld.

* AD-Authentifizierung, die mit anderen Clienttreibern

  * JDBC: [mithilfe von Kerberos die integrierte Authentifizierung, um SQLServer herstellen](https://docs.microsoft.com/sql/connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server)
  * ODBC: [mithilfe der integrierten Authentifizierung](https://docs.microsoft.com/sql/connect/odbc/linux/using-integrated-authentication)
  * ADO.NET: [Verbindungszeichenfolgensyntax](https://msdn.microsoft.com/library/system.data.sqlclient.sqlauthenticationmethod(v=vs.110).aspx)
  
## <a name="next-steps"></a>Nächste Schritte

In diesem Lernprogramm durchlaufen, wird durch die Schritte zum Einrichten der Active Directory-Authentifizierung mit SQL Server on Linux. Sie haben gelernt, wie auf:
> [!div class="checklist"]
> * Join [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Host mit AD-Domäne
> * Erstellen Sie AD-Benutzer für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] und Festlegen des SPN
> * Konfigurieren Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Dienst Keytab-Datei
> * Erstellen von AD-basierte Anmeldungen in Transact-SQL
> * Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe der AD-Authentifizierung

Untersuchen Sie anschließend andere Sicherheitsszenarien für SQL Server unter Linux.

> [!div class="nextstepaction"]
>[Verschlüsseln von Verbindungen zu SQLServer on Linux](sql-server-linux-encrypted-connections.md)
