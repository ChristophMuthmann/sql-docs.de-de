---
title: Importieren einer BACPAC-Datei zum Erstellen einer neuen Benutzerdatenbank | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb. importdac.results.f1
- sql13.swb.importdac.settings.f1
- sql13.swb.importdac.storagebrowser.f1
- sql13.swb.importdac.results.f1
- sql13.swb.importdac.progress.f1
- sql13.swb. importdac.summary.f1
- sql13.swb.importdac.summary.f1
- sql13.swb. importdac.progress.f1
- sql13.swb.importdac.welcome.f1
- sql13.swb. importdac.settings.f1
helpviewer_keywords:
- Data-tier application
- SQL Server DAC
- Migrate database
- DAC
ms.assetid: 736d8d9a-39f1-4bf8-b81f-2e56c134d12e
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4226b33bd805aca7e38781d5a55eb990f61e4e69
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="import-a-bacpac-file-to-create-a-new-user-database"></a>Importieren einer BACPAC-Datei zum Erstellen einer neuen Benutzerdatenbank
  Importieren Sie eine Datei einer Datenebenenanwendung (DAC) (eine BACPAC-Datei), um eine Kopie der ursprünglichen Datenbank mit den Daten auf einer neuen Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]oder auf [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]zu erstellen. Die Export-/Importvorgänge können kombiniert werden, um eine DAC oder Datenbank zwischen Instanzen zu migrieren oder eine logische Sicherung zu erstellen. Dazu gehört z. B. das Erstellen einer lokalen Kopie einer in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]bereitgestellten Datenbank.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
 Beim Importvorgang wird in zwei Phasen eine neue DAC erstellt.  
  
1.  Beim Import wird mithilfe der in der Exportdatei gespeicherten DAC-Definition eine neue DAC und eine zugeordnete Datenbank erstellt. Dieser Vorgang entspricht dem Erstellen einer neuen DAC aus der Definition in einer DAC-Paketdatei bei einer DAC-Bereitstellung.  
  
2.  Beim Import werden die Daten per Massenkopieren in die Exportdatei kopiert.  
  
## <a name="sql-server-utility"></a>SQL Server-Hilfsprogramm  
 Beim Importieren einer DAC in eine verwaltete Instanz des Datenbankmoduls wird die importierte DAC in das SQL Server-Hilfsprogramm integriert, wenn der Hilfsprogramm-Sammlungssatz das nächste Mal von der Instanz an den Steuerungspunkt für das Hilfsprogramm gesendet wird. Die DAC ist dann unter dem Knoten **Bereitgestellte Datenebenenanwendungen** im [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Utility Explorer** and reported in the **Bereitgestellte Datenebenenanwendungen** details page.  
  
## <a name="database-options-and-settings"></a>Datenbankoptionen und -einstellungen  
 Standardmäßig verfügt die während des Imports erstellte Datenbank über alle Standardeinstellungen aus der CREATE DATABASE-Anweisung, mit der Ausnahme, dass die Datenbanksortierung und der Kompatibilitätsgrad auf die in der DAC-Exportdatei festgelegten Werte gesetzt sind. Eine DAC-Exportdatei verwendet die Werte aus der ursprünglichen Datenbank.  
  
 Einige Datenbankoptionen, z. B. TRUSTWORTHY, DB_CHAINING und HONOR_BROKER_PRIORITY, können nicht im Rahmen des Importprozesses angepasst werden. Physische Eigenschaften, z. B. die Anzahl der Dateigruppen oder die Anzahl und Größe der Dateien, können nicht im Rahmen des Importprozesses geändert werden. Nachdem der Import abgeschlossen wurde, können Sie die ALTER DATABASE-Anweisung, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]oder PowerShell für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden, um die Datenbank individuell anzupassen. Weitere Informationen finden Sie unter [Databases](../../relational-databases/databases/databases.md).  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Eine DAC kann in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]oder eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] , die unter [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) oder höher ausgeführt wird, importiert werden. Wenn Sie eine DAC aus einer höheren Version exportieren, kann die DAC Objekte enthalten, die von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]nicht unterstützt werden. Sie können diese DACs nicht auf Instanzen von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]bereitstellen.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 Das Importieren einer DAC-Exportdatei aus unbekannten oder nicht vertrauenswürdigen Quellen wird nicht empfohlen. Solche Dateien können schädlichen Code enthalten, der möglicherweise unbeabsichtigten Transact-SQL-Code ausführt oder Fehler verursacht, indem er das Schema ändert. Bevor Sie eine Exportdatei aus einer unbekannten oder nicht vertrauenswürdigen Quelle verwenden, entpacken Sie die DAC, und untersuchen Sie den Code, z. B. gespeicherte Prozeduren und anderen benutzerdefinierten Code. Weitere Informationen zum Ausführen dieser Tests finden Sie unter [Validate a DAC Package](https://msdn.microsoft.com/library/ee633948(SQL.130).aspx).  
  
## <a name="security"></a>Sicherheit  
 Zur Erhöhung der Sicherheit werden die Anmeldenamen für die SQL Server-Authentifizierung ohne Kennwort in eine DAC-Exportdatei gespeichert. Sobald die Datei importiert wird, wird der Anmeldename als deaktivierter Anmeldename mit einem generierten Kennwort erstellt. Um die Anmeldenamen zu aktivieren, melden Sie sich unter einem Anmeldenamen an, der über die ALTER ANY LOGIN-Berechtigung verfügt, und verwenden ALTER LOGIN, um den Anmeldenamen zu aktivieren und ein neues Kennwort zuzuweisen, das dem Benutzer mitgeteilt werden kann. Dies ist für Anmeldenamen der Windows-Authentifizierung nicht erforderlich, da die zugehörigen Kennwörter nicht von SQL Server verwaltet werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Eine DAC kann nur von Mitgliedern der festen Serverrollen **sysadmin** oder **serveradmin** importiert werden bzw. unter Verwendung von Anmeldenamen aus der festen Serverrolle **dbcreator** , die über ALTER ANY LOGIN-Berechtigungen verfügen. Außerdem kann das integrierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemadministratorkonto mit der Bezeichnung **sa** zum Importieren einer DAC verwendet werden. Um eine DAC mit Anmeldungen bei [!INCLUDE[ssSDS](../../includes/sssds-md.md)] importieren zu können, müssen Sie Mitglied der Rollen "loginmanager" oder "serveradmin" sein. Um eine DAC ohne Anmeldungen bei [!INCLUDE[ssSDS](../../includes/sssds-md.md)] importieren zu können, müssen Sie Mitglied der Rolle "dbmanager" oder "serveradmin" sein.  
  
## <a name="using-the-import-data-tier-application-wizard"></a>Verwenden des Assistenten zum Importieren von Datenebenenanwendungen  
 **Gehen Sie folgendermaßen vor, um den Assistenten zu starten:**  
  
1.  Stellen Sie entweder lokal oder in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]eine Verbindung zu einer Instanz von [!INCLUDE[ssSDS](../../includes/sssds-md.md)]her.  
  
2.  Klicken Sie im ****Objekt-Explorer mit der rechten Maustaste auf **Datenbanken**, und wählen Sie dann den Menübefehl **Datenebenenanwendung importieren** aus, um den Assistenten zu starten.  
  
3.  Bearbeiten Sie die Dialogfenster des Assistenten:  
  
    -   [Seite "Einführung"](#Introduction)  
  
    -   [Importeinstellungen (Seite)](#Import_settings)  
  
    -   [Datenbankeinstellungen (Seite)](#Database_settings)  
  
    -   [Seite "Zusammenfassung"](#Summary)  
  
    -   [Status (Seite)](#Progress)  
  
    -   [Ergebnisse (Seite)](#Results)  
  
###  <a name="Introduction"></a> Seite "Einführung"  
 Auf dieser Seite werden die Schritte für den Assistenten zum Importieren von Datenebenenanwendungen beschrieben.  
  
 **Optionen**  
  
-   **Diese Seite nicht mehr anzeigen.** – Aktivieren Sie dieses Kontrollkästchen, damit die Einführungsseite in Zukunft nicht mehr angezeigt wird.  
  
-   Durch**Weiter** gelangen Sie zur Seite **Importeinstellungen** .  
  
-   **Abbrechen** – bricht den Vorgang ab und schließt den Assistenten.  
  
###  <a name="Import_settings"></a> Importeinstellungen (Seite)  
 Verwenden Sie diese Seite, um den Speicherort der zu importierenden BACPAC-Datei anzugeben.  
  
-   **Vom lokalen Datenträger importieren** – Klicken Sie auf **Durchsuchen** , um den lokalen Computer zu durchsuchen, oder geben Sie den Pfad im dafür vorgesehenen Feld an. Der Pfadname muss einen Dateinamen und die Erweiterung BACPAC enthalten.  
  
-   **Aus Azure importieren** – Importiert eine BACPAC-Datei aus einem Microsoft Azure-Container. Sie müssen eine Verbindung mit einem Microsoft Azure-Container herstellen, um diese Option zu überprüfen. Beachten Sie, dass diese Option auch erfordert, dass Sie ein lokales Verzeichnis für die temporäre Datei angeben. Die temporäre Datei wird am angegebenen Speicherort erstellt und verbleibt dort, nachdem der Vorgang abgeschlossen wurde.  
  
     Wenn Sie Azure durchsuchen, können Sie zwischen Containern innerhalb eines Kontos wechseln. Sie müssen eine einzelne BACPAC-Datei angeben, um den Importvorgang fortzusetzen. Beachten Sie, dass Sie Spalten nach **Name**, **Größe**oder **Geändert am**sortieren können.  
  
     Um fortzufahren, geben Sie die zu importierende BACPAC-Datei an, und klicken Sie dann auf **Öffnen**.  
  
###  <a name="Database_settings"></a> Datenbankeinstellungen (Seite)  
 Auf dieser Seite können Sie Einzelheiten zu der Datenbank angeben, die erstellt wird.  
  
 **Für eine lokale Instanz von SQL Server:**  
  
-   **Neuer Datenbankname** – Geben Sie einen Namen für die importierte Datenbank an.  
  
-   **Datendateipfad** - Stellen Sie ein lokales Verzeichnis für Datendateien bereit. Klicken Sie auf **Durchsuchen** , um den lokalen Computer zu durchsuchen, oder geben Sie den Pfad im dafür vorgesehenen Feld an.  
  
-   **Protokolldateipfad** – Geben Sie ein lokales Verzeichnis für Protokolldateien an. Klicken Sie auf **Durchsuchen** , um den lokalen Computer zu durchsuchen, oder geben Sie den Pfad im dafür vorgesehenen Feld an.  
  
 Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
 **Für eine Azure SQL-Datenbank:**  
  
 - **[Importieren einer BACPAC-Datei zum Erstellen einer neuen Azure SQL-Datenbank](https://azure.microsoft.com/documentation/articles/sql-database-import/)** enthält Schritt-für-Schritt-Anweisungen für das Azure-Portal, PowerShell, SSMS oder SqlPackage.  
 - In **[SQL-Datenbankoptionen und -leistung: Grundlegendes zum Angebot in den einzelnen Tarifen](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)** erhalten Sie einen detaillierten Einblick in die verschiedenen Dienstebenen.  

### <a name="validation-page"></a>Überprüfung (Seite)  
 Verwenden Sie diese Seite, um sämtliche Probleme zu überprüfen, die den Vorgang blockieren. Beheben Sie zum Fortfahren die Blockierungsprobleme, und klicken Sie dann auf **Überprüfung erneut ausführen** , um sicherzustellen, dass die Überprüfung erfolgreich ist.  
  
 Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
###  <a name="Summary"></a> Seite "Zusammenfassung"  
 Verwenden Sie diese Seite, um die angegebene Quelle und die Zieleinstellungen für den Vorgang zu überprüfen. Klicken Sie auf **Fertig stellen**, um den Importvorgang mithilfe der angegebenen Einstellungen abzuschließen. Klicken Sie auf **Abbrechen**, um den Importvorgang abzubrechen und den Assistenten zu beenden.  
  
###  <a name="Progress"></a> Status (Seite)  
 Auf dieser Seite wird eine Statusanzeige angezeigt, die den Status des Vorgangs anzeigt. Klicken Sie auf die Option **Details anzeigen** , um ausführliche Informationen anzuzeigen.  
  
 Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
###  <a name="Results"></a> Ergebnisse (Seite)  
 Auf dieser Seite wird angegeben, ob die Vorgänge zum Importieren und Erstellen der Datenbank erfolgreich waren oder ob Fehler bei den einzelnen Aktionen auftraten. Für alle Aktionen, die fehlerhaft waren, ist in der Spalte **Ergebnis** ein Link enthalten. Klicken Sie auf den Link, um einen Bericht des für diese Aktion aufgetretenen Fehlers anzuzeigen.  
  
 Klicken Sie auf **Schließen** , um den Assistenten zu schließen.  
  
## <a name="see-also"></a>Siehe auch  
[Importieren einer BACPAC-Datei zum Erstellen einer neuen Azure SQL-Datenbank](https://azure.microsoft.com/en-us/documentation/articles/sql-database-import/)  
 [Datenebenenanwendungen](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Exportieren einer Datenebenenanwendung](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)  
  
  

