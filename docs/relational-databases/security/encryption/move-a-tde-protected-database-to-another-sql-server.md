---
title: "Verschieben einer TDE-geschützten Datenbank auf einen anderen SQL-Server | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Transparent Data Encryption, moving
- TDE, moving a database
ms.assetid: fb420903-df54-4016-bab6-49e6dfbdedc7
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 61dab0bbd770679206c7eebee438f2fa22807ac2
ms.lasthandoff: 04/11/2017

---
# <a name="move-a-tde-protected-database-to-another-sql-server"></a>Verschieben einer TDE-geschützten Datenbank auf einen anderen SQL-Server
  In diesem Thema wird die Vorgehensweise zum Schutz einer Datenbank anhand transparenter Datenverschlüsselung (TDE) und das Verschieben der Datenbank in eine andere Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]beschrieben. Die TDE führt die E/A-Verschlüsselung und -Entschlüsselung der Daten und der Protokolldateien in Echtzeit durch. Die Verschlüsselung verwendet einen Verschlüsselungsschlüssel für die Datenbank (Database Encryption Key, DEK), der in der Datenbankstartseite gespeichert wird, damit er während der Wiederherstellung verfügbar ist. Der DEK ist ein symmetrischer Schlüssel, der durch ein in der **master** -Datenbank des Servers gespeichertes Zertifikat gesichert wird, oder ein asymmetrischer Schlüssel, der von einem EKM-Modul geschützt wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So erstellen Sie eine durch transparente Datenverschlüsselung geschützte Datenbank mit**  
  
     [SQL Server Management Studio](#SSMSCreate)  
  
     [Transact-SQL](#TsqlCreate)  
  
-   **So verschieben Sie eine Datenbank mit**  
  
     [SQL Server Management Studio](#SSMSMove)  
  
     [Transact-SQL](#TsqlMove)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Beim Verschieben einer TDE-geschützten Datenbank muss auch das Zertifikat oder der asymmetrische Schlüssel verschoben werden, mit dem der DEK geöffnet wird. Das Zertifikat oder der asymmetrische Schlüssel muss in der **Masterdatenbank** des Zielservers installiert sein, damit von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf die Datenbankdateien zugegriffen werden kann. Weitere Informationen finden Sie unter [Transparente Datenverschlüsselung &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md).  
  
-   Bewahren Sie Kopien der Zertifikatdatei und der Datei mit dem privaten Schlüssel auf, um das Zertifikat wiederherzustellen. Das Kennwort für den privaten Schlüssel muss nicht mit dem Kennwort für den Datenbank-Hauptschlüssel übereinstimmen.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQL Server speichert die hier erstellten Dateien standardmäßig in **C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA** . Die Dateinamen und -orte können individuell abweichen.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
  
-   Erfordert **CONTROL DATABASE** -Berechtigung für die **Masterdatenbank** , um den Datenbankhauptschlüssel zu erstellen.  
  
-   Erfordert **CREATE CERTIFICATE** -Berechtigung für die **Masterdatenbank** , um das Zertifikat zu erstellen, von dem der DEK geschützt wird.  
  
-   Erfordert die **CONTROL DATABASE** -Berechtigung für die verschlüsselte Datenbank und die **VIEW DEFINITION** -Berechtigung für das Zertifikat oder den asymmetrischen Schlüssel, die zum Verschlüsseln des Verschlüsselungsschlüssels für die Datenbank verwendet werden.  
  
##  <a name="SSMSProcedure"></a> So erstellen Sie eine durch transparente Datenverschlüsselung geschützte Datenbank  
  
###  <a name="SSMSCreate"></a> Verwendung von SQL Server Management Studio  
  
1.  Erstellen Sie einen Datenbank-Hauptschlüssel und ein Zertifikat in der **master** -Datenbank. Weitere Informationen finden Sie weiter unten unter **Verwenden von Transact-SQL** .  
  
2.  Erstellen Sie eine Sicherung des Serverzertifikats in der **Masterdatenbank** . Weitere Informationen finden Sie weiter unten unter **Verwenden von Transact-SQL** .  
  
3.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Ordner **Datenbanken** , und klicken Sie dann auf **Neue Datenbank**.  
  
4.  Geben Sie im Dialogfeld **Neue Datenbank** in das Feld **Datenbankname** den Namen der neuen Datenbank ein.  
  
5.  Geben Sie im Feld **Besitzer** den Namen des Besitzers der neuen Datenbank ein. Klicken Sie alternativ auf die Auslassungspunkte **(…)** , um das Dialogfeld **Datenbankbesitzer auswählen** zu öffnen. Weitere Informationen zum Erstellen einer neuen Datenbank finden Sie unter [Create a Database](../../../relational-databases/databases/create-a-database.md).  
  
6.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um den Ordner **Datenbank** zu erweitern.  
  
7.  Klicken Sie mit der rechten Maustaste auf die Datenbank, die Sie erstellt haben, zeigen Sie auf **Tasks**, und wählen Sie **Datenbankverschlüsselung verwalten**aus.  
  
     Die folgenden Optionen sind im Dialogfeld **Datenbankverschlüsselung verwalten** verfügbar.  
  
     **Verschlüsselungsalgorithmus**  
     Zeigt den für die Datenbankverschlüsselung zu verwendenden Algorithmus an oder legt ihn fest. Der Standardalgorithmus ist**AES128** . Dieses Feld darf nicht leer sein. Weitere Informationen zur Verschlüsselung von Algorithmen finden Sie unter [Choose an Encryption Algorithm](../../../relational-databases/security/encryption/choose-an-encryption-algorithm.md).  
  
     **Serverzertifikat verwenden**  
     Legt fest, dass die Verschlüsselung durch ein Zertifikat gesichert wird. Wählen Sie einen Eintrag aus der Liste aus. Wenn Sie nicht über die Berechtigung **VIEW DEFINITION** verfügen, ist diese Liste leer. Wenn als Verschlüsselungsmethode das Zertifikat ausgewählt wird, darf dieser Wert nicht leer sein. Weitere Informationen zu Zertifikaten finden Sie unter [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
     **Asymmetrischen Serverschlüssel verwenden**  
     Legt fest, dass die Verschlüsselung durch einen asymmetrischen Schlüssel gesichert wird. Nur verfügbare asymmetrische Schlüssel werden angezeigt. Nur ein asymmetrischer von einem EKM-Modul geschützter Schlüssel kann mit TDE eine Datenbank verschlüsseln.  
  
     **Datenbankverschlüsselung aktivieren**  
     Ändert die Datenbank, um TDE zu aktivieren bzw. zu deaktivieren.  
  
8.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
###  <a name="TsqlCreate"></a> Verwenden von Transact-SQL  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Create a database master key and a certificate in the master database.  
    USE master ;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1';  
    GO  
    CREATE CERTIFICATE TestSQLServerCert   
    WITH SUBJECT = 'Certificate to protect TDE key'  
    GO  
    -- Create a backup of the server certificate in the master database.  
    -- The following code stores the backup of the certificate and the private key file in the default data location for this instance of SQL Server   
    -- (C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA).  
  
    BACKUP CERTIFICATE TestSQLServerCert   
    TO FILE = 'TestSQLServerCert'  
    WITH PRIVATE KEY   
    (  
        FILE = 'SQLPrivateKeyFile',  
        ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1'  
    );  
    GO  
    -- Create a database to be protected by TDE.  
    CREATE DATABASE CustRecords ;  
    GO  
    -- Switch to the new database.  
    -- Create a database encryption key, that is protected by the server certificate in the master database.   
    -- Alter the new database to encrypt the database using TDE.  
    USE CustRecords;  
    GO  
    CREATE DATABASE ENCRYPTION KEY  
    WITH ALGORITHM = AES_128  
    ENCRYPTION BY SERVER CERTIFICATE TestSQLServerCert;  
    GO  
    ALTER DATABASE CustRecords  
    SET ENCRYPTION ON;  
    GO  
    ```  
  
 Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-certificate-transact-sql.md)  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
-   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)  
  
-   [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)  
  
##  <a name="TsqlProcedure"></a> So verschieben Sie eine Datenbank  
  
###  <a name="SSMSMove"></a> Verwendung von SQL Server Management Studio  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste, auf die oben verschlüsselte Datenbank, zeigen Sie auf **Tasks** , und wählen Sie **Trennen**aus.  
  
     Die folgenden Optionen sind im Dialogfeld **Datenbank trennen** verfügbar.  
  
     **Zu trennende Datenbanken**  
     Führt die zu trennenden Datenbanken auf.  
  
     **Database Name**  
     Zeigt den Namen der zu trennenden Datenbank an.  
  
     **Verbindungen löschen**  
     Trennt die Verbindungen zu der angegebenen Datenbank.  
  
    > [!NOTE]  
    >  Sie können eine Datenbank mit aktiven Verbindungen nicht trennen.  
  
     **Statistikaktualisierung**  
     Standardmäßig werden durch den Trennvorgang beim Trennen der Datenbank die veralteten Optimierungsstatistiken beibehalten. Um die vorhandenen Optimierungsstatistiken zu aktualisieren, aktivieren Sie dieses Kontrollkästchen.  
  
     **Volltextkataloge beibehalten**  
     Standardmäßig werden während des Trennvorgangs alle der Datenbank zugeordneten Volltextkataloge beibehalten. Um sie zu entfernen, deaktivieren Sie das Kontrollkästchen **Volltextkataloge beibehalten** . Diese Option wird nur beim Aktualisieren einer Datenbank von [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]angezeigt.  
  
     **Status**  
     Zeigt für den Status einen der folgenden Werte an: **Bereit** oder **Nicht bereit**.  
  
     **MessageBox**  
     Unter **Meldung** können folgende Informationen zur Datenbank angezeigt werden:  
  
    -   Wenn eine Datenbank an einer Replikation beteiligt ist, hat der **Status** den Wert **Nicht bereit** , und unter **Meldung** wird **Die Datenbank wurde repliziert**angezeigt.  
  
    -   Wenn eine Datenbank über eine oder mehrere Verbindungen verfügt, hat der **Status** den Wert **Nicht bereit**, und unter **Meldung** wird *<Anzahl_aktiver_Verbindungen>***Aktive Verbindung(en)** angezeigt, z.B.: **1 Aktive Verbindung(en)**. Bevor Sie die Datenbank trennen können, müssen Sie durch Auswählen der Option **Verbindungen löschen**alle aktiven Verbindungen trennen.  
  
     Weitere Informationen zu einer Meldung erhalten Sie, indem Sie auf den Linktext klicken, um den Aktivitätsmonitor zu öffnen.  
  
2.  Klicken Sie auf **OK**.  
  
3.  Verwenden Sie den Windows-Explorer, um Datenbankdateien vom Quellserver an den gleichen Ort auf dem Zielserver zu verschieben oder zu kopieren.  
  
4.  Verwenden Sie Windows-Explorer, um die Sicherung des Serverzertifikats und die Datei mit dem privaten Schlüssel vom Quellserver an den gleichen Ort auf dem Zielserver zu verschieben oder zu kopieren.  
  
5.  Erstellen Sie für die Zielinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]einen Datenbank-Hauptschlüssel. Weitere Informationen finden Sie weiter unten unter **Verwenden von Transact-SQL** .  
  
6.  Erstellen Sie anhand der entsprechenden Sicherungsdatei das Serverzertifikat neu. Weitere Informationen finden Sie weiter unten unter **Verwenden von Transact-SQL** .  
  
7.  Klicken Sie im Objekt-Explorer in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]mit der rechten Maustaste auf den Ordner **Datenbanken** , und klicken Sie dann auf **Anfügen**.  
  
8.  Klicken Sie im Dialogfeld **Datenbanken anfügen** unter **Anzufügende Datenbanken**auf **Hinzufügen**.  
  
9. Wählen Sie im Dialogfeld **Datenbankdateien suchen –***Servername* die Datenbankdatei aus, die dem neuen Server angefügt werden soll, und klicken Sie auf **OK**.  
  
     Die folgenden Optionen sind im Dialogfeld **Datenbanken anfügen** verfügbar.  
  
     **Anzufügende Datenbanken**  
     Zeigt Informationen zu den ausgewählten Datenbanken an.  
  
     \<Keine Spaltenüberschrift>  
     Zeigt ein Symbol an, das den Status des Anfügevorgangs angibt. Die möglichen Symbole werden in der unten stehenden Beschreibung von **Status** beschrieben.  
  
     **Speicherort für MDF-Datei**  
     Zeigt den Pfad und den Dateinamen der ausgewählten MDF-Datei an.  
  
     **Database Name**  
     Zeigt den Namen der Datenbank an.  
  
     **Anfügen als**  
     Gibt wahlweise einen anderen Namen für die anzufügende Datenbank an.  
  
     **Besitzer**  
     Zeigt eine Dropdownliste mit möglichen Datenbankbesitzern an, aus der Sie wahlweise einen anderen Besitzer auswählen können.  
  
     **Status**  
     Zeigt den Status der Datenbank an (siehe folgende Tabelle).  
  
    |Symbol|Statustext|Beschreibung|  
    |----------|-----------------|-----------------|  
    |(Kein Symbol)|(Kein Text)|Das Anfügen hat noch nicht begonnen oder steht für dieses Objekt noch aus. Dies ist der Standardwert bei Öffnen des Dialogfelds.|  
    |Grünes, nach rechts zeigendes Dreieck|Vorgang wird ausgeführt|Das Anfügen hat begonnen, ist aber noch nicht abgeschlossen.|  
    |Grünes Häkchen|Success|Das Objekt wurde erfolgreich angefügt.|  
    |Roter Kreis mit einem weißen Kreuz darin|Fehler|Beim Anfügen ist ein Fehler aufgetreten. Der Vorgang konnte deshalb nicht erfolgreich abgeschlossen werden.|  
    |Kreis mit zwei schwarzen Quadranten (links und rechts) und zwei weißen Quadranten (oben und unten) darin|Beendet|Das Anfügen wurde nicht erfolgreich abgeschlossen, weil der Benutzer den Vorgang angehalten hat.|  
    |Kreis mit einem gekrümmten Pfeil darin, der entgegengesetzt der Uhrzeigerrichtung zeigt|Rollback wurde ausgeführt|Anfügen war erfolgreich, es wurde jedoch ein Rollback durchgeführt, weil beim Anfügen eines anderen Objekts ein Fehler aufgetreten ist.|  
  
     **MessageBox**  
     Zeigt entweder eine leere Meldung oder einen "Datei nicht gefunden"-Link an.  
  
     **Hinzufügen**  
     Suchen Sie die erforderlichen Hauptdatenbankdateien. Wenn der Benutzer eine MDF-Datei auswählt, werden entsprechende Informationen automatisch in die jeweiligen Felder des Rasters **Anzufügende Datenbank** eingetragen.  
  
     **Entfernen**  
     Entfernt die ausgewählte Datei aus dem Raster **Anzufügende Datenbank** .  
  
     **"** *<database_name>* **" Datenbankdetails für**  
     Zeigt die Namen der anzufügenden Dateien an. Um den Pfadnamen einer Datei zu überprüfen bzw. zu ändern, klicken Sie auf die Schaltfläche **Durchsuchen** (**…**).  
  
    > [!NOTE]  
    >  Wenn eine Datei nicht vorhanden ist, wird in der Spalte **Meldung** "Nicht gefunden" angezeigt. Wenn keine Protokolldatei gefunden wird, liegt sie in einem anderen Verzeichnis oder wurde gelöscht. Dann müssen Sie entweder den Dateipfad im Raster **Datenbankdetails** ändern, um auf den richtigen Pfad zu verweisen, oder die Protokolldatei aus dem Raster entfernen. Wenn keine .ndf-Datei gefunden wurde, müssen Sie ihren Pfad im Raster aktualisieren, um auf den richtigen Pfad zu verweisen.  
  
     **Originaldateiname**  
     Zeigt den Namen der angefügten Datei an, die zur Datenbank gehört.  
  
     **Dateityp**  
     Gibt den Dateityp an: **Datendatei** oder **Protokolldatei**.  
  
     **Aktueller Dateipfad**  
     Zeigt den Pfad zur ausgewählten Datenbankdatei an Die Pfadangabe kann manuell bearbeitet werden.  
  
     **MessageBox**  
     Zeigt entweder eine leere Meldung oder einen „**Datei nicht gefunden**“-Hyperlink an.  
  
###  <a name="TsqlMove"></a> Verwenden von Transact-SQL  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Detach the TDE protected database from the source server.   
    USE master ;  
    GO  
    EXEC master.dbo.sp_detach_db @dbname = N'CustRecords';  
    GO  
    -- Move or copy the database files from the source server to the same location on the destination server.   
    -- Move or copy the backup of the server certificate and the private key file from the source server to the same location on the destination server.   
    -- Create a database master key on the destination instance of SQL Server.   
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1';  
    GO  
    -- Recreate the server certificate by using the original server certificate backup file.   
    -- The password must be the same as the password that was used when the backup was created.  
  
    CREATE CERTIFICATE TestSQLServerCert   
    FROM FILE = 'TestSQLServerCert'  
    WITH PRIVATE KEY   
    (  
        FILE = 'SQLPrivateKeyFile',  
        DECRYPTION BY PASSWORD = '*rt@40(FL&dasl1'  
    );  
    GO  
    -- Attach the database that is being moved.   
    -- The path of the database files must be the location where you have stored the database files.  
    CREATE DATABASE [CustRecords] ON   
    ( FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\CustRecords.mdf' ),  
    ( FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\CustRecords_log.LDF' )  
    FOR ATTACH ;  
    GO  
    ```  
  
 Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [sp_detach_db &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Anfügen und Trennen von Datenbanken &#40;SQL Server&#41;](../../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [Transparente Datenverschlüsselung in Azure SQL-Datenbank](../../../relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database.md)  
  
  
