---
title: "Verschlüsseln von Verbindungen zu SQLServer on Linux | Microsoft Docs"
description: "Dieses Thema beschreibt Verschlüsseln von Verbindungen zu SQL Server unter Linux."
author: tmullaney
ms.date: 10/02/2017
ms.author: meetb;rickbyh
manager: jhubbard
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
helpviewer_keywords:
- Linux, encrypted connections
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 41c2caf816ca412e4a6048713dc66f97da5155ae
ms.openlocfilehash: d6beb6350c0d48d35cb3153c2df8eebaec0e4f34
ms.contentlocale: de-de
ms.lasthandoff: 10/07/2017

---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>Verschlüsseln von Verbindungen zu SQLServer on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]unter Linux können Transport Layer Security (TLS) zum Verschlüsseln von Daten, die in einem Netzwerk zwischen einer Clientanwendung und einer Instanz von übertragenen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]unterstützt die gleichen TLS-Protokolle unter Windows und Linux: TLS 1.2, 1.1 und 1.0. Die Schritte zum Konfigurieren von TLS sind jedoch speziell für das Betriebssystem auf dem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ausgeführt wird.  

## <a name="requirements-for-certificates"></a>Anforderungen für Zertifikate 
Bevor wir beginnen, müssen Sie sicherstellen, dass Ihre Zertifikate die folgenden Voraussetzungen erfüllen:
- Die aktuelle Systemzeit muss hinter der gültig von-Eigenschaft des Zertifikats und vor gültig bis-Eigenschaft des Zertifikats sein.
- Das Zertifikat muss für die Serverauthentifizierung vorgesehen sein. Dies erfordert die Enhanced Key Usage-Eigenschaft des Zertifikats Serverauthentifizierung (1.3.6.1.5.5.7.3.1) angeben.
- Das Zertifikat muss mit der Option KeySpec AT_KEYEXCHANGE erstellt werden. Das Zertifikat schlüsselverwendungseigenschaft (KEY_USAGE) gehören in der Regel auch Schlüsselverschlüsselung (CERT_KEY_ENCIPHERMENT_KEY_USAGE).
- Der Subject-Eigenschaft des Zertifikats muss angeben, dass der allgemeine Name (CN) als den Hostnamen oder den vollqualifizierten Domänennamen (FQDN) des Servercomputers übereinstimmt. Hinweis: Zertifikate mit Platzhalter werden unterstützt. 

## <a name="overview"></a>Übersicht
TLS ist zum Verschlüsseln von Verbindungen von einer Clientanwendung zum [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Bei ordnungsgemäßer Konfiguration bietet TLS Vertraulichkeit und Integrität der Daten für die Kommunikation zwischen dem Client und dem Server.  TLS-Verbindungen können entweder Client Intiated oder Server Initited sein. 


## <a name="client-initiated-encryption"></a>Vom Client initiierte Verschlüsselung 
- **Generieren Sie ein Zertifikat** (CN übereinstimmen, vollqualifizierten Domänennamen der SQL Server-Hostname)

> [!NOTE]
> Für dieses Beispiel, dass wir ein selbstsigniertes Zertifikat verwenden sollte dies nicht für Produktionsszenarien verwendet werden. Sie sollten ZS-Zertifikate verwenden. 

        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **Konfigurieren von SQLServer**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0 

- **Registrieren des Zertifikats auf dem Clientcomputer (Windows, Linux oder MacOS)**

    -   Bei Verwendung von Zertifizierungsstelle signiertes Zertifikat müssen Sie das Zertifikat (Certificate Authority, CA), anstatt das Zertifikat auf den Clientcomputer kopiert. 
    -   Wenn Sie das selbstsignierte Zertifikat nur verwenden, kopieren Sie die PEM-Datei in die folgenden Ordner je nach Verteilung, und führen Sie die Befehle aktivieren 
        - **Ubuntu** : Copy-Zertifikat- ```/usr/share/ca-certificates/``` umbenennen Erweiterung .crt verwenden Dpkg Reconfigure Zertifizierungsstellenzertifikate, um ihn als System CA-Zertifikat zu aktivieren. 
        - **RHEL** : Copy-Zertifikat- ```/etc/pki/ca-trust/source/anchors/``` verwenden ```update-ca-trust``` um ihn als System CA-Zertifikat zu aktivieren.
        - **SUSE** : Copy-Zertifikat- ```/usr/share/pki/trust/anchors/``` verwenden ```update-ca-certificates``` ermöglichen dem System CA-Zertifikat.
        - **Windows**: importieren, die die PEM-Datei als ein Zertifikat unter "aktuelle Benutzer" -> vertrauenswürdiger Stammzertifizierungsstellen-Zertifikate >
        - **MacOS**: 
           - Kopieren Sie das Zertifikat an```/usr/local/etc/openssl/certs```
           - Führen Sie den folgenden Befehl aus, um den Hashwert abzurufen:```/usr/local/Cellar/openssql/1.0.2l/openssql x509 -hash -in mssql.pem -noout```
           - Benennen Sie das Zertifikat in Wert. Beispiel: ```mv mssql.pem dc2dd900.0``` Stellen Sie sicher, dass dc2dd900.0 wird```/usr/local/etc/openssl/certs```
    
-   **Exemplarische Verbindungszeichenfolgen** 

    - **[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]**   
  ![SSMS-Verbindungsdialogfeld](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "SSMS-Verbindungsdialogfeld")  
  
    - **SQLCMD** 

            sqlcmd  -S <sqlhostname> -N -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=True; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=Yes; TrustServerCertificate=no;" 
    - **JDBC** 
    
            "encrypt=true; trustServerCertificate=false;" 

## <a name="server-initiated-encryption"></a>Vom Server initiierte Verschlüsselung 

- **Generieren Sie ein Zertifikat** (CN übereinstimmen, vollqualifizierten Domänennamen der SQL Server-Hostname)
        
        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **Konfigurieren von SQLServer**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1 
        
-   **Exemplarische Verbindungszeichenfolgen** 

    - **SQLCMD**

            sqlcmd  -S <sqlhostname> -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=False; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=no; TrustServerCertificate=no;"  
    - **JDBC** 
    
            "encrypt=false; trustServerCertificate=false;" 
            
> [!NOTE]
> Legen Sie **"TrustServerCertificate"** auf "true", wenn der Client überprüft die Echtheit des Zertifikats der Zertifizierungsstelle hergestellt werden kann

## <a name="common-connection-errors"></a>Allgemeine Verbindungsfehler  

|Fehlermeldung |Fix |
|--- |--- |
|Die Zertifikatkette wurde von einer Zertifizierungsstelle ausgestellt, die nicht vertrauenswürdig ist.  |Dieser Fehler tritt auf, wenn von Clients kann nicht zum Überprüfen der Signatur des Zertifikats durch SQL Server während der TLS-Handshake dargestellt wird. Stellen Sie sicher, dass der Client vertraut wird entweder die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] direkt Zertifikat oder der Zertifizierungsstelle, die das SQL Server-Zertifikat signiert. |
|Der Zielprinzipalname ist falsch.  |Stellen Sie sicher, dass allgemeine Namensfeld für SQL Server Zertifikat in der Client-Verbindungszeichenfolge angegebene Servername entspricht. |  
|Eine vorhandene Verbindung wurde vom Remotehost geschlossen. |Dieser Fehler kann auftreten, wenn der Client die TLS-Protokollversion, die erforderlich sind, von SQL Server nicht unterstützt. Z. B. wenn [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] TLS 1.2 erfordern, stellen Sie sicher, dass Ihre Clients unterstützen auch das TLS 1.2-Protokoll konfiguriert ist. |
| | |   

