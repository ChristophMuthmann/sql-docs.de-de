---
title: Bereitstellen einer Datenebenenanwendung | Microsoft-Dokumentation
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
- sql13.swb.deploydacwizard.introduction.f1
- sql13.swb.deploydacwizard.deploydac.f1
- sql13.swb.deploydacwizard.summary.f1
- sql13.swb.deploydacwizard.updateconfiguration.f1
- sql13.swb.deploydacwizard.selectdac.f1
helpviewer_keywords:
- Deploy data-tier application
- deploy DAC
- data-tier application [SQL Server], deploy
- How to [DAC], deploy
- wizard [DAC], deploy
ms.assetid: c117af35-aa53-44a5-8034-fa8715dc735f
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: eeda8a1432ad975caaf74134ce598b0c70c16d29
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="deploy-a-data-tier-application"></a>Bereitstellen einer Datenebenenanwendung
  Mithilfe eines Assistenten oder eines PowerShell-Skripts können Sie eine Datenebenenanwendung (DAC) von einem DAC-Paket für eine vorhandene Instanz des Datenbankmoduls oder der Azure SQL-Datenbank bereitstellen. 
  
 Beim Bereitstellungsprozess wird eine DAC-Instanz registriert, indem die DAC-Definition in der **msdb**-Systemdatenbank (**master** in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]) gespeichert und eine Datenbank erstellt wird, die anschließend mit allen in der DAC definierten Datenbankobjekten aufgefüllt wird.  
 
  
## <a name="deploy-the-same-dac-package-multiple-times"></a>Mehrfaches Bereitstellen desselben DAC-Pakets 
 Dasselbe DAC-Paket kann mehrmals an eine einzelne [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz bereitgestellt werden, die Bereitstellungen müssen jedoch einzeln ausgeführt werden. Der für die einzelnen Bereitstellungen angegebene DAC-Instanzname muss innerhalb der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]eindeutig sein.  
  
## <a name="managed-instances"></a>Verwaltete Instanzen  
 Beim Bereitstellen einer DAC an eine verwaltete Instanz des Datenbankmoduls wird die bereitgestellte DAC in das **SQL Server-Hilfsprogramm** integriert, wenn der Hilfsprogramm-Sammlungssatz das nächste Mal von der Instanz an den Steuerungspunkt für das Hilfsprogramm gesendet wird. Die DAC ist dann unter dem Knoten **Bereitgestellte Datenebenenanwendungen** im [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Utility Explorer** and reported in the **Bereitgestellte Datenebenenanwendungen** details page.  
  
###  <a name="database-options-and-settings"></a>Datenbankoptionen und -einstellungen  
 Die während der Bereitstellung erstellte Datenbank verfügt standardmäßig über alle Standardeinstellungen der CREATE DATABASE-Anweisung mit folgenden Ausnahmen:  
  
-   Für Datenbanksortierung und Kompatibilitätsgrad werden die im DAC-Paket definierten Werte festgelegt. Ein aus einem Datenbankprojekt in SQL Server Developer Tools erstelltes DAC-Paket verwendet die im Datenbankprojekt festgelegten Werte. Ein aus einer vorhandenen Datenbank extrahiertes Paket verwendet die Werte aus der ursprünglichen Datenbank.  
  
-   Sie können einige der Datenbankeinstellungen, z. B. Datenbanknamen und Dateipfade, auf der Seite **Konfiguration aktualisieren** anpassen. Beim Bereitstellen auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)]können Sie die Dateipfade nicht festlegen.  
  
 Einige Datenbankoptionen, z. B. TRUSTWORTHY, DB_CHAINING und HONOR_BROKER_PRIORITY, können nicht im Rahmen des Bereitstellungsprozesses angepasst werden. Physische Eigenschaften, z. B. die Anzahl der Dateigruppen oder die Anzahl und Größe der Dateien, können nicht im Rahmen des Bereitstellungsprozesses geändert werden. Nachdem die Bereitstellung abgeschlossen wurde, können Sie die ALTER DATABASE-Anweisung, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]oder PowerShell für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden, um die Datenbank individuell anzupassen.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Eine DAC kann für [!INCLUDE[ssSDS](../../includes/sssds-md.md)]bereitgestellt werden, oder für eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] , die [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 oder höher ausführt. Wenn Sie eine DAC mit einer späteren Version erstellen, enthält die DAC möglicherweise Objekte, die von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]nicht unterstützt werden. Sie können diese DACs nicht auf Instanzen von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]bereitstellen.  
    
## <a name="security-and-permissions"></a>Sicherheit und Berechtigungen
Anmeldenamen für die Authentifizierung werden ohne Kennwort in einem DAC-Paket gespeichert. Sobald das Paket bereitgestellt oder aktualisiert wird, wird der Anmeldename als deaktivierter Anmeldename mit einem generierten Kennwort erstellt. Um die Anmeldenamen zu aktivieren, melden Sie sich unter einem Anmeldenamen an, der über die ALTER ANY LOGIN-Berechtigung verfügt, und verwenden ALTER LOGIN, um den Anmeldenamen zu aktivieren und ein neues Kennwort zuzuweisen, das dem Benutzer mitgeteilt werden kann. Dies ist für Anmeldenamen der Windows-Authentifizierung nicht erforderlich, da die zugehörigen Kennwörter nicht von SQL Server verwaltet werden.  
  
 Eine DAC kann nur von Mitgliedern der festen Serverrollen **sysadmin** oder **serveradmin** bereitgestellt werden bzw. unter Verwendung von Anmeldenamen aus der festen Serverrolle **dbcreator**, die über ALTER ANY LOGIN-Berechtigungen verfügen. Außerdem kann das integrierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemadministratorkonto mit der Bezeichnung **sa** zum Bereitstellen einer DAC verwendet werden. 

Um eine DAC mit Anmeldungen bei [!INCLUDE[ssSDS](../../includes/sssds-md.md)] bereitstellen zu können, müssen Sie Mitglied der Rollen "loginmanager" oder "serveradmin" sein. Um eine DAC ohne Anmeldenamen in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] bereitstellen zu können, müssen Sie Mitglied der Rollen "dbmanager" oder "serveradmin" sein.  
  
## <a name="deploy-a-dac-using-the-wizard"></a>Bereitstellen einer DAC mithilfe des Assistenten  
  
1.  Erweitern Sie im **Objekt-Explorer**den Knoten für die Instanz, für die Sie die DAC bereitstellen möchten.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Knoten **Datenbanken** , und wählen Sie **Datenebenenanwendung bereitstellen...**aus.  
  
3.  Führen Sie die Dialogfenster des Assistenten aus, und klicken Sie auf „Fertig stellen“.
Im Folgenden erfahren Sie mehr über einige Seiten des Assistenten: 
     
### <a name="select-dac-package-page"></a>Seite "DAC-Paket auswählen"  
 Geben Sie das DAC-Paket an, das die bereitzustellende Datenebenenanwendung enthält. Die Seite durchläuft drei Statusübergänge.  
    
### <a name="select-the-dac-package"></a>Auswählen des DAC-Pakets  
 Wählen Sie das bereitzustellende DAC-Paket aus. Das DAC-Paket muss eine gültige DAC-Paketdatei sein und die Erweiterung .dacpac aufweisen.  
  
 **DAC-Paket** : Geben Sie den Pfad und den Dateinamen des DAC-Pakets an, das die bereitzustellende Datenebenenanwendung enthält. Sie können die Schaltfläche **Durchsuchen** rechts neben dem Feld auswählen, um zum Speicherort des DAC-Pakets zu wechseln.  
  
 **Anwendungsname** : Ein schreibgeschütztes Feld mit dem DAC-Namen, der beim Erstellen oder Extrahieren der DAC aus einer Datenbank zugewiesen wurde.  
  
 **Version** : Ein schreibgeschütztes Feld mit der Version, die beim Erstellen oder Extrahieren der DAC aus einer Datenbank zugewiesen wurde.  
  
 **Beschreibung** : Ein schreibgeschütztes Feld mit der Beschreibung, die beim Erstellen oder Extrahieren der DAC aus einer Datenbank erstellt wurde.  
  
### <a name="validating-the-dac-package"></a>Überprüfen des DAC-Pakets  
 Zeigt eine Statusanzeige an, da der Assistent bestätigt, dass es sich bei der ausgewählten Datei um ein gültiges DAC-Paket handelt. Wenn das DAC-Paket überprüft wird, geht der Assistent zur abschließenden Version der Seite **Paket auswählen** über. Dort können Sie die Ergebnisse der Überprüfung einsehen. Wenn die Datei kein gültiges DAC-Paket ist, verbleibt der Assistent auf der Seite **DAC-Paket auswählen**. Wählen Sie entweder ein anderes gültiges DAC-Paket aus, oder brechen Sie den Assistenten ab, und generieren Sie ein neues DAC-Paket.  
  
  ### <a name="review-policy-page"></a>Seite "Richtlinie überprüfen"  
 Überprüfen Sie die Auswertungsergebnisse der DAC-Richtlinie zur Serverauswahl (falls verwendet). Die DAC-Richtlinie zur Serverauswahl ist optional und wird der DAC während der Erstellung in Visual Studio zugewiesen. Die Richtlinie verwendet Facets für die Richtlinie zur Serverauswahl, um Bedingungen anzugeben, die eine [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz zum Hosten der DAC erfüllen sollte.  
  
 **Auswertungsergebnisse der Richtlinienbedingungen**: Zeigt an, ob die Bedingungen der Richtlinie zur DAC-Bereitstellung erfüllt sind. Die Auswertungsergebnisse für die einzelnen Bedingungen werden in einer separaten Zeile angezeigt.  
  
 Beim Bereitstellen von DAC auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)]ergeben die folgenden Serverauswahlrichtlinien immer false: Betriebssystemversion, Sprache, Named Pipes aktiviert, Plattform und tcp aktiviert.  
  
 **Richtlinienverletzungen ignorieren** : Verwenden Sie dieses Kontrollkästchen, um mit der Bereitstellung fortzufahren, wenn eine oder mehrere Richtlinienbedingungen nicht erfüllt wurden. Aktivieren Sie diese Option nur, wenn Sie sicher sind, dass keine der fehlgeschlagenen Bedingungen die erfolgreiche Ausführung der DAC verhindert.  
   
### <a name="update-configuration-page"></a>Seite "Konfiguration aktualisieren"  
 Geben Sie die Namen der bereitgestellten DAC-Instanz und der bei der Bereitstellung erstellten Datenbank an, und legen Sie Datenbankoptionen fest.  
  
 **Datenbankname** : Geben Sie den Namen der Datenbank an, die von der Bereitstellung erstellt werden soll. Standardmäßig wird der Name der Quelldatenbank verwendet, aus der die DAC extrahiert wurde. Der Name muss innerhalb der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz eindeutig sein und den Regeln für [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Bezeichner entsprechen.  
  
 Wenn Sie den Datenbanknamen ändern, werden die Namen der Datendatei und der Protokolldateien entsprechend dem neuen Wert angepasst.  
  
 Der Datenbankname wird auch als Name der DAC-Instanz verwendet. Der Instanzname wird im Knoten der DAC unter dem Knoten **Datenebenenanwendungen** im **Objekt-Explorer**oder im Knoten **Bereitgestellte Datenebenenanwendungen** im **Hilfsprogramm-Explorer**angezeigt.  
  
 Die folgenden Optionen gelten nicht für [!INCLUDE[ssSDS](../../includes/sssds-md.md)]und werden beim Bereitstellen auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)]nicht angezeigt.  
  
 **Standardspeicherort für Datenbankdatei verwenden** : Wählen Sie diese Option aus, um die Datenbankdaten- und Protokolldateien am Standardspeicherort der Instanz des [!INCLUDE[ssDE](../../includes/ssde-md.md)]s abzulegen. Die Dateinamen werden anhand des Datenbanknamens erstellt.  
  
 **Datenbankdateien angeben** : Wählen Sie diese Option aus, um einen anderen Speicherort oder Namen für die Daten- und Protokolldateien anzugeben.  
  
 **Pfad und Name der Datendatei** : Geben Sie den vollständigen Pfad- und Dateinamen für die Datendatei an. Das Feld wird mit dem Standardpfad und -dateinamen aufgefüllt. Bearbeiten Sie die Zeichenfolge im Feld, um den Standardeintrag zu ändern, oder verwenden Sie die Schaltfläche Durchsuchen, um zum Ordner zu navigieren, in dem die Datendatei abgelegt werden soll.  
  
 **Pfad und Name der Protokolldatei** : Geben Sie den vollständigen Pfad- und Dateinamen für die Protokolldatei an. Das Feld wird mit dem Standardpfad und -dateinamen aufgefüllt. Bearbeiten Sie die Zeichenfolge im Feld, um den Standardeintrag zu ändern, oder verwenden Sie die Schaltfläche **Durchsuchen** , um zum Ordner zu navigieren, in dem die Protokolldatei abgelegt werden soll.  
  
###  <a name="Summary"></a> Seite "Zusammenfassung"  
 Verwenden Sie diese Seite, um die Aktionen zu überprüfen, die der Assistent beim Bereitstellen der DAC ausführt.  
  
 **Die folgenden Einstellungen werden zur Bereitstellung der DAC verwendet.** – Überprüfen Sie die angezeigten Informationen darauf, ob die ergriffenen Maßnahmen richtig sind. Im Fenster werden das ausgewählte DAC-Paket und der für die bereitgestellte DAC-Instanz ausgewählte Name angezeigt. Im Fenster werden auch die Einstellungen angezeigt, die beim Erstellen der mit der DAC verbundenen Datenbank verwendet werden.  
   
### <a name="deploy-page"></a>Seite "Bereitstellen"  
 Auf dieser Seite wird angegeben, ob der Bereitstellungsvorgang erfolgreich war oder fehlgeschlagen ist.  
  
 **DAC wird bereitgestellt** : Gibt an, ob die Aktionen zur Bereitstellung der DAC erfolgreich oder fehlerhaft waren. Überprüfen Sie die Informationen, um zu bestimmen, ob die einzelnen Aktionen erfolgreich waren oder fehlgeschlagen sind. Für alle Aktionen, die fehlerhaft waren, ist in der Spalte **Ergebnis** ein Link enthalten. Klicken Sie auf den Link, um einen Bericht des für diese Aktion aufgetretenen Fehlers anzuzeigen.  
  
 **Bericht speichern** : Klicken Sie auf diese Schaltfläche, um den Bereitstellungsbericht in einer HTML-Datei zu speichern. In der Datei ist der Status der einzelnen Aktionen aufgeführt, einschließlich aller durch die Aktionen generierten Fehler. Der Standardordner ist der Ordner "SQL Server Management Studio\DAC Packages" im Ordner "Dokumente" unter Ihrem Windows-Konto.  
  
  
##  <a name="deploy-a-dac-using-powershell"></a>Bereitstellen einer DAC mit PowerShell  
  
1.  Erstellen Sie ein SMO-Serverobjekt, und legen Sie es auf die Instanz fest, auf der Sie die DAC bereitstellen möchten.  
  
2.  Öffnen Sie ein **ServerConnection** -Objekt, und stellen Sie eine Verbindung mit derselben Instanz her.  
  
3.  Laden Sie die DAC-Paketdatei mithilfe von **System.IO.File** .  
  
4.  Verwenden Sie **add_DacActionStarted** und **add_DacActionFinished** , um die DAC-Bereitstellungsereignisse zu abonnieren.  
  
5.  Legen Sie die **DatabaseDeploymentProperties**fest.  
  
6.  Verwenden Sie die **DacStore.Install** -Methode zum Bereitstellen der DAC.  
  
7.  Schließen Sie den Dateidatenstrom, der zum Lesen der DAC-Paketdatei verwendet wurde.  
  
## <a name="powershell-examples"></a>PowerShell-Beispiele  
 Im folgenden Beispiel wird eine DAC mit dem Namen "MyApplication" auf einer Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]bereitgestellt, wobei eine DAC-Definition aus einem MyApplication.dacpac-Paket verwendet wird.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC deployment events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Deploy the DAC and create the database.  
$dacName  = "MyApplication"  
$evaluateTSPolicy = $true  
$deployProperties = New-Object Microsoft.SqlServer.Management.Dac.DatabaseDeploymentProperties($serverconnection,$dacName)  
$dacstore.Install($dacType, $deployProperties, $evaluateTSPolicy)  
$fileStream.Close()  
```  
  
## <a name="more-information"></a>Weitere Informationen 
 [Datenebenenanwendungen](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Extrahieren einer DAC aus einer Datenbank](../../relational-databases/data-tier-applications/extract-a-dac-from-a-database.md)   
 [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md)  
  
  

