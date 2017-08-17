---
title: Herunterladen von SQL Server Management Studio (SSMS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- Installieren von SSMS, Herunterladen von SSMS, neueste SSMS-Version
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- sql management studio install
- download sql management studio
- ms sql management studio
- install sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
caps.latest.revision: 145
author: stevestein
ms.author: sstein
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 3f12671ace99d5fefc199c7b1c2db31e5b3cfade
ms.openlocfilehash: a689293fadb1a442f94d88cc06a9e7a4ef06650f
ms.contentlocale: de-de
ms.lasthandoff: 08/08/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>Herunterladen von SQL Server Management Studio (SSMS)

SSMS ist eine integrierte Umgebung zum Verwalten jeder beliebigen SQL-Infrastruktur, von SQL Server bis hin zur SQL-Datenbank. SSMS stellt Tools zum Konfigurieren, Überwachen und Verwalten von Instanzen von SQL Server zur Verfügung. Verwenden Sie SSMS, um Abfragen und Skripts zu erstellen sowie die Datenebenenkomponenten bereitzustellen, zu überwachen und zu aktualisieren, die von Ihren Anwendungen verwendet werden.

Verwenden Sie SQL Server Management Studio (SSMS) zum Abfragen, Entwerfen und Verwalten Ihrer Datenbanken und Data Warehouses, unabhängig davon, ob sich diese auf Ihrem lokalen Computer oder in der Cloud befinden.

**SSMS ist kostenlos!**

SSMS 17.X ist die größte Generation von *SQL Server Management Studio* und stellt Unterstützung für SQL Server 2017 bereit.

**Download[ ![](../ssdt/media/download.png)Download SQL Server Management Studio 17.2 (Herunterladen von SQL Server Management Studio 17.2)](https://go.microsoft.com/fwlink/?linkid=854085)**

**Download[ ![](../ssdt/media/download.png)Download SQL Server Management Studio 17.2 Upgrade Package (upgrades 17.x to 17.2) (Herunterladen des Upgradepakets von SQL Server Management Studio 17.2 (Upgrades 17.X bis 17.2))](https://go.microsoft.com/fwlink/?linkid=854087)**

Die Installation von SSMS 17.X upgradet oder ersetzt nicht die Versionen 16.X oder früher von SSMS. SSMS 17.x wird parallel zu früheren Versionen installiert, damit beide Versionen zur Verfügung stehen.
Wenn ein Computer parallele SSMS-Installationen enthält, sollten Sie sich vergewissern, dass Sie die richtige Version für Ihre speziellen Anforderungen starten. Die neueste Version heißt *Microsoft SQL Server Management Studio 17* und verfügt über ein neues Symbol: 
 
   ![SSMS 17.X](media/download-sql-server-management-studio-ssms/version-icons.png)


> [!NOTE]
> Das SQL Server PowerShell-Modul ist nun eine separate Installation über den PowerShell-Katalog.  Weitere Informationen finden Sie in den [Downloadanweisungen](download-sql-server-ps-module.md).

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

**Versionsinformationen**

Versionsnummer: 17.2 Buildnummer dieser Version: 14.0.17177.0

## <a name="new-in-this-release"></a>In dieser Version neu

SSMS 17.2 ist die neueste Version von SQL Server Management Studio. Die Generation 17.X von SSMS bietet Support für beinahe alle Featurebereiche unter SQL Server 2008 bis SQL Server 2017. Version 17.X unterstützt auch SQL Analysis Service-PaaS.

Version 17.2 enthält Folgendes:

- Multi-Factor Authentication (MFA)
  - Azure AD-Authentifizierung für mehrere Benutzer für eine universelle Authentifizierung mit Multi-Factor Authentication (UA mit MFA)
  - Ein neues Eingabefeld für Benutzeranmeldeinformationen wurde der universellen Authentifizierung mit MFA hinzugefügt, um die Authentifizierung für mehrere Benutzer zu unterstützen.
- Das Dialogfeld „Verbindung“ unterstützt nun die folgenden fünf Authentifizierungsmethoden:
  - Windows-Authentifizierung
  - SQL Server-Authentifizierung
  - Active Directory: Universell mit MFA-Unterstützung
  - Active Directory: Kennwort
  - Active Directory: Integriert

- Der Assistent für Datenbankimport und -export für DacFx kann nun die universelle Authentifizierung mit MFA verwenden.
- Informationen zur API-Unterstützung finden Sie unter [IUniversalAuthProvider-Schnittstelle](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx).
- Die von ADAL verwaltete Bibliothek, die von der universellen Authentifizierung mit MFA in Azure AD verwendet wird, wurde auf Version 3.13.9 aktualisiert.
- Eine neue CLI-Schnittstelle, die Azure AD-Administratoreinstellungen für SQL Datenbank und SQL Data Warehouse unterstützt.

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
 - Einige auf Pfade bezogene Probleme wurden behoben
 - Verbesserungen der Stabilität des Aktivitätsmonitors
 - Das Dialogfeld „Verbindungseigenschaften“ zeigt die korrekte Plattform an
- Der Leistungsdashboard-Serverbericht ist nun als Standardbericht verfügbar:
  - Verbindung zu SQL Server 2008 und höheren Versionen möglich.
  - Der Unterbericht zu fehlenden Indizes verwendet Bewertungen, um das Identifizieren der nützlichsten Indizes zu unterstützen.
  - Der Unterbericht zum Verlauf der Wartezustände aggregiert die Wartevorgänge nun nach Kategorie. Wartevorgänge, die sich im Leerlauf oder Ruhezustand befinden, werden standardmäßig herausgefiltert.
  - Ein neuer Unterbericht für den Verlauf von Latches.
- Die Showplan-Knotensuche ermöglicht die Suche in Planeigenschaften. Einfache Suche nach beliebigen Operatoreigenschaften wie z.B. Tabellennamen. Das Verwenden dieser Option beim Anzeigen eines Plans:
  - Klicken Sie mit der rechten Maustaste auf „Plan“ und im Kontextmenü auf die Option „Knoten finden“
  - Drücken Sie STRG+F

Die vollständige Liste der Änderungen finden Sie unter [SQL Server Management Studio - Changelog (SSMS) (SQL Server Management Studio: Änderungsprotokoll (SSMS))](../ssms/sql-server-management-studio-changelog-ssms.md).

Informationen zur Benutzerdatensammlung finden Sie unter [SQL Server Privacy Statement (Datenschutzbestimmungen für SQL Server)](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx).

## <a name="supported-sql-offerings"></a>Unterstützte SQL-Angebote

* Diese Version von SSMS funktioniert mit allen [unterstützten Versionen von SQL Server 2008 – SQL Server 2017](https://support.microsoft.com/lifecycle?C2=1044) und bietet das höchste verfügbare Maß an Unterstützung für die Arbeit mit den neuesten Cloudfunktionen in Azure SQL-Datenbank und Azure SQL Data Warehouse.
* Es besteht keine explizite Sperre für SQL Server 2000 oder SQL Server 2005, jedoch funktionieren einige Features möglicherweise nicht ordnungsgemäß.
* Zusätzlich kann SSMS 17.X zusammen mit SSMS 16.X oder SQL Server 2014 SSMS und früher installiert werden.

## <a name="supported-operating-systems"></a>Unterstützte Betriebssysteme
  
Dieses Release von SSMS unterstützt die folgenden 64-Bit-Plattformen, wenn sie mit dem aktuellen Service Pack ausgestattet sind:
- Windows 10 (64-Bit)
- Windows 8.1 (64-Bit)
- Windows 8 (64-Bit)
- Windows 7 (SP1) (64-Bit)
- Windows Server 2016 *
- Windows Server 2012 R2 (64-Bit)
- Windows Server 2012 (64-Bit)
- Windows Server 2008 R2 (64-Bit)

\* SSMS 17.X basiert auf der isolierten Visual Studio 2015-Shell, die vor Windows Server 2016 veröffentlicht wurde. Microsoft nimmt die App-Kompatibilität ernst und stellt sicher, dass bereits versendete Anwendungen weiterhin unter den neuesten Windows-Versionen ausgeführt werden. Um Probleme bei der Ausführung von SSMS unter Windows Server 2016 zu minimieren, stellen Sie sicher, dass SSMS über die neuesten Updates verfügt. Wenn Sie auf Probleme mit SSMS unter Windows Server 2016 stoßen, kontaktieren Sie den Support. Das Supportteam bestimmt, ob das Problem bei SSMS, Visual Studio oder bei der Windows-Kompatibilität liegt. Das Problem wir dann zur weiteren Untersuchung an das entsprechende Team weitergeleitet.

## <a name="ssms-installation-tips-and-issues"></a>Tipps und Probleme bei der Installation von SSMS

### <a name="minimize-installation-reboots"></a>Minimieren von Installationsneustarts

* Führen Sie die folgenden Aktionen durch, um zu verhindern, dass das SSMS-Setup einen Neustart am Ende der Installation benötigt:
  * Stellen Sie sicher, dass Sie eine aktuelle Version von Microsoft Visual C++ 2013 Redistributable Package ausführen. Die Version 12.00.40649.5 (oder höher) ist erforderlich. Es wird nur die x64-Version benötigt.
  * Überprüfen Sie, ob die .NET Framework-Version auf dem Computer 4.6.1 (oder höher) ist.
  * Schließen Sie alle anderen Instanzen von Visual Studio, die auf dem Computer geöffnet sind.
  * Stellen Sie sicher, dass die neuesten Betriebssystemupdates auf dem Computer installiert sind.
  * Die registrierten Aktionen werden normalerweise nur einmal benötigt. Es gibt einige Fälle, in denen ein Neustart während zusätzlichen Upgrades auf dieselbe Hauptversion von SSMS notwendig sind. Für kleinere Upgrades sind alle Voraussetzungen für SSMS bereits auf dem Computer installiert.

* Eine Liste bekannter Probleme und Problemumgehungen finden Sie in den [Versionshinweisen für SQL Server Management Studio](../ssms/sql-server-management-studio-release-notes.md).

## <a name="available-languages"></a>Verfügbare Sprachen

> [!NOTE]
> In andere Sprachen als Englisch lokalisierte Versionen von SSMS benötigen das [KB 2862966-Sicherheitsupdate-Paket](https://support.microsoft.com/en-us/kb/2862966) für die Installation unter: Windows 8, Windows 7, Windows Server 2012 und Windows Server 2008 R2.

Diese Version von SSMS kann in folgenden Sprachen installiert werden:

SQL Server Management Studio 17.2:<br>
[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40a)

Upgradepaket von SQL Server Management Studio 17.2 (Upgrades 17.X bis 17.2):<br>
[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x40a)

## <a name="release-notes"></a>Versionsanmerkungen

Version 17.2 weist folgende Probleme und Einschränkungen auf:

- Bei Abfragefenstern, die die universelle Active Directory-Authentifizierung mit MFA-Unterstützung verwenden, kann ein Fehler ähnlich dem Folgenden auftreten, wenn versucht wird, eine Abfrage durchzuführen, nachdem das Fenster für eine Stunde oder länger geöffnet war:

   `Msg 0, Level 11, State 0, Line 0
The connection is broken and recovery is not possible. The client driver attempted to recover the connection one or more times and all attempts failed. Increase the value of *ConnectRetryCount* to increase the number of recovery attempts.`

   Ein erneutes Ausführen der Abfrage sollte den Fehler überwinden und erfolgreich sein.

- Die folgenden SSMS-Funktionalitäten werden in Azure AD nicht unterstützt, wenn die universelle Authentifizierung mit MFA verwendet wird:
  - Der Designer **Neue Tabelle/Sicht** zeigt die Anmeldeaufforderung im alten Format an, außerdem funktioniert die Azure AD-Authentifizierung nicht.
  - Das Feature **Die ersten 200 Zeilen bearbeiten** unterstützt die Azure AD-Authentifizierung nicht.
  - Die Komponente **Registrierter Server** unterstützt die Azure AD-Authentifizierung nicht.
  - Der **Datenbankoptimierungsratgeber** wird für die Azure AD-Authentifizierung nicht unterstützt. Es liegt ein bekanntes Problem vor, bei dem der Benutzer eine wenig hilfreiche Fehlermeldung angezeigt bekommt: *Datei oder Assembly ‚Microsoft.IdentityModel.Clients.ActiveDirectory,…‘ konnte nicht geladen werden* Entgegen der Erwartung *wird die Microsoft Azure SQL-Datenbank nicht vom Datenbankoptimierungsratgeber unterstützt. (DTAClient)*.

**AS**

- Der Objekt-Explorer in SSAS zeigt den Benutzernamen der Windows-Authentifizierung nicht in den AS Azure-Verbindungseigenschaften an.
Weitere Informationen finden Sie im [SSMS-Änderungsprotokoll](sql-server-management-studio-changelog-ssms.md).

## <a name="previous-releases"></a>Vorgängerversionen

[Vorgängerversionen von SQL Server Management Studio](../ssms/sql-server-management-studio-changelog-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>Feedback

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL Client Tools-Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Ein Problem bei Microsoft Connect melden oder einen Vorschlag einbringen](https://connect.microsoft.com/SQLServer/Feedback)

## <a name="see-also"></a>Siehe auch

- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Dokumentation zu SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Weitere Updates und Service Packs](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [Herunterladen von SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

