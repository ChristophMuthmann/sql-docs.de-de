---
title: "Versionshinweise für SQL Server Management Studio | Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b95337b-80bf-4624-8f5d-cdaf6181d3b8
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: fe6de2b16b9792a5399b1c014af72a2a5ee52377
ms.openlocfilehash: f593303a681e2f52161777fc48f0fb1b479d20d9
ms.contentlocale: de-de
ms.lasthandoff: 06/23/2017

---
# <a name="sql-server-management-studio----release-notes"></a>Versionshinweise für SQL Server Management Studio
Herzlich willkommen! Dies ist das allgemein verfügbare Release von SQL Server Management Studio.  Diese Version von SQL Server Management Studio (SSMS) ist eine eigenständige Installation außerhalb der SQL Server-Version. Wir haben uns zum Ziel gesetzt, sie häufig zu aktualisieren und neue Funktionen, Korrekturen und Hilfestellungen für die neuesten Funktionen von SQL Server und der Azure SQL-Datenbank bereitzustellen.  
  
Informationen zum Installieren des aktuellen Release von SQL Server Management Studio finden Sie unter [Download SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  
  
Dies sind Probleme und Einschränkungen, die in Verbindung mit diesem SQL Server Management Studio-Release bestehen:  

1. **Restore-Assistent generiert eine falsche Pfadmuster für Datenbank-Dateispeicherort Ziel** 
    Dies ist ein bekanntes Problem, wenn SSMS auf einem Linux-Server verbunden ist. Auch wenn der Pfad falsch/ungerade aussieht, ordnungsgemäß auf dem Server verarbeitet wird, d. h. Es gibt keine funktionale Problem.

2. **Datei-Browser-Probleme**
    - Bei der Arbeit mit einem Windows-basierte SQL Server 2017 CTP 2.0-Instanz möglicherweise die Dateibrowser Benutzeroberfläche in SSMS zu öffnen, wenn der Server eine leere Diskettenlaufwerk oder einen Datenträger mit fester Größe geschützt durch Bitlocker installiert hat. 
    - Versionen von SQL Server-2017 vor CTP 2.0 wird von der Dateibrowser UI nicht mehr unterstützt.
    


3. **Bei Verwendung der universellen Active Directory-Authentifizierung kann sich nur ein einziges Azure Active Directory-Konto für eine SSMS-Instanz anmelden.**  
    Diese Einschränkung gilt lediglich für die universelle Active Directory-Authentifizierung. Bei Verwendung der Active Directory-Kennwortauthentifizierung, der integrierten Active Directory-Authentifizierung oder der SQL Server-Authentifizierung können Sie sich bei unterschiedlichen Servern anmelden.
    
    Um dieses Problem zu umgehen, können Sie eine andere SSMS-Instanz verwenden, um sich als ein anderes Azure Active Directory-Konto anzumelden. 
    
4. **DacFx-Befehle (Data-Tier Application Framework) und der Schema-Designer in SSMS bieten keine Unterstützung für die universelle Active Directory-Authentifizierung.**  
    Befehle, die DacFx verwenden (z.B. Import- und Exportbefehle) und der Schema-Designer in SSMS bieten aktuell keine Unterstützung für die universelle Active Directory-Authentifizierung.
    
    Um das Problem zu umgehen, können Sie die anderen Authentifizierungsmethoden verwenden, die in SSMS verfügbar sind: Active Directory-Kennwortauthentifizierung, integrierte Active Directory-Authentifizierung und SQL Server-Authentifizierung.

5. **SSMS kann sich ausschließlich mit SSIS 2016-Instanzen (SQL Server 2016 Integration Services) verbinden.**  
    Es gibt eine bekannte Kompatibilitätseinschränkung bei SQL Server Integration Services, die Verbindungen mit vorherigen Versionen verhindert.
    
    Als Problemumgehung verbinden Sie sich über [das SSMS-Release, das auf Ihre SSIS-Instanz ausgerichtet ist](../ssms/previous-sql-server-management-studio-releases.md), mit Ihrer SQL Server Integration Services-Instanz. 
  
5. **SSMS speichert keine Wartungspläne für SQL Server 2008 R2 und frühere SQL Server-Versionen.**  
    Dies ist eine bekannte Einschränkung, und wir arbeiten daran, diese in einem zukünftigen Release zu beheben. In der Zwischenzeit können Sie das [SSMS 2014-Release](../ssms/previous-sql-server-management-studio-releases.md) unten verwenden, um Wartungspläne zu speichern.  
    
5. **Für SSMS-Installationen in anderen Sprachen als Englisch ist möglicherweise die Installation eines zusätzlichen Sicherheitspakets erforderlich.**  
Lokalisierte Versionen von SSMS (andere Sprachen als Englisch) [benötigen das KB 2862966-Sicherheitsupdatepaket](https://support.microsoft.com/en-us/kb/2862966) für die Installation unter Windows 8, Windows 7, Windows Server 2012 und Windows Server 2008 R2.

5. **Die Hilfe wird durch Klicken auf „Hilfe“ oder Drücken auf die F1-Taste nicht geöffnet**  
Einige Umgebungen zeigen Folgendes an, wenn Sie auf „Hilfe“ klicken oder die F1-Taste drücken: **You'll need a new app to open ms-xhelp** (Zum Öffnen von ms-xhelp benötigen Sie eine neue App). Dieser Fehler ist ein bekanntes Problem und wird in einer zukünftigen Version behoben.
  
## <a name="feedback"></a>Feedback  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL Client Tools-Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Ein Problem bei Microsoft Connect melden oder einen Vorschlag einbringen](https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Siehe auch  
[SQL Server Management Studio-Lernprogramm](../ssms/use-sql-server-management-studio.md)  
[Herunterladen von SQL Server Management Studio &amp;#40;SSMS&amp;#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[Vorgängerversionen von SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  

  

