---
title: Herstellen einer Verbindung mit einer Azure SQL-Datenbank | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 49645b1f-39b1-4757-bda1-c51ebc375c34
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 454dbfc43af720a7c2bb8c875c0e119437dc4d92
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-an-azure-sql-database"></a>Herstellen einer Verbindung mit einer Azure SQL-Datenbank
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  In diesem Thema werden Probleme behandelt, bei Verwendung der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] zur Verbindung mit einem [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]. Weitere Informationen zum Verbinden mit einem [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], finden Sie unter:  
  
-   [SQL Azure-Datenbank](http://go.microsoft.com/fwlink/?LinkID=202490)  
  
-   [Vorgehensweise: Herstellen einer Verbindung mit SQL Azure mithilfe von JDBC](http://msdn.microsoft.com/library/gg715284.aspx)  
  
-   [Verwenden von SQL Azure in Java](http://msdn.microsoft.com/library/windowsazure/hh749029(VS.103).aspx)

-   [Connecting using Azure Active Directory Authentication (Herstellen einer Verbindung mithilfe der Azure Active Directory-Authentifizierung)](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)  
  
## <a name="details"></a>Details  
 Beim Herstellen einer Verbindung mit einem [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], Sie müssen eine Verbindung mit der master-Datenbank aufrufen **SQLServerDatabaseMetaData.getCatalogs**.  
 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] die Rückgabe sämtlicher Kataloge aus einer Benutzerdatenbank unterstützt nicht. **SQLServerDatabaseMetaData.getCatalogs** verwendet die sys.databases-Sicht, um die Kataloge abzurufen. Finden Sie in der Beschreibung der Berechtigungen in [sys.databases (SQL Azure-Datenbank)](http://go.microsoft.com/fwlink/?LinkId=217396) verstehen **SQLServerDatabaseMetaData.getCatalogs** Verhalten auf ein [!INCLUDE[ssAzure](../../includes/ssazure_md.md)].  
  
 Getrennte Verbindungen  
 Beim Herstellen einer Verbindung mit einem [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], Verbindungen im Leerlauf können nach einem Zeitraum der Inaktivität durch eine Netzwerkkomponente (z. B. eine Firewall) getrennt werden. In diesem Kontext werden zwei Arten von inaktiven Verbindungen behandelt:  
  
-   Inaktive Verbindungen auf der TCP-Ebene, wobei Verbindungen von einer beliebigen Anzahl von Netzwerkgeräten gelöscht werden können.  
  
-   Durch das SQL Azure-Gateway im Leerlauf befindet, auf dem TCP **"Keepalive"** -Meldungen möglicherweise (Hierdurch wird die Verbindung aus TCP-Sicht nicht inaktiv), jedoch wurde nicht in 30 Minuten keine aktive Abfrage. In diesem Szenario wird durch das Gateway ermittelt, ob die TDS-Verbindung 30 Minuten inaktiv war, und die Verbindung wird beendet.  
  
 Um zu vermeiden, dass Verbindungen im Leerlauf durch eine Netzwerkkomponente getrennt werden, sollten die folgenden Registrierungseinstellungen (bzw. deren Nicht-Windows-Äquivalente) für das Betriebssystem festgelegt werden, unter dem der Treiber geladen wurde:  
  
|Registrierungseinstellung|Empfohlener Wert|  
|----------------------|-----------------------|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Dienste \ Tcpip \ Parameter \ KeepAliveTime|30000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Dienste \ Tcpip \ Parameter \ KeepAliveInterval|1000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Dienste \ Tcpip \ Parameter \ TcpMaxDataRetransmissions|10|  
  
 Anschließend müssen Sie den Computer neu starten, damit die Registrierungseinstellungen wirksam werden.  
  
 Um diese Aktion in Windows Azure auszuführen, erstellen Sie einen Starttask, durch den die Registrierungsschlüssel hinzugefügt werden.  Fügen Sie der Dienstdefinitionsdatei beispielsweise folgenden Starttask hinzu:  
  
```  
<Startup>  
    <Task commandLine="AddKeepAlive.cmd" executionContext="elevated" taskType="simple">  
    </Task>  
</Startup>  
```  
  
 Fügen Sie dem Projekt anschließend die Datei „AddKeepAlive.cmd“ hinzu. Legen Sie die Einstellung „In Ausgabeverzeichnis kopieren“ auf „Immer kopieren“ fest. Das folgende Beispiel veranschaulicht eine Datei „AddKeepAlive.cmd“:  
  
```  
if exist keepalive.txt goto done  
time /t > keepalive.txt  
REM Workaround for JDBC keep alive on SQL Azure  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveTime /t REG_DWORD /d 30000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveInterval /t REG_DWORD /d 1000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v TcpMaxDataRetransmissions /t REG_DWORD /d 10 >> keepalive.txt  
shutdown /r /t 1  
:done  
```  
  
 Anfügen des Servernamens an die UserId in der Verbindungszeichenfolge  
 Vor Version 4.0 die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]beim Herstellen einer Verbindung mit einer [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], mussten Sie, den Servernamen an die UserId in der Verbindungszeichenfolge angefügt werden soll. Beispiel: user@servername. Ab Version 4.0 von der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], es ist nicht mehr erforderlich, anzufügende @servername an die UserId in der Verbindungszeichenfolge angegeben.  
  
 Einstellung "hostNameInCertificate" zur Verwendung der Verschlüsselung erforderlich  
 Beim Herstellen einer Verbindung mit einer [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], geben Sie **HostNameInCertificate** bei Angabe von **Verschlüsseln = "true"**. (Wenn der Servername in der Verbindungszeichenfolge ist *ShortName*. *DomainName*legen die **HostNameInCertificate** Eigenschaft \*. *DomainName*.)  
  
 Beispiel:  
  
```  
jdbc:sqlserver://abcd.int.mscds.com;databaseName= myDatabase;user=myName;password=myPassword;encrypt=true;hostNameInCertificate= *.int.mscds.com;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verbinden von SQL Server mit dem JDBC-Treiber](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
