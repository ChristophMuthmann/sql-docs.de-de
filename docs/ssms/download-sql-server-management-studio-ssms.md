---
title: Herunterladen von SQL Server Management Studio (SSMS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/03/2017
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
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cc827737cec19c11d2102f968dc2b8bc638bda86
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>Herunterladen von SQL Server Management Studio (SSMS)
SQL Server Management Studio (SSMS) ist eine integrierte Umgebung für den Zugriff, die Konfiguration, die Verwaltung und die Entwicklung aller SQL Server-Komponenten. SSMS kombiniert eine Vielzahl grafischer Tools mit einer Reihe umfassender Skript-Editoren, um Entwicklern und Administratoren mit verschiedenem Kenntnisstand den Zugriff auf SQL Server zu ermöglichen. Dieses Release bietet verbesserte Kompatibilität mit früheren Releases von SQL Server, ein eigenständiges Webinstallationsprogramm und Popupbenachrichtigungen innerhalb von SSMS, wenn neue Releases verfügbar sind.  

    
| ![Download verfügbar ist](../ssdt/media/download.png) Herunterladen von SQL Server Management Studio (SSMS)  |  |
|:---|:---|
|**[Hier können Sie SQL Server Management Studio (16.5.3) herunterladen](https://go.microsoft.com/fwlink/?LinkID=840946)**|Aktuelle Version für den Einsatz in der Produktion.|
|**[SQL Server Management Studio herunterladen – Release Candidate (17.0 RC3)](../ssms/sql-server-management-studio-ssms-release-candidate.md)**|Bietet Unterstützung für SQL Server vNext CTP1.3 und kann parallel zu Version 16.x ausgeführt werden, wird aber für den Einsatz in der Produktion nicht empfohlen.| 


> [!NOTE]
> Der Name der SSMS-Releases umfasst nicht länger eine Monatsangabe, sondern eine Nummer. SSMS ist kostenlos! Eine Lizenz für die Installation und Verwendung ist nicht erforderlich.  


## <a name="sql-server-management-studio"></a>SQL Server Management Studio   
**Versionsinformationen**  
  
Versionsnummer: 16.5.3  
Buildnummer dieser Version: 13.0.16106.4
  
**Unterstützte SQL Server-Versionen**  
  
* Diese Version von SSMS funktioniert mit allen [unterstützten Versionen von SQL Server (SQL Server 2008 – SQL Server 2016)](https://support.microsoft.com/en-us/lifecycle?C2=1044) , und bietet das höchste verfügbare Maß an Unterstützung für die Arbeit mit den neuesten Cloudfeatures in Azure SQL-Datenbank und Azure SQL Data Warehouse.  
* Es besteht keine explizite Sperre für SQL Server 2000 oder SQL Server 2005, jedoch funktionieren einige Features möglicherweise nicht ordnungsgemäß.  
* Darüber hinaus kann eine SSMS 16.x-Version oder SSMS 2016 parallel zu früheren Versionen von SSMS 2014 und früher installiert werden. 
  
**Unterstützte Betriebssysteme**  
  
Diese Version von SSMS unterstützt die folgenden Plattformen, wenn sie mit dem aktuellen Servicepack ausgestattet sind:   
 Windows 10, Windows 8, Windows 8.1, Windows 7 (SP1), Windows Server 2012 (64-Bit), Windows Server 2012 R2 (64-Bit), Windows Server 2008 R2 (64-Bit)  
   
 **Verfügbare Sprachen**  
> [!NOTE]  
> In andere Sprachen als Englisch lokalisierte Versionen von SSMS benötigen das [KB 2862966-Sicherheitsupdate-Paket](https://support.microsoft.com/en-us/kb/2862966) für die Installation unter: Windows 8, Windows 7, Windows Server 2012 und Windows Server 2008 R2. 
  
 Diese Version von SSMS kann in folgenden Sprachen installiert werden:  
[Chinesisch (Volksrepublik China)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804) | [Chinesisch (Taiwan)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404) | [Englisch (Vereinigte Staaten)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409) | [Französisch](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c)  
[Deutsch](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407) | [Italienisch](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410) | [Japanisch](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411) | [Koreanisch](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412) | [Portugiesisch (Brasilien)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416) | [Russisch](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419) | [Spanisch](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)  

 
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





Eine vollständige Auflistung der einzelnen Funktionen finden Sie unter   
                [SQL Server Management Studio – Änderungsprotokoll (SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md)  
  
Eine Liste der bekannten Probleme und Problemumgehungen finden Sie unter   
                [SQL Server Management Studio – Anmerkungen zu dieser Version](../ssms/sql-server-management-studio-release-notes.md)  
  
Informationen zur Sammlung von Benutzerdaten finden Sie unter   
                [SQL Server-Datenschutzerklärung](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx).  
  
## <a name="previous-releases"></a>Vorgängerversionen  
[Vorgängerversionen von SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  
  
## <a name="feedback"></a>Feedback  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL Client Tools-Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Ein Problem bei Microsoft Connect melden oder einen Vorschlag einbringen](https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Siehe auch  
[Tutorial: SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[Dokumentation zu SQL Server Management Studio](https://msdn.microsoft.com/library/hh213248(v=sql.130).aspx)  
[Microsoft SQL Server](https://msdn.microsoft.com/library/bb545450.aspx)  
[Weitere Updates und Service Packs](https://technet.microsoft.com/sqlserver/ff803383.aspx)  
[Herunterladen von SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  



