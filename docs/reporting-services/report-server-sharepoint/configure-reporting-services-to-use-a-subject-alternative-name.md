---
title: Konfigurieren von Reporting Services zum Verwenden eines alternativen Antragstellernamens | Microsoft Docs
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 73f48b2978055481f1ee93952fb3a35eb84ec416
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name"></a>Konfigurieren von Reporting Services zum Verwenden eines alternativen Antragstellernamens

In diesem Thema wird erläutert, wie so konfigurieren Sie Reporting Services (SSRS) durch die Verwendung ein alternativen Antragstellernamen (SAN) die Datei "rsreportserver.config" ändern und verwenden das Netsh.exe-Tool wird.

Die Anweisungen gelten sowohl für die Berichtsdienst-URL als auch die Webdienst-URL.

Zum Verwenden eines SAN muss das SSL-Zertifikat auf dem Server registriert und signiert sein und über den privaten Schlüssel verfügen. Sie können kein selbstsigniertes Zertifikat verwenden.  
  
 URLs in Reporting Services können zur Verwendung eines SSL-Zertifikats konfiguriert werden. Ein Zertifikat verfügt normalerweise nur über einen Antragstellernamen, der nur eine URL für eine SSL-Sitzung (Secure Sockets Layer) zulässt. Der SAN ist ein zusätzliches Feld im Zertifikat, das einen SSL-Dienst für viele URLs überwachen und zur Freigabe des SSL-Ports mit anderen Anwendungen ermöglicht. Der SAN sieht wie `www.s2.com`.  
  
 Weitere Informationen zu SSL-Einstellungen für Reporting Services finden Sie unter [Konfigurieren von SSL-Verbindungen auf einem Berichtsserver im einheitlichen Modus](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md).  
  
## <a name="configure-ssrs-to-use-a-subject-alternative-name-for-web-service-url"></a>Konfigurieren von SSRS für die Verwendung ein alternativen Antragstellernamens für Webdienst-URL verwenden.
  
1.  Starten Sie den Konfigurations-Manager für Reporting Services.  
  
     Weitere Informationen finden Sie unter [Reporting Services-Konfigurations-Manager &#40;einheitlicher Modus&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2.  Wählen Sie auf der Seite **Webdienst-URL** einen SSL-Port und ein SSL-Zertifikat aus.  
  
     ![Reporting Services-Konfigurations-Manager](../../reporting-services/report-server-sharepoint/media/reportingservices-configurationmanager.png "Reporting Services-Konfigurations-Manager")  
  
     Der Konfigurations-Manager registriert das SSL-Zertifikat für den Port.  
  
3.  Öffnen Sie die Datei rsreportserver.config.  
  
     Für den einheitlichen SSRS-Modus befindet sich die Datei standardmäßig im folgenden Ordner:  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
4.  Kopieren Sie den URL-Abschnitt für die Berichtsserver-Webdienstanwendung.  
  
     Beispielsweise ist die ursprüngliche URL nachfolgend ein:  
  
    ```  
        <URL>  
         <UrlString>https://localhost:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
     Die folgenden modifizierte URL-Abschnitt ist:
  
    ```  
    <URL>  
         <UrlString>https://www.s1.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
        <URL>  
         <UrlString>https://www.s2.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
5.  Speichern Sie die Datei rsreportserver.config.  
  
6.  Starten Sie eine Eingabeaufforderung als Administrator, und führen Sie das Tool Netsh.exe aus.  
  
    ```  
    C:\windows\system32\netsh  
    ```  
  
7.  Wechseln Sie zum HTTP-Kontext, indem Sie Folgendes eingeben.  
  
    ```  
    Netsh>http  
    ```  
  
8.  Zeigen Sie die vorhandenen URL-ACLs an, indem Sie Folgendes eingeben:
  
    ```  
    Netsh http>show urlacl  
    ```  
  
     Ein Eintrag wie der folgenden wird angezeigt.  
  
    ```  
    Reserved URL            : https:// www.s1.com:443/ReportServer/  
        User: NT SERVICE\ReportServer  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;S-1-5-80-1234567890-123456789-123456789-123456789-1234567890)  
    ```  
  
     Eine URL-ACL ist eine besitzverwaltete Zugriffssteuerungsliste (Discretionary Access Control List, DACL) für eine reservierte URL.  
  
9. Erstellen Sie einen neuen Eintrag für den alternativen Antragstellernamen mit demselben Benutzer und derselben SDDL wie beim vorhandenen Eintrag, indem Sie Folgendes eingeben.  
  
    ```  
    netsh http>add urlacl  url=https://www.s2.com:443/ReportServer    
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-1234567980-12346579-123456789-123456789-1234567890)  
  
    ```  
  
10. Klicken Sie im Konfigurations-Manager für Reporting Services auf der Seite **Berichtsserverstatus** auf **Beenden** , und klicken Sie dann auf **Starten** , um den Berichtsserver neu zu starten.  
  
## <a name="see-also"></a>Siehe auch

 [Konfigurationsdatei "rsreportserver.config"](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Konfigurations-Manager für Reporting Services](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Ändern einer Reporting Services-Konfigurationsdatei](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Konfigurieren von Berichtsserver-URLs](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)

