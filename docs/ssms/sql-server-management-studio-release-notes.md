---
title: "Versionshinweise für SQL Server Management Studio | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/30/2017
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
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 51e336a22d0c1052c48b8e569330aef26f2af094
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-management-studio----release-notes"></a>Versionshinweise für SQL Server Management Studio
Herzlich willkommen! Dies ist das allgemein verfügbare Release von SQL Server Management Studio.  Diese Version von SQL Server Management Studio (SSMS) ist eine eigenständige Installation außerhalb der SQL Server-Version. Wir haben uns zum Ziel gesetzt, sie häufig zu aktualisieren und neue Funktionen, Korrekturen und Hilfestellungen für die neuesten Funktionen von SQL Server und der Azure SQL-Datenbank bereitzustellen.  
  
Informationen zum Installieren des aktuellen Release von SQL Server Management Studio finden Sie unter [Download SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  
  
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

## <a name="feedback"></a>Feedback  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL Client Tools-Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Ein Problem bei Microsoft Connect melden oder einen Vorschlag einbringen](https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Siehe auch  
[SQL Server Management Studio-Lernprogramm](../ssms/use-sql-server-management-studio.md)  
[Herunterladen von SQL Server Management Studio &amp;#40;SSMS&amp;#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[Vorgängerversionen von SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  

  

