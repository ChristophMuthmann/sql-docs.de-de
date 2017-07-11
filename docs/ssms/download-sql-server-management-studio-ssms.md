---
title: Herunterladen von SQL Server Management Studio (SSMS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/27/2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 60bdb820d74be98dd051d4729463d375d2a5202a
ms.contentlocale: de-de
ms.lasthandoff: 07/03/2017

---
<a id="download-sql-server-management-studio-ssms" class="xliff"></a>

# Herunterladen von SQL Server Management Studio (SSMS)
SQL Server Management Studio (SSMS) ist eine integrierte Umgebung zum Verwalten jeder beliebigen SQL-Infrastruktur, von SQL Server bis hin zur SQL-Datenbank. SSMS stellt Tools zum Konfigurieren, Überwachen und Verwalten von Instanzen von SQL Server zur Verfügung, wo auch immer Sie SQL Server bereitstellen. Mit SSMS können Sie Abfragen und Skripts erstellen sowie die Datenebenenkomponenten bereitstellen, überwachen und aktualisieren, die von Ihren Anwendungen verwendet werden. 

Dieses Release bietet verbesserte Kompatibilität mit früheren Releases von SQL Server, ein eigenständiges Webinstallationsprogramm und Popupbenachrichtigungen innerhalb von SSMS, wenn neue Releases verfügbar sind.  
  
Der ![Download](../ssdt/media/download.png) von SSMS ist kostenlos! **[Herunterladen von SQL Server Management Studio 17.1](https://go.microsoft.com/fwlink/?linkid=849819)** SSMS 17.X ist die größte Generation von SQL Server Management Studio und stellt Unterstützung für SQL Server 2017 bereit. 

![Download](../ssdt/media/download.png) **[Herunterladen des Upgradepakets von SQL Server Management Studio 17.1 (Upgrades 17.0 bis 17.1)](https://go.microsoft.com/fwlink/?linkid=849821)**

> [!NOTE]
> Das SQL Server PowerShell-Modul ist nun eine separate Installation über den PowerShell-Katalog.  Weitere Informationen finden Sie in den [Downloadanweisungen](download-sql-server-ps-module.md).

<a id="sql-server-management-studio" class="xliff"></a>

## SQL Server Management Studio   
**Versionsinformationen**  
  
Versionsnummer: 17.1  
Buildnummer dieser Version: 14.0.17119.0

<a id="new-in-this-release" class="xliff"></a>

## In dieser Version neu  

SSMS 17.1 ist das erste Update zur Generation 17.X von SQL Server Management Studio.  Die 17.X-Generation bietet Support für beinahe alle Features unter SQL Server 2008 über SQL Server 2017.  Die Version 17.X ist ebenso die Generierung von SSMS, die SQL Analysis Service-PaaS unterstützt.

Version 17.1 enthält Folgendes:

* Problembehebungen für einige von Benutzern gemeldete Probleme 
* Ein neues Integration Services-Verwaltungstool zum horizontalen Hochskalieren

Eine vollständige Auflistung der Änderungen finden Sie unter   
                [SQL Server Management Studio – Änderungsprotokoll (SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md)  
   
Informationen zur Sammlung von Benutzerdaten finden Sie unter   
                [SQL Server-Datenschutzerklärung](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx) 
  
<a id="supported-sql-offerings" class="xliff"></a>

## Unterstützte SQL-Angebote
  
* Diese Version von SSMS funktioniert mit allen [unterstützten Versionen von SQL Server 2008 – SQL Server 2017](https://support.microsoft.com/en-us/lifecycle?C2=1044) und bietet das höchste verfügbare Maß an Unterstützung für die Arbeit mit den neuesten Cloudfeatures in Azure SQL-Datenbank und Azure SQL Data Warehouse.  
* Es besteht keine explizite Sperre für SQL Server 2000 oder SQL Server 2005, jedoch funktionieren einige Features möglicherweise nicht ordnungsgemäß.  
* Zusätzlich kann SSMS 17.X zusammen mit SSMS 16.X oder SQL Server 2014 SSMS und früher installiert werden. 
  
<a id="supported-operating-systems" class="xliff"></a>

## Unterstützte Betriebssysteme
  
Diese Version von SSMS unterstützt die folgenden Plattformen, wenn sie mit dem aktuellen Servicepack ausgestattet sind:   
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7 (SP1)
- Windows Server 2016
- Windows Server 2012 (64-Bit) 
- Windows Server 2012 R2 (64-Bit) 
- Windows Server 2008 R2 (64-Bit)  

>[!NOTE]
>SSMS 17.X basiert auf der isolierten Visual Studio 2015-Shell, die vor Windows Server 2016 veröffentlicht wurde. Microsoft nimmt die App-Kompatibilität ernst und stellt sicher, dass bereits versendete Anwendungen weiterhin unter den neuesten Windows-Versionen ausgeführt werden. Um Probleme bei der Ausführung von SSMS unter Windows Server 2016 zu minimieren, stellen Sie sicher, dass SSMS über die neuesten Updates verfügt. Wenn Sie auf Probleme mit SSMS unter Windows Server 2016 stoßen, kontaktieren Sie den Support. Der Support bestimmt, ob das Problem bei SSMS, Visual Studio oder bei der Windows-Kompatibilität liegt. Das Problem wir dann an das entsprechende Team weitergeleitet.

<a id="ssms-installation-tips-and-issues" class="xliff"></a>

## Tipps und Probleme bei der Installation von SSMS
**Minimieren von Installationsneustarts**

- Führen Sie die folgenden Aktionen durch, um zu verhindern, dass das SSMS-Setup einen Neustart am Ende der Installation benötigt.
  - Stellen Sie sicher, dass Sie eine aktuelle Version von Microsoft Visual C++ 2013 Redistributable Package ausführen. Die Version 12.00.40649.5 (oder höher) ist erforderlich. Es wird nur die x64-Version benötigt.
  - Überprüfen Sie, ob die .NET Framework-Version auf dem Computer 4.6.1 (oder höher) ist.
  - Schließen Sie alle anderen Instanzen von Visual Studio, die auf dem Computer geöffnet sind.
  - Stellen Sie sicher, dass die neuesten Betriebssystemupdates auf dem Computer installiert sind.
  - Die registrierten Aktionen werden normalerweise nur einmal benötigt. Es gibt einige Fälle, in denen ein Neustart während zusätzlichen Upgrades auf dieselbe Hauptversion von SSMS notwendig sind. Für nebensächliche Upgrades sind alle Voraussetzungen für SSMS bereits auf dem Computer installiert.

- Eine Liste bekannter Probleme und Problemumgehungen finden Sie in den [Versionshinweisen für SQL Server Management Studio](../ssms/sql-server-management-studio-release-notes.md).

<a id="available-languages" class="xliff"></a>

## Verfügbare Sprachen  
> In andere Sprachen als Englisch lokalisierte Versionen von SSMS benötigen das [KB 2862966-Sicherheitsupdate-Paket](https://support.microsoft.com/en-us/kb/2862966) für die Installation unter: Windows 8, Windows 7, Windows Server 2012 und Windows Server 2008 R2. 
  
Diese Version von SSMS kann in folgenden Sprachen installiert werden:

SQL Server Management Studio 17.1:<br>
[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x404) | [Englisch (USA)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40a)

Upgradepaket von SQL Server Management Studio 17.1 (Upgrades 17.0 bis 17.1):<br>
[Chinesisch (Volksrepublik China)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x804) | [Chinesisch (Taiwan)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x404) | [Englisch (Vereinigte Staaten)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x409) | [Französisch](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x40c) | [Deutsch](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x407) | [Italienisch](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x410) | [Japanisch](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x411) | [Koreanisch](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x412) | [Portugiesisch (Brasilien)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x416) | [Russisch](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x419) | [Spanisch](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x40a)

<a id="previous-releases" class="xliff"></a>

## Vorgängerversionen  
[Vorgängerversionen von SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  
  
<a id="feedback" class="xliff"></a>

## Feedback  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL Client Tools-Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Ein Problem bei Microsoft Connect melden oder einen Vorschlag einbringen](https://connect.microsoft.com/SQLServer/Feedback)  
  
<a id="see-also" class="xliff"></a>

## Siehe auch  
[Tutorial: SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[Dokumentation zu SQL Server Management Studio](https://msdn.microsoft.com/library/hh213248(v=sql.130).aspx)  
[Microsoft SQL Server](https://msdn.microsoft.com/library/bb545450.aspx)  
[Weitere Updates und Service Packs](https://technet.microsoft.com/sqlserver/ff803383.aspx)  
[Herunterladen von SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  



