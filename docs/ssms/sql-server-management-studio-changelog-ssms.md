---
title: "SQL Server Management Studio – Änderungsprotokoll (SSMS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 12/07/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 051c080de8a5b670a7fe3dbe70ccebf73bfb57a3
ms.sourcegitcommit: c77a8ac1ab372927c09bf241d486e96881b61ac9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio – Änderungsprotokoll (SSMS)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Dieser Artikel enthält Details zu Updates, Verbesserungen und Fehlerbehebungen für die aktuellen und früheren Versionen von SSMS. Laden Sie die [previous SSMS versions below (Vorgängerversionen von SSMS weiter unten)](#previous-ssms-releases) herunter.


## <a name="ssms-174download-sql-server-management-studio-ssmsmd"></a>[SSMS 17.4](download-sql-server-management-studio-ssms.md)
Allgemein verfügbar | Buildnummer: 14.0.17213.0

### <a name="whats-new"></a>Neues

**SSMS Allgemein**

Sicherheitsrisikobewertung:
- Es wurde ein neuer SQL-Risikoanalysedienst hinzugefügt, der Ihre Datenbanken auf potentielle Sicherheitsrisiken und Abweichungen von bewährten Methoden untersuchen kann, wie etwa Fehlkonfigurationen, übermäßige Berechtigungen und unzureichend geschützte vertrauliche Daten. 
- Zu den Ergebnissen der Bewertung zählen Aktionsschritte zum Beheben der jeweiligen Probleme und ggf. benutzerdefinierte Skripts zur Wiederherstellung. Der Bewertungsbericht kann für die verschiedenen Umgebungen und an spezifische Anforderungen angepasst werden. Weitere Informationen finden Sie unter [SQL-Sicherheitsrisikobewertung](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment).

SMO:
- Das Problem, bei dem *HasMemoryOptimizedObjects* unter Azure eine Ausnahme auslöste, wurde behoben.
- Unterstützung für die neue CATALOG_COLLATION-Funktion wurde hinzugefügt.

AlwaysOn-Dashboard:
- Verbesserungen an der Latenzanalyse in Verfügbarkeitsgruppen.
- Zwei neue Berichte: *AlwaysOn\_Latenz\_primär* und *AlwaysOn\_Latenz\_sekundär*.

Showplan:
- Aktualisierte Links verweisen auf die korrekte Dokumentation.
- Die Analyse von Einzelplänen ist direkt aus dem generierten eigentlichen Plan heraus möglich.
- Neuer Symbolsatz.
- Unterstützung für die Erkennung von „Logische Operatoren anwenden“, wie GbApply, InnerApply.
        
XE-Profiler:
- In XEvent Profiler umbenannt.
- Die Menübefehle „Stopp“/„Start“ führen jetzt standardmäßig zum Beenden/Starten der Sitzung.
- Aktivierte Tastenkombinationen (z. B. STRG-F zum Suchen).
- Hinzugefügte Aktionen ‚database\_name‘ und ‚client\_hostname‘ zu den entsprechenden Ereignissen in XEvent Profiler-Sitzungen. Damit die Änderung wirksam wird, müssen Sie möglicherweise vorhandene QuickSessionStandard- oder QuickSessionTSQL-Instanzen auf den Servern löschen – [Connect 3142981](https://connect.microsoft.com/SQLServer/feedback/details/3142981)

Befehlszeile:
- Neue Befehlszeilenoption („-G“), die verwendet werden kann, um SSMS automatisch eine Verbindung mit einem Server/einer Datenbank mithilfe von Active Directory-Authentifizierung (wahlweise ‚Integrated‘ oder ‚Password‘) herstellen zu lassen. Weitere Informationen finden Sie unter [Ssms-Hilfsprogramm](ssms-utility.md).

Assistent zum Importieren von Flatfiles:
- Neue Möglichkeit zur Auswahl eines anderen als des Standardschemanamens („dbo“) beim Erstellen der Tabelle.

Abfragespeicher:
- Der Bericht „Rückläufige Abfragen“ beim Erweitern der Liste der verfügbaren Berichte im Abfragespeicher wurde wiederhergestellt.

**Integration Services (IS)**
- Neue Funktion zur Paketüberprüfung im Bereitstellungs-Assistenten, die dem Benutzer hilft, Komponenten innerhalb von SSIS-Paketen zu erkennen, die in Azure-SSIS IR nicht unterstützt werden.

### <a name="bug-fixes"></a>Behebung von Programmfehlern

**SSMS Allgemein**

- Objekt-Explorer:
    - Ein Problem wurde behoben, bei dem der Tabellenwertfunktions-Knoten in Datenbankmomentaufnahmen nicht angezeigt wurde – [Connect 3140161](https://connect.microsoft.com/SQLServer/feedback/details/3140161).
    - Verbesserte Leistung beim Erweitern der Knotens *Datenbanken*, wenn der Server über AUTOCLOSE-Datenbanken verfügt.
- Abfrage-Editor:
    - Ein Problem wurde behoben, bei dem IntelliSense für Benutzer nicht verfügbar war, die keinen Zugriff auf die Masterdatenbank besitzen.
    - Es wurde ein Problem behoben, das in manchen Fällen zu Abstürzen von SSMS führte, wenn die Verbindung mit einem Remotecomputer geschlossen wurde – [Connect 3142557](https://connect.microsoft.com/SQLServer/feedback/details/3142557).
- XEvent-Viewer:
    - Die Funktionalität zum Exportieren nach XEL wurde wieder aktiviert.
    - Es wurden Probleme behoben, bei denen der Benutzer manchmal nicht in der Lage war, eine gesamte XEL-Datei zu laden.
- XEvent-Profiler:
    - Es wurde ein Problem behoben, das zu Abstürzen von SSMS führte, wenn der Benutzer nicht über die *VIEW SERVER STATE*-Berechtigungen verfügte.
    - Es wurde ein Problem behoben, bei dem das Schließen des XE Profiler-Livedatenfensters nicht zum Beendigen der zugrundeliegenden Sitzung führte.
- Registrierte Server:
    - Es wurde ein Problem behoben, bei dem der Befehl „Verschieben nach…“ nicht mehr funktionierte – [Connect 3142862](https://connect.microsoft.com/SQLServer/feedback/details/3142862) und [Connect 3144359](https://connect.microsoft.com/SQLServer/feedback/details/3144359/).
- SMO:
    - Es wurde ein Problem behoben, bei dem die TransferData-Methode für das Transfer-Objekt nicht funktionierte.
    - Es wurde ein Problem behoben, bei dem die Serverdatenbanken eine Ausnahme für angehaltene SQL DW-Datenbanken auslösten.
    - Es wurde ein Problem behoben, bei dem Skripts für SQL-Datenbank in SQL DW zur Erzeugung falscher T-SQL-Parameterwerte führte.
    - Es wurde ein Problem behoben, bei dem Skripts für eine Stretchingdatenbank fälschlicherweise zur Ausgabe der Option *DATA\_COMPRESSION* führten.
- Auftragsaktivitätsmonitor:
    - Es wurde ein Problem behoben, bei dem der Benutzer einen Fehler „Der Index lag außerhalb des Bereichs. Er darf nicht negativ und kleiner als die Sammlung sein. 
        Parametername: Index (System.Windows.Forms)“ erhielt, wenn er versuchte, nach der Kategorie zu filtern – [Connect 3138691](https://connect.microsoft.com/SQLServer/feedback/details/3138691).
- Verbindungsdialogfeld:
    - Es wurde ein Problem behoben, bei dem Benutzer ohne Zugriff auf einen Domänencontroller mit Lese-/Schreibzugriff sich nicht mithilfe von SQL-Authentifizierung bei einem SQL-Server anmelden konnte – [Connect 2373381](https://connect.microsoft.com/SQLServer/feedback/details/2373381).
- Replikation:
    - Es wurde ein Problem behoben, bei dem beim Anzeigen der Eigenschaften eines Pullabonnements in SQL Server ein Fehler der Art „Der Wert ‚NULL‘ kann nicht auf die Eigenschaft ServerInstance angewendet werden“ angezeigt wurde.
- SSMS-Setup:
    - Es wurde ein Problem behoben, bei dem das SSMS-Setup fälschlicherweise zu einer Neukonfiguration aller auf dem Computer installierten Produkte führte.
- Benutzereinstellungen:
   - Mit diesem Fix erhalten Benutzer der souveränen US Government-Cloud ununterbrochenen Zugriff auf ihre Azure SQL-Datenbank- und ARM-Ressourcen mithilfe von SSMS über universelle Authentifizierung und Azure Active Directory-Anmeldung.  Benutzer früherer Versionen von SSMS müssen „Extras“|„Optionen“|„Azure-Dienste“ öffnen und unter „Ressourcen-Management“ die Konfiguration der Eigenschaft „Active Directory-Autorität“ in „https://login.microsoftonline.us“ ändern.

**Analysis Services (AS)**

- Profiler: Es wurde ein Problem beim Herstellen von Verbindungen unter Verwendung von Windows-Authentifizierung für Azure AS behoben.
- Es wurde ein Problem behoben, das beim Stornieren von Verbindungsdetails für ein Modell 1400 zu einem Absturz führen konnte.
- Wenn beim Aktualisieren von Anmeldeinformationen ein Azure-Blob-Schlüssel im Verbindungseigenschaften-Dialogfeld festgelegt wird, wird er jetzt visuell maskiert.
- Es wurde ein Problem im Azure Analysis Services-Dialogfeld zur Benutzerauswahl behoben, bei dem bei der Suche die GUID der Anwendungs-ID anstelle der Objekt-ID angezeigt wurde.
- Es wurde ein Problem in der Symbolleiste des Datenbank durchsuchen\MDX-Abfrage-Designers behoben, das für einige Schaltflächen zu einer fehlerhaften Zuordnung der Symbole führte.
- Es wurde ein Problem behoben, das ein Herstellen von Verbindungen mit SSAS mithilfe von IIS-Http/Https-Adressen von msmdpump verhinderte.
- Mehrere Zeichenfolgen im Benutzerauswahl-Dialogfeld von Azure Analysis Services wurden jetzt für weitere Sprachen übersetzt.
- Die Eigenschaft „MaxConnections“ ist jetzt für Datenquellen in Tabellenmodellen sichtbar.
- Der Bereitstellungs-Assistent generiert jetzt korrekte JSON-Definitionen für Mitglieder der Azure AS-Rolle.
- Es wurde ein Problem in SQL Profiler behoben, bei dem das Auswählen von Windows-Authentifizierung für Azure AS trotzdem zur Anmeldeaufforderung führte.


## <a name="previous-ssms-releases"></a>Vorgängerversionen von SSMS

Laden Sie die Vorgängerversionen von SSMS herunter, indem Sie die Titellinks in den folgenden Abschnitten anklicken.

## <a name="downloadssdtmediadownloadpng-ssms-173httpsgomicrosoftcomfwlinklinkid858904"></a>![download (Herunterladen von)](../ssdt/media/download.png) [SSMS 17.3](https://go.microsoft.com/fwlink/?linkid=858904)
Allgemein verfügbar | Buildnummer: 14.0.17199.0

[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40a)


### <a name="enhancements"></a>Erweiterungen

- Es wurde ein neuer Assistent zum Importieren von Flatfiles hinzugefügt, um den Import von CSV-Dateien mithilfe eines intelligenten Frameworks zu optimieren, wozu minimale Benutzerintervention oder spezielles Domänenwissen erforderlich ist. Weitere Informationen finden Sie unter [Import Flat File to SQL Wizard (Importieren einer Flat File zum SQL-Assistenten)](../relational-databases/import-export/import-flat-file-wizard.md).
- Hinzugefügter „XEvent Profiler“-Knoten zum Objekt-Explorer. Weitere Informationen finden Sie unter [Use the SSMS XEvent Profiler (Verwenden des SSMS XEvent Profiler)](../relational-databases/extended-events/use-the-ssms-xe-profiler.md).
- Aktualisierte Wartevorgangsfilterung und -kategorisierung in historischen Wartevorgangsberichten des Performance Dashboards.
- Die Syntaxprüfung der „Predict“-Funktion wurde hinzugefügt.
- Die Syntaxprüfung der Abfragen der externen Bibliotheksverwaltung wurde hinzugefügt.
- SMO-Unterstützung für die externe Bibliotheksverwaltung wurde hinzugefügt.
- Die Unterstützung „PowerShell starten“ wurde dem Fenster „Registrierte Server“ hinzugefügt (erfordert ein neues SQL PowerShell-Modul).
- Always On: [die schreibgeschützte Routingunterstützung](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md) für Verfügbarkeitsgruppen wurde hinzugefügt.
- Eine Option zum Senden von Ablaufverfolgungsdetails an das Ausgabefenster für „Active Directory: universell mit MFA-Unterstützung“-Logins wurde hinzugefügt (standardmäßig deaktiviert, muss in den Benutzereinstellungen unter „Tools > Optionen > Azure-Dienste > Azure Cloud > Ablaufverfolgungsebene für ADAL-Ausgabefenster“ aktiviert werden). 
- Abfragespeicher: 
  - Es kann auf die Abfragespeicher-Benutzeroberfläche zugegriffen werden, auch wenn QDS deaktiviert ist, solange QDS Daten aufgezeichnet hat.
  - Die Abfragespeicher-Benutzeroberfläche macht die Kategorisierung von Wartevorgängen in allen vorhandenen Berichten verfügbar. Dadurch können Kunden die Szenarios der wichtigsten wartenden Abfragen und vieles mehr entsperren.
- Inklusionen der Header von Skriptparametern sind jetzt optional (standardmäßig deaktiviert, kann in den Benutzereinstellungen unter „Tools > Optionen > SQL Server-Objekt-Explorer > Skripts > Header für Skriptparameter einbeziehen“ aktiviert werden) – [Connect-Artikel 3139199](https://connect.microsoft.com/SQLServer/feedback/details/3139199).
- Das „RC“-Branding wurde entfernt.

### <a name="bug-fixes"></a>Fehlerbehebungen

**SSMS Allgemein**

- XEvent: 
   - Problem wurde behoben, bei dem SSMS nur einen Teil der Ereignisse in der XEL-Datei öffnet.
   - Verbesserte „Anzeigen von Livedaten“-Erfahrung, wenn die Standarddatenbank nicht die Bezeichnung „Master“ hat – [Connect-Artikel 1222582](https://connect.microsoft.com/SQLServer/feedback/details/1222582).
- Always On: Problem wurde behoben, bei dem „Wiederherstellen von Protokollsicherungen“ möglicherweise mit folgendem Fehler fehlschlägt: „Das Protokoll in diesem Sicherungssatz endet bei LSN x. Dies ist zu früh für die Anwendung des Sicherungssatzes auf die Datenbank.“
- Auftragsaktivitätsmonitor: inkonsistente Symbole wurden berichtigt – [Connect-Artikel 3133100](https://connect.microsoft.com/SQLServer/feedback/details/3133100).
- Abfragespeicher: Problem wurde behoben, bei dem Benutzer den Datumsbereich „benutzerdefiniert“ für Abfragespeicherberichte nicht auswählen konnte. Weitere Informationen finden Sie in den folgenden Artikeln.
   - [Connect-Artikel 3139842](https://connect.microsoft.com/SQLServer/feedback/details/3139842)
   - [Connect-Artikel 3139399](http://connect.microsoft.com/SQLServer/feedback/details/3139399)
- Problem wurde behoben, bei dem das Verbindungsdialogfeld die kürzlich verwendete Datenbank nicht „löscht“, wenn gespeicherte Informationen eine benannte Datenbank besitzt, und der Benutzer <default> auswählt.
- Skripterstellung für Objekte:
    - Problem wurde behoben, bei dem „Datenbankskript generieren“ nicht funktioniert und ein Fehler ausgelöst wird, wenn der Benutzer eine angehaltene DW-Datenbank auf dem Server hat, jedoch eine andere Nicht-DW-Datenbank ausgewählt hat und versucht hat, für diese ein Skript zu erstellen.
    - Problem wurde behoben, bei dem der Header für skriptbasierte gespeicherte Prozeduren nicht mit den Skripteinstellungen übereingestimmt hat, was zu einem irreführenden Skript geführt hat – [Connect-Artikel 3139784](http://connect.microsoft.com/SQLServer/feedback/details/3139784).
    - Die Schaltfläche „Skript“ wurde bei Abzielen auf SQL Azure-Objekt erneut aktiviert.
    - Problem wurde behoben, bei dem SSMS die Skripterstellung für „Alter“ oder „Execute“ für einige Objekte (UDF, View, SP, Trigger) beim Herstellen einer Verbindung zu einer Azure SQL-Datenbank nicht zugelassen hat – [Connect-Artikel 3136386](https://connect.microsoft.com/SQLServer/feedback/details/3136386).
- Abfrage-Editor:
  - Verbesserte IntelliSense-Funktion beim Nutzen von Azure SQL-Datenbanken.
  - Problem wurde behoben, bei dem Abfragen aufgrund eines abgelaufenen Authentifizierungstokens (Universelle Authentifizierung) fehlgeschlagen sind.
  - Verbesserte IntelliSense-Funktion beim Arbeiten mit Azure SQL-Datenbanken (besonders, wenn eine Verbindung zu Azure SQL-Datenbank hergestellt wird, wird die neueste T-SQL-Grammatik (140) verwendet).
  - Problem wurde behoben, bei dem das Öffnen eines Abfragefensters mit einer Verbindung zu einer Nicht-DataWarehouse-Datenbank auf einem Server veranlassen würde, dass alle nachfolgenden Abfragefenster für diesen Server für DataWarehouse-Datenbanken mehrere Fehler zu nicht unterstützen Typen/Optionen ausgeben würden.
- Always On:
   - Spalte im Seedingmodus wurde dem Always On-Dashboard und den AG-Eigenschaftenseiten hinzugefügt.
   - Problem wurde behoben, bei dem es nicht möglich war, eine Linux-AG zu erstellen, wenn sich das primäre Element unter Windows befindet – [Connect-Artikel 3139856](https://connect.microsoft.com/SQLServer/feedback/details/3139856).
- Mehrere Probleme mit „Nicht genügend Arbeitsspeicher.“ wurden in SSMS beim Ausführen von Abfragen behoben – [Connect-Artikel 2845190](https://connect.microsoft.com/SQLServer/feedback/details/2845190), [Connect-Artikel 3123864](https://connect.microsoft.com/SQLServer/feedback/details/3123864).
- Profiler: 
   - Problem wurde behoben, bei dem der Profiler nicht funktioniert hat, als er für SQL 2005 benutzt wurde.
   - Problem wurde behoben, bei dem der Profiler die Verbindungsoption „Dem Serverzertifikat vertrauen“ nicht berücksichtigt hat.
- Aktivitätsmonitor: Problem wurde behoben, bei dem der Aktivitätsmonitor nicht funktioniert, wenn er auf einen Server von SQL Server unter Linux gezeigt wird.
- Problem mit der SMO-Übertragungsklasse wurde behoben, bei dem External Data Source- oder externe File Format-Objekte nicht übertragen wurden. Diese Art Objekte sollten nun ordnungsgemäß in der Übertragung enthalten sein.
- Registrierte Server:
   - Aktivierte Multiserverabfrage für Benutzer-Agent-Server (es wird versucht, das gleiche Token für jeden Benutzer-Agent-Server in der Gruppe zu verwenden).
- Universelle AD-Authentifizierung:
   - Problem wurde behoben, bei dem die Azure AD-Authentifizierung nicht unterstützt wurde.
   - Problem wurde behoben, bei dem der Tabellen/Sicht-Designer nicht funktioniert hat.
   - Problem wurde behoben, bei dem „Die ersten 1000 Zeilen auswählen“ und „Die ersten 200 Zeilen bearbeiten“ nicht funktioniert haben.
- Datenbankwiederherstellung: Problem wurde behoben, bei dem die Wiederherstellung den letzten Ordner im Pfad bei der Verschiebung von Dateien zu einem anderen Speicherort ausgelassen hat.
- Assistent für die Komprimierung:
   - Problem wurde bei der Verwaltung des Assistenten für die Komprimierung für Indizes behoben. Ein weiteres Problem wurde behoben, bei dem Assistenten zum Komprimieren von Daten für SQL 2016 und niedriger fehlerhaft waren.
        https://connect.microsoft.com/SQLServer/feedback/details/3139342
   - Assistent zum Komprimieren wurde den Azure-Tabellen und -Indizes hinzugefügt.
- Showplan: 
   - Problem wurde behoben, bei dem PDW-Operatoren nicht erkannt wurden.
- Servereigenschaften:
   - Problem wurde behoben, bei dem nicht möglich war, die Prozessoraffinität des Servers zu ändern.


**Analysis Services (AS)**

- Eine Reihe von Problemen wurden mit dem Assistent für die Bereitstellung behoben, um den tabellarischen 1400-Kompatibilitätsgradmodus und Power Query-Datenquellen zu unterstützen.
- Der Assistent für die Bereitstellung kann nun auf AS Azure bereitstellen, wenn er auf einer Befehlszeile ausgeführt wird.
- Bei Verwendung von Windows Auth in AS Azure wird dem Benutzer nun der Namen des Benutzerkontos im Objekt-Explorer korrekt angezeigt.


### <a name="known-issues-in-this-173-release"></a>Bekannte Probleme in dieser Version 17.3:

**SSMS Allgemein**

- Die folgenden SSMS-Funktionen werden für die Azure AD-Authentifizierung nicht unterstützt, wenn die universelle Authentifizierung mit MFA verwendet wird:
   - Der Datenbankoptimierungsratgeber wird für die Azure AD-Authentifizierung nicht unterstützt. Es liegt ein bekanntes Problem vor, bei dem dem Benutzer die folgende kryptische Fehlermeldung angezeigt wird: „Could not load file or assembly 'Microsoft.IdentityModel.Clients.ActiveDirectory,…“ (Datei oder Assembly ‚Microsoft.IdentityModel.Clients.ActiveDirectory,…‘ konnte nicht geladen werden), obwohl man eigentlich folgende Fehlermeldung erwarten würde: „Database Engine Tuning Advisor does not support Microsoft Azure SQL Database. (DTAClient)“ (Die Microsoft Azure SQL-Datenbank wird vom Datenbankoptimierungsratgeber nicht unterstützt).
- Bei dem Versuch, eine Abfrage in DTA zu analysieren entsteht folgender Fehler: "Object must implement IConvertible. (mscorlib)“ (Objekt muss IConvertible implementieren).
- *Rückläufige Abfragen* fehlen in der Liste der Berichte im Abfragespeicher im Objekt-Explorer.
   - Problemumgehung: Klicken Sie mit der rechten Maustaste auf den Knoten **Abfragespeicher**, und wählen Sie **View Regressed Queries (Rückläufige Abfragen anzeigen)** aus.

**Integration Services (IS)**

- Der [Ausführungspfad] in [Katalog].[Ereignismeldungen] ist für Paketausführungen in Scale Out falsch. Der [Ausführungspfad] beginnt mit „\Package“ anstelle des Objektnamens des ausführbaren Pakets. Beim Anzeigen der Übersichtsberichte von Paketausführungen in SSMA kann der Link zum „Ausführungspfad“ in der Übersicht über die Ausführung nicht funktionieren. Klicken Sie im Übersichtsbericht auf „Nachrichten anzeigen“, um alle Ereignismeldungen zu prüfen.


## <a name="downloadssdtmediadownloadpng-ssms-172httpsgomicrosoftcomfwlinklinkid854085"></a>![download (Herunterladen von)](../ssdt/media/download.png) [SSMS 17.2](https://go.microsoft.com/fwlink/?linkid=854085)
Allgemein verfügbar | Buildnummer: 14.0.17177.0

[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40a)

### <a name="enhancements"></a>Erweiterungen

- Multi-Factor Authentication (MFA)
  - Azure AD-Authentifizierung für mehrere Benutzer für eine universelle Authentifizierung mit Multi-Factor Authentication (UA mit MFA)
  - Ein neues Eingabefeld für Benutzeranmeldeinformationen wurde der universellen Authentifizierung mit MFA hinzugefügt, um die Authentifizierung für mehrere Benutzer zu unterstützen.
- Das Dialogfeld „Verbindung“ unterstützt nun die folgenden fünf Authentifizierungsmethoden:
  - Windows-Authentifizierung
  - SQL Server-Authentifizierung
  - Active Directory: Universell mit MFA-Unterstützung
  - Active Directory: Kennwort
  - Active Directory: Integriert

- Verwenden der universellen Authentifizierung mit MFA durch den Assistenten für Datenbankimport und -export für DacFx.
- Informationen zur API-Unterstützung finden Sie unter [IUniversalAuthProvider-Schnittstelle](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx).
- Die von ADAL verwaltete Bibliothek, die von der universellen Authentifizierung mit MFA in Azure AD verwendet wird, wurde auf Version 3.13.9 aktualisiert.
- Zusätzlich wurde eine neue CLI-Schnittstelle erstellt, die Azure AD-Administratoreinstellungen für SQL Datenbank und SQL Data Warehouse unterstützt.

 Weitere Informationen zu den Authentifizierungsmethoden in Active Directory finden Sie unter [Universal Authentication with SQL Database and SQL Data Warehouse (SSMS support for MFA) (Universelle Authentifizierung mit SQL-Datenbank und SQL Data Warehouse (SSMS-Unterstützung für MFA))](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) und [Configure Azure SQL Database multi-factor authentication for SQL Server Management Studio (Konfigurieren der mehrstufigen Authentifizierung in Azure SQL-Datenbank für SQL Server Management Studio)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure).

- Das Ausgabefenster enthält Einträge für Abfragen, die während der Erweiterung der Objekt-Explorer-Knoten ausgeführt wurden
- Aktivierter Sicht-Designer für Azure SQL-Datenbanken
- Die Standardoptionen für die Skripterstellung für Skripterstellungsobjekte aus dem Objekt-Explorer in SSMS haben sich geändert:
  - Zuvor war das generierte Skript bei einer neuen Installation standardmäßig auf die neueste Version von SQL Server (aktuell SQL Server 2017) ausgerichtet.
  - Mit SSMS 17.2 wurde eine neue Option hinzugefügt: *Skripteinstellungen mit Quelle abgleichen*. Mit der Einstellung *TRUE* ist das generierte Skript auf dieselbe Version, denselben Modultyp und dieselbe Moduledition wie die des Servers, von dem aus das Skript für das Objekt erstellt wird, ausgerichtet.
  - Der Wert für *Skripteinstellungen mit Quelle abgleichen* ist standardmäßig auf *TRUE* festgelegt. Neue Installationen von SSMS verfügen somit automatisch über die Standardeinstellung, dass die Skripte von Objekten an dasselbe Ziel wie das des Originalservers gerichtet werden.
  - Wenn der Wert für *Skripteinstellungen mit Quelle abgleichen* auf *FALSE* festgelegt ist, werden die normalen Zieloptionen für die Skripterstellung aktiviert und funktionieren wie bisher.
    - Zusätzlich wurden alle Skripterstellungsoptionen in ihren eigenen Abschnitt verschoben: *Versionsoptionen*. Sie befinden sich nicht länger unter*Allgemeine Skriptoptionen*.

- Unterstützung für nationale Clouds in „Wiederherstellen aus URL“
- Die QueryStoreUI-Berichte unterstützen nun zusätzliche Metriken (RowCount, DOP, CLR Time usw.) aus „sys.query_store_runtime_stats“.
- IntelliSense wird nun für die Azure SQL-Datenbank unterstützt
    - https://connect.microsoft.com/SQLServer/feedback/details/3100677/ssms-2016-would-be-nice-to-have-intellisense-on-azure-sql-databases
- Sicherheit: Das Verbindungsdialogfeld stuft Serverzertifikate standardmäßig als nicht vertrauenswürdig ein und fordert Verschlüsselung für Azure SQL-Datenbankverbindungen an
- Allgemeine Verbesserungen für die Unterstützung von SQL Server unter Linux:
 - Der Knoten „Datenbank-E-Mail“ ist zurück
 - Verschiedene auf Pfade bezogene Probleme wurden behoben
 - Der Aktivitätsmonitor ist stabiler
 - Das Dialogfeld „Verbindungseigenschaften“ zeigt die korrekte Plattform an
- Der Leistungsdashboard-Serverbericht ist nun als Standardbericht verfügbar:
  - Verbindung zu SQL Server 2008 und höheren Versionen möglich.
  - Der Unterbericht zu fehlenden Indizes verwendet Bewertungen, um das Identifizieren der nützlichsten Indizes zu unterstützen.
  - Der Unterbericht zum Verlauf der Wartezustände aggregiert die Wartevorgänge nun nach Kategorie. Wartevorgänge, die sich im Leerlauf oder Ruhezustand befinden, werden standardmäßig herausgefiltert.
  - Ein neuer Unterbericht für den Verlauf von Latches.
- Die Showplan-Knotensuche ermöglicht die Suche in Planeigenschaften. Einfache Suche nach beliebigen Operatoreigenschaften wie z.B. Tabellennamen. Das Verwenden dieser Option beim Anzeigen eines Plans:
  - Klicken Sie mit der rechten Maustaste auf „Plan“ und im Kontextmenü auf die Option „Knoten finden“
  - Drücken Sie STRG+F


**Analysis Services (AS)**

- Neue AAD-Rollenmemberauswahl für Benutzer ohne E-Mail-Adressen in AS Azure-Modellen in SSMS

**Integration Services (IS)**

- Eine neue Spalte („Anzahl von Ausführungen“) wurde dem Ausführungsbericht für SSIS hinzugefügt

### <a name="known-issues-in-this-release"></a>Bekannte Probleme in dieser Version:

- Bei Abfragefenstern, die die universelle Active Directory-Authentifizierung mit MFA-Unterstützung verwenden, kann ein Fehler ähnlich dem Folgenden auftreten, wenn versucht wird, eine Abfrage durchzuführen, nachdem das Fenster für eine Stunde geöffnet war:

   `Msg 0, Level 11, State 0, Line 0
The connection is broken and recovery is not possible. The client driver attempted to recover the connection one or more times and all attempts failed. Increase the value of ConnectRetryCount to increase the number of recovery attempts.`

   Ein erneutes Ausführen der Abfrage sollte den Fehler überwinden und erfolgreich sein.

- Die folgenden SSMS-Funktionalitäten werden für die Azure AD-Authentifizierung nicht unterstützt, wenn die universelle Authentifizierung mit MFA verwendet wird:
  - Der Designer **Neue Tabelle/Sicht** zeigt die Anmeldeaufforderung im alten Format an, außerdem funktioniert die Azure AD-Authentifizierung nicht.
  - Das Feature **Die ersten 200 Zeilen bearbeiten** unterstützt die Azure AD-Authentifizierung nicht.
  - Die Komponente **Registrierter Server** unterstützt die Azure AD-Authentifizierung nicht.
  - Der **Datenbankoptimierungsratgeber** wird für die Azure AD-Authentifizierung nicht unterstützt. Es liegt ein bekanntes Problem vor, bei dem der Benutzer eine wenig hilfreiche Fehlermeldung angezeigt bekommt: *Datei oder Assembly ‚Microsoft.IdentityModel.Clients.ActiveDirectory,…‘ konnte nicht geladen werden* Entgegen der Erwartung *wird die Microsoft Azure SQL-Datenbank nicht vom Datenbankoptimierungsratgeber unterstützt. (DTAClient)*.

**Analysis Services (AS)**

- Der Objekt-Explorer in SSAS zeigt den Benutzernamen der Windows-Authentifizierung nicht in den AS Azure-Verbindungseigenschaften an.

### <a name="bug-fixes"></a>Behebung von Programmfehlern

- Ein Problem behoben, das beim Versuch auftrat, die Ergebnisse einer Abfrage als Text zu drucken.  https://connect.microsoft.com/SQLServer/feedback/details/3055225/
- Es wurde ein Problem behoben, bei dem SSMS Tabellen und andere Objekte falsch gelöscht hat, wenn ein Skript für die Löschung dieser Objekte in einer SQL Azure-Datenbank erstellt wurde.
- Es wurde ein Problem behoben, bei dem SSMS gelegentlich den Start verweigert hat mit einem Fehler wie: „Eine oder mehrere Komponenten können nicht gefunden werden. Bitte installieren Sie die Anwendung neu“
- Es wurde ein Problem behoben, bei dem die SPID in der SSMS-Benutzeroberfläche veraltet und nicht mehr synchron angezeigt werden konnte. https://connect.microsoft.com/SQLServer/feedback/details/1898875
- Es wurde ein Problem bei der automatischen Installation von SSMS behoben, bei dem das Argument /passive als /quiet behandelt wurde.
- Es wurde ein Problem behoben, bei dem SSMS beim Start gelegentlich den Fehler „Objektverweis ist nicht auf eine Instanz des Objekts festgelegt“ ausgegeben hat. http://connect.microsoft.com/SQLServer/feedback/details/3134698
- Es wurde ein Problem mit dem „Datenkomprimierungs-Assistenten“ behoben, das einen Absturz von SSMS verursacht hat, wenn auf der Graph-Tabelle ‚Berechnen‘ angeklickt wurde
- Es wurde ein Leistungsproblem behoben, das beim Rechtsklicken auf einen Index für eine Tabelle (bei einer langsamen Internetverbindung) auftrat. https://connect.microsoft.com/SQLServer/feedback/details/3120783
- Es wurde ein Problem behoben, bei dem es SSMS nicht möglich war, Sicherungsdateien auf Servern mit einer Sammlung, bei der nach Groß- und Kleinschreibung unterschieden wird, aufzulisten. http://connect.microsoft.com/SQLServer/feedback/details/3134787 und https://connect.microsoft.com/SQLServer/feedback/details/3137000
- Showplan und Showplan vergleichen verschiedene Problembehebungen
- Es wurde ein Problem behoben, bei dem das Verbindungsdialogfeld dem Benutzer nicht gestattet hat, das „Netzwerkprotokoll“ anzugeben, das für die Verbindung verwendet werden soll, falls SQL Server nicht auf dem Computer installiert ist, auf dem SSMS ausgeführt wird. https://connect.microsoft.com/SQLServer/feedback/details/3134997
- Verbesserte Unterstützung für die Konfigurationen für mehrere Monitore, bei denen manche SSMS-Dialogfelder an zufälligen Orten angezeigt wurden. Die neue Option „Aufgabendialogfeld“ wurde unter den Benutzereinstellungen von „SQL Server-Objekt-Explorer | Befehle“ hinzugefügt, durch die es ermöglicht wird, die Position eines Aufgabendialogfelds oder Eigenschaftsblatts zu speichern, wenn es geschlossen wird. https://connect.microsoft.com/SQLServer/feedback/details/889169, https://connect.microsoft.com/SQLServer/feedback/details/1158271, https://connect.microsoft.com/SQLServer/feedback/details/3135260 
- Es wurde ein Problem behoben, bei dem SSMS keine Datenbankeigenschaften für verschlüsselte Azure SQL-Datenbanken ändern konnte
- Die Option „Ergebnisse nach der Ausführung verwerfen“ wurde verbessert. https://connect.microsoft.com/SQLServer/feedback/details/1196581
- Es wurde ein Problem behoben bzw. verbessert, bei dem es Benutzern nicht möglich war, auf Azure-Abonnements zuzugreifen, für die sie keine Administratorrechte besitzen.
- Der Assistent für die Datenbankwiederherstellung wurde verbessert, damit die Zieldatenbank in OE unabhängig von der Auswahl der Quelldatenbank ausgewählt bleibt. https://connect.microsoft.com/SQLServer/feedback/details/3118581
- Es wurde ein Problem behoben, bei dem der Objekt-Explorer neu hinzugefügte „nativ kompilierte gespeicherte Prozeduren“ nicht korrekt sortiert hat. http://connect.microsoft.com/SQLServer/feedback/details/3133365
- Es wurde ein Problem behoben, bei dem „SELECT TOP N ROWS“ die Klausel „TOP“ nicht enthalten hat. Für Azure SQLDW. https://connect.microsoft.com/SQLServer/feedback/details/3133551 und https://connect.microsoft.com/SQLServer/feedback/details/3135874
- QueryStoreUI: Es wurde ein Problem behoben, bei dem nicht benutzerdefinierte Zeitintervalle nicht bei allen Berichten ordnungsgemäß funktioniert haben.
- Always Encrypted:
    - Verbessertes Messaging für den AKV-Berechtigungsstatus im neuen CMK-Dialogfenster
    - Zur CEK-Dropdownliste wurde QuickInfo hinzugefügt, um die Entscheidung von CEKs mit langen Namen zu erleichtern
    - Es wurde ein Problem behoben, bei dem einige CNG-Schlüsselspeicheranbieter nicht im Dialogfeld „Neuer Spaltenhauptschlüssel“ für Always Encrypted angezeigt wurden
- Inkonsistenz bei „Anwendungsname“ für SSMS-Verbindungen wurde behoben. http://connect.microsoft.com/SQLServer/feedback/details/3135115
- Es wurde ein Problem behoben, bei dem SSMS inkorrekte Skripts für SQL Azure generiert hat (Tabellen und Indizes mit der Option „DATA_COMPRESSIONS“). https://connect.microsoft.com/SQLServer/feedback/details/3133148
- Es wurde ein Problem behoben, bei dem es dem Benutzer nicht möglich war, die Tastenkombination STRG+Q zu verwenden, um den Schnellstart auszuführen (Hinweis: Die neuen Tastenkombinationen, um die Option „IntelliSense aktiviert“ im Abfrage-Editor umzuschalten, sind nun STRG+B und STRG+I). https://connect.microsoft.com/SQLServer/feedback/details/3131968
- Es wurde ein Problem in „Datenbank wiederherstellen“ behoben, bei dem SSMS eine Ausnahme beim Versuch ausgelöst hat, ein Speicherkonto aus einem Abonnement auszuwählen, in dem sich Konten mit benutzerdefinierten Domänen befinden
- Es wurde ein Problem in „Datenbankdiagramm“ behoben, bei dem SSMS den Fehler „Der Index war außerhalb des Arraybereichs.“ ausgelöst hat. Außerdem war es dem Benutzer nicht möglich, die „Tabellenansicht“ in eine andere Einstellung als „Standard“ zu ändern. https://connect.microsoft.com/SQLServer/feedback/details/3133792 und http://connect.microsoft.com/SQLServer/feedback/details/3135326
- Es wurde ein Problem in „Sicherung/Wiederherstellung in die URL“ behoben, bei dem SSMS keine klassischen Speicherkonten aufgelistet hat.
- Es wurde ein Problem behoben, bei dem eine Ausnahme bei dem Versuch ausgelöst wurde, schemagebundene sicherungsfähige Elemente zu den Datenbankrollen hinzuzufügen. https://connect.microsoft.com/SQLServer/feedback/details/3118143
- Es wurde ein Problem behoben, bei dem SSMS gelegentlich folgenden Fehler angezeigt hat: „‘Data‘ ist NULL. Diese Methode oder Eigenschaft kann nicht für NULL-Werte aufgerufen werden.“ Beim Erweitern eines Tabellenknotens http://connect.microsoft.com/SQLServer/feedback/details/3136283
- DTA: Es wurde ein Problem behoben, bei dem „DTAEngine.exe“ mit Heapbeschädigung beendet wurde, wenn die Partitionsfunktion mit bestimmten Begrenzungswerten ausgewertet wurde.


**Analysis Services (AS)**

- Es wurde ein Problem behoben, bei dem „Datenbank wiederherstellen“ in AS zu einem Fehler führt, wenn die Datenbank einen anderen Namen als die ID trägt
- Es wurde ein Problem behoben, bei dem das DAX-Abfragefenster die Menüoption zum Umschalten von „IntelliSense aktiviert“ ignoriert hat
- Es wurde ein Problem behoben, bei dem die Verbindung zu SSAS durch IIS-Adressen (http/https) verhindert wurde, die „msmdpump“ enthalten
- Die Verbindung zu AS Azure mit einem Kennwort, das einen Semikolon enthält, ist nun möglich
- Das Ausgeben des AS-Befehls „Datenbank wiederherstellen“ mit der Option „Mitgliedschaft auslassen“ schließt die neue entsprechende JSON-Option ein, wenn SQL Server 2017, AS Server oder AS Azure verwendet wird
- Es wurde ein sehr seltenes Problem behoben, bei dem das Dialogfeld „Datenbank löschen“ beim Laden einen Fehler auslösen konnte
- Es wurde ein Problem behoben, das beim Versuch auftreten konnte, Partitionen im Modell mit Kompatibilitätsgrad 1400 anzuzeigen, die eine Mischung aus SQL-Abfragen und Partitionsdefinitionen enthalten

**Integration Services (IS)**
- Es wurde ein Problem behoben, bei dem die Berichte zu Ausführungsinformationen des SSISDB-Katalogs nicht angezeigt werden konnten
- Es wurde ein Problem in SSMS behoben, bei dem eine große Anzahl von Projekten/Paketen zu Leistungsproblemen führen konnte

## <a name="downloadssdtmediadownloadpng-ssms-171httpsgomicrosoftcomfwlinklinkid799832"></a>![download (Herunterladen von)](../ssdt/media/download.png) [SSMS 17.1](https://go.microsoft.com/fwlink/?linkid=799832)
Allgemein verfügbar | Buildnummer: 14.0.17119.0

[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

### <a name="enhancements"></a>Erweiterungen

- Profiler: „Hilfe“ > „Info“ zeigt jetzt die Versionsnummer (z.B. 17.1) an.
- Benutzer von Analysis Services können die Anmeldeinformationen für ihre Datenquellen für 1200 TM-Modelle und höher über das Kontextmenü auf der Datenquelle aktualisieren
- Integrierte SSIS-Berichte zeigen nun Protokolle der Ausführung der SSIS-Horizontalskalierung in CTP 2.1 an
- Verwaltungsanwendung der SSIS-Horizontalskalierung
  - Anzeigen grundlegender Informationen zum Master für horizontales Skalieren
  - Einfaches Hinzufügen eines Workers zur Bereitstellung für horizontales Skalieren
  - Anzeigen aller Worker für horizontales Skalieren und grundlegender Informationen zu diesen sowie deren einfache Aktivierung oder Deaktivierung

### <a name="bug-fixes"></a>Behebung von Programmfehlern
- Always On:
  - Ein Problem wurde behoben, bei dem die Eigenschaften eines Verfügbarkeitsreplikats immer im Modus „Automatisches Failover“ für WSFC-Verfügbarkeitsgruppen angezeigt wurden.
  - Ein Problem wurde behoben, bei dem die schreibgeschützte Routingliste beim Aktualisieren der Verfügbarkeitsgruppe überschrieben wurde
- Always Encrypted: Ein Problem wurde behoben, bei dem in der generierten Protokolldatei die Informationen von DacFx fehlten.
- ShowPlan: Ein Problem wurde behoben, bei dem auf der Benutzeroberfläche immer das tatsächliche Jointyp-Attribut für nichtadaptive Verknüpfungsoperatoren angezeigt wurde.
- Setup:
  - Ein Problem wurde behoben, bei dem SSMS 17.0 SSDT auf Visual Studio 2013 unterbrach [Microsoft Connect-Artikel 3133479]
  - Ein Problem wurde behoben, bei dem das Klicken auf „Neustart“ am Ende des Setups nicht zu einem Neustart des Computers führte
- Skripterstellung: Es wird vorübergehend verhindert, dass SSMS versehentlich Azure-Datenbankobjekte löscht, wenn versucht wird, ein Skript für den Löschvorgang zu erstellen, indem diese Option deaktiviert wird.  Dies wird in einer zukünftigen Version von SSMS behoben.
- Objekt-Explorer: Ein Problem wurde behoben, bei dem der Knoten „Datenbanken“ nicht erweitert wurde, wenn er mit einer Azure-Datenbank verbunden wurde, die mit „AS COPY“ erstellt wurde.

## <a name="downloadssdtmediadownloadpng-ssms-170httpgomicrosoftcomfwlinklinkid799832"></a>![download (Herunterladen von)](../ssdt/media/download.png) [SSMS 17.0](http://go.microsoft.com/fwlink/?LinkID=799832)
Allgemein verfügbar | Buildnummer: 14.0.17099.0

[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

### <a name="enhancements"></a>Erweiterungen 

- Upgradepaket und Windows Software Update Services (WSUS) 
    - Zukünftige 17.X-Versionen enthalten ein kleineres, kumulatives Updatepaket 
  - Das Updatepaket wird auch im WSUS-Katalog veröffentlicht werden  
- Symbolupdates
    - Symbole wurden aktualisiert, sind nun mit den von VS Shell bereitgestellten Symbolen konsistent und unterstützen hohe DPI-Auflösungen
    - Neue SSMS- und Profiler-Programmsymbole zur Unterscheidung zwischen 16.X und 17.X-Versionen
- SQL PowerShell-Modul
  - Das SQL Server PowerShell-Modul wurde aus SSMS entfernt und wird nun über den PowerShell-Katalog geliefert (PowerShell 5.0 ist nun erforderlich, um die Modulversionsverwaltung zu unterstützen)
  - Verschiedene Verbesserungen der Darstellung (Formatierung) einiger SMO-Objekte (z.B. zeigen Datenbanken nun die Größe und den verfügbaren Speicherplatz an und Tabellen zeigen Zeilenanzahl und Speicherplatznutzung an)
  - Eine neu hinzugefügte farbliche Kennzeichnung beim Aufrufen der PowerShell-Eingabeaufforderung im Menü „PowerShell starten“ in Outlook Express
  - Parameter -ClusterType und -RequiredCopiesToCommit zu VG-Cmdlets hinzugefügt (Cmdlets New-SqlAvailabilityGroup, Join-SqlAvailabilityGroup und Set-SqlAvailabilityGroup)
  - Parameter -ActiveDirectoryAuthority und -AzureKeyVaultResourceId zu Cmdlet Add-SqlAzureAuthenticationContext hinzugefügt
  - Die Cmdlets „Revoke-SqlAvailabilityGroupCreateAnyDatabase“, „Grant-SqlAvailabilityGroupCreateAnyDatabase“ und „Set-SqlAvailabilityReplicaRoleToSecondary“ wurden hinzugefügt
  - Der Parameter „-SeedingMode“ wurde zu den Cmdlets „Set-SqlAvailabilityReplica“ und „New-SqlAvailabilityReplica“ hinzugefügt
  - Der Parameter „-ConnectionString“ wurde zu „Get-SqlDatabase“ hinzugefügt
- SQL Server unter Linux
    - Allgemeine Verbesserungen und Fehlerbehebungen für den Protokollversand
  - Unterstützung für die nativen Linux-Pfade „Datenbank anfügen“, „Datenbank wiederherstellen“ und „Datenbank sichern“ wurde hinzugefügt
  - Unterstützung für native Linux-Pfade für den Zielordner von Überwachungsprotokollen wurde hinzugefügt
- Analysis Services
  - DAX-Abfragefenster:
    - Im Editor übereinstimmende Klammern
    - Syntaxunterstützung von DEFINE MEASURE und DEFINE VAR
    - Verschiedene IntelliSense-Verbesserungen
  - Universelle Authentifizierung
    - Ermöglicht Benutzern das Festlegen eines Benutzernamens ohne Kennwort und das Azure-Anmeldedialogfeld kümmert sich um die Verbindung
  - SSMS-PQ-Integration: 
    - Skripterstellung für strukturierte Datenquellen funktioniert 
    - Anzeigen und Bearbeiten strukturierter Datenquellen auf der PQ-Benutzeroberfläche
- Neue Vorlage für „Add Unique Constraint“ (Eindeutige Einschränkung hinzufügen)
- Showplan
    - Im Eigenschaftenfenster für verstrichene Zeit über alle Threads hinweg „max“ statt „sum“ anzeigen
    - Neue Mem Grant Operator-Eigenschaften verfügbar machen
    - Schaltfläche „Edit Query“ (Abfrage bearbeiten) in der Live-Abfragestatistik wurde aktiviert
    - Unterstützung für verschachtelte Ausführung
  - Neue Option bei „Tatsächlichen Ausführungsplan analysieren“
  - Allgemeine Verbesserungen beim Showplan-Vergleich
  - Eine neu eingeführte Funktion im Feature „Showplan-Vergleich“, die es ermöglicht, Unterschiede der Kardinalitätsschätzung zwischen abgeglichenen Knoten zweier Abfragepläne zu erkennen und grundlegende Analysen möglicher Hauptursachen durchzuführen
- Configuration Manager wurde vom Registrierte Server-Explorer entfernt
- Lesen von Überwachungsprotokollen vom Azure-Blobspeicher aktivieren
- Zusätzliche Parametrisierung für „Always Encrypted“; weitere Informationen finden Sie [hier](https://blogs.msdn.microsoft.com/sqlsecurity/2016/12/13/parameterization-for-always-encrypted-using-ssms-to-insert-into-update-and-filter-by-encrypted-columns/) 
- AUTH-Verbindung von AAD Universal zur Azure SQL-Datenbank unterstützt benutzerdefinierte Mandanten-ID 
- „Skripts generieren“ für die Azure SQL-Datenbank skriptet jetzt Volltext, Regeln und Datenbanken
- Korrekturen beim Branding auf dem Begrüßungsbildschirm von SSMS und Profiler
- Die Benutzeroberfläche des Steuerungspunkts für Hilfsprogramme wurde aus SSMS entfernt
- SSMS kann nun SQL Azure-Datenbanken der PremiumRS-Edition erstellen
- AlwaysOn-Verfügbarkeitsgruppen
  - Unterstützung für neue Clustertypen wurde hinzugefügt: EXTERNE und KEINE
    - Unterstützung für SQL Server unter Linux wurde hinzugefügt
    - Automatisches Seeding wurde als Option für die anfängliche Datensynchronisierung hinzugefügt
    - Einige Mängel z.B. beim Umgang mit der Endpunkt-URL, bei der Datenbankaktualisierung und beim Layout der Benutzeroberfläche wurden behoben
    - Mit Azure-Replikaten verbundene Funktionen wurden entfernt
  - IntelliSense wurde für mehrere Schlüsselwörter von Verfügbarkeitsgruppen verbessert
- Aktivitätsmonitor
  - Im SSMS-Ausgabefenster wurde der neue Bereich „Aktivitätsmonitor“ hinzugefügt
  - Die Meldung zu Verbindungsfehler/Timeout wurde so geändert, dass sie Informationen an das Ausgabefenster und nicht an eine Popupmeldung protokolliert
  - Das leere Diagramm (5. Diagramm) im Abschnitt „Übersicht“ wurde entfernt
  - Beim Titel in „Übersicht“ wird nun „(angehalten)“ angezeigt, wenn die Datensammlung für den Aktivitätsmonitor angehalten wird
  - Graph-Erweiterungen für SQL Server 
    - Neue Symbole für Diagrammknoten und Rahmentabellen
    - Diagrammknoten und Rahmentabellen werden im Ordner „Graph-Tabellen“ angezeigt
    - Vorlagen zum Erstellen von Diagrammknoten und Rahmentabellen sind verfügbar
- Darstellungsmodus
    - 3 neue Aufgaben, die über Schnellstart (STRG-Q) verfügbar sind
    - PresentOn: Präsentationsmodus aktivieren
    - PresentEdit: Präsentationsschriftgrade für Präsentationsmodus bearbeiten.  „Text Editor font“ (Text Editor-Schriftart) für den Abfrageeditor.  „Environment font“ (Umgebungsschriftart) für andere Komponenten.
    - RestoreDefaultFonts – Auf Standardeinstellungen zurücksetzen.
    - *Hinweis: Es ist derzeit kein PresentOff-Befehl verfügbar.  Verwenden Sie RestoreDefaultFonts, um den Präsentationsmodus zu deaktivieren*

### <a name="bug-fixes"></a>Behebung von Programmfehlern

- Ein Problem wurde behoben, bei dem SSMS abstürzte, wenn Showplan über das Touchpad des Surface Books gescrollt wurde
- Ein Problem wurde behoben, bei dem SSMS für lange Zeit hing, während die Eigenschaften einer Datenbank abgerufen wurden, die wiederhergestellt wurde oder offline war 
- Ein Problem wurde behoben, bei dem „Help Viewer“ in RC-Builds nicht geöffnet werden konnte
- Ein Problem wurde behoben, bei dem Elemente der Toolbox „Wartungsplantasks“ in SSMS fehlten
- Ein Problem in SSMS wurde behoben, bei dem ein Benutzer eine Datenbank nicht verkleinern konnte, wenn deren Name geschweifte Klammern enthielt [Microsoft Connect-Artikel](https://connect.microsoft.com/SQLServer/feedback/details/3122618)
- Ein Problem wurde behoben, bei dem SSMS versuchte, ein Skript für den Löschvorgang einer Azure-Datenbank zu erstellen, dabei aber die Datenbank selbst löschte [Microsoft Connect-Artikel](http://connect.microsoft.com/SQLServer/feedback/details/3131458/)
- Ein Problem wurde behoben, bei dem für Standardwerte für benutzerdefinierte Tabellentypen kein Skript erstellt wurde. [Microsoft Connect-Artikel](https://connect.microsoft.com/SQLServer/feedback/details/3119027)
- Eine weitere Runde von Leistungsverbesserungen um das Kontextmenü für Indizes. [Microsoft Connect-Artikel](https://connect.microsoft.com/SQLServer/feedback/details/3120783)
- Ein Problem wurde behoben, das übermäßiges Flimmern verursachte, wenn der Mauszeiger auf einen fehlenden Index im Ausführungsplan zeigte. [Microsoft Connect-Artikel](https://connect.microsoft.com/SQLServer/feedback/details/3118510)
- Ein Problem wurde behoben, bei dem SSMS die Datenbank beim Erstellen des Skripts [Connect Item (Connect-Artikel)](https://connect.microsoft.com/SQLServer/feedback/details/3118550) offline schaltete
- Verschiedene UI-Fehlerbehebungen auf lokalisierten (nicht englischen) Versionen von SSMS.
- Ein Problem wurde behoben, bei dem der Knoten „Always Encrypted Keys“ (Always Encrypted-Schlüssel) beim Adressieren von SQL 2016 SP1 Standard Edition fehlte.
- Always Encrypted
    - Das Menü „Always Encrypted“ wurde beim Adressieren von SQL 2016 RTM Standard Edition oder eines beliebigen SQL 2014-Servers (und früher) falsch aktiviert
    - Ein Problem wurde behoben, bei dem IntelliSense einen Fehler meldet, wenn die Syntax CREATE OR ALTER verwendet wird
    - Ein Problem wurde behoben, bei dem die Verschlüsselung versagt, falls CMK/CEK Zeichen enthalten, die mit Escapezeichen versehen (d.h. in Klammern eingeschlossen) werden sollten
    - Tritt eine Ausnahme in SSMS auf, dass nicht genügend Arbeitsspeicher vorhanden ist, wird dem Benutzer ein Fehler angezeigt, der stattdessen die Verwendung der nativen (64-Bit) PowerShell vorschlägt.
    - Ein Problem wurde behoben, bei dem der AE-Assistent einen Fehler verursacht hat, wenn der Benutzer Resource Group Manager-Abonnements anstelle von klassischen Azure-Abonnements verwendete
    - Ein Problem wurde behoben, bei dem der AE-Assistent einen falschen Fehler anzeigte, wenn der Benutzer keine Berechtigungen in Abonnements hatte oder in diesen nicht über Azure Key Vault verfügte.
    - Ein Problem im AE-Assistent wurde behoben, bei dem im Fall von mehreren AADs die Azure-Abonnements nicht auf der Azure Key Vault-Anmeldeseite angezeigt wurden
    - Ein Problem im AE-Assistent wurde behoben, bei dem die Azure-Abonnements, für die der Benutzer über eine Leseberechtigung verfügt, nicht auf der Azure Key Vault-Anmeldeseite angezeigt wurden
  - Ein Problem wurde behoben, bei dem Ressourcendateien nicht ordnungsgemäß geladen werden, was zu ungenauen Fehlermeldungen führte
- Verbesserter Kontrast von Hyperlinks auf SSMS-Setup-Seite
- Ein Problem wurde behoben, bei dem Polybase-Knoten bei Verbindung mit SQL Server Express (2016 SP1) nicht angezeigt wurden
- Ein Problem wurde behoben, bei dem SSMS den Kompatibilitätsgrad einer Azure-Datenbank nicht auf v140 ändern konnte
- Verbesserte Leistung von Objekt-Explorer beim Erweitern der Liste der Azure-Datenbanken [Connect Item (Connect-Artikel)](https://connect.microsoft.com/SQLServer/feedback/details/3100675)
- Ein Problem wurde behoben, bei dem das Kontextmenüelement „View SQL Server Log“ (SQL Server-Protokoll anzeigen) für nicht-relationale Servertypen (AS\RS\IS) nicht ordnungsgemäß angezeigt wurde 
- Ein Problem wurde behoben, bei dem das Prüfen der Syntax einer Analysis Services-Partitionsabfrage mithilfe von SQL-Authentifizierung zu einer Benachrichtigung führen konnte, dass die Anmeldung fehlgeschlagen ist
- Ein Problem wurde behoben, bei dem das Umbenennen eines mit Preview 1400 kompatiblen Tabellenmodells der Ebene AS in SSMS fehlschlug
- Ein Problem vom Typ „operation failed on model” (Fehler beim Vorgang auf Modell), das in seltenen Fällen nach dem Versuch auftreten konnte, eine ungültige Operation auf dem AS-Server durchzuführen, lokale Änderungen nach nicht erfolgreichem Speichern auf dem Modell zurücksetzen
- Ein Tippfehler im Popup-Dialogfeld „Analysis Services Synchronize Database“ wurde verbessert
- Dialogfelder von „Backup/Restore container“ (Container sichern/wiederherstellen) werden bei mehreren Bildschirmeinstellungen abseits des Bildschirms angezeigt. 
- „SecurityPolicy create“ (Sicherheitsrichtlinie erstellen) schlägt fehl, wenn das Zielobjekt eine eckige Klammer (]) im Namen hat.
- Das Menü „Zuletzt verwendete öffnen“ in SSMS 2016 zeigt keine zuletzt gespeicherten Dateien an. [Microsoft Connect-Artikel](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)
- Das Zurücksetzen der Benutzereinstellungen nach einem VS-Shell Update wurde behoben.
- Ein Problem wurde behoben, das einen Benutzer daran hinderte, den Kompatibilitätsgrad einer Datenbank in SQL Server 2017 anzupassen
- Abfragefenster, die die Authentifizierung mit AAD Universal verwenden, können die Abfrage nach einer Stunde nicht mehr aktualisieren.
- Die Benutzeroberfläche des Steuerungspunkts für Hilfsprogramme wurde aus SSMS entfernt.
- Verbindungen, die mit der Authentifizierung von AD Universal hergestellt wurden, können Daten nach Ablauf das anfänglichen Tokens nicht mehr abfragen.
- Das Skripten von Regeln von der Azure SQL-Datenbank in die Azure SQL-Datenbank ist nicht möglich.
- Das Problem wurde behoben, das dazu führte, das SQL-PowerShell keine Legacy-SQL-Instanzen verbinden konnte (2014 und älter). [Microsoft Connect-Artikel](https://connect.microsoft.com/SQLServer/feedback/details/1138754/sql-server-sqlps-powershell-module-fails-connection-to-sql-2012-instance)
- Das Problem wurde behoben, das zum Absturz von SSMS geführt hat, wenn das Importieren registrierter Server fehlgeschlagen war.
- Ein Problem wurde behoben, das zum Absturz von SSMS geführt hat, wenn ein Benutzer bestimmte Berechtigungen in einer Datenbank hatte. 
- SSMS – Tabellen verschwinden beim Prüfen der Sichten von der Entwurfsoberfläche. [Microsoft Connect-Artikel](https://connect.microsoft.com/SQLServer/feedback/details/2946125/ssms-tables-disappears-from-design-surface-while-reviewing-views) 
- Der Benutzer kann mit der Bildlaufleiste einer Tabelle nicht durch den Tabelleninhalt scrollen – dies ist nur mit den Nach-Oben/Nach-unten-Pfeiltasten möglich. Außerdem ist es möglich, durch den Tabelleninhalt zu scrollen, nachdem man versucht hat mithilfe der Bildlaufleiste zu scrollen – das ist ein Programmfehler. [Microsoft Connect-Artikel](
http://connect.microsoft.com/SQLServer/feedback/details/3106561/sql-server-manager-2016-bug-in-design-view) 
- Registrierte Server zeigen keine Symbole mehr an, nachdem der Stammknoten aktualisiert wurde.
- Die Skript-Schaltfläche für „Datenbank erstellen“ auf Servern von Azure v12 führt ein Skript aus und zeigt anschließend die Meldung „No action to be scripted“ (Keine Aktion für das Skript vorhanden) an.
- Das Dialogfeld „Verbindung mit Server herstellen“ in SSMS löscht die Registerkarte „Weitere Eigenschaften“ nicht für jede neue Verbindung.
- „Task-Skript generieren“ generiert keine Skripts für „Datenbank erstellen“ in der Azure SQL-Datenbank.
- Die Bildlaufleiste im Sicht-Designer scheint deaktiviert zu sein.
- AVK-Schlüsselpfade „Always Encrypted“ enthalten keine Versions-IDs.
- Verminderte Anzahl der Modul-Editionsabfragen im Abfragefenster. [Microsoft Connect-Artikel](http://connect.microsoft.com/SQLServer/feedback/details/3113387)
- Fehler bei „Always Encrypted“ durch das Aktualisieren von Modulen nach der Verschlüsselung werden falsch verarbeitet.
- Verändertes Standardverbindungstimeout für OLTP und OLAP zwischen 15 und 30 Sekunden, um eine Klasse ignorierter Verbindungsfehler zu korrigieren. 
- Der Absturz von SSMS nach dem Starten eines benutzerdefinierten Berichts wurde behoben. [Microsoft Connect-Artikel](http://connect.microsoft.com/SQLServer/feedback/details/3118856)
- Ein Problem wurde behoben, bei dem „Skript generieren“ für Azure SQL-Datenbanken fehlschlug
- „Script As“ und der „Assistent zum Generieren von Skripts“ wurden korrigiert, sodass keine zusätzlichen Zeilenvorschübe mehr eingefügt werden, wenn Objekte wie z.B. gespeicherte Prozeduren geskriptet werden. [Microsoft Connect-Artikel](http://connect.microsoft.com/SQLServer/feedback/details/3115850)
- SQLAS-PowerShell-Anbieter: Einfügen der Eigenschaft „Zuletzt verarbeitet“ in den Ordner „Dimension and MeasureGroup“ (Dimension und Measuregruppe). [Microsoft Connect-Artikel](http://connect.microsoft.com/SQLServer/feedback/details/3111879)
- Live-Abfragestatistik: das Problem wurde behoben, dass nur die erste Abfrage in einem Batch angezeigt wurde. [Microsoft Connect-Artikel] (http://connect.microsoft.com/SQLServer/feedback/details/3114221)  
- Showplan: im Eigenschaftenfenster über alle Threads hinweg „max“ statt „sum“ anzeigen.
- Abfragespeicher: einen neuen Bericht in Abfragen mit hoher Ausführungsvariation hinzufügen.
- Leistungsprobleme des Objekt-Explorers: [Microsoft Connect-Artikel](http://connect.microsoft.com/SQLServer/feedback/details/3114074)
    - Das Tabellenkontextmenü hängt vorübergehend
    - SSMS ist sehr langsam, wenn mit der rechten Maustaste auf den Tabellenindex geklickt wurde (über eine Remote(internet)verbindung). 
    - Tabellenabfragen, bei denen die Sortierung auf dem Server stattfindet, vermeiden
- Azure Bereitstellungsassistent (Datenbank in Azure VM bereitstellen) wurde aus SSMS entfernt
- Das Problem wurde behoben, dass fehlende Indices nicht im Ausführungsplan von SSMS angezeigt wurden [Microsoft Connect-Artikel](http://connect.microsoft.com/SQLServer/feedback/details/3114194)
- Häufig auftretende Probleme beim Beenden von SSMS (Absturz) wurden behoben.
- Problem beim Öffnen des Kontextmenüs (Fehler) auf den Knoten der Polybase- und Erweiterungsgruppen im Objektexplorer behoben [Microsoft Connect-Artikel](http://connect.microsoft.com/SQLServer/feedback/details/3115128)
- Problem beim Anzeigen der Berechtigungen einer Datenbank (Absturz) behoben
- Abfragespeicher: allgemeine Erweiterungen von Kontextmenüelementen für Ergebnisrastern von Abfragespeicherberichten
- Konfigurieren von „Always Encrypted“ schlägt für eine vorhandene Tabelle fehl mit Fehlern für nicht verknüpfte Objekte. [Microsoft Connect-Artikel](http://connect.microsoft.com/SQLServer/feedback/details/3103181)
- Konfigurieren von „Always Encrypted“ funktioniert nicht für eine vorhandene Datenbank mit mehreren Schemas. [Microsoft Connect-Artikel] (http://connect.microsoft.com/SQLServer/feedback/details/3109591)
- Der Assistent für „Always Encrypted“ und „Verschlüsselte Spaltendaten“ versagt, wenn die Datenbank Sichten enthält, die auf Systemsichten verweisen. [Microsoft Connect-Artikel] (http://connect.microsoft.com/SQLServer/feedback/details/3111925)
- Bei der Verschlüsselung mit „Always Encrypted“ werden Fehler durch das Aktualisieren von Modulen nach der Verschlüsselung falsch verarbeitet.
- Probleme mit dem Absturz der Benutzeroberfläche im Dialogfeld „Neue Serverregistrierung“ wurden behoben
- Beheben eines DMF-Problems, die Benutzeroberfläche aktualisiert Ausdrücke inkorrekt, die konstante Zeichenfolgewerte mit Anführungszeichen enthalten
- Das Problem wurde behoben, das zum Absturz von SSMS beim Ausführen von benutzerdefinierten Berichten geführt hat
- Das Menüelement „Execution in Scale Out...“ (Ausführung in horizontaler Hochskalierung) wurde dem Ordnerknoten hinzugefügt
- Ein Problem mit der Funktion zum Erstellen von IP-Adressen-Whitelists für die Firewall einer Azure SQL-Datenbank wurde behoben
- Ein Problem in SSMS wurde behoben, bei dem beim Bearbeiten der Source einer multidimensionalen AS-Partition die Ausnahme ausgelöst wurde, dass der Objektverweis nicht festgelegt ist
- Ein Problem in SSMS wurde behoben, bei dem beim Löschen einer Kundenassembly von einem multidimensionalen AS-Server die Ausnahme ausgelöst wurde, dass der Objektverweis nicht festgelegt ist
- Ein Problem wurde behoben, bei dem das Umbenennen einer tabellarischen AS-Datenbank 1400 fehlschlug
- Ein Problem bei der Skripterstellung für eine tabellarische AS-Datenquelle mit Kompatibilitätsgrad 1400 aus dem Dialogfeld „Verbindungseigenschaften“ wurde behoben
- Die Annahme wurde entfernt, dass Tabellen im AS-Modell mit Kompatibilitätsgrad 1400 mindestens eine Partition aufweisen
- Mit CTRL+R kann nun der Ergebnisbereich im DAX-Abfrage-Editor von SSMS umgeschaltet werden


## <a name="downloadssdtmediadownloadpng-ssms-1653httpgomicrosoftcomfwlinklinkid799832"></a>![download (Herunterladen von)](../ssdt/media/download.png) [SSMS 16.5.3](http://go.microsoft.com/fwlink/?LinkID=799832)
Allgemein verfügbar | Buildnummer: 13.0.16106.4

[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

In dieser Version wurden folgende Probleme behoben:

* Das seit SSMS 16.5.2 auftretende Problem wurde behoben, das die Erweiterung des Knotens „Tabelle“ verursacht hat, wenn die Tabelle mindestens eine Sparsespalte aufwies.

* Benutzer können SSIS-Pakete bereitstellen, die den OData-Verbindungs-Manager enthalten und die eine AX/CRM-Onlineressource von Microsoft Dynamix mit dem SSIS-Katalog verbinden. Weitere Informationen finden Sie unter [OData-Verbindungs-Manager](../integration-services/connection-manager/odata-connection-manager.md).

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


## <a name="ssms-1651"></a>SSMS 16.5.1
Allgemein verfügbar | Buildnummer: 13.0.16100.1

* Es wurde ein Problem behoben, bei dem Invoke-Sqlcmd fälschlicherweise mehrere Zeilen einfügt, wenn CHECK-Einschränkungen auftreten. [Microsoft Connect-Element: 811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

* Es wurde ein Problem behoben, das dazu geführt hat, dass nicht-ENU Sprachversionen beim Erstellen von Verfügbarkeitsgruppen nicht vollständig funktionieren.

* Es wurde ein Problem behoben, das dazu geführt hat, dass durch Klicken auf die Abfrageplan-XML nicht die richtige SSMS-Benutzeroberfläche geöffnet wurde.


## <a name="downloadssdtmediadownloadpng-ssms-165httpgomicrosoftcomfwlinklinkid799832"></a>![download (Herunterladen von)](../ssdt/media/download.png) [SSMS 16.5](http://go.microsoft.com/fwlink/?LinkID=799832)
Allgemein verfügbar | Buildnummer: 13.0.16000.28


[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

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


## <a name="downloadssdtmediadownloadpng-ssms-1641-september-2016httpgomicrosoftcomfwlinklinkid799832"></a>![download (Herunterladen von)](../ssdt/media/download.png) [SSMS 16.4.1 (September 2016)](http://go.microsoft.com/fwlink/?LinkID=799832)
Allgemein verfügbar | Buildnummer: 13.0.15900.1

[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

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
    
*  Es wurde ein Problem behoben, das dazu geführt hat, dass kein Zugriff auf das Monitorfenster einer Stretch-Datenbank möglich war.
    
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



## <a name="downloadssdtmediadownloadpng-ssms-163-august-2016httpgomicrosoftcomfwlinklinkid799832"></a>![download (Herunterladen von)](../ssdt/media/download.png) [SSMS 16.3 (August 2016)](http://go.microsoft.com/fwlink/?LinkID=799832)
Allgemein verfügbar | Versionsnummer: 13.0.15700.28


[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

* Die monatlichen Releases von SSMS werden nun nummeriert.

* [Neue Authentifizierungsoption**„Universelle Active Directory-Authentifizierung“**](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Dieser tokenbasierte Authentifizierungsmechanismus wird durch Azure Active Directory gestützt und bietet Unterstützung für mehrstufige, kennwortbasierte und integrierte Authentifizierungsmechanismen.

* Neue Vorlagen für erweiterte Ereignisse mit derselben Funktionalität wie SQL Server Profiler-Vorlagen [(Microsoft Connect-Element #2543925)](../tools/sql-server-profiler/sql-server-profiler-templates.md).

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
## <a name="downloadssdtmediadownloadpng-ssms-july-2016-hotfix-updatehttpgomicrosoftcomfwlinklinkid799832"></a>![download (Herunterladen des)](../ssdt/media/download.png) [SSMS July 2016 hotfix update (Hotfixupdates für SSMS (Juli 2016))](http://go.microsoft.com/fwlink/?LinkID=799832)
Allgemein verfügbar | Versionsnummer: 13.0.15600.2

[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

* **Programmfehlerbehebung in SSMS, um fehlende Kontextmenüelemente zu aktivieren**.  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2883440](https://connect.microsoft.com/SQLServer/feedback/details/2883440/lost-table-design-and-edit-top-n-rows-in-tables-context-menu)  
[Microsoft Connect-Element #2909644](https://connect.microsoft.com/SQLServer/feedback/details/2909644/ssms-2016-is-missing-edit-options-against-sql-express-2014)  
[Microsoft Connect-Element #2924345](https://connect.microsoft.com/SQLServer/feedback/details/2924345/some-ssms-object-explorer-right-click-menu-options-missing-in-july-update)

---
## <a name="ssms-july-2016"></a>SSMS Juli 2016 
Allgemein verfügbar | Versionsnummer: 13.0.15500.91

* *Bearbeitung 5. Juli:* Verbesserte Unterstützung für tabellarische SQL Server 2016-Datenbanken (Kompatibilitätsstufe 1200) im Dialogfeld „Analysis Services-Prozess“ und im Bereitstellungs-Assistenten für Analysis Services.

* *Bearbeitung 5. Juli:* Neue Option im SSMS-Dialogfeld „Abfrageausführungsoptionen“ zum Festlegen von ‚XACT_ABORT‘. Diese Option ist in dieser Version von SSMS standardmäßig aktiviert und weist SQL Server an, beim Auftreten eines Laufzeitfehlers ein Rollback der gesamten Transaktion auszuführen und den Batch abzubrechen.

* Unterstützung für Azure SQL Data Warehouse in SSMS.

* Umfangreiche Updates am SQL Server PowerShell-Modul. Zu diesen gehören ein neues [SQL PowerShell-Modul und neue CMDLETs für Always Encrypted, SQL Agent und SQL-Fehlerprotokolle](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update).

* Unterstützung für die PowerShell-Skripterstellung im Always Encrypted-Assistenten.

* Deutlich verbesserte Verbindungszeiten für Azure SQL-Datenbanken.

* Neues Dialogfeld „URL-Sicherung“, das die Erstellung von Azure-Speicheranmeldeinformationen für Datenbanksicherungen von SQL Server 2016 unterstützt. Dieser Dialog bietet eine optimierte Benutzeroberfläche zum Speichern von Datenbanksicherungen unter einem Azure-Speicherkonto.
 
* Neues Wiederstellen-Dialogfeld zur Optimierung der Wiederherstellung einer SQL Server 2016-Datenbanksicherung aus dem Microsoft Azure-Speicherdienst.
 
* Fehlerbehebung im SSMS-Abfrage-Designer, um das Hinzufügen von Tabellen zum Designer zu ermöglichen, wenn ein Benutzer nicht über SELECT-Berechtigungen für die Tabellen verfügt.

* Programmfehlerbehebung zum Hinzufügen von IntelliSense-Unterstützung für die Funktionen TRY_CAST() und TRY_CONVERT().  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2453461](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast).

* Programmfehlerbehebung im PowerShell-Modul, um das Laden der SQLAS-Erweiterung von Analysis Services zu ermöglichen.  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2544902](https://connect.microsoft.com/SQLServer/feedback/details/2544902/ssms-march-2016-refresh-sqlps-failed-to-load-the-sqlas-extension).

* Programmfehlerbehebung im SSMS-Editor-Fenster, um das Öffnen von SQL-Dateien per Drag & Drop zu ermöglichen.  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2690658](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios).

* Fehlerbehebung im Profiler, um den Absturz von Profiler beim Beenden zu beheben.  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2616550](https://connect.microsoft.com/SQLServer/feedback/details/2616550/sql-server-2016-rc2-profiler-version-13-0-1300-275-wont-close-after-trace-is-started-even-after-trace-is-stopped).  
[Microsoft Connect-Element #2319968](https://connect.microsoft.com/SQLServer/Feedback/Details/2319968).

* Programmfehlerbehebung in SSMS zum Verhindern des Absturzes beim Bearbeiten einer Join-Verknüpfung im SSMS-Tabellen-Designer.  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2721052](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms).

* Fehlerbehebung in SSMS, um die Datenbank-Skripterstellung für Mitglieder der db_owner-Rolle zu ermöglichen.  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2869241](https://connect.microsoft.com/SQLServer/feedback/details/2869241/error-with-script-database-as-create-to-in-ssms-2008r2-and-ssms-2016-june).

* Programmfehlerbehebung im SSMS-Editor zum Entfernen der Verzögerung beim Schließen einer Abfrageregisterkarte, wenn der Server offline gesetzt wurde.  
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2656058](https://connect.microsoft.com/SQLServer/feedback/details/2656058/ssms-2014-2016-query-tab-takes-significantly-longer-to-close-if-the-instance-it-was-connected-to-is-now-offline).

* Programmfehlerbehebung zum Aktivieren der Sicherungsoption in SQL Server Express-Datenbanken. 
*Verwandte Fehleranfragen von Kunden:*  
[Microsoft Connect-Element #2801910](https://connect.microsoft.com/SQLServer/feedback/details/2801910/ssms-2016-backup-option-not-appearing-in-tasks).  
[Microsoft Connect-Element #2874434](https://connect.microsoft.com/SQLServer/feedback/details/2874434/backup-missing-from-tasks-context-menu-in-ssms-2016-when-you-are-connected-to-an-express-instance).

* Fehlerbehebung in Analysis Services, um den Data Feed-Anbieter für mehrdimensionale Analysis Services-Modelle ordnungsgemäß anzuzeigen.

----
## <a name="downloadssdtmediadownloadpng-ssms-june-2016httpgomicrosoftcomfwlinklinkid799832"></a>![download (Herunterladen von)](../ssdt/media/download.png) [SSMS June 2016 (SSMS (Juni 2016))](http://go.microsoft.com/fwlink/?LinkID=799832)
Allgemein verfügbar | Versionsnummer: 13.0.15000.23

[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

* SSMS ist mit dem Release aus Juni 2016 allgemein verfügbar.

* Dialogfeld für die Schnellsuche in SSMS, das besser in das aktuelle Dokument integriert ist und eine Suche über reguläre Ausdrücke ermöglicht. 
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/>

* Verbesserungen beim SSMS-Installationsprogramm, um den Installationsfortschritt nachverfolgen und Exitcodes bei unbeaufsichtigten Installationen über Skripts zu verarbeiten.

* Programmfehlerbehebung für die kontextbezogene F1-Hilfe in SSMS, um Hilfedokumente und -artikel ordnungsgemäß anzuzeigen.

* Programmfehlerbehebung in der Ansicht „Zurückgestellte Abfragen“ des Abfragedatenspeichers, der beim Scrollen zu einem Absturz von SSMS geführt hat.

* Programmfehlerbehebung beim OLEDB-Connector von Excel Analysis Services, um Verbindungen von Excel 2016 mit SQL Server Analysis Services zu ermöglichen.

* Programmfehlerbehebung für das SSMS-Verbindungsdialogfeld, um das Verbindungsdialogfeld bei Verwendung von mehreren Monitoren auf demselben Monitor anzuzeigen wie das SSMS-Hauptsystem.  
*Verwandte Fehleranfragen von Kunden:*  
<https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/>
<https://connect.microsoft.com/SQLServer/feedback/details/755689/sql-server-management-studio-connect-to-server-popup-dialog/>  
<https://connect.microsoft.com/SQLServer/feedback/details/389165/sql-server-management-studio-gets-confused-dealing-with-multiple-displays/>

* Programmfehlerbehebungen für Always Encrypted-Features. Der Fehler, bei dem die Always Encrypted-Menüoption nicht ordnungsgemäß für Stretch-Datenbanken aktiviert wurde, wurde behoben. Außerdem wurde der Fehler im Always Encrypted-Assistenten behoben, bei dem der HSM-Anbieter SafeNet (Luna SA) nicht ordnungsgemäß verwendet wurde.


## <a name="additional-downloads"></a>Weitere Downloads  
Eine Liste aller SQL Server Management Studio-Downloads finden Sie im [Microsoft Download Center](https://www.microsoft.com/en-us/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending).  
  
Das aktuelle Release von SQL Server Management Studio finden Sie unter [Herunterladen von SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  
