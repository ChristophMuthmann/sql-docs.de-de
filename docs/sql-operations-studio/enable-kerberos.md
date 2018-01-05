---
title: "Verwenden Sie Active Directory-Authentifizierung (Kerberos), bei der Verbindung mit SQL-Vorgänge Studio (Vorschau) | Microsoft Docs"
description: "Informationen Sie zum Aktivieren von Kerberos mit Active Directory-Authentifizierung für SQL-Vorgänge Studio (Vorschau)"
ms.custom: tools|sos
ms.date: 11/17/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: meet-bhagdev
ms.author: meetb
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fcc9e91255317d53a63dd9867f6060af591f36e3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="connect-includename-sosincludesname-sos-shortmd-to-your-sql-server-using-windows-authentication---kerberos"></a>Verbinden [!INCLUDE[name-sos](../includes/name-sos-short.md)] auf dem SQL Server mithilfe der Windows-Authentifizierung – Kerberos 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]unterstützt das Herstellen einer Verbindung mit SQL Server mithilfe von Kerberos.

Um die integrierte Authentifizierung (Windows-Authentifizierung) für MacOS oder Linux verwenden zu können, müssen Sie zum Einrichten einer **Kerberos-Ticket** verknüpfen Ihres aktuellen Benutzers in ein Windows-Domänenkonto. 

## <a name="prerequisites"></a>Voraussetzungen

- Zugriff auf eine Windows-Domäne eingebundenen Computer zum Abfragen der Kerberos-Domänencontroller.
- SQL Server müssen zum Zulassen von Kerberos-Authentifizierung konfiguriert werden. Für den Clienttreiber auf Unix ausgeführt wird wird nur integrierte Authentifizierung unterstützt mithilfe von Kerberos. Weitere Informationen zum Einrichten der Sql Server die Authentifizierung mit Kerberos verwendbaren [hier](https://support.microsoft.com/en-us/help/319723/how-to-use-kerberos-authentication-in-sql-server). Es darf Dienstprinzipalnamen für jede Instanz von Sql Server, die Sie herstellen möchten. Informationen über das Format von SQL Server-SPNs aufgelisteten [hier](https://technet.microsoft.com/en-us/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats)


## <a name="checking-if-sql-server-has-kerberos-setup"></a>Überprüft, ob Sql Server mit Kerberos-Setup hat

Melden Sie sich den Hostcomputer des Sql Server. Verwenden von Windows-Eingabeaufforderung die `setspn -L %COMPUTERNAME%` zum Auflisten aller Dienstprinzipalnamen für den Host. Einträge sollte, die mit MSSQLSvc/HostName.Domain.com, was bedeutet beginnen, dass Sql Server einen SPN registriert wurde und bereit zur Annahme von Kerberos-Authentifizierung ist angezeigt werden. 
- Wenn Sie haben keinen Zugriff auf den Host des Sql-Servers, von allen anderen Windows-Betriebssystemen mit derselben Active Directory verknüpft, können Sie den Befehl `setspn -L <SQLSERVER_NETBIOS>` , wobei < SQLSERVER_NETBIOS > den Namen des der Hsot von Sql Server ist.


## <a name="get-the-kerberos-key-distribution-center"></a>Das Kerberos-Schlüsselverteilungscenter abrufen

Suchen Sie die Kerberos-KDC (Key Distribution Center)-Konfigurationswert. Führen Sie den folgenden Befehl auf einem Windows-Computer, der mit Ihrer Active Directory-Domäne verknüpft ist: 

Starten Sie `cmd.exe` und führen Sie `nltest`.

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where “DOMAIN.COMPANY.COM” maps to your domain’s name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
Kopieren Sie den DC-Namen, der die erforderlichen KDC-Konfigurationswert, in diesem Fall dc-33.domain.company.com ist

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>Verknüpfen Sie Ihr Betriebssystem, mit dem Active Directory-Domänencontroller

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

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

Nun überprüfen Sie, ob Ihre `/etc/resolv.conf` Datei enthält eine Zeile wie folgt:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
```
   
### <a name="redhat-enterprise-linux"></a>Red Hat Enterprise Linux
```bash
sudo yum install realmd krb5-workstation
```

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

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>MacOS

- Verknüpfen Sie Ihre MacOS mit Active Directory-Domänencontroller, indem [folgendermaßen] (https://support.apple.com/kb/PH26282?viewlocale=en_US & Gebietsschema En_US =).



## <a name="configure-kdc-in-krb5conf"></a>Konfigurieren von KDC in krb5.conf

Bearbeiten der `/etc/krb5.conf` in einem Editor Ihrer Wahl. Konfigurieren Sie die folgenden Schlüssel

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

Speichern Sie die Datei krb5.conf, und beenden

> [!NOTE]
> Domäne muss in Großbuchstaben sein.


## <a name="test-the-ticket-granting-ticket-retrieval"></a>Testen Sie das Ticket Granting Ticket abrufen

Rufen Sie ein Ticket Ticket (TGT) vom KDC erteilen.

```bash
kinit username@DOMAIN.COMPANY.COM
```

Zeigen Sie die verfügbaren Tickets Kinit verwenden. Wenn die Kinit erfolgreich war, sollte ein Ticket angezeigt werden. 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-includename-sosincludesname-sos-shortmd"></a>Verbindung herstellen über[!INCLUDE[name-sos](../includes/name-sos-short.md)]

* Erstellen Sie ein neues Profil

* Wählen Sie **Windows-Authentifizierung** als Authentifizierungstyp

* Das Verbindungsprofil abgeschlossen ist, klicken Sie auf **verbinden**

Nachdem die Verbindung erfolgreich hergestellt, Ihre Server angezeigt wird, der *Server* Randleiste.
