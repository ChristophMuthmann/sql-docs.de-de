---
title: Herunterladen von SQL Server Management Studio (SSMS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 10/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
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
caps.latest.revision: "145"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0c9f20a8c5f251728ce8050e9c6fc2cab4b55a55
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="download-sql-server-management-studio-ssms"></a>Herunterladen von SQL Server Management Studio (SSMS)

SSMS ist eine integrierte Umgebung zum Verwalten jeder beliebigen SQL-Infrastruktur, von SQL Server bis hin zur SQL-Datenbank. SSMS stellt Tools zum Konfigurieren, Überwachen und Verwalten von Instanzen von SQL Server zur Verfügung. Verwenden Sie SSMS, um Abfragen und Skripts zu erstellen sowie die Datenebenenkomponenten bereitzustellen, zu überwachen und zu aktualisieren, die von Ihren Anwendungen verwendet werden.

Verwenden Sie SQL Server Management Studio (SSMS) zum Abfragen, Entwerfen und Verwalten Ihrer Datenbanken und Data Warehouses, unabhängig davon, ob sich diese auf Ihrem lokalen Computer oder in der Cloud befinden.

**SSMS ist kostenlos!**

SSMS 17.X ist die größte Generation von *SQL Server Management Studio* und stellt Unterstützung für SQL Server 2017 bereit.

**[![Download](../ssdt/media/download.png) Herunterladen von SQL Server Management Studio 17.3](https://go.microsoft.com/fwlink/?linkid=858904)**

**[![Download](../ssdt/media/download.png) Herunterladen des Upgradepakets von SQL Server Management Studio 17.3 (Upgrades 17.X bis 17.3)](https://go.microsoft.com/fwlink/?linkid=858906)**

Die Installation von SSMS 17.X upgradet oder ersetzt nicht die Versionen 16.X oder früher von SSMS. SSMS 17.x wird parallel zu früheren Versionen installiert, damit beide Versionen zur Verfügung stehen.
Wenn ein Computer parallele SSMS-Installationen enthält, sollten Sie sich vergewissern, dass Sie die richtige Version für Ihre speziellen Anforderungen starten. Die neueste Version heißt *Microsoft SQL Server Management Studio 17* und verfügt über ein neues Symbol: 
 
   ![SSMS 17.X](media/download-sql-server-management-studio-ssms/version-icons.png)


> [!NOTE]
> Das SQL Server PowerShell-Modul ist nun eine separate Installation über den PowerShell-Katalog.  Weitere Informationen finden Sie in den [Downloadanweisungen](download-sql-server-ps-module.md).

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

**Versionsinformationen**

Versionsnummer: 17.3

Buildnummer dieses Release: 14.0.17199.0

## <a name="new-in-this-release"></a>In dieser Version neu

SSMS 17.3 ist die neueste Version von SQL Server Management Studio. Die Generation 17.X von SSMS bietet Support für beinahe alle Featurebereiche unter SQL Server 2008 bis SQL Server 2017. Version 17.X unterstützt auch SQL Analysis Service-PaaS.

Version 17.3 enthält Folgendes:

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

SQL Server Management Studio 17.3:<br>
[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40a)

Upgradepaket für SQL Server Management Studio 17.3 (Upgrades 17.X bis 17.3):<br>
[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x40a)

## <a name="release-notes"></a>Versionsanmerkungen

Version 17.3 weist folgende Probleme und Einschränkungen auf:

**SSMS Allgemein**

- Die folgenden SSMS-Funktionen werden für die Azure AD-Authentifizierung nicht unterstützt, wenn die universelle Authentifizierung mit MFA verwendet wird:
   - Der Datenbankoptimierungsratgeber wird für die Azure AD-Authentifizierung nicht unterstützt. Es liegt ein bekanntes Problem vor, bei dem dem Benutzer die folgende kryptische Fehlermeldung angezeigt wird: „Could not load file or assembly 'Microsoft.IdentityModel.Clients.ActiveDirectory,…“ (Datei oder Assembly ‚Microsoft.IdentityModel.Clients.ActiveDirectory,…‘ konnte nicht geladen werden), obwohl man eigentlich folgende Fehlermeldung erwarten würde: „Database Engine Tuning Advisor does not support Microsoft Azure SQL Database. (DTAClient)“ (Die Microsoft Azure SQL-Datenbank wird vom Datenbankoptimierungsratgeber nicht unterstützt).
- Bei dem Versuch, eine Abfrage in DTA zu analysieren entsteht folgender Fehler: "Object must implement IConvertible. (mscorlib)“ (Objekt muss IConvertible implementieren).
- *Rückläufige Abfragen* fehlen in der Liste der Berichte im Abfragespeicher im Objekt-Explorer.
   - Problemumgehung: Klicken Sie mit der rechten Maustaste auf den Knoten **Abfragespeicher**, und wählen Sie **View Regressed Queries (Rückläufige Abfragen anzeigen)** aus.

**Integration Services (IS)**

- Der [Ausführungspfad] in [Katalog].[Ereignismeldungen] ist für Paketausführungen in Scale Out falsch. Der [Ausführungspfad] beginnt mit „\Package“ anstelle des Objektnamens des ausführbaren Pakets. Beim Anzeigen der Übersichtsberichte von Paketausführungen in SSMA kann der Link zum „Ausführungspfad“ in der Übersicht über die Ausführung nicht funktionieren. Klicken Sie im Übersichtsbericht auf „Nachrichten anzeigen“, um alle Ereignismeldungen zu prüfen.



## <a name="previous-releases"></a>Vorgängerversionen

[Vorgängerversionen von SQL Server Management Studio](../ssms/sql-server-management-studio-changelog-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>Feedback

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL Client Tools-Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Ein Problem bei Microsoft Connect melden oder einen Vorschlag einbringen](https://connect.microsoft.com/SQLServer/Feedback)

## <a name="see-also"></a>Siehe auch

- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Dokumentation zu SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Weitere Updates und Service Packs](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [Herunterladen von SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
