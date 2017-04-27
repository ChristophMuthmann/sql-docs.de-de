---
title: "SQL Server Management Studio – Änderungsprotokoll (SSMS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
caps.latest.revision: 72
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f2144751277bb10897e0ed39ee24dbad8a32b4ce
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio - Changelog (SSMS)

## <a name="ssms-1653-release"></a>Veröffentlichung von SSMS 16.5.3
Allgemein verfügbar | Buildnummer: 13.0.16106.4

In dieser Version wurden folgende Probleme behoben:

* Das seit SSMS 16.5.2 auftretende Problem wurde behoben, das die Erweiterung des Knotens „Tabelle“ verursacht hat, wenn die Tabelle mindestens eine Spalte mit geringer Dichte aufwies.

* Benutzer können SSIS-Pakete bereitstellen, die den OData-Verbindungs-Manager enthalten und die eine AX/CRM-Onlineressource von Microsoft Dynamix mit dem SSIS-Katalog verbinden. Weitere Informationen finden Sie unter [OData-Verbindungs-Manager](https://msdn.microsoft.com/library/dn584133.aspx).

* Konfigurieren von „Always Encrypted“ schlägt für eine vorhandene Tabelle fehl mit Fehlern für nicht verknüpfte Objekte. [Connect-ID 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* Konfigurieren von „Always Encrypted“ funktioniert nicht für eine vorhandene Datenbank mit mehreren Schemas. [Connect-ID 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* Der Assistent für „Always Encrypted“ und „Verschlüsselte Spaltendaten“ versagt, wenn die Datenbank Sichten enthält, die auf Systemsichten verweisen. [Connect-ID 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* Bei der Verschlüsselung mit „Always Encrypted“ werden Fehler durch das Aktualisieren von Modulen nach der Verschlüsselung falsch verarbeitet.

* Das Menü *Zuletzt verwendete öffnen* zeigt keine zuletzt gespeicherten Dateien an. [Connect-ID 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* SSMS ist sehr langsam, wenn mit der rechten Maustaste auf den Tabellenindex geklickt wurde (über eine Remote(internet)verbindung). [Connect-ID 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)
 
* Ein Problem mit der Bildlaufleiste von SQL Designer wurde behoben. [Connect-ID 3114856](http://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* Das Tabellenkontextmenü hängt vorübergehend 
 
* SSMS löst gelegentlich Ausnahmen auf dem Aktivitätsmonitor aus und stürzt anschließen ab. [Connect-ID 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* SSMS 2016 stürzt ab mit der Fehlermeldung „The process was terminated due to an internal error in the .NET Runtime at IP 71AF8579 (71AE0000) with exit code 80131506“ (Der Vorgang wurde aufgrund eines internen Fehlers in der .NET-Laufzeit in der IP 71AF8579 (71AE0000) mit dem Exitcode 80131506 beendet).


## <a name="ssms-1651-release"></a>Release von SSMS 16.5.1
Allgemein verfügbar | Buildnummer: 13.0.16100.1

* Es wurde ein Problem behoben, bei dem Invoke-Sqlcmd fälschlicherweise mehrere Zeilen einfügt, wenn CHECK-Einschränkungen auftreten. [Microsoft Connect-Element: 811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

* Es wurde ein Problem behoben, das dazu geführt hat, dass nicht-ENU Sprachversionen beim Erstellen von Verfügbarkeitsgruppen nicht vollständig funktionieren.

* Es wurde ein Problem behoben, das dazu geführt hat, dass durch Klicken auf die Abfrageplan-XML nicht die richtige SSMS-Benutzeroberfläche geöffnet wurde.


## <a name="ssms-165-release"></a>Release von SSMS 16.5
Allgemein verfügbar | Buildnummer: 13.0.16000.28

* Es wurde ein Problem behoben, bei dem ein Absturz passieren könnte, wenn eine Datenbank mit dem Tabellennamen, der „;:“ enthält, angeklickt wird.
* Es wurde ein Problem behoben, bei dem Änderungen, die auf der Seite„Neues Modell“ im Fenster „AS Tabular Database Properties“ (Datenbankeigenschaften der AS-Tabelle) durchgeführt wurden, die ursprüngliche Definition ausgeben würden. 
[Microsoft Connect-Element: 3080744](https://connect.microsoft.com/SQLServer/feedback/details/3080744) 
* Es wurde ein Problem behoben, bei dem die temporären Dateien zur Liste „Zuletzt verwendete Dateien“ hinzugefügt werden.  
[Microsoft Connect-Element: 2558789](https://connect.microsoft.com/SQLServer/feedback/details/2558789)
* Es wurde ein Problem behoben, bei dem das Menüelement „Komprimierung verwalten für die Benutzertabelle in der Objekt-Explorer-Struktur deaktiviert ist.  
[Microsoft Connect-Element: 3104616](https://connect.microsoft.com/SQLServer/feedback/details/3104616)

* Es wurde ein Problem behoben, bei dem der Benutzer nicht den Schriftgrad für den Objekt-Explorer, den registrierten Server-Explorer, den Vorlagen-Explorer sowie Details für den Objekt Explorer festlegen kann. Die Schriftart für die Explorer wird die Umgebungsschriftart sein.  
[Microsoft Connect-Element: 691432](https://connect.microsoft.com/SQLServer/feedback/details/691432)

* Es wurde ein Problem behoben, bei dem SSMS sich immer mit der Standarddatenbank verbindet, wenn die Verbindung unterbrochen wurde.  
[Microsoft Connect-Element: 3102337](https://connect.microsoft.com/SQLServer/feedback/details/3102337)

* Viele der Probleme mit hoher DPI in der Richtlinienverwaltung und dem Abfrage-Editorfenster, einschließlich der Symbole im grafischen Ausführungsplan, wurden behoben.

* Es wurde ein Problem behoben, bei dem die Option zum Konfigurieren der Schriftart und der Farbe für das erweiterte Ereignis fehlen.

* Es wurde ein Problem behoben, bei dem SSMS-Abstürze auftreten, wenn die Anwendung geschlossen wird, oder wenn sie versucht, das Fehlerdialogfeld anzuzeigen.


## <a name="ssms-1641-september-2016-release"></a>SSMS-Release 16.4.1 (September 2016)
Allgemein verfügbar | Buildnummer: 13.0.15900.1

*  Problem behoben, das zu einem Fehler beim Ausführen von ALTER/Modify einer gespeicherten Prozedur führt:  
[Microsoft Connect-Element #3103831](https://connect.microsoft.com/SQLServer/feedback/details/3103831)

* Neue Cmdlets „Read-SqlTableData“, „Read-SqlViewData“ und „Write-SqlTableData“ zum Anzeigen und Schreiben von Daten mithilfe von PowerShell.  
[Trello-Karte zu „Read-SqlTableData“](https://trello.com/c/FXVUNJ8x/131-read-sqltabledata)  
[Microsoft Connect-Element #2685363](https://connect.microsoft.com/SQLServer/feedback/details/2685363)
    
* Neues Cmdlet „Add-SqlLogin“ für neue Anmeldeverwaltungsszenarios mithilfe von PowerShell.  
[Microsoft Connect-Element #2588952](https://connect.microsoft.com/SQLServer/feedback/details/2588952)
    
*  Verbesserte Unterstützung und Nutzbarkeit für Benutzer, die Verbindungen mit verschiedenen nationalen Clouds herstellen.
    
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass Ausnahmen wegen unzureichenden Arbeitsspeichers ausgelöst wurden.  
[Microsoft Connect-Element #3062914](https://connect.microsoft.com/SQLServer/feedback/details/3062914)  
[Microsoft Connect-Element #3074856](https://connect.microsoft.com/SQLServer/feedback/details/3074856)
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass Filtern nach einem Schema keine gültige Filteroption war.  
[Microsoft Connect-Element #3058105](https://connect.microsoft.com/SQLServer/feedback/details/3058105)  
[Microsoft Connect-Element #3101136](https://connect.microsoft.com/SQLServer/feedback/details/3101136)
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass kein Zugriff auf das Monitorfenster einer gestreckten Datenbank möglich war.
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass die F1-Hilfe immer Onlineinhalt geöffnet hat. Benutzer können jetzt über den Befehl „Hilfeeinstellungen festlegen“ aus dem Menü „Hilfe“ festlegen, ob Online- oder Offlinehilfe angezeigt werden soll.   
[Microsoft Connect-Element #2826366](https://connect.microsoft.com/SQLServer/feedback/details/2826366)
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass das skriptgesteuerte Auslesen eines tabellarischen Analysis Services-Modells auf Level 1200 nicht das Kennwort für Skripterstellung hervorgebracht hat, obwohl die Serverversion dies getan hat [das Clientmodellobjekt wird nun vor der Skripterstellung synchronisiert].
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass „SELECT TOP N ROWS“ eine veraltete Syntax für den TOP-Operator generiert hat.  
[Microsoft Connect-Element #3065435](https://connect.microsoft.com/SQLServer/feedback/details/3065435)
    
*  Es wurden verschiedene Layoutprobleme im gesamten SSMS behoben, einschließlich der Seite „Anmeldungseigenschaften“ und der Optionen zur erweiterten Abfrageausführung.   
[Microsoft Connect-Element #3058199](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect-Element #3079122](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect-Element #3071384](https://connect.microsoft.com/SQLServer/feedback/details/3071384)
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass automatisch immer dann eine Lösung erstellt wurde, wenn ein Benutzer ein neues Abfragefenster erstellt hat.   
[Microsoft Connect-Element #2924667](https://connect.microsoft.com/SQLServer/feedback/details/2924667)    
[Microsoft Connect-Element #2917742](https://connect.microsoft.com/SQLServer/feedback/details/2917742)   
[Microsoft Connect-Element #2612635](https://connect.microsoft.com/SQLServer/feedback/details/2612635)
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass temporale Tabellen im Objekt-Explorer in Systemdatenbanken nicht erweitert werden konnten.  
[Microsoft Connect-Element #2551649](https://connect.microsoft.com/SQLServer/feedback/details/2551649)
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass SSMS nach der Ausführung eines Batches eine Abfrage mit SELECT @@trancount ausgeführt hat.    
[Microsoft Connect-Element #3042364](https://connect.microsoft.com/SQLServer/feedback/details/3042364)
    
*  Es wurde ein Problem in Analysis Services behoben, das dazu geführt hat, dass beim Erstellen eines Skripts über die Seite „Eigenschaften“ eines Servers das Dialogfeld „Verbindung“ ausgeblendet wurde.
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass mit STRG+Q nicht die Schnellstart-Symbolleiste ausgewählt wurde.
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass ein Ändern der maximalen Größe (MaxSize) einer Datenbank über das Dialogfeld „Servereigenschaften“ für Datenbanken > 2 TB nicht funktioniert hat.  
[Microsoft Connect-Element #1231091](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass der Assistent zum Wiederherstellen einer Datenbank keine Dateinamen mit führenden Leerzeichen akzeptiert hat:   
[Microsoft Connect-Element #2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="ssms-163-august-2016-release"></a>SSMS-Release 16.3 (August 2016)
Allgemein verfügbar | Versionsnummer: 13.0.15700.28

* Die monatlichen Releases von SSMS werden nun nummeriert.

* [Neue Authentifizierungsoption**„Universelle Active Directory-Authentifizierung“**](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Dieser tokenbasierte Authentifizierungsmechanismus wird durch Azure Active Directory gestützt und bietet Unterstützung für mehrstufige, kennwortbasierte und integrierte Authentifizierungsmechanismen.

* Neue Vorlagen für erweiterte Ereignisse mit derselben Funktionalität wie SQL Server Profiler-Vorlagen [(Microsoft Connect-Element #2543925)](https://connect.microsoft.com/SQLServer/feedback/details/2543925/sql-server-extended-events-profiler-tool). Weitere Informationen zu den enthaltenen [SQL Server Profiler-Vorlagen](https://msdn.microsoft.com/library/ms190176.aspx).

* Neue Dialogfelder zum Erstellen von Datenbanken sowie für Datenbankeigenschaften für Azure SQL-Datenbanken.

* Neue Cmdlets „Get-SqlLogin“ und „Remove-SqlLogin“ für die SQL Server-Anmeldeverwaltung mithilfe von PowerShell.  
*Verwandte Fehleranfragen von Kunden:*   
[Microsoft Connect-Element #2588952.](https://connect.microsoft.com/SQLServer/feedback/details/2588952/)

* Neues PowerShell-Cmdlet „New-SqlColumnMasterKeySettings“, mit dem Unterstützung für das Erstellen von Spaltenhauptschlüsseln für beliebige Anbieter und Schlüsselpfade hinzugefügt wird.

* Neues Dialogfeld „Datenbank erstellen“ zum Optimieren von Azure SQL-Datenbanken in SSMS>

* Unterstützung für das Filtern von Datenbanken im Knoten „Datenbanken“ des Objekt-Explorers von SSMS. Navigieren Sie im Objekt-Explorer zum Knoten „Datenbanken“, und klicken Sie auf das Filtersymbol in der Symbolleiste des Objekt-Explorers, um die Liste der Datenbanken zu filtern.

* Unterstützung für ARM-Speicherkonten (Azure Resource Manager) in den Sicherungs- und Wiederherstellungs-Assistenten.

* [Anfängliche Betaunterstützung für die Anzeige mit hoher Auflösung](https://blogs.msdn.microsoft.com/sqlreleaseservices/ssms-highdpi-support/).  
*Verwandte Fehleranfragen von Kunden:*   
[Microsoft Connect-Element #1129301](https://connect.microsoft.com/SQLServer/feedback/details/1129301/management-studio-is-unusable-on-a-4k-display), [Microsoft Connect-Element #1858763](https://connect.microsoft.com/SQLServer/feedback/details/1858763/), [Microsoft Connect-Element #1852671](https://connect.microsoft.com/SQLServer/feedback/details/1852671/), [Microsoft Connect-Element #1487643](https://connect.microsoft.com/SQLServer/feedback/details/1487643/),  [Microsoft Connect-Element #1355641](https://connect.microsoft.com/SQLServer/feedback/details/1355641/), [Microsoft Connect-Element #2161595](https://connect.microsoft.com/SQLServer/feedback/details/2161595/), [Microsoft Connect-Element #1854041](https://connect.microsoft.com/SQLServer/feedback/details/1854041/), [Microsoft Connect-Element #1055617](https://connect.microsoft.com/SQLServer/feedback/details/1055617/), [Microsoft Connect-Element #2448774](https://connect.microsoft.com/SQLServer/feedback/details/2448774/), [Microsoft Connect-Element #1521405](https://connect.microsoft.com/SQLServer/feedback/details/1521405/), [Microsoft Connect-Element #2117853](https://connect.microsoft.com/SQLServer/feedback/details/2117853/), [Microsoft Connect-Element #2014256](https://connect.microsoft.com/SQLServer/feedback/details/2014256/), [Microsoft Connect-Element #2162218](https://connect.microsoft.com/SQLServer/feedback/details/2162218/), [Microsoft Connect-Element #2344551](https://connect.microsoft.com/SQLServer/feedback/details/2344551/), [Microsoft Connect-Element #1664436](https://connect.microsoft.com/SQLServer/feedback/details/1664436/), [Microsoft Connect-Element #2554043](https://connect.microsoft.com/SQLServer/feedback/details/2554043/), [Microsoft Connect-Element #2983216](https://connect.microsoft.com/SQLServer/feedback/details/2983216/), [Microsoft Connect-Element #2021706](https://connect.microsoft.com/SQLServer/feedback/details/2021706/)

* Verbesserungen beim Datenbankoptimierungsratgeber (Database Engine Tuning Advisor, DTA), um das automatische Lesen von Workloads aus dem SQL Server-Abfragespeicher zu unterstützen.

* Verbesserungen beim Datenbankoptimierungsratgeber (Database Engine Tuning Advisor, DTA), um Indexempfehlungen für gruppierte Columnstore-Indizes, nicht gruppierte Columnstore-Indizes und Rowstore-Indizes anzuzeigen.

* Unterstützung für das Senden von Datenbankkonsolenbefehlen (DBCC) mithilfe von PowerShell-Cmdlets aus SQL Server Analysis Services.

* Programmfehlerbehebung, um den Klartext entschlüsselter Always Encrypted-LOB-Spalten (Large Object) in SSMS anzuzeigen.  
*Verwandte Fehleranfragen von Kunden:*   
[Microsoft Connect-Element #2413024](https://connect.microsoft.com/SQLServer/feedback/details/2413024/cannot-view-cleartext-of-alwaysencrypted-lob-columns-in-ssms)

* Programmfehlerbehebung im Always Encrypted-Dialogfeld, um einen Absturz zu behandeln, wenn Windows-Formatierungsvisualisierungen nicht aktiviert sind (z.B. Aktivierung der Anzeige mit hohem Kontrast).

* Programmfehlerbehebung für den Fehler „Methode nicht gefunden“, der Verbindungen mit SQL Server-Instanzen verhindert.

* Programmfehlerbehebung für den Absturz von SSMS beim Erstellen einer Partitionsfunktion mit „datetime offset“.

* Programmfehlerbehebung, um die Anforderung zu entfernen, dass Microsoft .NET 3.5 zum Starten des Distributed Replay-Verwaltungstools (DReplay.exe) erforderlich ist.

* Programmfehlerbehebung beim Bereitstellungs-Assistenten für Analysis Services, um vollqualifizierte Servernamen zu unterstützen.

* Programmfehlerbehebung in SSMS, um Partitionen in tabellarischen Analysis Services-Modellen mit einem 2016-Kompatibilitätsmodell anzuzeigen.  
*Verwandte Fehleranfragen von Kunden:*   
[Microsoft Connect-Element #2845053](https://connect.microsoft.com/SQLServer/feedback/details/2845053/ssms-cannot-display-partitions-in-tabular-models-in-2016-compatibility-level) 

* Leistungsverbesserungen und Programmfehlerbehebungen in tabellarischen Analysis Services-Modellen und freigegebenen Verwaltungsobjekten für Microsoft SQL Server. 


---
## <a name="ssms-july-2016-hotfix-update-release"></a>Hotfixupdate für SSMS – Juli 2016 
Allgemein verfügbar | Versionsnummer: 13.0.15600.2

* **Programmfehlerbehebung in SSMS, um fehlende Kontextmenüelemente zu aktivieren**.  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2883440](https://connect.microsoft.com/SQLServer/feedback/details/2883440/lost-table-design-and-edit-top-n-rows-in-tables-context-menu)  
[Microsoft Connect-Element #2909644](https://connect.microsoft.com/SQLServer/feedback/details/2909644/ssms-2016-is-missing-edit-options-against-sql-express-2014)  
[Microsoft Connect-Element #2924345](https://connect.microsoft.com/SQLServer/feedback/details/2924345/some-ssms-object-explorer-right-click-menu-options-missing-in-july-update)

---
## <a name="ssms-july-2016-release"></a>SSMS-Release Juli 2016 
Allgemein verfügbar | Versionsnummer: 13.0.15500.91

* *Bearbeitung 5. Juli:* **Verbesserte Unterstützung für tabellarische SQL Server 2016-Datenbanken (Kompatibilitätsstufe 1200) im Dialogfeld „Analysis Services-Prozess“ und im Bereitstellungs-Assistenten für Analysis Services.**

* *Bearbeitung 5. Juli:* **Neue Option im SSMS-Dialogfeld „Abfrageausführungsoptionen“ zum Festlegen von XACT_ABORT. Diese Option ist in dieser Version von SSMS standardmäßig aktiviert und weist SQL Server an, beim Auftreten eines Laufzeitfehlers einen Rollback der gesamten Transaktion auszuführen und den Batch abzubrechen.**

* **Unterstützung für Azure SQL Data Warehouse in SSMS.**

* **Umfangreiche Updates am SQL Server PowerShell-Modul. Zu diesen gehören ein neues [SQL PowerShell-Modul und neue CMDLETs für Always Encrypted, SQL Agent und SQL-Fehlerprotokolle](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update)**.

* **Unterstützung für die PowerShell-Skripterstellung im Always Encrypted-Assistenten**.

* **Deutlich verbesserte Verbindungszeiten für Azure SQL-Datenbanken.**

* **Neues Dialogfeld „URL-Sicherung“, das die Erstellung von Azure-Speicheranmeldeinformationen für Datenbanksicherungen von SQL Server 2016 unterstützt. Es bietet eine optimierte Benutzeroberfläche zum Speichern von Datenbanksicherungen unter einem Azure-Speicherkonto.**
 
* **Neues Wiederstellen-Dialogfeld zur Optimierung der Wiederherstellung einer SQL Server 2016-Datenbanksicherung aus dem Microsoft Azure-Speicherdienst.**
 
* **Programmfehlerbehebung im SSMS-Abfrage-Designer, um das Hinzufügen von Tabellen zum Designer zu ermöglichen, wenn ein Benutzer nicht über SELECT-Berechtigungen für die Tabellen verfügt.**

* **Programmfehlerbehebung zum Hinzufügen von IntelliSense-Unterstützung für die Funktionen TRY_CAST() und TRY_CONVERT().**  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2453461](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast).

* **Programmfehlerbehebung im PowerShell-Modul, um das Laden der SQLAS-Erweiterung von Analysis Services zu ermöglichen.**  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2544902](https://connect.microsoft.com/SQLServer/feedback/details/2544902/ssms-march-2016-refresh-sqlps-failed-to-load-the-sqlas-extension).

* **Programmfehlerbehebung im SSMS-Editor-Fenster, um das Öffnen von SQL-Dateien per Drag &amp; Drop zu ermöglichen.**  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2690658](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios).

* **Fehlerbehebung im Profiler, um den Absturz von Profiler beim Beenden zu beheben.**  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2616550](https://connect.microsoft.com/SQLServer/feedback/details/2616550/sql-server-2016-rc2-profiler-version-13-0-1300-275-wont-close-after-trace-is-started-even-after-trace-is-stopped).  
[Microsoft Connect-Element #2319968](https://connect.microsoft.com/SQLServer/Feedback/Details/2319968).

* **Programmfehlerbehebung in SSMS zum Verhindern des Absturzes beim Bearbeiten einer Join-Verknüpfung im SSMS-Tabellen-Designer.**  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2721052](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms).

* **Fehlerbehebung in SSMS, um die Datenbank-Skripterstellung für Mitglieder der db_owner-Rolle zu ermöglichen.**  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2869241](https://connect.microsoft.com/SQLServer/feedback/details/2869241/error-with-script-database-as-create-to-in-ssms-2008r2-and-ssms-2016-june).

* **Programmfehlerbehebung im SSMS-Editor zum Entfernen der Verzögerung beim Schließen einer Abfrageregisterkarte, wenn der Server offline gesetzt wurde.**  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2656058](https://connect.microsoft.com/SQLServer/feedback/details/2656058/ssms-2014-2016-query-tab-takes-significantly-longer-to-close-if-the-instance-it-was-connected-to-is-now-offline).

* **Programmfehlerbehebung zum Aktivieren der Sicherungsoption in SQL Server Express-Datenbanken.**  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2801910](https://connect.microsoft.com/SQLServer/feedback/details/2801910/ssms-2016-backup-option-not-appearing-in-tasks).  
[Microsoft Connect-Element #2874434](https://connect.microsoft.com/SQLServer/feedback/details/2874434/backup-missing-from-tasks-context-menu-in-ssms-2016-when-you-are-connected-to-an-express-instance).

* **Fehlerbehebung in Analysis Services, um den Data Feed-Anbieter für mehrdimensionale Analysis Services-Modelle ordnungsgemäß anzuzeigen.**

----
## <a name="ssms-june-2016-generally-available-release"></a>SSMS-Release aus Juni 2016 allgemein verfügbar
Allgemein verfügbar | Versionsnummer: 13.0.15000.23

* **SSMS ist mit dem Release aus Juni 2016 allgemein verfügbar.**

* **Dialogfeld für die Schnellsuche in SSMS, das besser in das aktuelle Dokument integriert ist und eine Suche über reguläre Ausdrücke ermöglicht.**  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/>

* **Verbesserungen beim SSMS-Installationsprogramm, um den Installationsfortschritt nachverfolgen und Exitcodes bei unbeaufsichtigten Installationen über Skripts zu verarbeiten.**

* **Programmfehlerbehebung für die kontextbezogene F1-Hilfe in SSMS, um Hilfedokumente und -artikel ordnungsgemäß anzuzeigen.**

* **Programmfehlerbehebung in der Ansicht „Zurückgestellte Abfragen“ des Abfragedatenspeichers, der beim Scrollen zu einem Absturz von SSMS geführt hat.** 

* **Programmfehlerbehebung beim OLEDB-Connector von Excel Analysis Services, um Verbindungen von Excel 2016 mit SQL Server Analysis Services zu ermöglichen.**

* **Programmfehlerbehebung für das SSMS-Verbindungsdialogfeld, um das Verbindungsdialogfeld bei Verwendung von mehreren Monitoren auf demselben Monitor anzuzeigen wie das SSMS-Hauptsystem.**  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/>
<https://connect.microsoft.com/SQLServer/feedback/details/755689/sql-server-management-studio-connect-to-server-popup-dialog/>  
<https://connect.microsoft.com/SQLServer/feedback/details/389165/sql-server-management-studio-gets-confused-dealing-with-multiple-displays/>

* **Programmfehlerbehebungen für Always Encrypted-Features. Der Fehler, bei dem die Always Encrypted-Menüoption nicht ordnungsgemäß für Stretch-Datenbanken aktiviert wurde, wurde behoben. Außerdem wurde der Fehler im Always Encrypted-Assistenten behoben, bei dem der HSM-Anbieter SafeNet (Luna SA) nicht ordnungsgemäß verwendet wurde.**

---
## <a name="ssms-april-2016-preview"></a>SSMS April 2016 (Vorschau) 
Versionsnummer: 13.0.14000.36
  
* **Verbesserung beim SSMS-Installationsprogramm, um lesbare Fehlermeldungen hinzuzufügen.**  
  
* **Verbesserung im Assistenten für Stretch-Datenbanken, um Unterstützung von Prädikaten hinzuzufügen**.  
  
* **Verbesserungen im Always Encrypted PowerShell-Cmdlet, um Schlüsselverschlüsselungs-APIs hinzuzufügen**.  
  
* **Programmfehlerbehebung zum Deaktivieren von IntelliSense auf der SSMS-Symbolleiste, wenn dieses Feature im Dialogfeld „Tools &gt; Optionen“ deaktiviert wurde.**  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2555163/sql-2016-rc2-turning-off-intellisense-from-options-does-not-turn-it-off-on-toolbar/>  
    
* **Verbesserungen und Programmfehlerbehebungen für die Benutzeroberfläche für den Showplan-Vergleich, um den von langen Abfrageplänen verwendeten Abstand zu verringern**.  
  
* **Programmfehlerbehebungen in SSMS, um Probleme zu behandeln, die zu einem Absturz von SSMS beim Beenden des Programms geführt haben**.   
  
* **Programmfehlerbehebungen im Always Encrypted-Assistenten, um Benutzerberechtigungen während der Verschlüsselung beizubehalten und Trennvorgänge für die Datenbank zu ermöglichen, nachdem der Assistent abgeschlossen wurde**.  
  
* **Programmfehlerbehebung im Always Encrypted-Dialogfeld für neue Spaltenhauptschlüssel, um Feedback zu geben, wenn ein Benutzer versucht, einen Schlüssel unter Verwendung eines nicht unterstützten Kryptografiealgorithmusanbieters (CNG-Anbieter) zu erstellen.**  
  
---  
## <a name="ssms-march-2016-preview-refresh"></a>SSMS März 2016 (Vorschauaktualisierung)
Versionsnummer: 13.0.13000.55
  
* **SSMS verwendet jetzt die Visual Studio 2015 Isolated Shell.**  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2390544/update-ssms-to-use-visual-studio-2015-dependencies/>  
  
* **Neue Schnellstartsymbolleiste, um im Handumdrehen nach Menüelementen und Optionen suchen zu können. (VS 2015 Isolated Shell)**  
  
* **Verbesserungen bei den SSMS-Designoptionen, um Unterstützung für ein helles SSMS-Design hinzuzufügen. (VS 2015 Isolated Shell)**  
  
* **Programmfehlerbehebung bei den Optionen im SSMS-Toolmenü, um Abfrageverknüpfungen bei Auswahl der Schaltfläche „Standard wiederherstellen“ ordnungsgemäß zurückzusetzen.**  
  
* **Programmfehlerbehebung bei neuen SSMS-Projektvorlagen, um gut lesbare Vorlagennamen anzuzeigen.**  
  
* **Der Fehler beim Anzeigen des SQL Agent-Auftragsverlaufs in SSMS wurde behoben.**  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2458860/error-viewing-job-history-microsoft-datawarehouse-sqm/>  
    
* **Programmfehlerbehebung, um eine Offline-Installation von SSMS zu ermöglichen. SSMS kann nun auch ohne Internetverbindung installiert werden. (VS 2015 Isolated Shell)**  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2497178/cannot-install-ssms-when-server-has-no-internet-access/>  
    
* **Programmfehlerbehebung, um das aktuelle Verzeichnis des Benutzers beim Import des SQL Server PowerShell-Moduls (SQLPS) beizubehalten.**  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2434605/loading-sqlps-module-changes-current-directory-to-ps-sqlserver/>  
    
* **Programmfehlerbehebung im SQL Server PowerShell-Modul (SQLPS) für die Verwendung genehmigter PowerShell-Verben.**  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2432891/sqlps-module-uses-unapproved-powershell-verbs/>  
    
* **Programmfehlerbehebung im SQL Server PowerShell-Modul (SQLPS) zur Beschleunigung des Modulladevorgangs.**  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2429153/sqlps-module-is-slow-to-load/>  
    
* **Programmfehlerbehebung in SQL Agent-Auftragsschritten, um das Ändern von Auftragsschritten zu ermöglichen.**  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2453996/issues-with-agent-in-ssms-2016-rc0-13-0-12000-65/>  
    
* **Programmfehlerbehebung im Objekt-Explorer von SSMS, um Tabellen alphabetisch aufzulisten.**  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2424718/sql-server-2016-ssms-table-list-confusing/>  
    
* **Programmfehlerbehebung in der Dropdownliste „Verfügbare Datenbanken“, um eine korrekte Liste mit Datenbanknamen anzuzeigen, wenn eine SQL Server-Verbindung geändert wird.**  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2513420/available-databases-drop-down-box-does-not-update-when-connection-changes-in-ssms/>  
    
* **Programmfehlerbehebung bei SSMS-Tastenkombinationen, um die Dropdownliste „Verfügbare Datenbanken“ zu markieren, wenn STRG-U gedrückt wird.**  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2534820/ssms-ctrl-u-doesnt-work/>  
  
---  
## <a name="ssms-march-2016-preview"></a>SSMS März 2016 (Vorschau) 
Versionsnummer: 13.0.12500.29 
  
* **Verbesserung im SSMS-Webinstaller, um eine Navigation über die Tastatur zu ermöglichen.**  
  
* **Verbesserung im Always Encrypted-Assistenten, um Unterstützung von Aliasdatentypen für die Verschlüsselung hinzuzufügen.**  
  
* **Programmfehlerbehebung im Always On-Assistenten „Neue Verfügbarkeitsgruppe“, um die richtige maximale Anzahl von Zielen für ein automatisches Failover anzuzeigen.**  
*Verwandte Fehleranfragen von Kunden:* <https://connect.microsoft.com/SQLServer/feedback/details/2333670/ssms-is-showing-the-wrong-number-of-maximum-automatic-failover-targets/>  
    
* **Programmfehlerbehebung im SSMS-Webinstaller, um Fehler zu behandeln, die sich auf die Installation auswirken.**  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2181548/sql-server-2016-ctp-3-2-management-studio-setup/>  
    
* **Programmfehlerbehebung im SSMS-Vorschaurelease, um das Speichern von Wartungsplänen bei Verwendung von SQL Server 2012 und niedrigeren Versionen zu ermöglichen.**  
      
* **Programmfehlerbehebung im Sicherungs-Assistenten, um mehrere benutzerdefinierte Sicherungsnamen für Stripesetsicherungen zu ermöglichen und den richtigen Namen der Sicherungsdatei anzuzeigen, wenn nach der Auswahl von Speicheranmeldeinformationen ein neuer Name eingegeben wird.**  
  
---  
## <a name="ssms-february-2016-preview"></a>SSMS Februar 2016 (Vorschau) 
Versionsnummer: 13.0.12000.65
  
* **Verbesserung beim Aktivitätsmonitor, um Textoptionen anzuzeigen, wenn Einstellungen für hohen Kontrast in SSMS aktiviert sind.**  
  
* **Verbesserungen im Dialogfeld des Always Encrypted-Assistenten, um eine Warnung anzuzeigen, wenn die Sortierung für eine Spalte während der Verschlüsselung geändert wird.**  
  
* **Verbesserungen bei der Richtlinienverwaltung, um Unterstützung für das Erstellen von Bedingungen für Spaltenverschlüsselungsschlüssel, Spaltenverschlüsselungsschlüsselwerte und Spaltenhauptschlüssel hinzuzufügen.**  
  
* **Programmfehlerbehebung, um die Benutzerfreundlichkeit des Dialogfelds zum Bereinigen von Always Encrypted-Hauptschlüsseln sowie von Always Encrypted-Fehlermeldungen zu verbessern.**  
  
* **Programmfehlerbehebung, um die Rotation der Always Encrypted-Spaltenhauptschlüssel zu deaktivieren, wenn nur ein Schlüssel vorhanden ist.**  
  
* **Programmfehlerbehebung für den Typeninitialisiererfehler, der auftritt, wenn das Always Encrypted-Dialogfeld unter Verwendung des SSMS-Release aus Januar oder über das SSMS-Release in Kombination mit den SQL Server RC0-Medien gestartet wird.**  
  
---  
## <a name="ssms-january-2016-preview"></a>SSMS Januar 2016 (Vorschau) 
Versionsnummer: 13.0.11000.78 
  
* **Programmfehlerbehebung in SSMS, um das Löschen von Sitzungen für Erweiterte Ereignisse (XEvent) zu ermöglichen.**  
  
* **Programmfehlerbehebung, um das Dialogfeld „Eigenschaften“ für eine Verfügbarkeitsgruppe von SQL Server 2014 zu öffnen.**  
 *Verwandte Fehleranfragen von Kunden:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/1609719/>  
     
* **Programmfehlerbehebung, um die Möglichkeit zu aktivieren, einer Verfügbarkeitsgruppe ein Azure-Replikat hinzuzufügen.**  
 *Verwandte Fehleranfragen von Kunden:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2029135/>  
     
* **Programmfehlerbehebung, um das Dialogfeld „Eigenschaften“ für SQL Server 2014-Datenbanken zu öffnen.**  
 *Verwandte Fehleranfragen von Kunden:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2080209/>  
     
* **Programmfehlerbehebung, um doppelte Spalten zu entfernen, die beim Verbinden mit einer Azure SQL-Datenbank für jede Tabelle angezeigt werden.**  
 *Verwandte Fehleranfragen von Kunden:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2103116/>  
---  
## <a name="ssms-december-2015-preview"></a>SSMS Dezember 2015 (Vorschau) 
Versionsnummer: 13.0.900.73
  
* **Verbesserungen am Showplan-Vergleich, um den Vergleich des aktuellen Abfrageausführungsplans mit einem in einer Datei gespeicherten zu ermöglichen.**  
  
* **Verbesserte IntelliSense-Unterstützung für Columnstore-Inlineindizes in SSMS.**  
  
* **Programmfehlerbehebung im Assistenten für Sitzungen für erweiterte Ereignisse, um bei bestehender Verbindung mit einem Azure V12-Server die Auswahl von Vorlagen zu ermöglichen.**  
  
* **Neue Tabstopps in den Dialogfeldern „Überwachung erstellen“ und „Neue Anmeldung“ unter dem Ordner „Sicherheit“, um die Navigation per Tastatur zu erleichtern.**  
  
* **Programmfehlerbehebung, um die Funktionalität zum „Wechseln zur Registerkarte ‚Ergebnisse‘ nach der Abfrageausführung“ zu aktivieren, wenn in SSMS die Darstellung von Ergebnissen im Rasterformat festgelegt ist.**   
 *Verwandte Fehleranfragen von Kunden:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1390296/switch-to-results-tab-after-query-execution-grid-mode-in-ssms-2016>  
  
* **Programmfehlerbehebung, um Spaltenköpfe ohne Abschneiden anzuzeigen, wenn für SSMS die Darstellung von Ergebnissen im Rasterformat festgelegt ist.**  
 *Verwandte Fehleranfragen von Kunden:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/2004111/bugbash-column-headers-in-grid-mode-truncated-with-courier-new-8>  
      
* **Programmfehlerbehebungen, um die ordnungsgemäße Installation des SSMS-Webinstallationsprogramms zu ermöglichen.**  
 *Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2003865/ssms-october-preview-incoherent-error-message>  
<https://connect.microsoft.com/SQLServer/feedback/details/2079557/unable-to-instal-sql-server-update-13-0-800-111-over-13-0-700-242-error-code-2711>  
  
---  
## <a name="ssms-november-2015-preview"></a>SSMS November 2015 (Vorschau)
Versionsnummer: 13.0.800.111
  
* **Unterstützung für die Skalierung von Bitmaps für hochauflösende Anzeigen in SSMS.**  
  
* **Verbesserungen an der Benutzeroberfläche der Dialogfelder und Assistenten für Always Encrypted zum Vereinfachen der Erstellung von Datenbank-Verschlüsselungsschlüsseln.**  
  
* **Neue Option für das Kontextmenü in der Liste „Prozesse“ – im Aktivitätsmonitor zum Anzeigen von Statistiken zu aktiven Abfragen.**  
  
* **Programmfehlerbehebung, um die ordnungsgemäße Deinstallation von SSMS-Vorschauversionen von Clientcomputern zu ermöglichen.**  
  *Verwandte Fehleranfragen von Kunden:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1868474/ssms-2016-preview-can-be-installed-but-not-uninstalled>  
  
* **Programmfehlerbehebung, um die Bearbeitung von Auftragsschritten im SQL-Auftrags-Agent auch bei fehlenden Dateien zu ermöglichen**.  
  *Verwandte Fehleranfragen von Kunden:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1769778/management-studio-2016-sql-job-agent>  
    <https://connect.microsoft.com/SQLServer/feedback/details/1502100/ssms-preview-error>  
      
* **Programmfehlerbehebung in der Menüoption „Zieldaten anzeigen“ für eine Sitzung für erweiterte Ereignisse in einer Datenbank, die auf einem virtuellen Azure-Computer ausgeführt wird.**  
  *Verwandte Fehleranfragen von Kunden*:  
  <https://connect.microsoft.com/SQLServer/feedback/details/1769778/management-studio-2016-sql-job-agent>  
***  

## <a name="ssms-october-2015-preview"></a>SSMS Oktober 2015 (Vorschau) 
Versionsnummer: 13.0.700.242  
* **Moderneres Webinstallationsprogramm, das den Download und die Installation von SSMS vereinfacht.**  
  
* **Der neue Always Encrypted-Spaltenverschlüsselungs-Assistent vereinfacht die clientseitige Ver- und Entschlüsselung von ausgewählten Spalten.**  
  
* **Das neue Drehungsdialogfeld für Spaltenhauptschlüssel (Column Master Key, CMK) vereinfacht bei Immer-verschlüsselt-Datenbanken die Drehung von Verschlüsselungsschlüsseln, damit die Daten sicher bleiben.**  
  
* **Die neue Stretch-Datenbanküberwachung ermöglicht die Problembehandlung und Überwachung des Migrationsstatus von Daten in die Azure-Cloud.**  
  
* **Verbesserungen am Stretch-Datenbank-Assistent zur Unterstützung der Auswahl eines Microsoft Azure-Servers, der nicht zum standardmäßigen Microsoft Azure-Abonnement gehört.**  
  *Verwandte Fehleranfragen von Kunden:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1687063/cannot-choose-from-multiple-microsoft-azure-subscriptions>  
* **Programmfehlerbehebung, um eine ordnungsgemäße Anzeige des Live-Ausführungsplans in SSMS zu ermöglichen.**  
  *Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1774446/viewing-live-execution-plan-from-activity-monitor-crashes-ssms>    
* **Programmfehlerbehebung zum Entfernen ungültiger Optionen in der SSMS-Skripterstellung für Datenbank-Momentaufnahmen**  
  *Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1515168/ssms-scripting-of-database-snapshots-includes-invalid-options>  
* **Programmfehlerbehebung in der Benutzeroberfläche des Abfragedatenspeichers, um Details im Bereich „Erste Abfragen nach Ressourcenverbrauch“ anzuzeigen.**  
  *Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1737185/sql-server-2016-overall-resource-consumption-query-store-pane-issue>  
***  

## <a name="ssms-september-2015-preview"></a>SSMS September 2015 (Vorschau) 
Versionsnummer: 13.0.600.65  
* **Dialogfeld für neue Firewallregeln, mit dem das Herstellen einer Verbindung mit einer Azure SQL-Datenbank optimiert wird.**      
    
* **Aktualisiertes Dialogfeld „Neuer Index“, das die Erstellung von nicht gruppierten Rowstore-Indizes auch dann zulässt, wenn ein gruppierter Columnstore-Index vorhanden ist. Diese Funktionalität ist ab SQL 2016 verfügbar.**      
  *Verwandte Fehleranfragen von Kunden:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1552617/creation-of-nc-index-when-clustered-columnstore-index>  
      
* **Programmfehlerbehebung, um das Anzeigen und Bearbeiten von Auftragsschritten des SQL Agent in Vorschauversionen von SSMS unter Windows 7 zu ermöglichen.**      
  *Verwandte Fehleranfragen von Kunden:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1548140/cannot-view-or-edit-any-sql-agent-job-step>,    
  <https://connect.microsoft.com/SQLServer/feedback/details/1626895/unable-to-load-dll-dts>,    
  <https://connect.microsoft.com/SQLServer/feedback/details/1576662/error-creating-new-job-step>     
      
* **Programmfehlerbehebung zum Anzeigen von Auslöserknoten in SSMS für SQL Server 2014 und höher zu ermöglichen.**      
  *Verwandte Fehleranfragen von Kunden:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1617533/trigger-node-missing>   
      
* **Programmfehlerbehebungen in der Benutzeroberfläche von Standardberichten, um Versionsinformationen aus den Kopfdaten auszuschließen.**      
  *Verwandte Fehleranfragen von Kunden:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1387471/report-headings-wrongly-named>  
      
* **Programmfehlerbehebung, um die Anzeige von Abfragen in der dynamischen Abfragestatistik als abgeschlossen zu verhindern, wenn dies nicht zutrifft.**      
  *Verwandte Fehleranfragen von Kunden:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1589096/live-query-statistics-node-shows-as-completed>  
  
***      
## <a name="ssms-august-2015-preview"></a>SSMS August 2015 (Vorschau) 
Versionsnummer: 13.0.500.53
  
* **Updates am Objekt-Explorer, um die Ladeverzögerung bei einer größeren Datenbankanzahl zu verhindern.**  
  
* **Verbesserungen für die Installation von SSMS auf Windows 10-Computern.**  
  
* **Programmfehlerbehebungen am SQL Server-Konfigurations-Manager und an der Benutzeroberfläche für Benutzerberichte**    
***  
  
## <a name="ssms-july-2015-preview"></a>SSMS Juli 2015 (Vorschau)
Versionsnummer: 13.0.400.91
  
* **Datenbankdiagramme für Azure SQL-Datenbank (V12).**  
  
* **Verbesserte IntelliSense-Unterstützung für die neue Syntax von temporalen Tabellen.**  
  
* **Aktualisierte DacFx-Bibliothek zur Unterstützung der neuesten SQL Azure-Datenbankfunktionen, einschließlich Sicherheit auf Zeilenebene und Azure Active Directory-Authentifizierung.**  
  
* **Programmfehlerbehebungen (aktualisierte Benutzeroberfläche für die Prüfung auf Updates, korrigierte Benutzeroberfläche in der Liste „Kompatibilitätsgrad“ und mehr).**  
***  
  
## <a name="ssms-june-2015-preview"></a>SSMS Juni 2015 (Vorschau) 
Versionsnummer: 13.0.300.44
  
* **Neues kompaktes SSMS-Webinstallationsprogramm.**  
  
* **Automatische Prüfung auf Updates.**  
  
* **SSMS unterstützt jetzt die Volltextsuche für Azure SQL-Datenbank (V12).**  
  
* **Berücksichtigte häufige Kundenanfragen:**  
  * „Oberste 200 Zeilen bearbeiten“ für Tabellen und Sichten im Objekt-Explorer aktiviert.  
  * Tabellen-Designer für Azure SQL-Datenbank (V12) aktiviert.  
  * Eigenschaften- und Tabellen-Dialogfelder für Azure SQL-Datenbank (V12) aktiviert.  
    
 * **Neue Option zum Überspringen der Aufforderung zum Speichern von T-SQL-Dateien.**  
   
 * **Unterstützung für den Import/Export-Assistenten für neue Dienstebenen von Azure SQL-Datenbank (Basic, Standard, Premium).**  
   
 * **Zahlreiche Programmfehlerbehebungen (Skripterstellungsszenarios, Aktivieren der Änderungsnachverfolgung für SQL-Datenbanken und mehr).**   
     
  
  
  
  
  
  
    

