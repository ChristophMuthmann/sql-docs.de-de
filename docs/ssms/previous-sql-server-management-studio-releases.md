---
title: "Vorgängerversionen von SQL Server Management Studio | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 87f593c3-8b76-4c12-963a-31d35f2fb294
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 0927784589c1f7227b432ff49f81f29de20083ec
ms.openlocfilehash: 200753bf64d92043171788852227c6199b64711d
ms.contentlocale: de-de
ms.lasthandoff: 05/27/2017

---
# <a name="previous-sql-server-management-studio-releases"></a>Vorgängerversionen von SQL Server Management Studio
  
Die folgenden Vorgängerversionen von SQL Server Management Studio sind verfügbar.
   
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-1653-releasehttpgomicrosoftcomfwlinklinkid840946"></a>![herunterladen](../ssdt/media/download.png) [Version von SQL Server Management Studio 16.5.3](http://go.microsoft.com/fwlink/?LinkID=840946)

**Versionsinformationen**  
  
*In dieser Version von SSMS wird die Visual Studio 2015 Isolated Shell verwendet.*  
Versionsnummer: 16.5.3  
Buildnummer dieser Version: 13.0.16106.4

## <a name="changelog"></a>Änderungsprotokoll  

16.5.3

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



## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-165-releasehttpgomicrosoftcomfwlinklinkid832812"></a>![Download](../ssdt/media/download.png) [SQL Server Management Studio Version 16.5](http://go.microsoft.com/fwlink/?LinkID=832812)

**Versionsinformationen**  
  
*In diesem Release von SSMS wird die Visual Studio 2015 Isolated Shell verwendet.*  
Versionsnummer: 16.5  
Buildnummer dieser Version: 13.0.16000.28

**Bekannte Probleme mit diesem Build**  

1. Invoke-Sqlcmd fügt fälschlicherweise mehrere Zeilen ein, wenn CHECK-Einschränkungen auftreten. [Microsoft Connect-Element: 811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

2. Nicht-ENU-Sprachversionen funktionieren beim Erstellen von Verfügbarkeitsgruppen nicht vollständig.

3. Durch Klicken auf die Abfrageplan-XML wird nicht die richtige SSMS-Benutzeroberfläche geöffnet.

**Änderungsprotokoll**

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


   
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-1641-september-2016-releasehttpgomicrosoftcomfwlinklinkid828615"></a>![Download](../ssdt/media/download.png) [SQL Server Management Studio 16.4.1-Release (September 2016)](http://go.microsoft.com/fwlink/?LinkID=828615)

**Versionsinformationen**  
  
*In dieser Version von SSMS wird die Visual Studio 2015 Isolated Shell verwendet.*  
Versionsnummer: 16.4.1  
Buildnummer dieser Version: 13.0.15900.1
  
**Bekannte Probleme mit diesem Build**  

1. **Bei Verwendung der universellen Active Directory-Authentifizierung kann sich nur ein einziges Azure Active Directory-Konto für eine SSMS-Instanz anmelden.**  
    Diese Einschränkung gilt lediglich für die universelle Active Directory-Authentifizierung. Bei Verwendung der Active Directory-Kennwortauthentifizierung, der integrierten Active Directory-Authentifizierung oder der SQL Server-Authentifizierung können Sie sich bei unterschiedlichen Servern anmelden.
    
    Um dieses Problem zu umgehen, können Sie eine andere SSMS-Instanz verwenden, um sich als ein anderes Azure Active Directory-Konto anzumelden. 
    
2. **DacFx-Befehle (Data-Tier Application Framework) und der Schema-Designer in SSMS bieten keine Unterstützung für die universelle Active Directory-Authentifizierung.**  
    Befehle, die DacFx verwenden (z.B. Import- und Exportbefehle) und der Schema-Designer in SSMS bieten aktuell keine Unterstützung für die universelle Active Directory-Authentifizierung.
    
    Um das Problem zu umgehen, können Sie die anderen Authentifizierungsmethoden verwenden, die in SSMS verfügbar sind: Active Directory-Kennwortauthentifizierung, integrierte Active Directory-Authentifizierung und SQL Server-Authentifizierung.

3. **SSMS kann sich ausschließlich mit SSIS 2016-Instanzen (SQL Server 2016 Integration Services) verbinden.**  
    Es gibt eine bekannte Kompatibilitätseinschränkung bei SQL Server Integration Services, die Verbindungen mit vorherigen Versionen verhindert.
    
    Als Problemumgehung verbinden Sie sich über [das SSMS-Release, das auf Ihre SSIS-Instanz ausgerichtet ist](../ssms/previous-sql-server-management-studio-releases.md), mit Ihrer SQL Server Integration Services-Instanz. 
  
4. **SSMS speichert keine Wartungspläne für SQL Server 2008 R2 und frühere SQL Server-Versionen.**  
    Dies ist eine bekannte Einschränkung, und wir arbeiten daran, diese in einem zukünftigen Release zu beheben. In der Zwischenzeit können Sie das [SSMS 2014-Release](../ssms/previous-sql-server-management-studio-releases.md) unten verwenden, um Wartungspläne zu speichern.  
    
5. **Für SSMS-Installationen in anderen Sprachen als Englisch ist möglicherweise die Installation eines zusätzlichen Sicherheitspakets erforderlich.**  
Lokalisierte Versionen von SSMS (andere Sprachen als Englisch) [benötigen das KB 2862966-Sicherheitsupdatepaket](https://support.microsoft.com/en-us/kb/2862966) für die Installation unter Windows 8, Windows 7, Windows Server 2012 und Windows Server 2008 R2.
  
6. **Der SQL Server-Konfigurations-Manager kann nicht gestartet werden, wenn auf dem Clientcomputer keine SQL Server-Instanz installiert ist.**  
    Wenn auf Ihrem Clientcomputer keine SQL Server-Instanz installiert ist, und Sie den SQL Server-Konfigurations-Manager starten, wird der folgende Fehler angezeigt:   
     `Cannot connect to WMI provider. You do not have permission or the server is unreachable. Note that you can only manage SQL Server 2005 and later servers with SQL Server Configuration Manager. Invalid namespace \[0x8004100e]`,   
   
     * Wenn Sie Ihre SQL Server-Instanzen zur Liste „Registrierte Server“ in SSMS hinzugefügt haben:  
        1. Navigieren Sie zur Ansicht „Registrierte Server“ in SSMS.  
        2. Klicken Sie mit der rechten Maustaste auf die SQL Server-Instanz, die konfiguriert werden soll.  
        3. Wählen Sie „SQL Server-Konfigurations-Manager“ aus dem Kontextmenü aus.    
          
      * Wenn Sie Ihre SQL Server-Instanzen nicht zur Liste „Registrierte Server“ in SSMS hinzugefügt haben:  
        1. Öffnen Sie eine Eingabeaufforderung als Administrator.  
        2. Führen Sie das Tool Mofcomp mit dem folgenden Befehl aus:  
    `mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"`  
        3. Führen Sie nach der Ausführung des Tools Mofcomp die folgenden Befehle aus, um den WMI-Dienst neu zu starten und die Änderungen zu übernehmen:  
        `net stop "Windows Management Instrumentation"`  
        `net start “Windows Management Instrumentation”`  

 
**Änderungsprotokoll** 

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
    
*  Es wurde ein Problem in Analysis Services behoben, das die Ursache dafür bildete, dass ein Erstellen eines Skripts auf der Eigenschaftenseite eines Servers zu einem ausgeblendeten Verbindungsdialogfeld geführt hat.
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass mit STRG+Q nicht die Schnellstart-Symbolleiste ausgewählt wurde.
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass ein Ändern der maximalen Größe (MaxSize) einer Datenbank über das Dialogfeld „Servereigenschaften“ für Datenbanken > 2 TB nicht funktioniert hat.  
[Microsoft Connect-Element #1231091](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass der Assistent zum Wiederherstellen einer Datenbank keine Dateinamen mit führenden Leerzeichen akzeptiert hat:   
[Microsoft Connect-Element #2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)

*  Es wurde ein Problem behoben, das dazu geführt hat, dass der Assistent zum Wiederherstellen einer Datenbank keine Dateinamen mit führenden Leerzeichen akzeptiert hat:   
[Microsoft Connect-Element #2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-163-august-2016-releasehttpgomicrosoftcomfwlinklinkid824938"></a>![Download](../ssdt/media/download.png) [SQL Server Management Studio 16.3-Release (August 2016)](http://go.microsoft.com/fwlink/?LinkID=824938)
 15. August 2016 | Versionsnummer: 13.0.15700.28

**Funktionen**  
1. Neue Authentifizierungsoption „Universelle Active Directory-Authentifizierung“
2. Neue Cmdlets für das SQL Server PowerShell-Modul
3. Verbesserungen an Vorlagen für Datenbankoptimierungsratgeber und „Erweiterte Ereignisse“
4. Betaunterstützung für [Anzeige mit hoher Auflösung in SSMS](https://blogs.msdn.microsoft.com/sqlreleaseservices/ssms-highdpi-support/)

[Weitere Informationen zu Features sind im SSMS-Änderungsprotokoll verfügbar.](../ssms/sql-server-management-studio-changelog-ssms.md)

**Bekannte Probleme**

Dies sind Probleme und Einschränkungen, die in Verbindung mit diesem SQL Server Management Studio-Release bestehen:  

1. **Bei Verwendung der universellen Active Directory-Authentifizierung kann sich nur ein einziges Azure Active Directory-Konto für eine SSMS-Instanz anmelden.**  
    Diese Einschränkung gilt lediglich für die universelle Active Directory-Authentifizierung. Bei Verwendung der Active Directory-Kennwortauthentifizierung, der integrierten Active Directory-Authentifizierung oder der SQL Server-Authentifizierung können Sie sich bei unterschiedlichen Servern anmelden.
    
    Um dieses Problem zu umgehen, können Sie eine andere SSMS-Instanz verwenden, um sich als ein anderes Azure Active Directory-Konto anzumelden. 
    
2. **DacFx-Befehle (Data-Tier Application Framework) und der Schema-Designer in SSMS bieten keine Unterstützung für die universelle Active Directory-Authentifizierung.**  
    Befehle, die DacFx verwenden (z.B. Import- und Exportbefehle) und der Schema-Designer in SSMS bieten aktuell keine Unterstützung für die universelle Active Directory-Authentifizierung.
    
    Um das Problem zu umgehen, können Sie die anderen Authentifizierungsmethoden verwenden, die in SSMS verfügbar sind: Active Directory-Kennwortauthentifizierung, integrierte Active Directory-Authentifizierung und SQL Server-Authentifizierung.

3. **SSMS kann sich ausschließlich mit SSIS 2016-Instanzen (SQL Server 2016 Integration Services) verbinden.**  
    Es gibt eine bekannte Kompatibilitätseinschränkung bei SQL Server Integration Services, die Verbindungen mit vorherigen Versionen verhindert.
    
    Als Problemumgehung verbinden Sie sich über [das SSMS-Release, das auf Ihre SSIS-Instanz ausgerichtet ist](../ssms/previous-sql-server-management-studio-releases.md), mit Ihrer SQL Server Integration Services-Instanz. 
  
4. **SSMS speichert keine Wartungspläne für SQL Server 2008 R2 und frühere SQL Server-Versionen.**  
    Dies ist eine bekannte Einschränkung, und wir arbeiten daran, diese in einem zukünftigen Release zu beheben. In der Zwischenzeit können Sie das [SSMS 2014-Release](../ssms/previous-sql-server-management-studio-releases.md) unten verwenden, um Wartungspläne zu speichern.  
    
5. **Für SSMS-Installationen in anderen Sprachen als Englisch ist möglicherweise die Installation eines zusätzlichen Sicherheitspakets erforderlich.**  
Lokalisierte Versionen von SSMS (andere Sprachen als Englisch) [benötigen das KB 2862966-Sicherheitsupdatepaket](https://support.microsoft.com/en-us/kb/2862966) für die Installation unter Windows 8, Windows 7, Windows Server 2012 und Windows Server 2008 R2.
  
6. **Der SQL Server-Konfigurations-Manager kann nicht gestartet werden, wenn auf dem Clientcomputer keine SQL Server-Instanz installiert ist.**  
    Wenn auf Ihrem Clientcomputer keine SQL Server-Instanz installiert ist, und Sie den SQL Server-Konfigurations-Manager starten, wird der folgende Fehler angezeigt:   
     `Cannot connect to WMI provider. You do not have permission or the server is unreachable. Note that you can only manage SQL Server 2005 and later servers with SQL Server Configuration Manager. Invalid namespace \[0x8004100e]`,   
   
     * Wenn Sie Ihre SQL Server-Instanzen zur Liste „Registrierte Server“ in SSMS hinzugefügt haben:  
        1. Navigieren Sie zur Ansicht „Registrierte Server“ in SSMS.  
        2. Klicken Sie mit der rechten Maustaste auf die SQL Server-Instanz, die konfiguriert werden soll.  
        3. Wählen Sie „SQL Server-Konfigurations-Manager“ aus dem Kontextmenü aus.    
          
      * Wenn Sie Ihre SQL Server-Instanzen nicht zur Liste „Registrierte Server“ in SSMS hinzugefügt haben:  
        1. Öffnen Sie eine Eingabeaufforderung als Administrator.  
        2. Führen Sie das Tool Mofcomp mit dem folgenden Befehl aus:  
    `mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"`  
        3. Führen Sie nach der Ausführung des Tools Mofcomp die folgenden Befehle aus, um den WMI-Dienst neu zu starten und die Änderungen zu übernehmen:  
        `net stop "Windows Management Instrumentation"`  
        `net start “Windows Management Instrumentation”`  


**Problembehebungen**
1. Programmfehlerbehebung, um den Klartext entschlüsselter Always Encrypted-LOB-Spalten (Large Object) in SSMS anzuzeigen (Microsoft Connect-Element #2413024).
2. Programmfehlerbehebung im Always Encrypted-Dialogfeld, um einen Absturz zu behandeln, wenn Windows-Formatierungsvisualisierungen nicht aktiviert sind (z.B. Aktivierung der Anzeige mit hohem Kontrast).
3. Programmfehlerbehebung für den Fehler „Methode nicht gefunden“, der Verbindungen mit SQL Server-Instanzen verhindert.
4. Programmfehlerbehebung für den Absturz von SSMS beim Erstellen einer Partitionsfunktion mit „datetime offset“.
5. Programmfehlerbehebung, um die Anforderung zu entfernen, dass Microsoft .NET 3.5 zum Starten des Distributed Replay-Verwaltungstools (DReplay.exe) erforderlich ist.
6. Programmfehlerbehebung beim Bereitstellungs-Assistenten für Analysis Services, um vollqualifizierte Servernamen zu unterstützen.
7. Programmfehlerbehebung in SSMS, um Partitionen in tabellarischen Analysis Services-Modellen mit einem 2016-Kompatibilitätsmodell anzuzeigen (Microsoft Connect-Element #2845053).

[Weitere Informationen zu Fehlerbehebungen sind im SSMS-Änderungsprotokoll verfügbar.](../ssms/sql-server-management-studio-changelog-ssms.md)
 
---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-july-2016-hotfix-update-releasehttpgomicrosoftcomfwlinklinkid822301"></a>![Download](../ssdt/media/download.png) [SQL Server Management Studio – Hotfixupdate Juli 2016](http://go.microsoft.com/fwlink/?LinkID=822301)

13. Juli 2016 | Versionsnummer: 13.0.15600.2

**Funktionen**  
1. Unterstützung für Azure SQL Data Warehouse in SSMS.   
2. Umfangreiche Updates am SQL Server PowerShell-Modul.   
3. Deutlich verbesserte Verbindungszeiten für Azure SQL-Datenbanken.  
4. Verbesserte Unterstützung für tabellarische SQL Server 2016-Datenbanken (Kompatibilitätsstufe 1200) im Dialogfeld „Analysis Services-Prozess“ und im Bereitstellungs-Assistenten für Analysis Services.   

[Weitere Informationen und Features finden Sie im SSMS-Änderungsprotokoll.](../ssms/sql-server-management-studio-changelog-ssms.md)

**Bekannte Probleme** 
1. **Das Installationsprogramm für den SSMS-Hotfix aus Juli wird als SSMS-Release aus August angezeigt.**
Auf der Setupseite für den Updatehotfix aus Juli ist aufgrund einer internen Buildeinstellung „August“ angegeben. Bei diesem Paket handelt es sich jedoch um einen Hotfix für das Juli-Release von SSMS. 
2. **SSMS kann keine Verbindung mit SQL Server-Instanzen herstellen, nachdem der Hotfix aus Juli 2016 installiert wurde.**
Es ist ein bekanntes Problem, dass beim aktuellen SSMS-Update ein Problem auftritt, wenn eine Verbindung mit einem Server hergestellt werden soll. Bei diesem Problem wird folgender Fehler ausgegeben: 
   ```
    "Method not found: 'Void Microsoft.SqlServer.Management.Common.SqlConnectionInfo.set_ApplicationIntent(System.String)'"
    ```
  
    Dieses Problem wird mit dem nächsten SSMS-Release behoben. Als Problemumgehung können Sie SSMS deinstallieren und erneut installieren. Weitere Einzelheiten finden Sie [in unserem Microsoft Connect-Thread zu diesem Problem](https://connect.microsoft.com/SQLServer/feedback/details/2925257/not-able-to-connect-to-sql-server-instances-after-installing-ssms-2016-july-update).
    
3. **SSMS stürzt ab, wenn versucht wird, ein Azure-Speicherkonto auszuwählen.**
Das SSMS-Release aus Juli und der Hotfix aus Juli stürzen ab, wenn versucht wird, ein Azure-Speicherkonto auszuwählen, und Sie nicht über ein „klassisches“ Speicherkonto verfügen.
Dieses Problem wird in einem zukünftigen SSMS-Release behoben. Als Problemumgehung können Sie ein klassisches Speicherkonto erstellen oder [T-SQL für Sicherung und Wiederherstellung verwenden](https://msdn.microsoft.com/library/jj720552(v=sql.120).aspx), um Ihre Datenbanken in einem Azure-Speicherkonto zu sichern und wiederherzustellen.

4. **SSMS zeigt in den Assistenten für Sicherung/Wiederherstellung ausschließlich „klassische“ Azure-Speicherkonten an.**
Im SSMS-Release aus Juli und im Hotfix aus Juli werden ausschließlich „klassische“ Azure-Speicherkonten für die Erstellung neuer Anmeldeinformationen angezeigt, wenn Sie versuchen, Daten über die Assistenten für Sicherung und Wiederherstellung zu sichern oder wiederherzustellen.
Dieses Problem wird in einem zukünftigen SSMS-Release behoben. Als Problemumgehung können Sie Ihre Datenbanken im verfügbaren „klassischen“ Speicherkonto sichern/wiederherstellen oder [T-SQL für Sicherung und Wiederherstellung verwenden](https://msdn.microsoft.com/library/jj720552(v=sql.120).aspx), um Ihre Datenbanken in Speicherkonten vom Typ „ARM“ zu sichern und wiederherzustellen. 

5. **Für SSMS-Installationen in anderen Sprachen als Englisch ist möglicherweise die Installation eines zusätzlichen Sicherheitspakets erforderlich.**
In andere Sprachen als Englisch lokalisierte Versionen von SSMS benötigen das [KB 2862966-Sicherheitsupdate-Paket](https://support.microsoft.com/en-us/kb/2862966) für die Installation unter: Windows 8, Windows 7, Windows Server 2012 und Windows Server 2008 R2.
6. **SSMS kann sich ausschließlich mit SSIS 2016-Instanzen (SQL Server 2016 Integration Services) verbinden.** Es gibt eine bekannte Kompatibilitätseinschränkung bei SQL Server Integration Services, die Verbindungen mit vorherigen Versionen verhindert.
Als Problemumgehung können Sie Ihre SQL Server Integration Services-Instanz über das SSMS-Release verbinden, das auf Ihre SSIS-Instanz ausgerichtet ist.
7. **SSMS speichert keine Wartungspläne für SQL Server 2008 R2 und frühere SQL Server-Versionen.** Wir arbeiten an der Behebung dieses Problems. In der Zwischenzeit können Sie das SSMS 2014-Release unten verwenden, um Wartungspläne zu speichern.
8. **Der SQL Server-Konfigurations-Manager kann nicht gestartet werden, wenn auf dem Clientcomputer keine SQL Server-Instanz installiert ist.** Wenn auf Ihrem Clientcomputer keine SQL Server-Instanz installiert ist, und Sie den SQL Server-Konfigurations-Manager starten, wird der Fehler „Die Verbindung mit dem WMI-Anbieter kann nicht hergestellt werden“ angezeigt. Problemumgehung:
    * Öffnen Sie eine Eingabeaufforderung als Administrator.
    * Führen Sie das Tool Mofcomp mit dem folgenden Befehl aus:  
      mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"
    * Führen Sie nach der Ausführung des Tools Mofcomp die folgenden Befehle aus, um den WMI-Dienst neu zu starten und die Änderungen zu übernehmen:  
       net stop "Windows Management Instrumentation"  
       net start "Windows Management Instrumentation"

**Problembehebungen**  
1. Programmfehlerbehebung im SSMS-Abfrage-Designer, um das Hinzufügen von Tabellen zum Designer zu ermöglichen, wenn ein Benutzer nicht über SELECT-Berechtigungen für die Tabellen verfügt.
2. Fehlerbehebung zum Hinzufügen von IntelliSense-Unterstützung für die Funktionen TRY_CAST() und TRY_CONVERT() [(Microsoft Connect-Element #2453461)](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast).
3. Fehlerbehebung im SSMS-Editor-Fenster, um das Öffnen von SQL-Dateien per Drag-&amp;-Drop zu ermöglichen [(Microsoft Connect-Element #2690658)](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios).
4. Fehlerbehebung in Analysis Services, um den Data Feed-Anbieter für mehrdimensionale Analysis Services-Modelle ordnungsgemäß anzuzeigen.
5. Fehlerbehebung in SSMS zum Verhindern des Absturzes beim Bearbeiten einer Join-Verknüpfung im SSMS-Tabellen-Designer [(Microsoft Connect-Element #2721052)](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms).  

[Weitere Informationen und Programmfehlerbehebungen finden Sie im SSMS-Änderungsprotokoll.](../ssms/sql-server-management-studio-changelog-ssms.md)

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-june-2016-releasehttpgomicrosoftcomfwlinklinkid799832"></a>![Download](../ssdt/media/download.png) [SQL Server Management Studio-Release Juni 2016](http://go.microsoft.com/fwlink/?LinkID=799832)

1. Juni 2016 | Versionsnummer: 13.0.15000.23

**Funktionen**  
Neues optimiertes SSMS-Installationsprogramm. Eigenständige SSMS-Releases. Automatische Prüfung auf Updates. Neues Dialogfeld für die Schnellsuche. SSMS basierend auf der Visual Studio 2015-Shell und vieles mehr.   
[Weitere Informationen finden Sie im SSMS-Änderungsprotokoll.](../ssms/sql-server-management-studio-changelog-ssms.md)

**Bekannte Probleme** 
1. **Die PowerShell-Skripterstellung im Always Encrypted-Assistenten ist aktuell deaktiviert.**
Dieses Problem wird in einem zukünftigen monatlichen SSMS-Update behoben.
2. **Die Kontextmenüoption „Spalten verschlüsseln“ im Objekt-Explorer ist für Tabellen und Spalten deaktiviert, wenn Sie mit einer Azure SQL-Datenbank verbunden sind.** Dieses Problem wird in einem zukünftigen monatlichen SSMS-Update behoben. Als Problemumgehung klicken Sie im Objekt-Explorer mit der rechten Maustaste, und wählen Sie „Aufgaben“ und „Spalten verschlüsseln“, um Spalten und Tabellen aus Azure SQL-Datenbank zu verschlüsseln.
3. **SSMS kann sich ausschließlich mit SSIS 2016-Instanzen (SQL Server 2016 Integration Services) verbinden.** Es gibt eine bekannte Kompatibilitätseinschränkung bei SQL Server Integration Services, die Verbindungen mit vorherigen Versionen verhindert.
Als Problemumgehung können Sie Ihre SQL Server Integration Services-Instanz über das SSMS-Release verbinden, das auf Ihre SSIS-Instanz ausgerichtet ist.
4. **SSMS speichert keine Wartungspläne für SQL Server 2008 R2 und frühere SQL Server-Versionen.** Wir arbeiten an der Behebung dieses Problems. In der Zwischenzeit können Sie das SSMS 2014-Release unten verwenden, um Wartungspläne zu speichern.
5. **Der SQL Server-Konfigurations-Manager kann nicht gestartet werden, wenn auf dem Clientcomputer keine SQL Server-Instanz installiert ist.** Wenn auf Ihrem Clientcomputer keine SQL Server-Instanz installiert ist, und Sie den SQL Server-Konfigurations-Manager starten, wird der Fehler „Die Verbindung mit dem WMI-Anbieter kann nicht hergestellt werden“ angezeigt. Problemumgehung:
    * Öffnen Sie eine Eingabeaufforderung als Administrator.
    * Führen Sie das Tool Mofcomp mit dem folgenden Befehl aus:  
      mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"
    * Führen Sie nach der Ausführung des Tools Mofcomp die folgenden Befehle aus, um den WMI-Dienst neu zu starten und die Änderungen zu übernehmen:  
       net stop "Windows Management Instrumentation"  
       net start "Windows Management Instrumentation"

**Problembehebungen**  
1. Dialogfeld für die Schnellsuche in SSMS, das besser in das aktuelle Dokument integriert ist und eine Suche über reguläre Ausdrücke ermöglicht ([Microsoft Connect-Element #2735513](https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/)).
2. Programmfehlerbehebung für die kontextbezogene F1-Hilfe in SSMS, um Hilfedokumente und -artikel ordnungsgemäß anzuzeigen.
3. Programmfehlerbehebung in der Ansicht „Zurückgestellte Abfragen“ des Abfragedatenspeichers, der beim Scrollen zu einem Absturz von SSMS geführt hat.
4. Programmfehlerbehebung beim OLEDB-Connector von Excel Analysis Services, um Verbindungen von Excel 2016 mit SQL Server Analysis Services zu ermöglichen.
5. Programmfehlerbehebung für das SSMS-Verbindungsdialogfeld, um das Verbindungsdialogfeld bei Verwendung von mehreren Monitoren auf demselben Monitor anzuzeigen wie das SSMS-Hauptsystem ([Microsoft Connect-Element #724909)](https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/).
6. Programmfehlerbehebungen für Always Encrypted-Features. Der Fehler, bei dem die Always Encrypted-Menüoption nicht ordnungsgemäß für Stretch-Datenbanken aktiviert wurde, wurde behoben. Außerdem wurde der Fehler im Always Encrypted-Assistenten behoben, bei dem der HSM-Anbieter SafeNet (Luna SA) nicht ordnungsgemäß verwendet wurde.

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-2014-sp1httpdownloadmicrosoftcomdownload156156992e6-f7c7-4e55-833d-249bd2348138enux86sqlmanagementstudiox86enuexe"></a>![Download](../ssdt/media/download.png) [SQL Server Management Studio 2014 SP1](http://download.microsoft.com/download/1/5/6/156992E6-F7C7-4E55-833D-249BD2348138/ENU/x86/SQLManagementStudio_x86_ENU.exe)

14. Mai 2015 | Versionsnummer: 12.0.4100.1

**Funktionen**  
Verbesserte Azure SQL-Datenbank-Unterstützung mit neuem Open im Management-Portal-Menü, Tabellendesigner-Integration und vielem mehr.   
[Weitere Informationen finden Sie in den Anmerkungen zu dieser Version](https://support.microsoft.com/en-us/kb/3058865).

**Bekannte Probleme**  
–

**Problembehebungen**
1. SSMS stürzt bei Tasks zum Verschieben von Wartungsplänen ab, wenn der Name des Wartungsplans und der erste SUB_PLAN-Name identisch sind.
2. Für gespeicherte Prozeduren, die „sp_executesql“ aufrufen, ist in SQL Server Management Studio (SSMS) kein Debugging möglich. Beim Drücken von F11 wird die Fehlermeldung „Die Objektreferenz ist nicht auf eine Instanz eines Objekts gesetzt“ angezeigt ([Microsoft Connect-Element #736509](https://connect.microsoft.com/SQLServer/feedback/details/736509/sql-server-2012-rtm-management-studio-cannot-debug-sp-executesql)).
3. In SQL Server Express verwaltet SSMS Volltext nicht vollständig ([Microsoft Connect-Element #740181](https://connect.microsoft.com/SQLServer/feedback/details/740181/management-studio-does-not-fully-manage-full-text-in-sql-server-express)).
4. SSMS verarbeitet nummerierte gespeicherte Prozeduren nicht einheitlich [(Microsoft Connect-Element #764197](https://connect.microsoft.com/SQLServer/feedback/details/764197/ssms-2012-inconsistently-handles-numbered-procedures)).
5. SSMS stürzt gelegentlich beim Schließen ab, wodurch ein automatischer Neustart verursacht wird ([Microsoft Connect-Element #774317](https://connect.microsoft.com/SQLServer/feedback/details/774317/sql-server-management-studio-2012-2014-crashes-when-closing)).
6. Beim Erstellen von Skripts werden die Anweisungen dupliziert, wenn Berechtigungen auf Spaltenebene in SSMS definiert werden ([Microsoft Connect-Element #797967](https://connect.microsoft.com/SQLServer/feedback/details/797967/ssms-create-script-duplicates-the-statements-for-grant-or-deny-column-permissions)).
7. SSMS stürzt möglicherweise ab, wenn Sie versuchen, das SSMS-Fenstersymbol auf der Taskleiste zu aktualisieren ([Microsoft Connect-Element #799430](https://connect.microsoft.com/SQLServer/feedback/details/799430/ssms-2012-sp-1-cu-5-installed-crash-when-enforce-refresh-on-connect)).

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-2012-sp3httpdownloadmicrosoftcomdownloadf67f673709c-d371-4a64-8bf9-c1dd73f60990enux86sqlmanagementstudiox86enuexe"></a>![Download](../ssdt/media/download.png) [SQL Server Management Studio 2012 SP3](http://download.microsoft.com/download/F/6/7/F673709C-D371-4A64-8BF9-C1DD73F60990/ENU/x86/SQLManagementStudio_x86_ENU.exe)  
  
21. November 2015 | Versionsnummer: 11.0.6020.0

**Funktionen**  
Vollversionen der SSMS Express-Editionen. Codeausschnitte. Columnstore-Indizes und mehr.  
[Weitere Informationen finden Sie in den Anmerkungen zu dieser Version.](https://support.microsoft.com/en-us/kb/3072779)
 
**Bekannte Probleme**  
–

**Problembehebungen**
1. Fehlende Spalten können in der Fehlermeldung nicht angegeben werden, wenn Sie Daten mithilfe des Import-/Export-Assistenten importieren.
2. Beim Wiederherstellen differenzieller Sicherungen in SSMS wird der Fehler „Der Wiederherstellungsplan kann aufgrund einer unterbrochenen LSN-Kette nicht erstellt werden“ ausgegeben.

---
## <a name="additional-downloads"></a>Weitere Downloads  
Eine Liste aller SQL Server Management Studio-Downloads finden Sie im [Microsoft Download Center](https://www.microsoft.com/en-us/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending).  
  
Das aktuelle Release von SQL Server Management Studio finden Sie unter [Herunterladen von SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  

---  
## <a name="related-resources"></a>Verwandte Ressourcen
[Update Center für Microsoft SQL Server](https://technet.microsoft.com/sqlserver/ff803383.aspx)   
[Schnellstart mit SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[SQL Server Management Studio-Forum](https://social.msdn.microsoft.com/forums/en-us/home?forum=sqltools)  

  

