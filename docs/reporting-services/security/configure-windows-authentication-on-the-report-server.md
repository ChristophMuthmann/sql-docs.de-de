---
title: Windows-Authentifizierung auf dem Berichtsserver konfigurieren | Microsoft Docs
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Windows authentication [Reporting Services]
- Reporting Services, configuration
ms.assetid: 4de9c3dd-0ee7-49b3-88bb-209465ca9d86
caps.latest.revision: 25
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b59cdb7f5087ed7cb02300758f593ea952be3778
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="configure-windows-authentication-on-the-report-server"></a>Konfigurieren der Windows-Authentifizierung auf dem Berichtsserver
  In der Standardeinstellung werden [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Anforderungen übergeben, die die Negotiate- oder die NTLM-Authentifizierung angeben. Wenn eine Bereitstellung Clientanwendungen und Browser umfasst, die diese Sicherheitsanbieter nutzen, können Sie die Standardwerte ohne zusätzliche Konfiguration verwenden. Wenn Sie einen anderen Sicherheitsanbieter für die integrierte Sicherheit von Windows nutzen möchten (wenn Sie beispielsweise Kerberos direkt verwenden möchten) oder wenn Sie die Standardwerte verändert haben und die ursprünglichen Einstellungen wiederherstellen möchten, können Sie mithilfe der in diesem Thema enthaltenen Informationen die Authentifizierungseinstellungen auf dem Berichtsserver festlegen.  
  
 Um die integrierte Sicherheit von Windows nutzen zu können, muss jeder Benutzer, der Zugriff auf einen Berichtsserver benötigt, über ein gültiges Windows-Benutzerkonto verfügen oder Mitglied eines lokalen Windows-Gruppenkontos oder eines Windows-Domänengruppenkontos sein. Sie können Konten aus anderen Domänen angeben, sofern diese Domänen vertrauenswürdig sind. Die Konten benötigen Zugriff auf den Berichtsservercomputer und müssen anschließend Rollen zugewiesen werden, um auf bestimmte Berichtsservervorgänge zugreifen zu können.  
  
 Überdies müssen die folgenden zusätzlichen Anforderungen erfüllt werden:  
  
-   In den RSeportServer.config-Dateien muss **AuthenticationType** auf **RSWindowsNegotiate**, **RSWindowsKerberos**oder **RSWindowsNTLM**festgelegt werden. Standardmäßig enthält die Datei RSReportServer.config die **RSWindowsNegotiate** -Einstellung, wenn das Berichtsserver-Dienstkonto entweder NetworkService oder LocalSystem ist. Andernfalls wird die **RSWindowsNTLM** -Einstellung verwendet. Sie können **RSWindowsKerberos** hinzufügen, wenn Anwendungen vorhanden sind, die nur die Kerberos-Authentifizierung verwenden.  
  
    > [!IMPORTANT]  
    >  Die Verwendung von **RSWindowsNegotiate** hat einen Kerberos-Authentifizierungsfehler zur Folge, wenn der Berichtsserverdienst so konfiguriert wurde, dass er unter einem Domänenbenutzerkonto ausgeführt wird und für das Konto kein Dienstprinzipalname (Service Principal Name, SPN) registriert wurde. Weitere Informationen finden Sie unter [Beheben von Kerberos-Authentifizierungsfehlern beim Herstellen einer Verbindung mit einem Berichtsserver](#proxyfirewallRSWindowsNegotiate) in diesem Thema.  
  
-   [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] muss für die Windows-Authentifizierung konfiguriert werden. Standardmäßig enthalten die Dateien "Web.config" für die Berichtsserver-Webdienst die \<Authentifizierungsmodus = "Windows" > festlegen. Wenn Sie es ändern \<Authentifizierungsmodus = "Forms" >, die Windows-Authentifizierung für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] schlägt fehl.  
  
-   Die Web.config-Dateien muss der Berichtsserver-Webdienst über \<Identität = "true" / >.  
  
-   Die Clientanwendung bzw. der Browser muss die integrierte Sicherheit von Windows unterstützen.  

- Das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] benötigt keine weitere Konfiguration.
  
 Bearbeiten Sie die XML-Elemente und die Werte in der Datei RSReportServer.config, um die Berichtsserver-Authentifizierungseinstellungen zu ändern. Sie können die Beispiele in diesem Thema kopieren und einfügen, um bestimmte Kombinationen zu implementieren.  
  
 Die Standardeinstellungen eignen sich am besten, wenn sich die Client- und Servercomputer in derselben Domäne oder in einer vertrauenswürdigen Domäne befinden und der Berichtsserver für den Intranetzugriff hinter einer Unternehmensfirewall bereitgestellt wird. Vertrauenswürdige Domänen und Einzeldomänen sind eine Voraussetzung für die Weitergabe von Windows-Anmeldeinformationen. Die Anmeldeinformationen können nur dann mehrfach übergeben werden, wenn Sie das Kerberos-Protokoll, Version 5, für die Server aktivieren. Andernfalls können die Anmeldeinformationen nur einmal übergeben werden, bevor sie ablaufen. Weitere Informationen zum Konfigurieren von Anmeldeinformationen für mehrere Computerverbindungen finden Sie unter [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
 Die folgenden Anweisungen beziehen sich auf Berichtsserver, die im einheitlichen Modus ausgeführt werden. Wenn der Berichtserver im integrierten SharePoint-Modus bereitgestellt wird, müssen die Standardauthentifizierungseinstellungen verwendet werden, welche die integrierte Sicherheit von Windows angeben. Der Berichtsserver verwendet interne Funktionen der standardmäßigen Windows-Authentifizierungserweiterung, um Berichtserver im integrierten SharePoint-Modus zu unterstützen.  
  
## <a name="extended-protection-for-authentication"></a>Erweiterter Schutz für die Authentifizierung  
 Der erweiterte Schutz für die Authentifizierung wird ab [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]unterstützt. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Funktion unterstützt die Verwendung der Kanalbindung und Dienstbindung, um den Authentifizierungsschutz zu verbessern. Die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionen müssen mit einem Betriebssystem verwendet werden, das erweiterten Schutz unterstützt. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfiguration für erweiterten Schutz wird durch Einstellungen in der Datei RSReportServer.config bestimmt. Die Datei kann entweder durch Bearbeitung oder Verwendung der WMI-APIs aktualisiert werden. Weitere Informationen finden Sie unter [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md).  
  
### <a name="to-configure-a-report-server-to-use-windows-integrated-security"></a>So konfigurieren Sie einen Berichtsserver für die Verwendung der integrierten Sicherheit von Windows  
  
1.  Öffnen Sie RSReportServer.config in einem Text-Editor.  
  
2.  Suchen \< **Authentifizierung**>.  
  
3.  Kopieren Sie die XML-Struktur, die Ihren Anforderungen am besten entspricht. Sie können **RSWindowsNegotiate**, **RSWindowsNTLM**und **RSWindowsKerberos** in beliebiger Reihenfolge angeben. Sie sollten die Authentifizierungspersistenz aktivieren, wenn die Verbindung und nicht jede einzelne Anforderung authentifiziert werden soll. Bei Verwendung der Authentifizierungspersistenz werden alle Anforderungen, für die eine Authentifizierung erforderlich ist, zugelassen, solange die Verbindung besteht.  
  
     Die erste XML-Struktur ist die Standardkonfiguration, wenn das Berichtsserver-Dienstkonto entweder NetworkService oder LocalSystem ist:  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsNegotiate />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
     Die zweite XML-Struktur ist die Standardkonfiguration, wenn das Berichtsserver-Dienstkonto weder NetworkService noch LocalSystem ist:  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    ```  
  
     \</ Authentifizierung >  
  
     Die dritte XML-Struktur gibt sämtliche Sicherheitspakete an, die in der integrierten Sicherheit von Windows verwendet werden:  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsNegotiate />  
                 <RSWindowsKerberos />  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
    ```  
  
     Mit der vierten XML-Struktur wird NTLM nur für Bereitstellungen, die Kerberos nicht unterstützen, bzw. zur Umgehung von Kerberos-Authentifizierungsfehlern angegeben:  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
    ```  
  
4.  Fügen Sie ihn über die vorhandenen Einträge für \< **Authentifizierung**>.  
  
     Beachten Sie, dass **Custom** nicht mit den **RSWindows** -Typen verwendet werden kann.  
  
5.  Ändern Sie die Einstellungen für erweiterten Schutz nach Bedarf. Erweiterter Schutz ist standardmäßig deaktiviert.  Wenn diese Einträge nicht vorhanden sind, wird auf dem aktuellen Computer möglicherweise keine Version von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ausgeführt, die erweiterten Schutz unterstützt. Weitere Informationen finden Sie unter [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md).  
  
    ```  
          <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>  
          <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>  
    ```  
  
6.  Speichern Sie die Datei.  
  
7.  Wenn Sie eine horizontal skalierte Bereitstellung konfiguriert haben, wiederholen Sie diese Schritte für andere in der Bereitstellung vorhandene Berichtsserver.  
  
8.  Starten Sie den Berichtsserver neu, um alle momentan geöffneten Sitzungen zu beenden.  
  
##  <a name="proxyfirewallRSWindowsNegotiate"></a> Resolving Kerberos Authentication Errors When Connecting to a Report Server  
 Bei einem Berichtsserver, der zum Aushandeln oder für die Kerberos-Authentifizierung konfiguriert wurde, kann keine Clientverbindung mit dem Berichtsserver hergestellt werden, wenn ein Kerberos-Authentifizierungsfehler vorliegt. Kerberos-Authentifizierungsfehler treten bekanntermaßen auf, wenn eine der folgende Bedingungen zutrifft:  
  
-   Der Berichtsserverdienst wird unter einem Domänenbenutzerkonto ausgeführt, für das kein Dienstprinzipalname (SPN) registriert wurde.  
  
-   Der Berichtsserver wird mit der Einstellung **RSWindowsNegotiate** konfiguriert.  
  
-   Der Browser gibt im Authentifizierungsheader der Anforderung, die er an den Berichtsserver sendet, Kerberos statt NTLM an.  
  
 Sie können den Fehler erkennen, wenn Sie die Kerberos-Protokollierung aktiviert haben. Ein anderes Fehlersymptom ist, dass Sie mehrfach zur Eingabe von Anmeldeinformationen aufgefordert werden und dann ein leeres Browserfenster angezeigt wird.  
  
 Sie können sich davon überzeugen, dass ein Kerberos-Authentifizierungsfehler vorliegt, indem Sie den Eintrag < **RSWindowsNegotiate** /> aus der Konfigurationsdatei löschen und erneut versuchen, eine Verbindung herzustellen.  
  
 Nachdem Sie das Problem eindeutig identifiziert haben, können Sie es auf die folgenden Weisen beheben:  
  
-   Registrieren Sie unter dem Domänenbenutzerkonto einen SPN für den Berichtsserverdienst. Weitere Informationen finden Sie unter [Register a Service Principal Name &#40;SPN&#41; for a Report Server](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md) (Registrieren eines Dienstprinzipalnamens [SPN] für einen Berichtsserver).  
  
-   Ändern Sie das Dienstkonto so, dass es unter einem integrierten Konto ausgeführt wird, z. B. als Netzwerkdienst. Integrierte Konten ordnen den HTTP-SPN dem Host-SPN zu, der definiert wird, wenn Sie einen Computer in ein Netzwerk aufnehmen. Weitere Informationen finden Sie unter [Konfigurieren des Berichtsserver-Dienstkontos &#40;SSRS-Konfigurations-Manager&#41;](http://msdn.microsoft.com/library/25000ad5-3f80-4210-8331-d4754dc217e0).  
  
-   Verwenden Sie NTLM. NTLM funktioniert im Allgemeinen in Fällen, in denen die Kerberos-Authentifizierung fehlschlägt. Zur Verwendung von NTLM entfernen Sie den Eintrag **RSWindowsNegotiate** aus der Datei RSReportServer.config, und stellen Sie sicher, dass nur **RSWindowsNTLM** angegeben ist. Wenn Sie sich für diese Vorgehensweise entscheiden, können Sie auch dann weiterhin ein Domänenbenutzerkonto für den Berichtsserverdienst verwenden, wenn Sie keinen SPN dafür definiert haben.  
  
#### <a name="logging-information"></a>Protokollierungsinformationen  
 Es gibt mehrere Quellen von Protokollierungsinformationen, mit denen Probleme im Zusammenhang mit Kerberos gelöst werden können.  
  
##### <a name="user-account-control-attribute"></a>UserAccountControl-Attribut  
 Stellen Sie fest, ob für das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstkonto das erforderliche Attribut in Active Directory festgelegt wurde. Suchen Sie in der Ablaufverfolgungsprotokolldatei des Reporting Services-Diensts nach dem Wert, der für das UserAccountControl-Attribut protokolliert wurde. Der protokollierte Wert weist das Dezimalformat auf. Sie müssen den Dezimalwert in ein hexadezimales Format konvertieren. Anschließend suchen Sie diesen Wert im MSDN-Thema zum UserAccountControl-Attribut.  
  
-   Der Eintrag im Ablaufverfolgungsprotokoll des Reporting Services-Diensts sieht etwa wie folgt aus:  
  
    ```  
    appdomainmanager!DefaultDomain!8f8!01/14/2010-14:42:28:: i INFO: The UserAccountControl value for the service account is 590336  
    ```  
  
-   Eine Möglichkeit zum Konvertieren des Dezimalwerts in das hexadezimale Format besteht darin, den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Rechner zu verwenden. Der Windows-Rechner unterstützt mehrere Modi mit der Option Dez und Hex. Wählen Sie die Option Dez, geben Sie den in der Protokolldatei gefundenen Dezimalwert ein, bzw. fügen Sie ihn ein, und wählen Sie die Option Hex.  
  
-   Lesen Sie dann das Thema [User-Account-Control Attribute](http://go.microsoft.com/fwlink/?LinkId=183366) (UserAccountControl-Attribut), um das Attribut für das Dienstkonto abzuleiten.  
  
##### <a name="spns-configured-in-active-directory-for-the-reporting-services-service-account"></a>In Active Directory für das Reporting Services-Dienstkonto konfigurierte SPNs.  
 Um die SPNs in der Ablaufverfolgungsprotokolldatei des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Diensts zu protokollieren, können Sie die Funktion "Erweiterter Schutz" von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] vorübergehend aktivieren.  
  
-   Ändern Sie die Konfigurationsdatei **rsreportserver.config** , indem Sie folgende Einstellungen vornehmen:  
  
    ```  
    <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>   
    <RSWindowsExtendedProtectionScenario>Any</RSWindowsExtendedProtectionScenario>  
    ```  
  
-   Starten Sie den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst neu, und suchen Sie in der Ablaufverfolgungsprotokolldatei nach Einträgen wie:  
  
    ```  
    rshost!rshost!e44!01/14/2010-14:43:51:: i INFO: Registered valid SPNs list for endpoint 2: rshost!rshost!e44!01/14/2010-14:43:52:: i INFO: SPN Whitelist Added <Explicit> - \<HTTP/sqlpod064-13.w2k3.net>.  
    ```  
  
-   Die Werte unter \<Explicit > enthält die SPNs in Active Directory für konfiguriert die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstkonto.  
  
 Wenn Sie den erweiterten Schutz nicht weiterverwenden möchten, setzen Sie die Konfigurationswerte auf die Standardwerte zurück und starten das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstkonto neu.  
  
```  
<RSWindowsExtendedProtectionLevel>Off</RSWindowsExtendedProtectionLevel>  
<RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>  
```  
  
 Weitere Informationen finden Sie unter [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)  
  
#### <a name="how-the-browser-chooses-negotiated-kerberos-or-negotiated-ntlm"></a>Wie der Browser zwischen Aushandeln mit Kerberos und Aushandeln mit NTLM auswählt  
 Wenn Sie über Internet Explorer eine Verbindung mit dem Berichtsserver herstellen, gibt dieser im Authentifizierungsheader entweder ausgehandeltes Kerberos oder NTLM an. NTLM wird statt Kerberos verwendet, wenn eine der folgenden Bedingungen zutrifft:  
  
-   Die Anforderung wird an einen lokalen Berichtsserver gesendet.  
  
-   Die Anforderung wird an eine IP-Adresse des Berichtsservercomputers statt an einen Hostheader oder einen Servernamen gesendet.  
  
-   Firewallsoftware blockiert zur Kerberos-Authentifizierung verwendete Ports.  
  
-   Im Betriebssystem eines bestimmten Servers wurde Kerberos nicht aktiviert.  
  
-   Die Domäne enthält ältere Versionen von Windows-Client- und Serverbetriebssystemen, welche die Kerberos-Authentifizierungsfunktion von neueren Versionen des Betriebssystems nicht unterstützen.  
  
 Außerdem hängt die Wahl von ausgehandeltem Kerberos oder NTLM in Internet Explorer von der Konfiguration von URL, LAN und Proxyeinstellungen ab.  
  
###### <a name="report-server-url"></a>Berichtsserver-URL  
 Wenn die URL einen voll qualifizierten Domänennamen enthält, wählt Internet Explorer NTLM aus. Wenn als URL localhost angegeben wird, wählt Internet Explorer NTLM aus. Wird in der URL der Netzwerkname des Computers angegeben, wählt Internet Explorer Negotiate aus. Je nachdem, ob ein SPN für das Berichtsserver-Dienstkonto vorhanden ist, ist das Aushandeln erfolgreich oder es schlägt fehl.  
  
###### <a name="lan-and-proxy-settings-on-the-client"></a>LAN- und Proxyeinstellungen auf dem Client  
 In Internet Explorer festgelegte LAN- und Proxyeinstellungen können bestimmen, ob NTLM statt Kerberos gewählt wird. Da verschiedene Organisationen jedoch unterschiedliche LAN- und Proxyeinstellungen verwenden, ist es nicht möglich, die einzelnen Einstellungen genau zu bestimmen, die zu Kerberos-Authentifizierungsfehlern beitragen. Beispielsweise kann eine Organisation Proxyeinstellungen durchsetzen, mit denen Intranet-URLs in vollqualifizierte URLs mit Domänennamen umgewandelt werden, die über Internetverbindungen aufgelöst werden. Wenn verschiedene Authentifizierungsanbieter für unterschiedliche URL-Typen verwendet werden, kann es vorkommen, dass unerwartete Verbindungen erfolgreich hergestellt werden.  
  
 Wenn Verbindungsfehler auftreten, die Sie auf Authentifizierungsfehler zurückführen, können Sie verschiedene Kombinationen von LAN- und Proxyeinstellungen ausprobieren, um das Problem zu isolieren. In Internet Explorer befinden sich die LAN- und Proxyeinstellungen im Dialogfeld **LAN-Einstellungen** , das geöffnet wird, wenn Sie im Dialogfeld **Internetoptionen** auf der Registerkarte **Verbindungen** auf **LAN-Einstellungen**klicken.  
  
## <a name="external-resources"></a>Externe Ressourcen  
  
-   Weitere Informationen zu Kerberos und Berichtsservern finden Sie unter [Bereitstellung einer Business Intelligence-Lösung mit SharePoint, Reporting Services und PerformancePoint Monitoring Server mit Kerberos](http://go.microsoft.com/fwlink/?LinkID=177751)  
  
## <a name="see-also"></a>Siehe auch  
 [Authentifizierung mit dem Berichtsserver](../../reporting-services/security/authentication-with-the-report-server.md)   
 [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Konfigurieren der Standardauthentifizierung auf dem Berichtsserver](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)   
 [Konfiguration der benutzerdefinierten oder Formularauthentifizierung auf dem Berichtsserver](../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)   
 [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)  
  
  

