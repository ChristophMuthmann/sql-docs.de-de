---
title: Upgrade einer Datenebenenanwendung | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: data-tier-applications
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.upgradedacwizard.summary.f1
- sql13.swb.upgradedacwizard.reviewplan.f1
- sql13.swb.upgradedacwizard.upgradedac.f1
- sql13.swb.upgradedacwizard.selectpackage.f1
- sql13.swb.upgradedacwizard.reviewpolicy.f1
- sql13.swb.upgradedacwizard.selectoptions.f1
- sql13.swb.upgradedacwizard.checkdrift.f1
- sql13.swb.upgradedacwizard.introduction.f1
helpviewer_keywords:
- upgrade DAC
- data-tier application [SQL Server], upgrade
- wizard [DAC], upgrade
- How to [DAC], upgrade
ms.assetid: c117df94-f02b-403f-9383-ec5b3ac3763c
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d374f66debb936b1b57cb631d9e1643cc923fdc4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="upgrade-a-data-tier-application"></a>Upgrade einer Datenebenenanwendung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Verwenden Sie entweder den Assistenten zum Aktualisieren von Datenebenenanwendungen oder ein Windows PowerShell-Skript, um das Schema und die Eigenschaften einer derzeit bereitgestellten Datenebenenanwendung (DAC) so zu ändern, dass sie mit dem Schema und den Eigenschaften übereinstimmt, die in einer neuen Version der DAC definiert sind.  
  
-   **Vorbereitungen:**  [Auswählen von DAC-Aktualisierungsoptionen](#ChoseDACUpgOptions), [Einschränkungen](#LimitationsRestrictions), [Voraussetzungen](#Prerequisites), [Sicherheit](#Security), [Berechtigungen](#Permissions)  
  
-   **Aktualisieren einer DAC mit:**  [Assistent zum Aktualisieren von Datenebenenanwendungen](#UsingDACUpgradeWizard), [PowerShell](#UpgradeDACPowerShell)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
 Eine DAC-Aktualisierung ist ein direkter Prozess, mit dem das Schema der vorhandenen Datenbank so geändert wird, dass es dem in einer neuen Version der DAC definierten Schema entspricht. Die neue Version der DAC wird in einer DAC-Paketdatei bereitgestellt. Weitere Informationen zum Erstellen eines DAC-Pakets finden Sie unter [Datenebenenanwendungen](../../relational-databases/data-tier-applications/data-tier-applications.md).  
  
###  <a name="ChoseDACUpgOptions"></a> Auswählen von DAC-Aktualisierungsoptionen  
 Für eine parallele Aktualisierung stehen vier Aktualisierungsoptionen zur Verfügung:  
  
-   **Datenverlust ignorieren** – Wenn auf **True**festgelegt, wird die Aktualisierung auch dann fortgesetzt, wenn einige der Vorgänge zu Datenverlust führen. Wenn auf **False**festgelegt, wird bei solchen Vorgängen die Aktualisierung beendet. Wenn beispielsweise eine Tabelle in der aktuellen Datenbank im Schema der neuen DAC nicht vorhanden ist, wird die Tabelle gelöscht, wenn **True** festgelegt ist. Die Standardeinstellung ist **True**.  
  
-   **Bei Änderungen blockieren** – Wenn auf **True**festgelegt, wird die Aktualisierung beendet, wenn sich das Datenbankschema von dem in der vorherigen DAC definierten Schema unterscheidet. Wenn auf **False**festgelegt, wird die Aktualisierung auch dann fortgesetzt, wenn Änderungen erkannt werden. Die Standardeinstellung ist **False**.  
  
-   **Rollback bei Fehler** – Wenn auf **True**festgelegt, wird die Aktualisierung in eine Transaktion eingeschlossen, und wenn Fehler auftreten, wird ein Rollback versucht. Wenn auf **False**festgelegt, wird für alle Änderungen bei ihrer Erstellung ein Commit ausgeführt, und wenn Fehler auftreten, muss möglicherweise eine vorherige Sicherung der Datenbank wiederhergestellt werden. Die Standardeinstellung ist **False**.  
  
-   **Richtlinienüberprüfung überspringen** – Wenn auf **True**festgelegt, wird die DAC-Richtlinie zur Serverauswahl nicht überprüft. Wenn auf **False**festgelegt, wird die Richtlinie ausgewertet, und im Fall eines Fehlers wird die Aktualisierung beendet. Die Standardeinstellung ist **False**.  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
 DAC-Aktualisierungen können nur in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]oder [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ab Service Pack 4 (SP4) durchgeführt werden.  
  
###  <a name="Prerequisites"></a> Voraussetzungen  
 Vor dem Beginn der Aktualisierung muss eine vollständige Datenbanksicherung durchgeführt werden. Wenn bei einer Aktualisierung ein Fehler auftritt und kein Rollback für alle Aktualisierungen ausgeführt werden kann, müssen Sie möglicherweise die Sicherung wiederherstellen.  
  
 Vor dem Starten der Aktualisierung gibt es mehrere Aktionen, die Sie durchführen sollten, um das DAC-Paket und die Aktualisierungsaktionen zu validieren. Weitere Informationen zum Ausführen dieser Tests finden Sie unter [Validate a DAC Package](../../relational-databases/data-tier-applications/validate-a-dac-package.md).  
  
-   Es wird davon abgeraten, für die Aktualisierung ein DAC-Paket aus unbekannten oder nicht vertrauenswürdigen Quellen zu verwenden. Solche Pakete können schädlichen Code enthalten, der möglicherweise unbeabsichtigten Transact-SQL-Code ausführt oder Fehler verursacht, indem er das Schema ändert. Bevor Sie ein Paket aus einer unbekannten oder nicht vertrauenswürdigen Quelle verwenden, entpacken Sie die DAC, und untersuchen Sie den Code, z. B. gespeicherte Prozeduren oder sonstigen benutzerdefinierten Code.  
  
-   Wenn nach der Bereitstellung der letzten Version der DAC Änderungen an der aktuellen Datenbank vorgenommen wurden, verhindern einige Änderungen möglicherweise den erfolgreichen Abschluss der Aktualisierung, oder sie werden durch die Aktualisierung entfernt. Sie müssen zuerst einen Bericht mit solchen an der Datenbank vorgenommenen Änderungen generieren.  
  
-   Es ist unerlässlich, eine Liste der Änderungen des Schemas zu generieren, die bei der Aktualisierung durchgeführt werden, und diese auf mögliche Probleme zu überprüfen.  
  
 Der Anwendungsname im DAC-Paket muss mit dem Anwendungsnamen der gerade bereitgestellten DAC übereinstimmen. Wenn die aktuelle DAC z. B. den Anwendungsnamen **GeneralLedger**hat, können Sie die Aktualisierung nur mithilfe eines DAC-Pakets ausführen, das ebenfalls den Anwendungsnamen **GeneralLedger**aufweist.  
  
 Stellen Sie sicher, dass im Transaktionsprotokoll ausreichend Speicherplatz verfügbar ist, um alle Änderungen zu protokollieren.  
  
###  <a name="Security"></a> Sicherheit  
 Zur Erhöhung der Sicherheit werden die Anmeldenamen für die SQL Server-Authentifizierung ohne Kennwort in einem DAC-Paket gespeichert. Sobald das Paket bereitgestellt oder aktualisiert wird, wird der Anmeldename als deaktivierter Anmeldename mit einem generierten Kennwort erstellt. Um die Anmeldenamen zu aktivieren, melden Sie sich unter einem Anmeldenamen an, der über die ALTER ANY LOGIN-Berechtigung verfügt, und verwenden ALTER LOGIN, um den Anmeldenamen zu aktivieren und ein neues Kennwort zuzuweisen, das dem Benutzer mitgeteilt werden kann. Dies ist für Anmeldenamen der Windows-Authentifizierung nicht erforderlich, da die zugehörigen Kennwörter nicht von SQL Server verwaltet werden.  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Aktualisierung einer DAC kann nur von Mitgliedern der festen Serverrollen **sysadmin** oder **serveradmin** durchgeführt werden bzw. unter Verwendung von Anmeldenamen aus der festen Serverrolle **dbcreator** , die über ALTER ANY-LOGIN-Berechtigungen verfügen. Die Anmeldung muss als Besitzer der vorhandenen Datenbank erfolgen. Außerdem kann die DAC auch mit dem integrierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemadministratorkonto mit der Bezeichnung **sa** aktualisiert werden.  
  
##  <a name="UsingDACUpgradeWizard"></a> Verwenden des Assistenten zum Aktualisieren von Datenebenenanwendungen  
 **So aktualisieren Sie eine DAC mithilfe eines Assistenten**  
  
1.  Erweitern Sie im **Objekt-Explorer**den Knoten für die Instanz, die die zu aktualisierende DAC enthält.  
  
2.  Erweitern Sie nacheinander die Knoten **Verwaltung** und **Datenebenenanwendungen** .  
  
3.  Klicken Sie mit der rechten Maustaste auf den Knoten der zu aktualisierenden DAC, und wählen Sie dann **Datenebenenanwendung aktualisieren...**aus.  
  
4.  Bearbeiten Sie die Dialogfenster des Assistenten:  
  
    1.  [Seite "Einführung"](#Introduction)  
  
    2.  [Seite "Paket auswählen"](#Select_dac_package)  
  
    3.  [Seite "Richtlinie überprüfen"](#Review_policy)  
  
    4.  [Seite "Änderung erkennen"](#Detect_change)  
  
    5.  [Upgradeplan überprüfen](#ReviewUpgPlan)  
  
    6.  [Seite "Zusammenfassung"](#Summary)  
  
    7.  [Seite "DAC aktualisieren"](#Upgrade)  
  
##  <a name="Introduction"></a> Seite "Einführung"  
 Auf dieser Seite werden die Schritte zum Aktualisieren einer Datenebenenanwendung beschrieben.  
  
 **Diese Seite nicht mehr anzeigen.** – Aktivieren Sie dieses Kontrollkästchen, damit die Seite in Zukunft nicht mehr angezeigt wird.  
  
 **Weiter >**: Geht zur Seite **Paket auswählen** über.  
  
 **Abbrechen** : Beendet den Assistenten, ohne die DAC zu aktualisieren.  
  
##  <a name="Select_dac_package"></a> Seite "Paket auswählen"  
 Verwenden Sie diese Seite, um das DAC-Paket anzugeben, das die neue Version der Datenebenenanwendung enthält. Die Seite durchläuft zwei Statusübergänge.  
  
### <a name="select-the-dac-package"></a>Auswählen des DAC-Pakets  
 Verwenden Sie die Seite in ihrem Ausgangszustand, um das bereitzustellende DAC-Paket auszuwählen. Das DAC-Paket muss eine gültige DAC-Paketdatei sein und die Erweiterung .dacpac aufweisen. Der DAC-Anwendungsname im DAC-Paket muss dem Anwendungsnamen der aktuellen DAC entsprechen.  
  
 **DAC-Paket** : Geben Sie den Pfad und Dateinamen des DAC-Pakets an, das die neue Version der Datenebenenanwendung enthält. Sie können die Schaltfläche **Durchsuchen** rechts neben dem Feld auswählen, um zum Speicherort des DAC-Pakets zu wechseln.  
  
 **Anwendungsname** : Ein schreibgeschütztes Feld mit dem DAC-Anwendungsnamen, der beim Erstellen oder Extrahieren der DAC aus einer Datenbank zugewiesen wurde.  
  
 **Version** : Ein schreibgeschütztes Feld mit der Version, die beim Erstellen oder Extrahieren der DAC aus einer Datenbank zugewiesen wurde.  
  
 **Beschreibung**: Ein schreibgeschütztes Feld mit der Beschreibung, die beim Erstellen oder Extrahieren der DAC aus einer Datenbank erstellt wurde.  
  
 **< Zurück**: Kehrt zur Seite **Einführung** zurück.  
  
 **Weiter >**: Zeigt eine Statusanzeige an, da der Assistent bestätigt, dass es sich bei der ausgewählten Datei um ein gültiges DAC-Paket handelt.  
  
 **Abbrechen**: Beendet den Assistenten, ohne die DAC zu aktualisieren.  
  
### <a name="validating-the-dac-package"></a>Überprüfen des DAC-Pakets  
 Zeigt eine Statusanzeige an, da der Assistent bestätigt, dass es sich bei der ausgewählten Datei um ein gültiges DAC-Paket handelt. Wenn das DAC-Paket überprüft wird, geht der Assistent zur Seite **Richtlinie überprüfen** über. Wenn die Datei kein gültiges DAC-Paket ist, verbleibt der Assistent auf der Seite **DAC-Paket auswählen** . Wählen Sie entweder ein anderes gültiges DAC-Paket aus, oder brechen Sie den Assistenten ab, und generieren Sie ein neues DAC-Paket.  
  
 **Der DAC-Inhalt wird überprüft**: Die Statusanzeige, die den aktuellen Status des Überprüfungsprozesses angibt.  
  
 **< Zurück**: Kehrt zum Ausgangszustand der Seite **Paket auswählen** zurück.  
  
 **Weiter >**: Geht zur abschließenden Version der Seite **Paket auswählen** über.  
  
 **Abbrechen** : Beendet den Assistenten, ohne die DAC bereitzustellen.  
  
##  <a name="Review_policy"></a> Seite "Richtlinie überprüfen"  
 Verwenden Sie diese Seite, um die Auswertungsergebnisse der DAC-Richtlinie zur Serverauswahl zu überprüfen, wenn die DAC über eine Richtlinie verfügt. Die DAC-Richtlinie zur Serverauswahl ist optional und wird einer in Microsoft Visual Studio erstellten DAC zugewiesen. Die Richtlinie verwendet Facets für die Richtlinie zur Serverauswahl, um Bedingungen anzugeben, die eine [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz zum Hosten der DAC erfüllen sollte.  
  
 **Auswertungsergebnisse der Richtlinienbedingungen** : Ein schreibgeschützter Bericht, der anzeigt, ob die Auswertungen der Bedingungen in der DAC-Richtlinie zur Serverauswahl erfolgreich waren. Die Auswertungsergebnisse für die einzelnen Bedingungen werden in einer separaten Zeile angezeigt.  
  
 **Richtlinienverletzungen ignorieren** : Verwenden Sie dieses Kontrollkästchen, um mit dem Upgrade fortzufahren, wenn eine oder mehrere Richtlinienbedingungen nicht erfüllt wurden. Aktivieren Sie diese Option nur, wenn Sie sicher sind, dass keine der fehlgeschlagenen Bedingungen die erfolgreiche Ausführung der DAC verhindert.  
  
 **< Zurück**: Kehrt zur Seite **Paket auswählen** zurück.  
  
 **Weiter >**: Geht zur Seite **Änderung erkennen** über.  
  
 **Abbrechen** : Beendet den Assistenten, ohne die DAC zu aktualisieren.  
  
##  <a name="Detect_change"></a> Seite "Änderung erkennen"  
 Auf dieser Seite werden die Ergebnisse angezeigt, die die Assistenten bei der Suche nach Datenbankänderungen gefunden haben und die auf eine Abweichung zwischen dem Datenbankschema und der in der **msdb**-Datenbank in den DAC-Metadaten gespeicherten Schemadefinition hindeuten. Beispielsweise wurden die Anweisungen CREATE, ALTER oder DROP verwendet, um Objekte nach der ursprünglichen Bereitstellung der DAC zur Datenbank hinzuzufügen, Objekte zu ändern oder zu entfernen. Auf der Seite werden zuerst eine Statusanzeige und dann die Analyseergebnisse angezeigt.  
  
 **Änderung wird ermittelt. Dieser Vorgang kann einige Minuten dauern** : Zeigt eine Statusanzeige an, während der Assistent Unterschiede zwischen dem aktuellen Schema der Datenbank und den Objekten in der DAC-Definition sucht.  
  
 **Erkennungsergebnisse ändern** : Gibt an, dass die Analyse abgeschlossen wurde. Die Ergebnisse werden darunter angezeigt.  
  
 **Die DatabaseName-Datenbank wurde nicht geändert** : Der Assistent hat keine Unterschiede zwischen den in der Datenbank definierten Objekten und ihren Äquivalenten in der DAC-Definition festgestellt.  
  
 **Die DatabaseName-Datenbank wurde geändert** : Der Assistent hat Unterschiede zwischen den Objekten in der Datenbank und ihren Äquivalenten in der DAC-Definition festgestellt.  
  
 **Vorgang fortsetzen, obwohl Änderungen verloren gehen können** : Sie wurden informiert, dass einige der Objekte oder Daten in der aktuellen Datenbank nicht in der neuen Datenbank vorhanden sein werden, möchten die Aktualisierung aber dennoch fortsetzen. Sie sollten diese Schaltfläche nur aktivieren, wenn Sie den Änderungsbericht überprüft und verstanden haben, welche Schritte erforderlich sind, um Objekte oder Daten, die in der neuen Datenbank erforderlich sind, manuell zu übertragen. Wenn Sie nicht sicher sind, klicken Sie auf die Schaltfläche **Bericht speichern** , um den Änderungsbericht zu speichern, und klicken Sie dann auf **Abbrechen**. Analysieren Sie den Bericht, planen Sie die Übertragung erforderlicher Objekte und Daten nach dem Upgrade, und starten Sie den Assistenten erneut.  
  
 **Bericht speichern** : Klicken Sie auf die Schaltfläche, um einen Bericht der Änderungen zu speichern, die der Assistent zwischen den Objekten in der Datenbank und ihren Äquivalenten in der DAC-Definition festgestellt hat. Sie können dann den Bericht überprüfen, um zu bestimmen, ob Sie nach dem Upgrade Maßnahmen ergreifen müssen, um einige oder alle im Bericht aufgeführten Objekte in die neue Datenbank zu integrieren.  
  
 **< Zurück**: Kehrt zur Seite **DAC-Paket auswählen** zurück.  
  
 **Weiter >**: Geht zur Seite **Optionen** über.  
  
 **Abbrechen**: Beendet den Assistenten, ohne die DAC bereitzustellen.  
  
## <a name="options-page"></a>Seite "Optionen"  
 Verwenden Sie diese Seite, um das Rollback bei Fehlern für die Aktualisierung auszuwählen.  
  
 **Rollback bei Fehler** – Wählen Sie diese Option aus, um die Aktualisierung in eine Transaktion einzuschließen. Der Assistent kann beim Auftreten von Fehlern dann versuchen, ein Rollback durchzuführen. Weitere Informationen zu dieser Option finden Sie unter [Auswählen von DAC-Aktualisierungsoptionen](#ChoseDACUpgOptions).  
  
 **Standardwerte wiederherstellen**: Setzt die Option auf die Standardeinstellung „false“ zurück.  
  
 **< Zurück**: Geht zur Seite **Änderung erkennen** zurück.  
  
 **Weiter >**: Geht zur Seite **Upgradeplan überprüfen** über.  
  
 **Abbrechen** : Beendet den Assistenten, ohne die DAC bereitzustellen.  
  
##  <a name="ReviewUpgPlan"></a> Seite "Upgradeplan überprüfen"  
 Verwenden Sie diese Seite, um die Aktionen zu überprüfen, die beim Aktualisieren ausgeführt werden. Fahren Sie nur dann fort, wenn Sie sicher sind, dass durch die Aktualisierung keine Probleme verursacht werden.  
  
 **Die folgenden Aktionen werden zum Aktualisieren der DAC verwendet.** – Überprüfen Sie die angezeigten Informationen darauf, ob die ergriffenen Maßnahmen richtig sind. In der Spalte **Aktion** werden die Aktionen angezeigt, die für die Aktualisierung ausgeführt werden, z.B. Transact-SQL-Anweisungen. Die Spalte **Datenverlust** enthält eine Warnung, wenn durch die zugeordnete Aktion Daten gelöscht werden könnten.  
  
 **Aktualisieren** – Aktualisiert die Liste der Aktionen.  
  
 **Aktionsbericht speichern** – Speichert den Inhalt des Aktionsfensters in einer HTML-Datei.  
  
 **Vorgang fortsetzen, obwohl Änderungen verloren gehen können** : Sie wurden informiert, dass einige der Objekte oder Daten in der aktuellen Datenbank nicht in der neuen Datenbank vorhanden sein werden, möchten die Aktualisierung aber dennoch fortsetzen. Sie sollten diese Schaltfläche nur aktivieren, wenn Sie den Änderungsbericht überprüft und verstanden haben, welche Schritte erforderlich sind, um Objekte oder Daten, die in der neuen Datenbank erforderlich sind, manuell zu übertragen. Wenn Sie nicht sicher sind, klicken Sie auf die Schaltfläche **Aktionsbericht speichern** , um den Änderungsbericht zu speichern. Klicken Sie auf die Schaltfläche **Skripts speichern** , um das Transact-SQL-Skript zu speichern, und klicken Sie dann auf **Abbrechen**. Analysieren Sie den Bericht und das Skript, planen Sie die Übertragung erforderlicher Objekte und Daten nach der Aktualisierung, und starten Sie den Assistenten erneut.  
  
 **Skripts speichern** : Speichert die für die Aktualisierung verwendeten Transact-SQL-Anweisungen in einer Textdatei.  
  
 **Standardwerte wiederherstellen**: Setzt die Option auf die Standardeinstellung „false“ zurück.  
  
 **< Zurück**: Geht zur Seite **Änderung erkennen** zurück.  
  
 **Weiter >**: Geht zur Seite **Zusammenfassung** über.  
  
 **Abbrechen** : Beendet den Assistenten, ohne die DAC bereitzustellen.  
  
##  <a name="Summary"></a> Seite "Zusammenfassung"  
 Verwenden Sie diese Seite, um ein letztes Mal die Aktionen zu überprüfen, die der Assistent beim Aktualisieren der DAC ausführt.  
  
 **Die folgenden Einstellungen werden zum Aktualisieren der DAC verwendet.** – Überprüfen Sie die angezeigten Informationen darauf, ob die ergriffenen Maßnahmen richtig sind. Das Fenster zeigt die zur Aktualisierung ausgewählte DAC und das DAC-Paket an, das die neue Version der DAC enthält. Im Fenster wird außerdem angezeigt, ob die aktuelle Version der Datenbank der aktuellen DAC-Definition entspricht oder ob die Datenbank geändert wurde.  
  
 **< Zurück**: Geht zur Seite **Upgradeplan überprüfen** zurück.  
  
 **Weiter >**: Stellt die DAC bereit und zeigt die Ergebnisse auf der Seite **DAC aktualisieren** an.  
  
 **Abbrechen** : Beendet den Assistenten, ohne die DAC bereitzustellen.  
  
##  <a name="Upgrade"></a> Seite "DAC aktualisieren"  
 Auf dieser Seite wird angegeben, ob der Upgradevorgang erfolgreich war oder fehlgeschlagen ist.  
  
 **DAC wird aktualisiert** : Gibt an, ob die Aktionen zur Aktualisierung der DAC erfolgreich oder fehlerhaft waren. Überprüfen Sie die Informationen, um zu bestimmen, ob die einzelnen Aktionen erfolgreich waren oder fehlgeschlagen sind. Für alle Aktionen, die fehlerhaft waren, ist in der Spalte **Ergebnis** ein Link enthalten. Klicken Sie auf den Link, um einen Bericht des für diese Aktion aufgetretenen Fehlers anzuzeigen.  
  
 **Bericht speichern** : Klicken Sie auf diese Schaltfläche, um den Aktualisierungsbericht in einer HTML-Datei zu speichern. In der Datei ist der Status der einzelnen Aktionen aufgeführt, einschließlich aller durch die Aktionen generierten Fehler. Der Standardordner ist ein Ordner "SQL Server Management Studio\DAC Packages" im Ordner "Dokumente" unter Ihrem Windows-Konto.  
  
 **Fertig stellen** : Beendet den Assistenten.  
  
##  <a name="UpgradeDACPowerShell"></a> PowerShell  
 **Aktualisieren einer DAC mithilfe der IncrementalUpgrade()-Methode in einem PowerShell-Skript**  
  
1.  Erstellen Sie ein SMO-Serverobjekt, und legen Sie es auf die Instanz fest, die die zu aktualisierende DAC enthält.  
  
2.  Öffnen Sie ein **ServerConnection** -Objekt, und stellen Sie eine Verbindung mit derselben Instanz her.  
  
3.  Laden Sie die DAC-Paketdatei mithilfe von **System.IO.File** .  
  
4.  Verwenden Sie **add_DacActionStarted** und **add_DacActionFinished** , um die DAC-Aktualisierungsereignisse zu abonnieren.  
  
5.  Legen Sie die **DacUpgradeOptions**fest.  
  
6.  Verwenden Sie die **IncrementalUpgrade** -Methode zum Aktualisieren der DAC.  
  
7.  Schließen Sie den Dateidatenstrom, der zum Lesen der DAC-Paketdatei verwendet wurde.  
  
### <a name="example-powershell"></a>Beispiel (PowerShell)  
 Im folgenden Beispiel wird eine DAC mit dem Namen „MyApplication“ auf einer Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] aktualisiert, wobei eine neue DAC-Version in einem „MyApplication2017.dacpac“-Paket verwendet wird.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication2017.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC upgrade events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Upgrade the DAC and close the package.  
$dacName  = "MyApplication"  
  
## Set the upgrade options.  
$upgradeProperties = New-Object Microsoft.SqlServer.Management.Dac.DacUpgradeOptions  
$upgradeProperties.blockonchanges = $true  
$upgradeProperties.ignoredataloss = $false  
$upgradeProperties.rollbackonfailure = $true  
$ upgradeProperties.skippolicyvalidation = $false  
  
## Upgrade the DAC  
$dacstore.IncrementalUpgrade($dacName, $dacType, $upgradeProperties)  
## Close the package file.  
$fileStream.Close()  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenebenenanwendungen](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [SQL Server-PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
