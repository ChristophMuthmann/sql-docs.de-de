---
title: "Verschlüsseln von Verbindungen zu SQLServer on Linux | Microsoft Docs"
description: "Dieses Thema beschreibt Verschlüsseln von Verbindungen zu SQL Server unter Linux."
author: tmullaney
ms.date: 06/14/2017
ms.author: thmullan;rickbyh
manager: jhubbard
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
helpviewer_keywords:
- Linux, encrypted connections
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 47a15701730019aaf166743c47c606aa2059b7fe
ms.contentlocale: de-de
ms.lasthandoff: 08/28/2017

---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>Verschlüsseln von Verbindungen zu SQLServer on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]unter Linux können Transport Layer Security (TLS) zum Verschlüsseln von Daten, die in einem Netzwerk zwischen einer Clientanwendung und einer Instanz von übertragenen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]unterstützt die gleichen TLS-Protokolle unter Windows und Linux: TLS 1.2, 1.1 und 1.0. Die Schritte zum Konfigurieren von TLS sind jedoch speziell für das Betriebssystem auf dem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ausgeführt wird.  
 
## <a name="typical-scenario"></a>Typisches Szenario 
TLS ist zum Verschlüsseln von Verbindungen von einer Clientanwendung zum [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Bei ordnungsgemäßer Konfiguration bietet TLS Vertraulichkeit und Integrität der Daten für die Kommunikation zwischen dem Client und dem Server.  
Die folgenden Schritte beschreiben ein typisches Szenario:  

1. Datenbankadministrator generiert einen privaten Schlüssel und einer zertifikatsignierungsanforderung (CSR). Allgemeine Name der Zertifikatsignieranforderung sollte es sich um den Namen des Servers entsprechen, den Clients in ihrer SQL Server-Verbindungszeichenfolge angeben. Dieser allgemeine Name wird in der Regel den vollqualifizierten Domänennamen des der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Host. Um das gleiche Zertifikat für mehrere Server verwenden, können Sie einen Platzhalter in den allgemeinen Namen (z. B. `"*.contoso.com"` anstelle von `"node1.contoso.com"`).   
2. Die CSR ist eine Zertifizierungsstelle (CA) für die Signierung gesendet. Alle Clientcomputer, die Verbindung sollte die Zertifizierungsstelle vertrauenswürdig sein [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Die Zertifizierungsstelle gibt ein signiertes Zertifikat an den Datenbankadministrator.   
3. Datenbankadministrator konfiguriert [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] des privaten Schlüssels und das signierte Zertifikat für TLS-Verbindungen verwenden.   
4. Geben Sie die Clients `"Encrypt=True"` und `"TrustServerCertificate=False"` in ihrer Verbindungszeichenfolge angeben. (Die spezifischen Parameternamen möglicherweise variieren, je nachdem, welche Treiber verwendet wird). Jetzt versuchen Clients zunächst Verschlüsseln von Verbindungen zu SQL Server und überprüfen Sie die Gültigkeit des SQL Server Zertifikats, um Man-in-the-Middle-Angriffe zu verhindern.  
 
## <a name="configuring-tls-on-linux"></a>Konfigurieren von TLS unter Linux  

Verwendung `mssql-conf` so konfigurieren Sie TLS für eine Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf Linux ausgeführt wird. Die folgenden Optionen werden unterstützt:  

|Option |Description |
|--- |--- |
|`network.forceencryption` |Wenn der Wert 1, dann [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] erzwingt, dass alle Verbindungen verschlüsselt werden. Standardmäßig ist diese Option 0. |  
|`network.tlscert` |Der absolute Pfad zu dem Zertifikat-Datei mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für TLS-Verbindungen verwendet. Beispiel: `/etc/ssl/certs/mssql.pem` der Zertifikatsdatei muss der Mssql-Konto zugänglich sein. Microsoft empfiehlt, Einschränken des Zugriffs auf die Datei mit `chown mssql:mssql <file>; chmod 400 <file>`. |  
|`network.tlskey` |Der absolute Pfad zum privaten Schlüssel Datei, die mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für TLS-Verbindungen verwendet. Beispiel: `/etc/ssl/private/mssql.key` der Zertifikatsdatei muss der Mssql-Konto zugänglich sein. Microsoft empfiehlt, Einschränken des Zugriffs auf die Datei mit `chown mssql:mssql <file>; chmod 400 <file>`. | 
|`network.tlsprotocols` |Eine durch Trennzeichen getrennte Liste der TLS-Protokolle von SQL Server zulässig sind. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]immer versucht, die stärkste zulässige Protokoll ausgehandelt. Wenn ein Client ein zulässige Protokoll nicht unterstützt [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] lehnt der Verbindungsversuch fehl.  Aus Kompatibilitätsgründen sind alle unterstützten Protokolle (1,2, 1.1, 1.0) standardmäßig zulässig.  Wenn Ihre Clients TLS 1.2 unterstützt, empfiehlt Microsoft, sodass nur TLS 1.2. |  
|`network.tlsciphers` |Gibt an, welche Chiffren zulässig sind [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für TLS. Diese Zeichenfolge muss formatiert werden, pro [OpenSSLs-Chiffre Listenformat](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html). Im Allgemeinen müssen Sie nicht diese Option zu ändern. <br /> Standardmäßig sind die folgenden Chiffren zulässig: <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |   
| | |
 
## <a name="example"></a>Beispiel 
Dieses Beispiel verwendet ein selbst signiertes Zertifikat. In Produktionsszenarien normal würde das Zertifikat von einer Zertifizierungsstelle signiert werden, die von allen Clients als vertrauenswürdig eingestuft wird.  
 
### <a name="step-1-generate-private-key-and-certificate"></a>Schritt 1: Generieren von privaten Schlüssels und des Zertifikats 
Öffnen Sie einen Befehl Terminaldienste auf dem Linux-Computer, auf dem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ausgeführt wird. Führen Sie die folgenden Befehle ein:  

- Ein selbstsigniertes Zertifikat zu generieren. Stellen Sie sicher, dass die CN der SQL Server-Hostname erforderlichem vollqualifiziertem Domänennamen übereinstimmt. Sie können optional auch Platzhalter verwenden, z. B. `'/CN=*.contoso.com'`.    
   ```  
   openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
   ```  

- Beschränken des Zugriffs auf`mssql`  
   ```  
   sudo chown mssql:mssql mssql.pem mssql.key 
   sudo chmod 400 mssql.pem mssql.key 
   ```  
 
- Verschieben Sie den SSL-Dateisystemverzeichnissen (optional)  
   ```  
   sudo mv mssql.pem /etc/ssl/certs/ 
   sudo mv mssql.key /etc/ssl/private/ 
   ```  
 
### <a name="step-2-configure--includessnoversionincludesssnoversion-mdmd"></a>Schritt 2: Konfigurieren[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
Verwenden Sie `mssql-conf` so konfigurieren Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwenden das Zertifikat und Schlüssel für TLS. Zur Erhöhung der Sicherheit können Sie auch die TLS 1.2 als die einzige zulässige Protokoll festgelegt und erzwingen, dass alle Clients verschlüsselte Verbindungen verwenden.  

```  
sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1 
```
 
### <a name="step-3-restart-includessnoversionincludesssnoversion-mdmd"></a>Schritt 3: Starten Sie neu[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Neustart erforderlich, damit diese Änderungen wirksam werden.  
`sudo systemctl restart mssql-server`  
 
### <a name="step-4-copy-self-signed-certificate-to-client-machines"></a>Schritt 4: Kopieren Sie selbst signiertes Zertifikat auf den Clientcomputer 
Da in diesem Beispiel wird ein selbstsigniertes Zertifikat verwendet die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Host muss das Zertifikat (nicht den privaten Schlüssel) kopiert und installiert werden als ein vertrauenswürdiges Zertifikat auf allen Clientcomputern, die Verbindung [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Wenn das Zertifikat von einer Zertifizierungsstelle signiert ist, die von allen Clients bereits als vertrauenswürdig eingestuft wird, ist dieser Schritt nicht erforderlich. 
 
### <a name="step-5-connect-from-clients-using-tls"></a>Schritt 5: Verbinden von Clients mit TLS 
Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] von einem Client mit aktivierter Verschlüsselung und `TrustServerCertificate` festgelegt `False` in der Verbindungszeichenfolge angegeben. Hier sind einige Beispiele dafür, wie diese Parameter, die mit anderen Tools und Treiber angeben. 

sqlcmd  
`sqlcmd -N -C -S mssql.contoso.com -U sa -P '<YourPassword>'`  

[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]   
  ![SSMS-Verbindungsdialogfeld](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "SSMS-Verbindungsdialogfeld")  
  
ADO.NET  
`"Encrypt=true; TrustServerCertificate=true;"`  

ODBC   
`"Encrypt=yes; TrustServerCertificate=no;"`  

JDBC  
`"encrypt=true; trustServerCertificate=false;" `

 
## <a name="common-connection-errors"></a>Allgemeine Verbindungsfehler  

|Fehlermeldung |Fix |
|--- |--- |
|Die Zertifikatkette wurde von einer Zertifizierungsstelle ausgestellt, die nicht vertrauenswürdig ist.  |Dieser Fehler tritt auf, wenn von Clients kann nicht zum Überprüfen der Signatur des Zertifikats durch SQL Server während der TLS-Handshake dargestellt wird. Stellen Sie sicher, dass der Client vertraut wird entweder die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] direkt Zertifikat oder der Zertifizierungsstelle, die das SQL Server-Zertifikat signiert. |
|Der Zielprinzipalname ist falsch.  |Stellen Sie sicher, dass allgemeine Namensfeld für SQL Server Zertifikat in der Client-Verbindungszeichenfolge angegebene Servername entspricht. |  
|Eine vorhandene Verbindung wurde vom Remotehost geschlossen. |Dieser Fehler kann auftreten, wenn der Client die TLS-Protokollversion, die erforderlich sind, von SQL Server nicht unterstützt. Z. B. wenn [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] TLS 1.2 erfordern, stellen Sie sicher, dass Ihre Clients unterstützen auch das TLS 1.2-Protokoll konfiguriert ist. |
| | |   


