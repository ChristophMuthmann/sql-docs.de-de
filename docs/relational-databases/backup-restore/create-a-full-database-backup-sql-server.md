---
title: "Erstellen einer vollständigen Datenbanksicherung (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backing up databases [SQL Server], full backups
- backing up databases [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- database backups [SQL Server], SQL Server Management Studio
ms.assetid: 586561fc-dfbb-4842-84f8-204a9100a534
caps.latest.revision: 63
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: be884b2d1b316506592f939167c5be91ddc2a9f6
ms.openlocfilehash: 141c83e009e1cf135690297442c6a4864a871bfc
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="create-a-full-database-backup-sql-server"></a>Erstellen einer vollständigen Datenbanksicherung (SQL Server)

 > Gehen Sie für SQL Server 2014 unter [Erstellen einer vollständigen Datenbanksicherung (SQL Server)](https://msdn.microsoft.com/en-US/library/ms187510(SQL.120).aspx).

  In diesem Thema wird beschrieben, wie Sie in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]oder PowerShell eine vollständige Datenbanksicherung erstellen.  
  
>  Informationen zur SQL Server-Sicherung im Azure-BLOB-Speicherdienst finden Sie unter [SQL Server-Sicherung und -Wiederherstellung mit dem Microsoft Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) und [SQL Server-Sicherung über URLs](../../relational-databases/backup-restore/sql-server-backup-to-url.md):  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen 
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Die BACKUP-Anweisung ist nicht in einer expliziten oder implizierten Transaktion zulässig.  
  
-   Sicherungen, die mit aktuelleren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt werden, können in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht wiederhergestellt werden.  
  
-   Bevor Sie fortfahren, finden Sie eine Übersicht und einen tieferen Einblick in Sicherungskonzepte und -tasks unter [Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Wenn eine Datenbank größer wird, ist zum Abschließen von vollständigen Datenbanksicherungen jedoch mehr Zeit und mehr Speicherplatz erforderlich. Erwägen Sie für große Datenbanken die Ergänzung einer vollständigen Datenbanksicherung mit einer Reihe von [differenziellen Datenbanksicherungen]((../../relational-databases/backup-restore/differential-backups-sql-server.md). Weitere Informationen finden Sie unter [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  
  
-   Ein Schätzwert der Größe einer vollständigen Datenbanksicherung kann mithilfe der gespeicherten Systemprozedur [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) ermittelt werden.  
  
-   Standardmäßig wird bei jedem erfolgreichen Sicherungsvorgang dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll und dem Systemereignisprotokoll ein Eintrag hinzugefügt. Wenn Sie regelmäßig eine Sicherung durchführen, kumulieren diese Erfolgsmeldungen schnell und führen so zu großen Fehlerprotokollen! Dadurch kann sich die Suche nach anderen Meldungen erschweren. In solchen Fällen können Sie diese Sicherungsprotokolleinträge mithilfe des Ablaufverfolgungsflags 3226 unterdrücken, wenn keines der Skripts von diesen Einträgen abhängig ist. Weitere Informationen finden Sie unter [Ablaufverfolgungsflags &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
###  <a name="Security"></a> Sicherheit  
 Bei einer Datenbanksicherung ist TRUSTWORTHY auf OFF festgelegt. Weitere Informationen zum Festlegen von TRUSTWORTHY auf ON finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] werden die **PASSWORD** - und **MEDIAPASSWORD** -Optionen nicht mehr für die Erstellung von Sicherungen verwendet. Sie können jedoch immer noch mit Kennwörtern erstellte Sicherungen wiederherstellen.  
  
####  <a name="Permissions"></a> Berechtigungen  
 Mitglieder der festen Serverrolle **sysadmin** und der festen Datenbankrollen **db_owner** und **db_backupoperator** verfügen standardmäßig über BACKUP DATABASE- und BACKUP LOG-Berechtigungen.  
  
 Besitz- und Berechtigungsprobleme im Zusammenhang mit der physischen Datei des Sicherungsmediums können den Sicherungsvorgang beeinträchtigen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss **über Lese- und Schreibberechtigungen für das Medium verfügen. Das Konto, unter dem der** -Dienst ausgeführt wird, muss Schreibberechtigungen haben. Allerdings prüft die gespeicherte Prozedur [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), die den Systemtabellen einen Eintrag für ein Sicherungsmedium hinzufügt, nicht die Dateizugriffsberechtigungen. Solche Probleme mit der physischen Datei des Sicherungsmediums treten möglicherweise erst auf, wenn auf die physische Ressource zugegriffen wird, um einen Sicherungs- oder Wiederherstellungsvorgang auszuführen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
>  Wenn Sie mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Sicherungstask angeben, können Sie das entsprechende [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) -Skript generieren, indem Sie auf die Schaltfläche **Skript** klicken und ein Ziel für das Skript auswählen.  
  
### <a name="back-up-a-database"></a>So sichern Sie eine Datenbank  
  
1.  Klicken Sie nach dem Herstellen einer Verbindung mit der entsprechenden Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]im **Objekt-Explorer**auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Datenbanken**, und wählen Sie eine Benutzerdatenbank aus, oder erweitern Sie **Systemdatenbanken** , und wählen Sie eine Systemdatenbank aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, zeigen Sie auf **Tasks**, und klicken Sie anschließend auf **Sichern**. Das Dialogfeld **Datenbank sichern** wird angezeigt.  

  #### <a name="general-page"></a>**Seite Allgemein**
  
4.  Überprüfen Sie in der Dropdownliste **Datenbank** den Datenbanknamen. Sie können optional eine andere Datenbank aus der Liste auswählen.  
  
5.  Das Textfeld **Wiederherstellungsmodell** dient nur zu Referenzzwecken.  Eine Datenbanksicherung kann für jedes Wiederherstellungsmodell ausgeführt werden (**FULL**, **BULK_LOGGED**, oder **SIMPLE**).  
  
6.  Wählen Sie in der Dropdownliste **Sicherungstyp** den Wert **Vollständig**aus.  
  
     Beachten Sie, dass Sie nach dem Erstellen einer vollständigen Datenbanksicherung eine differenzielle Datenbanksicherung ausführen können. Weitere Informationen finden Sie unter [Erstellen einer differenziellen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md):  
  
7.  Optional können Sie das Kontrollkästchen **Kopiesicherung** aktivieren, um eine Kopiesicherung zu erstellen. Eine *Kopiesicherung* ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherung, die unabhängig von der Sequenz von herkömmlichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherungen erstellt wird. Weitere Informationen finden Sie unter [Kopiesicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  Für den Sicherungstyp **Differenziell** ist keine Kopiesicherung verfügbar.  

8.  Wählen Sie für **Sicherungskomponente**das Optionsfeld **Datenbank** aus.  
  
9. Verwenden Sie im Abschnitt **Ziel** die Dropdownliste **Sichern auf** aus, um das Sicherungsziel auszuwählen. Klicken Sie auf **Hinzufügen** , um weitere Sicherungsobjekte und/oder -ziele hinzuzufügen.
  
     Um einen Sicherungsziel zu entfernen, wählen Sie ihn aus, und klicken Sie auf **Entfernen**. Zum Anzeigen des Inhalts eines vorhandenen Sicherungsziels wählen Sie es aus, und klicken Sie auf **Inhalt**.  

  #### <a name="media-options-page"></a>**Seite „Medienoptionen“**  
10. Klicken Sie im Bereich **Seite auswählen** auf **Medienoptionen** , um die Medienoptionen anzuzeigen oder auszuwählen.   
    
11. Wählen Sie eine Option von **Medium überschreiben** aus, indem Sie auf eine der folgenden Optionen klicken: 

    > [!IMPORTANT]  
    >  Die Option **Medien überschreiben** ist deaktiviert, wenn Sie **URL** auf der Seite **Allgemein** als Sicherungsziel ausgewählt haben. Weitere Informationen finden Sie unter [Datenbank sichern &#40;Seite 'Medienoptionen'&#41;](../../relational-databases/backup-restore/back-up-database-media-options-page.md).  


  -   **Auf vorhandenen Mediensatz sichern**  
  
      > [!IMPORTANT]  
      >  Wenn Sie die Verschlüsselung verwenden möchten, sollten Sie diese Option nicht aktivieren. Wenn Sie diese Option aktivieren, werden die Verschlüsselungsoptionen auf der Seite **Sicherungsoptionen** deaktiviert. Die Verschlüsselung wird nicht unterstützt, wenn Sie Sicherungen an den vorhandenen Sicherungssatz anfügen.  
  
         Klicken Sie bei dieser Option entweder auf **An vorhandenen Sicherungssatz anfügen** oder auf **Alle vorhandenen Sicherungssätze überschreiben**. Weitere Informationen finden Sie unter [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md):  
  
         Sie können bei Bedarf das Kontrollkästchen **Mediensatznamen und Ablaufzeit des Sicherungssatzes überprüfen** aktivieren, damit beim Sicherungsvorgang das Datum und die Uhrzeit überprüft werden, an dem bzw. zu der der Mediensatz und der Sicherungssatz ablaufen.  
  
         Geben Sie optional einen Namen im Textfeld **Mediensatzname** ein. Wenn kein Name angegeben wurde, wird ein Mediensatz mit leerem Namen erstellt. Wenn Sie einen Mediensatznamen angeben, wird überprüft, ob der tatsächliche Name des Mediums (Band oder Datenträger) mit dem eingegebenen Namen übereinstimmt.  
  
-   **Auf neuen Mediensatz sichern und alle vorhandenen Sicherungssätze löschen**  
  
    Geben Sie bei dieser Option einen Namen in das Textfeld **Name für neuen Mediensatz** und optional eine Beschreibung des Mediensatzes in das Textfeld **Beschreibung für neuen Mediensatz** ein.  
  
14. Aktivieren Sie im Abschnitt **Zuverlässigkeit** optional folgende Kontrollkästchen:  
  
    -   **Sicherung nach dem Abschluss überprüfen**.  
  
    -   **Vor dem Schreiben auf die Medien Prüfsumme bilden**  Weitere Informationen finden Sie unter [Mögliche Medienfehler während der Sicherung und Wiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
    
    -   **Bei Fehler fortsetzen**. 

15. Der Abschnitt **Transaktionsprotokoll** ist inaktiv, es sei denn, Sie sichern ein Transaktionsprotokoll (wie im Abschnitt **Sicherungstyp** der Seite **Allgemein** angegeben).  
      
16. Im Abschnitt **Bandlaufwerk** ist die Option **Band nach dem Sichern entladen** aktiv, wenn Sie auf ein Bandlaufwerk sichern (gemäß der Konfiguration im Abschnitt **Ziel** der Seite **Allgemein** ). Wenn Sie auf diese Option klicken, wird die Option **Band vor dem Entladen zurückspulen** aktiviert.   

  #### <a name="backup-options-page"></a>**Seite „Sicherungsoptionen“**  

17. Klicken Sie im Bereich **Seite auswählen** auf **Sicherungsoptionen** , um die Sicherungsoptionen anzuzeigen und auszuwählen.  
  
18. Übernehmen Sie im Textfeld **Name** entweder den vorgeschlagenen Standardnamen für den Sicherungssatz, oder geben Sie einen anderen Namen für den Sicherungssatz ein.  
  
19. Im Textfeld **Beschreibung** können Sie optional eine Beschreibung des Sicherungssatzes eingeben.  
  
20. Geben Sie an, wann der Sicherungssatz abläuft und überschrieben werden kann, ohne die Überprüfung der Ablaufdaten explizit auszulassen:  
  
    -   Wenn der Sicherungssatz nach einer bestimmten Anzahl von Tagen ablaufen soll, klicken Sie auf **Nach** (die Standardoption), und geben Sie an, nach wie vielen Tagen der Sicherungssatz abläuft. Dieser Wert kann zwischen 0 und 99999 Tagen liegen. Ein Wert von 0 Tagen bedeutet, dass der Sicherungssatz nicht abläuft.  
  
         Der Standardwert wird in der Option **Standardbeibehaltung für Sicherungsmedien (in Tagen)** des Dialogfelds **Servereigenschaften** (Seite „Datenbankeinstellungen“) festgelegt. Klicken Sie hierzu mit der rechten Maustaste auf den Servernamen im Objekt-Explorer, und wählen Sie Eigenschaften aus. Wählen Sie anschließend die Seite **Datenbankeinstellungen** aus.  
  
    -   Zum Speichern des Sicherungssatzes an einem bestimmten Datum klicken Sie auf **Am**. Geben Sie das Datum ein, an dem der Sicherungssatz abläuft.  
  
         Weitere Informationen zum Ablaufdatum von Sicherungen finden Sie unter [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md):  
  
21. Verwenden Sie im Abschnitt **Komprimierung** die Dropdownliste **Sicherungskomprimierung festlegen** , um den gewünschten Komprimierungsgrad festzulegen.  [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] und höheren Versionen wird die [Sicherungskomprimierung](../../relational-databases/backup-restore/backup-compression-sql-server.md). Ob eine Sicherung standardmäßig komprimiert wird, ist vom Wert der Serverkonfigurationsoption **Komprimierungsstandard für Sicherung** abhängig. Sie können jedoch unabhängig von der aktuellen Standardeinstellung auf Serverebene eine Sicherung komprimieren, indem Sie die Option **Sicherung komprimieren**aktivieren, oder die Komprimierung verhindern, indem Sie die Option **Sicherung nicht komprimieren**aktivieren.  
  
     Weitere Informationen zu den Einstellungen für die Sicherungskomprimierung finden Sie unter [Anzeigen oder Konfigurieren der Serverkonfigurationsoption „Standardeinstellung für die Sicherungskomprimierung“](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
22. Verwenden Sie im Abschnitt **Verschlüsselung** das Kontrollkästchen **Sicherung verschlüsseln** , um festzulegen, ob für die Sicherung Verschlüsselung verwendet werden soll. Verwenden Sie die Dropdownliste **Algorithmus** , um einen Verschlüsselungsalgorithmus auszuwählen.  Verwenden Sie die Dropdownliste **Zertifikat oder asymmetrischer Schlüssel** , um ein vorhandenes Zertifikat oder einen asymmetrischen Schlüssel auszuwählen. Die Verschlüsselung wird in SQL Server 2014 und höheren Versionen unterstützt. Weitere Informationen zu den Verschlüsselungsoptionen finden Sie unter [Datenbank sichern &#40;Seite 'Sicherungsoptionen'&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md):  
  
  
Sie können den [Wartungsplanungs-Assistenten](https://msdn.microsoft.com/library/ms191002.aspx) zum Erstellen von Datenbanksicherungen verwenden. 

### <a name="examples"></a>Beispiele  
#### <a name="a--full-back-up-to-disk-to-default-location"></a>**A.  Vollständige Sicherung auf Datenträger am Standardspeicherort**
In diesem Beispiel wird die `Sales` -Datenbank auf dem Datenträger am standardmäßigen Sicherungsspeicherort gesichert.  Es wurde nie eine Sicherung von `Sales` erstellt.
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz des SQL Server-Datenbankmoduls her, und erweitern Sie anschließend diese Instanz.

2.  Erweitern Sie die **Datenbank**, klicken Sie mit der rechten Maustaste auf `Sales`,zeigen Sie auf **Tasks**, und klicken Sie anschließend auf **Sichern...**.

3.  Klicken Sie auf **OK**.

#### <a name="b--full-back-up-to-disk-to-non-default-location"></a>**B.  Vollständige Sicherung auf Datenträger an einem anderen als dem Standardspeicherort**
In diesem Beispiel wird die `Sales` -Datenbank auf Datenträger unter `E:\MSSQL\BAK`gesichert.  Frühere Sicherungen von `Sales` wurden erstellt.
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz des SQL Server-Datenbankmoduls her, und erweitern Sie anschließend diese Instanz.

2.  Erweitern Sie die **Datenbank**, klicken Sie mit der rechten Maustaste auf `Sales`,zeigen Sie auf **Tasks**, und klicken Sie anschließend auf **Sichern...**.

3.  Wählen Sie auf der Seite **Allgemein** im Abschnitt **Ziel** in der Dropdownliste **Sichern auf:****Datenträger** aus.

4.  Klicken Sie auf **Entfernen**, bis alle vorhandenen Sicherungsdateien entfernt wurden.

5.  Klicken Sie auf **Hinzufügen** , um das Dialogfeld **Sicherungsziel auswählen** zu öffnen.

6.  Geben Sie im Textfeld `E:\MSSQL\BAK\Sales_20160801.bak` Dateiname ****  ein.

7.  Klicken Sie auf **OK**.

8.  Klicken Sie auf **OK**.

#### <a name="c--create-an-encrypted-backup"></a>**C.  Erstellen einer verschlüsselten Sicherung**
In diesem Beispiel wird die `Sales` -Datenbank mit Verschlüsselung am standardmäßigen Sicherungsspeicherort gesichert.  Ein  [**Datenbank-Hauptschlüssel**](../../relational-databases/security/encryption/create-a-database-master-key.md) wurde bereits erstellt.  Ein  [**Zertifikat**](../../t-sql/statements/create-certificate-transact-sql.md) mit dem Namen `MyCertificate`wurde bereits erstellt. Ein T-SQL-Beispiel zum Erstellen eines **Datenbank-Hauptschlüssels** und eines **Zertifikats** finden Sie unter [Erstellen einer verschlüsselten Sicherung](../../relational-databases/backup-restore/create-an-encrypted-backup.md).  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz des SQL Server-Datenbankmoduls her, und erweitern Sie anschließend diese Instanz.

2.  Erweitern Sie die **Datenbank**, klicken Sie mit der rechten Maustaste auf `Sales`,zeigen Sie auf **Tasks**, und klicken Sie anschließend auf **Sichern...**.

3.  Wählen Sie auf der Seite **Medienoptionen** im Abschnitt **Medien überschreiben** **Auf neuen Mediensatz sichern und alle vorhandenen Sicherungssätze löschen**aus.

4.  Aktivieren Sie auf der Seite **Sicherungsoptionen** im Abschnitt **Verschlüsselung** das Kontrollkästchen **Sicherung verschlüsseln** .

5.  Wählen Sie in der Dropdownliste **Algorithmus** den Eintrag **AES 256**aus.

6.  Wählen Sie in der Dropdownliste **Zertifikat oder asymmetrischer Schlüssel** `MyCertificate`aus.

7.  Klicken Sie auf **OK**.

#### <a name="d--back-up-to-the-azure-blob-storage-service"></a>**D.  Sichern auf den Azure-BLOB-Speicherdienst**
#### <a name="common-steps"></a>**Allgemeine Schritte**  
In den drei folgenden Beispielen wird eine vollständige Sicherung der `Sales` -Datenbank in den Microsoft Azure BLOB-Speicherdienst ausgeführt.  Der Speicherkontoname lautet `mystorageaccount`.  Der Container heißt `myfirstcontainer`.  Aus Gründen der Übersichtlichkeit sind die ersten vier Schritte hier einmal aufgelistet und alle Beispiele beginnen mit **Schritt 5**.
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz des SQL Server-Datenbankmoduls her, und erweitern Sie anschließend diese Instanz.

2.  Erweitern Sie die **Datenbank**, klicken Sie mit der rechten Maustaste auf `Sales`,zeigen Sie auf **Tasks**, und klicken Sie anschließend auf **Sichern...**.

3.  Wählen Sie Option **URL** aus der Dropdownliste **Back up to:** (Sichern auf:) auf der Seite **Allgemein** im Abschnitt **Ziel** .

4.  Klicken Sie auf **Hinzufügen** , um das Dialogfeld **Sicherungsziel auswählen** zu öffnen.

    **D1.  Es existieren bereits eine Sicherung im Stripesetformat über URLs sowie eine SQL Server-Anmeldeinformation.**  
Eine gespeicherte Zugriffsrichtlinie wurde mit Lese-, Schreib-, und Auflistungsrechten erstellt.  Die SQL Server Anmeldeinformation `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`wurde mit einer Shared Access Signature (SAS) erstellt, die der gespeicherten Zugriffsrichtlinie zugeordnet ist.  
*
    5.  Wählen Sie `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` aus dem Textfeld **Azure-Speichercontainer:** .

    6.  Geben Sie im Textfeld **Sicherungsdatei:** `Sales_stripe1of2_20160601.bak`ein.

    7.  Klicken Sie auf **OK**.

    8.  Wiederholen Sie die Schritte **4** und **5**.

    9.  Geben Sie im Textfeld **Sicherungsdatei:** `Sales_stripe2of2_20160601.bak`ein.

    10.  Klicken Sie auf **OK**.

    11.   Klicken Sie auf **OK**.

    **D2.  Eine Shared Access Signature ist vorhanden und eine SQL Server-Anmeldeinformation ist nicht vorhanden**
  5.    Geben Sie `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` in das Textfeld **Azure-Speichercontainer:** ein.
  
  6.    Geben Sie die SAS in das Textfeld **Shared Access Signature:** ein.
  
  7.    Klicken Sie auf **OK**.
  
  8.    Klicken Sie auf **OK**.

    **D3.  Es ist keine Shared Access Signature (SAS) vorhanden**
  5.    Klicken Sie auf **Neuer Container** . Das Dialogfeld **Verbindung mit einen Microsoft Abonnement herstellen** wird geöffnet.  
  
  6.    Füllen Sie das Dialogfeld **Verbindung mit einen Microsoft Abonnement herstellen** aus, und klicken Sie anschließend auf **OK** um zum Dialogfeld **Sicherungsziel auswählen** zurückzukehren.  Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einen Microsoft Abonnement](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md) .
  
  7.    Klicken Sie im Dialogfeld **Sicherungsziel auswählen** auf **OK** .
  
  8.    Klicken Sie auf **OK**.

  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
### <a name="create-a-full-database-backup"></a>Erstellen einer vollständigen Datenbanksicherung  
  
1.  Führen Sie die BACKUP DATABASE-Anweisung aus, um die vollständige Datenbanksicherung zu erstellen, und geben Sie dabei Folgendes an:  
  
    -   Den Namen der zu sichernden Datenbank.  
  
    -   Das Sicherungsmedium, auf das die vollständige Datenbanksicherung geschrieben wird.  
  
     Die grundlegende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Syntax zum Erstellen einer vollständigen Datenbanksicherung lautet:  
  
     BACKUP DATABASE *database*  
  
     TO *backup_device* [ **,**...*n* ]  
  
     [ WITH *mit_Optionen* [ **,**...*o* ] ] ;  
  
    |Option|Beschreibung|  
    |------------|-----------------|  
    |*database*|Die Datenbank, für die eine Sicherungskopie erstellt werden soll.|  
    |*backup_device* [ **,**...*n* ]|Gibt eine Liste an, die zwischen 1 und 64 Sicherungsmedien für den Sicherungsvorgang enthalten kann. Sie können ein physisches Sicherungsmedium angeben oder ein entsprechendes logisches Sicherungsmedium, sofern es bereits definiert wurde. Geben Sie das physische Sicherungsmedium mithilfe der Option DISK oder TAPE an:<br /><br /> { DISK &#124; TAPE } **=***physischer_Sicherungsmediumname*<br /><br /> Weitere Informationen finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).|  
    |WITH *with_options* [ **,**...*o* ]|Optional geben Sie eine oder mehrere zusätzliche Optionen an, *o*. Weitere Informationen zu einigen der grundlegenden Optionen finden Sie unter Schritt 2.|  
  
2.  Geben Sie optional eine oder mehrere WITH-Optionen an. Einige der grundlegenden WITH-Optionen werden hier beschrieben. Weitere Informationen zu allen WITH-Optionen finden Sie unter [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md):  
  
    -   Grundlegender Sicherungssatz von WITH-Optionen:  
  
         { COMPRESSION | NO_COMPRESSION }  
         Nur in [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] und höher verfügbar. Gibt an, ob für diese Sicherung eine [Sicherungskomprimierung](../../relational-databases/backup-restore/backup-compression-sql-server.md) verwendet wird, wodurch die Standardeinstellung auf Serverebene überschrieben wird.  
  
         VERSCHLÜSSELUNG (ALGORITHMUS, SERVERZERTIFIKAT | ASYMMETRISCHER SCHLÜSSEL)  
         Nur in SQL Server 2014 und höheren Versionen geben Sie den zu verwendenden Verschlüsselungsalgorithmus und das Zertifikat oder den asymmetrischen Schlüssel an, die die Sicherheit bei der Verschlüsselung erhöhen.  
  
         DESCRIPTION **=** { **'***text***'** | **@***text_variable* }  
         Gibt den Text an, mit dem der Sicherungssatz beschrieben wird. Die Zeichenfolge kann maximal 255 Zeichen haben.  
  
         NAME **=** { *backup_set_name* | **@***backup_set_name_var* }  
         Gibt den Namen des Sicherungssatzes an. Namen können maximal 128 Zeichen haben. Wird NAME nicht angegeben, erhält der Sicherungssatz einen leeren Namen.  
  
    -   Grundlegender Sicherungssatz von WITH-Optionen:  
  
         Standardmäßig fügt BACKUP die Sicherung einem vorhandenen Mediensatz an, wobei vorhandene Sicherungssätze beibehalten werden. Verwenden Sie die NOINIT-Option, um dies explizit anzugeben. Informationen über das Anfügen an vorhandene Sicherungssätze finden Sie unter [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md):  
  
         Verwenden Sie alternativ die FORMAT-Option, um die Sicherungsmedien zu formatieren:  
  
         FORMAT [ **,** MEDIANAME**=** { *media_name* | **@***media_name_variable* } ] [ **,** MEDIADESCRIPTION **=** { *text* | **@***text_variable* } ]  
         Verwenden Sie die FORMAT-Klausel, wenn Sie das Medium das erste Mal einsetzen oder alle vorhandenen Daten überschreiben möchten. Weisen Sie den neuen Medien optional einen Mediennamen und eine Beschreibung zu.  
  
        > [!IMPORTANT]  
        >  Gehen Sie mit den FORMAT- und INIT-Klauseln der BACKUP-Anweisung äußerst vorsichtig um, denn sie zerstören alle zuvor auf dem Sicherungsmedium gespeicherten Sicherungen.  
  
###  <a name="TsqlExample"></a> Beispiele (Transact-SQL)  
  
#### <a name="a-back-up-to-a-disk-device"></a>**A. Sichern auf ein Datenträgermedium**  
 In diesem Beispiel wird die gesamte [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank auf dem Datenträger gesichert, wobei mithilfe von `FORMAT` ein neuer Mediensatz erstellt wird.  
  
```tsql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH FORMAT,  
      MEDIANAME = 'Z_SQLServerBackups',  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="b-back-up-to-a-tape-device"></a>**B. Sichern auf ein Bandmedium**  
 Im folgenden Beispiel wird die gesamte [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank auf Band gesichert, wobei die Sicherung an vorherige Sicherungen angefügt wird.  
  
```tsql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="c-back-up-to-a-logical-tape-device"></a>**C. Sichern auf ein logisches Bandmedium**  
 Im folgenden Beispiel wird ein logisches Sicherungsmedium für ein Bandlaufwerk erstellt. Im Beispiel wird dann die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank vollständig auf diesem Medium gesichert.  
  
```tsql  
-- Create a logical backup device,   
-- AdventureWorks2012_Bak_Tape, for tape device \\.\tape0.  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'AdventureWorks2012_Bak_Tape', '\\.\tape0'; USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO AdventureWorks2012_Bak_Tape  
   WITH FORMAT,  
      MEDIANAME = 'AdventureWorks2012_Bak_Tape',  
      MEDIADESCRIPTION = '\\.\tape0',   
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
Verwenden Sie das **Backup-SqlDatabase** -Cmdlet. Um ausdrücklich anzugeben, dass dies eine vollständige Datenbanksicherung ist, geben Sie den **-BackupAction**  -Parameter mit dessen Standardwert **Database**an. Dieser Parameter ist bei vollständigen Datenbanksicherungen optional.  

### <a name="examples"></a>Beispiele
#### <a name="a--full-local-backup"></a>**A.  Vollständige lokale Sicherung**  
Im folgenden Beispiel wird eine vollständige Datenbanksicherung der `MyDB` -Datenbank am standardmäßigen Sicherungsspeicherort der Serverinstanz `Computer\Instance`erstellt. Optional wird im Beispiel **-BackupAction Database**angegeben.  
```powershell 
Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
```
 
#### <a name="b--full-backup-to-microsoft-azure"></a>**B.  Vollständige Sicherung für Microsoft Azure**  
Das folgende Beispiel erstellt eine vollständige Sicherung der Datenbank `Sales` in der `MyServer` -Instanz an den Microsoft Azure BLOB-Speicherdienst.  Eine gespeicherte Zugriffsrichtlinie wurde mit Lese-, Schreib-, und Auflistungsrechten erstellt.  Die SQL Server Anmeldeinformation `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`wurde mit einer Shared Access Signature (SAS) erstellt, die der gespeicherten Zugriffsrichtlinie zugeordnet ist.  Der PowerShell-Befehl verwendet den **BackupFile** -Parameter, um den Speicherort (URL) sowie den Namen der Sicherungsdaten anzugeben.

```powershell  
import-module sqlps;
$container = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer';
$FileName = 'Sales.bak';
$database = 'Sales';
$BackupFile = $container + '/' + $FileName ;
  
Backup-SqlDatabase -ServerInstance "MyServer" –Database $database -BackupFile $BackupFile;
```
 
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Erstellen einer vollständigen Datenbanksicherung (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Erstellen einer differenziellen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Wiederherstellen einer Datenbanksicherung unter dem einfachen Wiederherstellungsmodell &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [Wiederherstellen einer Datenbank bis zum Fehlerzeitpunkt im vollständigen Wiederherstellungsmodell &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Wiederherstellen einer Datenbank an einem neuen Speicherort &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
  
-   [Verwenden des Wartungsplanungs-Assistenten](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>Siehe auch  
**[Troubleshooting SQL Server backup and restore operations (Problembehandlung bei der Sicherung von SQL Server und Wiederherstellungsvorgänge)](https://support.microsoft.com/en-us/kb/224071)**          
[Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Datenbank sichern &#40;Seite Allgemein&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)   
 [Datenbank sichern &#40;Seite 'Sicherungsoptionen'&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)   
 [Differenzielle Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [Vollständige Datenbanksicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)  
  
  

