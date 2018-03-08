---
title: Herstellen einer Verbindung mit SQLServer | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b6ad6278da1a3e325356058df51238dc34018bf0
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="connecting-to-sql-server"></a>Herstellen einer Verbindung mit SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

In diesem Thema wird erläutert, wie Sie eine Verbindung zu erstellen können ein [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datenbank.  
  
## <a name="connection-properties"></a>Verbindungseigenschaften  

Finden Sie unter [DSN und Schlüsselwörter für Verbindungszeichenfolgen und Attribute](../../../connect/odbc/dsn-connection-string-attribute.md) für die Schlüsselwörter für Verbindungszeichenfolgen und die Attribute, die auf Linux- und Macintosh unterstützt

> [!IMPORTANT]  
> Geben Sie beim Herstellen einer Verbindung mit einer Datenbank, welche Datenbankspiegelung verwendet (oder einen Failoverpartner hat), nicht den Namen der Datenbank in der Verbindungszeichenfolge an. Schicken Sie stattdessen eine **verwenden** *Database_name* Befehl aus, um mit der Datenbank zu verbinden, bevor Sie Ihre Abfragen ausführen.  
  
Der an übergebene Wert den **Treiber** Schlüsselwort kann eines der folgenden sein:  
  
-   Der Name, den Sie verwendet haben, als Sie den Treiber installiert haben.

-   Der Pfad der Treiber-Bibliothek, die in die INI-Datei der Vorlage verwendet, um den Treiber installieren angegeben wurde.  

Um ein DSN zu erstellen, erstellen Sie (falls erforderlich), und bearbeiten Sie die Datei **~/.odbc.ini** (`.odbc.ini` in Ihrem Basisverzeichnis) für einen Benutzer-DSN, der Zugriff nur für den aktuellen Benutzer oder `/etc/odbc.ini` für ein System-DSN (Administratorrechte erforderlich.) Im folgenden finden eine Beispieldatei, die die minimal erforderlichen Einträge für eine DSN zeigt:  

```  
[MSSQLTest]  
Driver = ODBC Driver 13 for SQL Server  
Server = [protocol:]server[,port]  
#   
# Note:  
# Port is not a valid keyword in the odbc.ini file  
# for the Microsoft ODBC driver on Linux or macOS
#  
```  

Sie können optional das Protokoll und den Port für die Verbindung mit dem Server angeben. Beispielsweise **Server = Tcp:***Servername***, 12345**. Beachten Sie, dass das einzige Protokoll unterstützt, indem Sie die Treiber für Linux und MacOS `tcp`.

Verwenden Sie zum Verbinden mit einer benannten Instanz auf einen statischen Port <b>Server =</b>*Servername*,**Port_number**. Herstellen einer Verbindung mit einem dynamischen Port wird nicht unterstützt.  

Alternativ Sie können die DSN-Informationen in einer Vorlagendatei hinzufügen, und führen Sie den folgenden Befehl zum Hinzufügen `~/.odbc.ini` :
 - **Odbcinst -i -s -f** *Template_file*  
 
Sie können überprüfen, ob Ihr Treiber funktioniert mit `isql` So testen Sie die Verbindung, oder Sie können diesen Befehl verwenden:
 - **Bcp-master.INFORMATION_SCHEMA.TABLES out OutFile.dat -S <server> - U <name> - P<password>**  

## <a name="using-secure-sockets-layer-ssl"></a>Secure Sockets Layer (SSL) verwenden  
Sie können Secure Sockets Layer (SSL) zum Verschlüsseln von Verbindungen mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. SSL schützt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Benutzernamen und Kennwörter über das Netzwerk. SSL überprüft auch die Identität des Servers, um Schutz vor „man-in-the-middle“-Attacken (MITM) zu bieten.  

Das Aktivieren der Verschlüsselung erhöht die Sicherheit auf Kosten der Leistung.

Weitere Informationen finden Sie unter [Verschlüsseln von Verbindungen zu SQL Server](http://go.microsoft.com/fwlink/?LinkId=220900) und [mithilfe von Verschlüsselung ohne Überprüfung](https://docs.microsoft.com/en-us/sql/relational-databases/native-client/features/using-encryption-without-validation).

Unabhängig von den Einstellungen für **Encrypt** und **TrustServerCertificate**werden die Serveranmeldeinformationen (Benutzername und Kennwort) immer verschlüsselt. Die folgende Tabelle zeigt den Effekt der Einstellungen für **Encrypt** und **TrustServerCertificate** .  

||**TrustServerCertificate=no**|**"TrustServerCertificate" = Ja**|  
|-|-------------------------------------|------------------------------------|  
|**Encrypt=no**|Das Serverzertifikat wird nicht überprüft.<br /><br />Zwischen dem Client und dem Server verschickte Daten sind nicht verschlüsselt.|Das Serverzertifikat wird nicht überprüft.<br /><br />Zwischen dem Client und dem Server verschickte Daten sind nicht verschlüsselt.|  
|**Verschlüsseln = Ja**|Serverzertifikat wird überprüft.<br /><br />Zwischen dem Client und dem Server verschickte Daten sind verschlüsselt.<br /><br />Der Name (oder die IP-Adresse) in einem Antragsteller Common Name (CN) oder als alternativen Antragstellernamen (SAN) in einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL-Zertifikat sollte genau übereinstimmen, die Server Name (oder IP-Adresse) in der Verbindungszeichenfolge angegeben.|Das Serverzertifikat wird nicht überprüft.<br /><br />Zwischen dem Client und dem Server verschickte Daten sind verschlüsselt.|  

Standardmäßig überprüfen verschlüsselte Verbindungen immer das Zertifikat des Servers. Allerdings auch hinzufügen, wenn Sie eine Verbindung mit einem Server herzustellen, ein selbst signiertes Zertifikat ist, das `TrustServerCertificate` Option, überprüfen das Zertifikat anhand der Liste vertrauenswürdiger Zertifizierungsstellen zu umgehen:  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
SSL verwendet die OpenSSL-Bibliothek. Die folgende Tabelle zeigt die minimalen unterstützten Versionen von OpenSSL und die Zertifikatsvertrauensspeicherorte für jede Plattform:

|Platform|Minimale OpenSSL-Version|Standard-Zertifikatsvertrauensspeicherort|  
|------------|---------------------------|--------------------------------------------|
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71 |1.0.1|/etc/ssl/certs|
|macOS 10.13|1.0.2|/usr/local/etc/openssl/certs|
|macOS 10.12|1.0.2|/usr/local/etc/openssl/certs|
|OS X 10.11|1.0.2|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 12 |1.0.1|/etc/ssl/certs|
|SuSE Linux Enterprise 11 |0.9.8|/etc/ssl/certs|
|Ubuntu 17.10 |1.0.2|/etc/ssl/certs|
|Ubuntu 16.10 |1.0.2|/etc/ssl/certs|
|Ubuntu 16.04 |1.0.2|/etc/ssl/certs|
  
Sie können die Verschlüsselung auch angeben, in die Verbindungszeichenfolge mithilfe der `Encrypt` option bei Verwendung **SQLDriverConnect** eine Verbindung herstellen.

## <a name="see-also"></a>Siehe auch  
[Installieren von Microsoft ODBC Driver für SQL Server unter Linux und macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[Programmierrichtlinien](../../../connect/odbc/linux-mac/programming-guidelines.md)
