---
title: Bereitstellen einer Datenbank mit DAC | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dbdeployment.settings.f1
- sql13.swb.dbdeployment.progress.f1
- sql13.swb.dbdeployment.summary.f1
- sql13.swb.dbdeployment.results.f1
- sql13.swb.dbdeployment.welcome.f1
helpviewer_keywords:
- deploy database wizard
- database deploy [SQL Server]
ms.assetid: 08c506e8-4ba0-4a19-a066-6e6a5c420539
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 57703923bd142330e2a46e72eb4faaee18fa7285
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="deploy-a-database-by-using-a-dac"></a>Bereitstellen einer Datenbank mit DAC
  Verwenden Sie den Assistenten zum **Bereitstellen von Datenbanken auf SQL Azure** , um eine Datenbank zwischen einer [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz und einem [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] -Server bzw. zwischen zwei [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]-Servern bereitzustellen.  
  
##  <a name="BeforeBegin"></a> Vorbereitungen  
 Der Assistent verwendet die BACPAC-Archivdatei einer Datenebenenanwendung (DAC), um sowohl die Daten als auch die Definitionen von Datenbankobjekten bereitzustellen. Er führt einen DAC-Export von der Quelldatenbank und einen DAC-Import zum Ziel aus.  
  
###  <a name="DBOptSettings"></a> Datenbankoptionen und -einstellungen  
 Die während der Bereitstellung erstellte Datenbank verfügt standardmäßig über die Standardeinstellungen der CREATE DATABASE-Anweisung. Die Ausnahme besteht darin, dass die Datenbanksortierung und der Kompatibilitätsgrad auf die Werte der Quelldatenbank festgelegt werden.  
  
 Datenbankoptionen wie TRUSTWORTHY, DB_CHAINING und HONOR_BROKER_PRIORITY können nicht im Rahmen des Bereitstellungsprozesses angepasst werden. Physische Eigenschaften, z. B. die Anzahl der Dateigruppen oder die Anzahl und Größe der Dateien, können nicht im Rahmen des Bereitstellungsprozesses geändert werden. Nachdem die Bereitstellung abgeschlossen wurde, können Sie die ALTER DATABASE-Anweisung, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]oder PowerShell für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden, um die Datenbank individuell anzupassen.  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
 Der Assistent zum Bereitstellen von Datenbanken ****  unterstützt das Bereitstellen einer Datenbank:  
  
-   Von einer [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz auf [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
  
-   Von [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] auf eine [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz.  
  
-   Zwischen zwei [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] -Servern.  
  
 Das Bereitstellen von Datenbanken zwischen zwei [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanzen wird vom Assistenten nicht unterstützt.  
  
 Zur Unterstützung des Assistenten muss auf einer [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) oder höher ausgeführt werden. Wenn eine Datenbank auf einer [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz Objekte enthält, die unter [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]nicht unterstützt werden, kann der Assistent nicht zur Bereitstellung der Datenbank auf [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]verwendet werden. Wenn eine Datenbank unter [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] Objekte enthält, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nicht unterstützt werden, können Sie die Datenbank mithilfe des Assistenten nicht auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanzen bereitstellen.  
  
###  <a name="Security"></a> Sicherheit  
 Zur Erhöhung der Sicherheit werden die Anmeldenamen für die SQL Server-Authentifizierung ohne Kennwort in einer BACPAC-Exportdatei (DAC) gespeichert. Sobald die BACPAC-Datei importiert wird, wird der Anmeldename als deaktivierter Anmeldename mit einem generierten Kennwort erstellt. Um die Anmeldenamen zu aktivieren, melden Sie sich unter einem Anmeldenamen an, der über die ALTER ANY LOGIN-Berechtigung verfügt, und verwenden ALTER LOGIN, um den Anmeldenamen zu aktivieren und ein neues Kennwort zuzuweisen, das dem Benutzer mitgeteilt werden kann. Dies ist für Anmeldenamen der Windows-Authentifizierung nicht erforderlich, da die zugehörigen Kennwörter nicht von SQL Server verwaltet werden.  
  
#### <a name="permissions"></a>Berechtigungen  
 Der Assistent erfordert DAC-Exportberechtigungen für die Quelldatenbank. Zur Anmeldung werden mindestens die ALTER ANY LOGIN-Berechtigung und die VIEW DEFINITION-Berechtigung im Datenbankbereich sowie SELECT-Berechtigungen für **sys.sql_expression_dependencies**benötigt. Zum Exportieren einer DAC sind nur Mitglieder der festen Serverrolle "securityadmin" berechtigt, die ebenfalls Mitglieder der festen Datenbankrolle "database_owner" in der Datenbank sind, aus der die DAC exportiert wird. Mitglieder der festen Serverrolle „sysadmin“ oder des integrierten SQL Server-Systemadministratorkontos **sa** sind ebenfalls berechtigt, eine DAC zu exportieren.  
  
 Der Assistent benötigt DAC-Importberechtigungen für die Zielinstanz oder den Server. Der Anmeldename muss einem Mitglied der festen Serverrolle **sysadmin** , **serveradmin** oder **dbcreator** zugeordnet sein, das über ALTER ANY-LOGIN-Berechtigungen verfügt. Außerdem kann das integrierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemadministratorkonto mit der Bezeichnung **sa** zum Importieren einer DAC verwendet werden. Um eine DAC mit Anmeldungen bei [!INCLUDE[ssSDS](../../includes/sssds-md.md)] importieren zu können, müssen Sie Mitglied der Rollen "loginmanager" oder "serveradmin" sein. Um eine DAC ohne Anmeldungen bei [!INCLUDE[ssSDS](../../includes/sssds-md.md)] importieren zu können, müssen Sie Mitglied der Rolle "dbmanager" oder "serveradmin" sein.  
  
##  <a name="UsingDeployDACWizard"></a> Verwenden des Assistenten zum Bereitstellen von Datenbanken  
 **So migrieren Sie eine Datenbank mithilfe des Assistenten zum Bereitstellen von Datenbanken**  
  
1.  Stellen Sie eine Verbindung mit dem Speicherort der Datenbank her, die Sie bereitstellen möchten. Sie können entweder eine [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz oder einen [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] -Server angeben.  
  
2.  Erweitern Sie im **Objekt-Explorer**den Knoten für die Instanz, in der die Datenbank enthalten ist.  
  
3.  Erweitern Sie den Knoten **Datenbanken** .  
  
4.  Klicken Sie mit der rechten Maustaste auf die Datenbank, die Sie bereitstellen möchten, wählen Sie **Tasks**und dann **Datenbank in SQL Azure bereitstellen**aus.  
  
5.  Abschließen der Dialogfelder des Assistenten  
  
    -   [Seite "Einführung"](#Introduction)  
  
    -   [Bereitstellungseinstellungen](#Deployment_settings)  
  
    -   [Seite "Zusammenfassung"](#Summary)  
  
    -   [Status](#Progress)  
    
    -   [Ergebnisse](#Results)  
  
##  <a name="Introduction"></a> Seite "Einführung"  
 Auf dieser Seite werden die Schritte des Assistenten zum Bereitstellen von Datenbanken ****  beschrieben.  
  
 **Optionen**  
  
-   **Diese Seite nicht mehr anzeigen.** – Aktivieren Sie dieses Kontrollkästchen, damit die Einführungsseite in Zukunft nicht mehr angezeigt wird.  
  
-   **Weiter** – führt Sie zur Seite **Bereitstellungseinstellungen** .  
  
-   **Abbrechen** – bricht den Vorgang ab und schließt den Assistenten.  
  
##  <a name="Deployment_settings"></a> Bereitstellungseinstellungen (Seite)  
 Auf dieser Seite können Sie den Zielserver angeben sowie Details zur neuen Datenbank bereitstellen.  
  
 **Lokaler Host:**  
  
-   **Serververbindungen** – Geben Sie Serververbindungsdetails an, und klicken Sie dann auf **Verbinden** , um die Verbindung zu überprüfen.  
  
-   **Neuer Datenbankname** – Geben Sie einen Namen für die neue Datenbank an.  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Datenbankeinstellungen:**  
  
-   **[!INCLUDE[ssSDS](../../includes/sssds-md.md)] Edition** – Wählen Sie die Edition von [!INCLUDE[ssSDS](../../includes/sssds-md.md)] im Dropdownmenü aus.  
  
-   **Maximale Datenbankgröße** – Wählen Sie die maximale Datenbankgröße im Dropdownmenü aus.  
  
 **Andere Einstellungen:**  
  
-   Geben Sie ein lokales Verzeichnis für die temporäre Datei an, die der BACPAC-Archivdatei entspricht. Beachten Sie, dass die Datei am angegebenen Speicherort erstellt wird und dort verbleibt, nachdem der Vorgang abgeschlossen wurde.  
  
##  <a name="Summary"></a> Seite "Zusammenfassung"  
 Verwenden Sie diese Seite, um die angegebene Quelle und die Zieleinstellungen für den Vorgang zu überprüfen. Klicken Sie auf **Fertig stellen**, um den Bereitstellungsvorgang mithilfe der angegebenen Einstellungen abzuschließen. Klicken Sie auf **Abbrechen**, um den Bereitstellungsvorgang abzubrechen und den Assistenten zu beenden.  
  
##  <a name="Progress"></a> Status (Seite)  
 Auf dieser Seite wird eine Statusanzeige angezeigt, die den Status des Vorgangs anzeigt. Klicken Sie auf die Option **Details anzeigen** , um ausführliche Informationen anzuzeigen.  
  
##  <a name="Results"></a> Ergebnisse (Seite)  
 Auf dieser Seite wird angegeben, ob der Bereitstellungsvorgang erfolgreich war oder ob dabei Fehler auftraten, dabei werden die Ergebnisse jeder Aktion angezeigt. Für alle Aktionen, die fehlerhaft waren, ist in der Spalte **Ergebnis** ein Link enthalten. Klicken Sie auf den Link, um einen Bericht des für diese Aktion aufgetretenen Fehlers anzuzeigen.  
  
 Klicken Sie auf **Fertig stellen** , um den Assistenten zu schließen.  
  
## <a name="using-a-net-framework-application"></a>Verwenden einer .NET Framework-Anwendung  
 **Stellen Sie eine Datenbank mithilfe der Methoden DacStoreExport() und Import() in einer .NET Framework-Anwendung bereit.**  
  
 Laden Sie zum Anzeigen eines Codebeispiels die DAC-Beispielanwendung unter [Codeplex](http://go.microsoft.com/fwlink/?LinkId=219575)herunter.  
  
1.  Erstellen Sie ein SMO-Serverobjekt, und legen Sie es auf die Instanz oder den Server fest, die bzw. der die bereitzustellende Datenbank enthält.  
  
2.  Öffnen Sie ein **ServerConnection** -Objekt, und stellen Sie eine Verbindung mit derselben Instanz her.  
  
3.  Verwenden Sie die **Export** -Methode des **Microsoft.SqlServer.Management.Dac.DacStore** -Typs, um die Datenbank in eine BACPAC-Datei zu exportieren. Geben Sie den Namen der zu exportierenden Datenbank sowie den Pfad zum Ordner an, in dem die BACPAC-Datei abgelegt werden soll.  
  
4.  Erstellen Sie ein SMO-Serverobjekt, und legen Sie es auf die Zielinstanz oder den Zielserver fest.  
  
5.  Öffnen Sie ein **ServerConnection** -Objekt, und stellen Sie eine Verbindung mit derselben Instanz her.  
  
6.  Verwenden Sie die **Import** -Methode des **Microsoft.SqlServer.Management.Dac.DacStore** -Typs, um die BACPAC-Datei zu importieren. Geben Sie die beim Exportvorgang erstellte BACPAC-Datei an.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenebenenanwendungen](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Exportieren einer Datenebenenanwendung](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)   
 [Importieren einer BACPAC-Datei zum Erstellen einer neuen Benutzerdatenbank](../../relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)  
  
  
