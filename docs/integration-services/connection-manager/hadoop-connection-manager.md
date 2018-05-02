---
title: Hadoop-Verbindungs-Manager – SQL Server Integration Services | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ssis.designer.hadoopconn.f1
ms.assetid: 8bb15b97-9827-46bc-aca6-068534ab18c4
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 666bf41b06b8b1f64e191294ec05ec789080b740
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="hadoop-connection-manager"></a>Hadoop-Verbindungs-Manager
  Der Hadoop-Verbindungs-Manager ermöglicht die Verbindung eines SSIS-Pakets (SQL Server Integration Services) mit einem Hadoop-Cluster mithilfe der Werte, die Sie für die Eigenschaften angeben.  
  
## <a name="configure-the-hadoop-connection-manager"></a>Konfigurieren des Hadoop-Verbindungs-Managers  
  
1.  Wählen Sie im Dialogfeld **SSIS-Verbindungs-Manager hinzufügen** die Optionen **Hadoop** > **Hinzufügen** aus. Der **Hadoop-Verbindungs-Manager-Editor** wird geöffnet.  
  
2.  Um entsprechende Hadoop-Clusterinformationen zu konfigurieren, wählen Sie im linken Bereich die Registerkarte **WebHCat** oder **WebHDFS** aus.
  
3.  Wenn Sie die Option **WebHCat** aktivieren, um einen Hive- oder Pig-Auftrag in Hadoop aufzurufen, gehen Sie folgendermaßen vor: 
  
    1.  Geben Sie für **WebHCat-Host** den Server ein, der den WebHCat-Dienst hostet.  
  
    2.  Geben Sie für **WebHCat Port**den Port des WebHCat-Diensts ein. Dies ist standardmäßig 50111.  
  
    3.  Wählen Sie unter **Authentication** die Zugriffsmethode für den WebHCat-Dienst auf. Die verfügbaren Werte sind **Basic** und **Kerberos**.  
  
         ![Screenshot des Editors für den Hadoop-Verbindungs-Manager mit Standardauthentifizierung](../../integration-services/connection-manager/media/hadoop-cm-basic.png "Hadoop connection manager editor with basic authentication")  
  
         ![Screenshot des Editors für den Hadoop-Verbindungs-Manager mit Kerberos-Authentifizierung](../../integration-services/connection-manager/media/hadoop-cm-kerberos.png "Hadoop connection manager editor with Kerberos authentication")  
  
    4.  Geben Sie für **WebHCat User**im Feld **User** den für den Zugriff auf WebHCat autorisierten Benutzer ein.  
  
    5.  Wenn Sie als Authentifizierungsoption **Kerberos** wählen, geben Sie in die Felder **Password** und **Domain**das Kennwort und die Domäne des Benutzers ein.  
  
4.  Wenn Sie die Option **WebHDFS** aktivieren, um Daten aus oder in HDFS zu kopieren, gehen Sie folgendermaßen vor: 
  
    1.  Geben Sie für **WebHDFS Host**den Server ein, der den WebHDFS-Dienst hostet.  
  
    2.  Geben Sie für **WebHDFS Port**den Port des WebHDFS-Diensts ein. Dies ist standardmäßig 50070.  
  
    3.  Wählen Sie unter **Authentication** die Zugriffsmethode für den WebHDFS-Dienst aus. Die verfügbaren Werte sind **Basic** und **Kerberos**.  
  
    4.  Geben Sie für **WebHDFS User**den für den Zugriff auf HDFS autorisierten Benutzer ein.  
  
    5.  Wenn Sie als Authentifizierungsoption **Kerberos** wählen, geben Sie in die Felder **Password** und **Domain**das Kennwort und die Domäne des Benutzers ein.  
  
5.  Klicken Sie auf **Verbindung testen**. (Nur die Verbindung, die Sie aktiviert, wird getestet.)  
  
6.  Wählen Sie **OK** aus, um das Dialogfeld zu schließen.  

## <a name="connect-with-kerberos-authentication"></a>Herstellen einer Verbindung mit der Kerberos-Authentifizierung
Es gibt zwei Möglichkeiten, um die lokale Umgebung für die Verwendung der Kerberos-Authentifizierung mit dem Hadoop-Verbindungs-Manager einzurichten. Sie können die Option wählen, die besser auf Ihre Anforderungen zugeschnitten ist.
-   Option 1: [Einbinden des SSIS-Computers in den Kerberos-Bereich](#kerberos-join-realm)
-   Option 2: [Aktivieren von gegenseitiger Vertrauensstellung zwischen der Windows-Domäne und dem Kerberos-Bereich](#kerberos-mutual-trust)

### <a name="kerberos-join-realm"></a>Option 1: Einbinden des SSIS-Computers in den Kerberos-Bereich

#### <a name="requirements"></a>Anforderungen:

-   Der Gatewaycomputer muss in den Kerberos-Bereich eingebunden und kann nicht in Windows-Domänen eingebunden werden.

#### <a name="how-to-configure"></a>Vorgehensweise zur Konfiguration:

Gehen Sie auf dem SSIS-Computer wie folgt vor:

1.  Führen Sie das **Ksetup**-Hilfsprogramm aus, um den Kerberos-KDC-Server (Key Distribution Center) und -Bereich zu konfigurieren.

    Der Computer muss als Mitglied einer Arbeitsgruppe konfiguriert werden, da sich ein Kerberos-Bereich von einer Windows-Domäne unterscheidet. Legen Sie wie im folgenden Beispiel gezeigt den Kerberos-Bereich fest, und fügen Sie einen KDC-Server hinzu. Ersetzen Sie `REALM.COM` ggf. durch Ihren eigenen entsprechenden Bereich.

    ```    
    C:> Ksetup /setdomain REALM.COM`
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    ```

    Nachdem Sie diese Befehle ausgeführt haben, starten Sie den Computer neu.

2.  Überprüfen Sie die Konfiguration mit dem **Ksetup**-Befehl. Die Ausgabe sollte wie im folgenden Beispiel aussehen:

    ```
    C:> Ksetup
    default realm = REALM.COM (external)
    REALM.com:
        kdc = <your_kdc_server_address>
    ```

### <a name="kerberos-mutual-trust"></a>Option 2: Aktivieren von gegenseitiger Vertrauensstellung zwischen der Windows-Domäne und dem Kerberos-Bereich

#### <a name="requirements"></a>Anforderungen:
-   Der Gatewaycomputer muss in eine Windows-Domäne eingebunden werden.
-   Sie benötigen die Berechtigung zum Aktualisieren der Einstellungen des Domänencontrollers.

#### <a name="how-to-configure"></a>Vorgehensweise zur Konfiguration:

> [!NOTE]
> Ersetzen Sie `REALM.COM` und `AD.COM` im folgenden Tutorial ggf. durch Ihren eigenen Bereich und Domänencontroller.

Gehen Sie auf dem KDC-Server wie folgt vor:

1.  Bearbeiten Sie die KDC-Konfiguration in der Datei **krb5.conf**. Erlauben Sie KDC, der Windows-Domäne zu vertrauen, indem Sie auf die folgende Konfigurationsvorlage verweisen. Standardmäßig befindet sich die Konfiguration unter **/etc/krb5.conf**.

    ```
    [logging]
    default = FILE:/var/log/krb5libs.log
    kdc = FILE:/var/log/krb5kdc.log
    admin_server = FILE:/var/log/kadmind.log

    [libdefaults]
    default_realm = REALM.COM
    dns_lookup_realm = false
    dns_lookup_kdc = false
    ticket_lifetime = 24h
    renew_lifetime = 7d
    forwardable = true

    [realms]
    REALM.COM = {
        kdc = node.REALM.COM
        admin_server = node.REALM.COM
        }
    AD.COM = {
        kdc = windc.ad.com
        admin_server = windc.ad.com
        }

    [domain_realm]
    .REALM.COM = REALM.COM
    REALM.COM = REALM.COM
    .ad.com = AD.COM
    ad.com = AD.COM

    [capaths]
    AD.COM = {
        REALM.COM = .
        }
    ```

    Starten Sie den KDC-Dienst nach der Konfiguration neu.

2.  Bereiten Sie einen Prinzipal mit dem Namen **krbtgt/REALM.COM@AD.COM** auf dem KDC-Server vor. Verwenden Sie den folgenden Befehl:

    `Kadmin> addprinc krbtgt/REALM.COM@AD.COM`

3.  Fügen Sie `RULE:[1:$1@$0](.*@AD.COM)s/@.*//` zur HDFS-Dienstkonfigurationsdatei **hadoop.security.auth_to_local** hinzu.

Gehen Sie auf dem Domänencontroller wie folgt vor:

1.  Führen Sie die folgenden **Ksetup**-Befehle aus, um einen Bereichseintrag hinzuzufügen:

    ```
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
    ```

2.  Stellen Sie Vertrauensstellung zwischen der Windows-Domäne und dem Kerberos-Bereich her. Im folgenden Beispiel ist `[password]` das Kennwort für den Prinzipal **krbtgt/REALM.COM@AD.COM**.

    `C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /password:[password]`

3.  Wählen Sie einen Verschlüsselungsalgorithmus für die Verwendung mit Kerberos aus.

    1. Navigieren Sie zu **Server-Manager** > **Gruppenrichtlinienverwaltung** > **Domäne**. Wählen Sie in dieser Ansicht die Optionen **Gruppenrichtlinienobjekte** > **Standard- oder aktive Domänenrichtlinie** > **Bearbeiten**.

    2. Navigieren Sie im Popupfenster **Gruppenrichtlinienverwaltungs-Editor** zu **Computerkonfiguration** > **Richtlinien** > **Windows-Einstellungen**. Wählen Sie in dieser Ansicht die Optionen **Sicherheitseinstellungen** > **Lokale Richtlinien** > **Sicherheitsoptionen**. Konfigurieren Sie **Netzwerksicherheit: Für Kerberos zulässige Verschlüsselungstypen konfigurieren**.

    3. Wählen Sie den Verschlüsselungsalgorithmus aus, den Sie zum Herstellen einer Verbindung mit KDC verwenden möchten. In der Regel können Sie eine der Optionen auswählen.

        ![Screenshot der Verschlüsselungstypen für Kerberos](media/hadoop-connection-manager/config-encryption-types-for-kerberos.png)

    4. Verwenden Sie den **Ksetup**-Befehl, um den für den jeweiligen Bereich zu verwendenden Verschlüsselungsalgorithmus anzugeben.

        `C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96`

4.  Um den Kerberos-Prinzipal in der Windows-Domäne zu verwenden, erstellen Sie die Zuordnung zwischen dem Domänenkonto und dem Kerberos-Prinzipal.

    1. Navigieren Sie zu **Verwaltungstools** > **Active Directory-Benutzer und -Computer**.

    2. Konfigurieren Sie erweiterte Funktionen unter **Ansicht** > **Erweiterte Funktionen**.

    3. Suchen Sie das Konto, für das Sie Zuordnungen erstellen möchten, klicken Sie zum Anzeigen von **Namenszuordnungen** mit der rechten Maustaste darauf, und wählen Sie dann die Registerkarte **Kerberos-Namen** aus.

    4. Fügen Sie einen Prinzipal aus dem Bereich hinzu.

        ![Screenshot des Dialogfelds „Sicherheitsidentitätszuordnung“](media/hadoop-connection-manager/map-security-identity.png)

Gehen Sie auf dem Gatewaycomputer wie folgt vor:

Führen Sie die folgenden **Ksetup**-Befehle aus, um einen Bereichseintrag hinzuzufügen.

    ```
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
    ```

## <a name="see-also"></a>Siehe auch  
 [Hadoop Hive-Task](../../integration-services/control-flow/hadoop-hive-task.md)   
 [Hadoop Pig-Task](../../integration-services/control-flow/hadoop-pig-task.md)   
 [Hadoop-Dateisystemtask](../../integration-services/control-flow/hadoop-file-system-task.md)  
  
  
