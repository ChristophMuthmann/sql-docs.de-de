---
title: Authentifizierung mit dem Berichtsserver | Microsoft Docs
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [Reporting Services], configuring
- connections [Reporting Services], accounts
- Windows authentication [Reporting Services]
- authentication [Reporting Services]
- Forms authentication
ms.assetid: 753c2542-0e97-4d8f-a5dd-4b07a5cd10ab
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c38fc293a297544710b77b52d054fae58273340e
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---

# <a name="authentication-with-the-report-server"></a>Authentifizierung mit dem Berichtsserver

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) bietet mehrere konfigurierbare Optionen zum Authentifizieren von Benutzern und Clientanwendungen für den Berichtsserver. Standardmäßig verwendet der Berichtsserver die integrierte Windows-Authentifizierung und geht von vertrauenswürdigen Beziehungen aus, wenn sich Client- und Netzwerkressourcen in der gleichen Domäne oder einer vertrauenswürdigen Domäne befinden. Abhängig von der Netzwerktopologie und den Anforderungen der Organisation können Sie das für die integrierte Windows-Authentifizierung verwendete Authentifizierungsprotokoll anpassen, die Standardauthentifizierung verwenden oder eine selbst bereitgestellte und auf einem benutzerdefinierten Formular basierende Authentifizierungserweiterung nutzen. Jeder dieser Authentifizierungstypen kann individuell aktiviert oder deaktiviert werden. Sie können mehrere Authentifizierungstypen aktivieren, wenn der Berichtsserver mehrere Arten von Anforderungen akzeptieren soll.
  
 Alle Benutzer oder Anwendungen, die Zugriff auf Berichtsserverinhalte oder -vorgänge anfordern, müssen vor Gewähren des Zugriffs authentifiziert werden.  
  
## <a name="authentication-types"></a>Authentifizierungstypen  
 Alle Benutzer oder Anwendungen, die Zugriff auf Berichtsserverinhalte oder -vorgänge anfordern, müssen vor Gewähren des Zugriffs mit dem Authentifizierungstyp authentifiziert werden, der auf dem Berichtsserver konfiguriert ist. In der folgenden Tabelle werden die von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]unterstützten Authentifizierungstypen beschrieben.  
  
|Name Authentifizierungstyp|Wert HTTP-Authentifizierungsebene|Standardmäßig verwendet|Description|  
|-----------------------------|-------------------------------------|---------------------|-----------------|  
|RSWindowsNegotiate|Aushandeln|Ja|Versucht für die integrierte Windows-Authentifizierung zunächst eine Kerberos-Authentifizierung zu verwenden, greift jedoch auf NTLM zurück, wenn Active Directory kein Ticket für die Client-Anforderung auf den Berichtsserver gewähren kann. Negotiate greift nur auf NTLM zurück, wenn das Ticket nicht verfügbar ist. Wenn der erste Versuch zu einem Fehler (außer einem nicht verfügbaren Ticket) führt, unternimmt der Berichtsserver keinen zweiten Versuch.|  
|RSWindowsNTLM|NTLM|Ja|Verwendet für die integrierte Windows-Authentifizierung NTLM.<br /><br /> Die Anmeldeinformationen werden nicht delegiert oder durch einen Identitätswechsel für andere Anforderungen verwendet. Nachfolgende Anforderungen befolgen eine neue Abfrage-/Rückmeldungs-Sequenz. Je nach den Einstellungen für die Netzwerksicherheit können Benutzer aufgefordert werden, Anmeldeinformationen einzugeben, oder die Authentifizierungsanforderung wird transparent verarbeitet.|  
|RSWindowsKerberos|Kerberos|Nein|Verwendet für die integrierte Windows-Authentifizierung Kerberos. Sie müssen Kerberos konfigurieren, indem Sie Dienstprinzipalnamen (Service Principle Names, SPNs) für die Dienstkonten einrichten, die Domänenadministratorberechtigungen erfordern. Wenn Sie für Kerberos die Identitätsdelegierung aktivieren, kann das Token des den Bericht anfordernden Benutzers auch für eine zusätzliche Verbindung zu den externen Datenquellen verwendet werden, die Daten für Berichte liefern.<br /><br /> Bevor Sie RSWindowsKerberos angeben, stellen Sie sicher, dass der von Ihnen verwendete Browsertyp diesen Authentifizierungstyp unterstützt. Wenn Sie Microsoft Edge oder Internet Explorer verwenden, wird die Kerberos-Authentifizierung nur über Negotiate unterstützt. Microsoft Edge oder Internet Explorer formuliert keine Authentifizierungsanforderung, die Kerberos direkt angibt.|  
|RSWindowsBasic|Standard|Nein|Die Standardauthentifizierung wird im HTTP-Protokoll definiert und kann nur verwendet werden, um HTTP-Anforderungen an den Berichtsserver zu authentifizieren.<br /><br /> Anmeldeinformationen werden mithilfe der Base64-Codierung an die HTTP-Anforderung übergeben. Bei der Standardauthentifizierung können Sie SSL (Secure Sockets Layer) zum Verschlüsseln der Benutzerkontoinformationen verwenden, bevor diese über das Netzwerk gesendet werden. SSL bietet einen verschlüsselten Kanal zum Senden einer Verbindungsanforderung vom Client an den Berichtsserver über eine HTTP TCP/IP-Verbindung. Weitere Informationen finden Sie auf der [TechNet-Website unter](http://go.microsoft.com/fwlink/?LinkId=71123) Using SSL to Encrypt Confidential Data [!INCLUDE[msCoName](../../includes/msconame-md.md)] .|  
|Benutzerdefiniert|(Anonym)|Nein|Die anonyme Authentifizierung weist den Berichtsserver an, den Authentifizierungsheader in einer HTTP-Anforderung zu ignorieren. Der Berichtsserver akzeptiert alle Anforderungen. Führen Sie den Aufruf jedoch mit einer benutzerdefinierten [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] Formularauthentifizierung aus, die Sie zur Authentifizierung des Benutzers bereitstellen.<br /><br /> Geben Sie **Custom** nur an, wenn Sie ein benutzerdefiniertes Authentifizierungsmodul bereitstellen, das alle Authentifizierungsanforderungen auf dem Berichtsserver verarbeitet. Sie können den benutzerdefinierten Authentifizierungstyp nicht mit der Standardauthentifizierungserweiterung von Windows verwenden.|  
  
## <a name="unsupported-authentication-methods"></a>Nicht unterstützte Authentifizierungsmethoden  
 Die folgenden Authentifizierungsmethoden und -anforderungen werden nicht unterstützt.  
  
|Authentifizierungsmethode|Erklärung|  
|---------------------------|-----------------|  
|Anonym|Der Berichtsserver akzeptiert nur die nicht authentifizierten Anforderungen anonymer Benutzer in Bereitstellungen, die eine benutzerdefinierte Authentifizierungserweiterung enthalten.<br /><br /> Berichts-Generator akzeptiert nicht authentifizierte Anforderungen, wenn Sie den Zugriff des Berichts-Generators auf einen Berichtsserver aktivieren, der für die Standardauthentifizierung konfiguriert ist.<br /><br /> In allen anderen Fällen werden die anonymen Anforderungen mit dem Fehler 'HTTP Status 401 Access Denied' abgelehnt, bevor die Anforderung [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]erreicht. Clients, die den Fehler '401 Access Denied' erhalten, müssen die Anforderung mit einem gültigen Authentifizierungstyp umformulieren.|  
|Technologie für einmaliges Anmelden (SSO, Single sign-on technologies)|In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] gibt es keine systemeigene Unterstützung der Technologien für einmaliges Anmelden. Wenn Sie eine Technologie für einmaliges Anmelden verwenden möchten, müssen Sie eine benutzerdefinierte Authentifizierungserweiterung erstellen.<br /><br /> Die Berichtsserver-Hostumgebung unterstützt keine ISAPI-Filter. Falls die verwendete SSO-Technologie als ISAPI-Filter implementiert ist, sollten Sie die in den ISA-Server integrierte Unterstützung für RSASecueID oder das RADIUS-Protokoll verwenden. Andernfalls können Sie eine ISA-Server-ISAPI oder ein HTTPModule für RS erstellen. Es wird jedoch die direkte Verwendung des ISA-Servers empfohlen.|  
|Passport|In SQL Server Reporting Services unterstützt nicht.|  
|Digest|In SQL Server Reporting Services unterstützt nicht.|  
  
## <a name="configuration-of-authentication-settings"></a>Konfigurieren von Authentifizierungseinstellungen  
 Authentifizierungseinstellungen werden für die Standardsicherheit konfiguriert, wenn die Berichtsserver-URL reserviert ist. Wenn Sie diese Einstellungen inkorrekt bearbeiten, gibt der Berichtsserver für Anforderungen, die nicht authentifiziert werden können, die Fehler ' HTTP 401 Access Denied' zurück. Beim Auswählen eines Authentifizierungstyps müssen Sie bereits wissen, wie die Windows-Authentifizierung in Ihrem Netzwerk unterstützt wird. Sie müssen mindestens einen Authentifizierungstyp angeben. Für RSWindows können mehrere Authentifizierungstypen angegeben werden. RSWindows-Authentifizierungstypen (d.h. **RSWindowsBasic**, **RSWindowsNTLM**, **RSWindowsKerberos**und **RSWindowsNegotiate**) schließen sich mit „Custom“ gegenseitig aus.  
  
> [!IMPORTANT]  
>  Reporting Services überprüft nicht, ob die von Ihnen angegebenen Einstellungen für die Computerumgebung korrekt sind. Es ist möglich, dass die Standardsicherheit für Ihre Installation nicht geeignet ist oder die von Ihnen angegebenen Konfigurationseinstellungen für Ihre Sicherheitsinfrastruktur nicht geeignet sind. Aus diesem Grund sollten Sie Ihre Berichtsserverbereitstellung in einer kontrollierten Testumgebung sorgfältig prüfen, bevor Sie sie Ihrer Organisation zur Verfügung stellen.  
  
 Der Berichtsserver-Webdienst und der [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] verwenden stets denselben Authentifizierungstyp. Sie können keine anderen Authentifizierungstypen für die Funktionsbereiche des Berichtsserverdienstes konfigurieren. In einem Bereitstellungsmodell für horizontales Skalieren sollten Sie sicherstellen, dass alle Ihre Änderungen auf allen Knoten der Bereitstellung dupliziert werden. Sie können keine anderen Knoten in der gleichen Bereitstellung für horizontales Skalieren konfigurieren, um andere Authentifizierungstypen zu verwenden.  
  
 Die Hintergrundverarbeitung akzeptiert keine Anforderungen von Endbenutzern. Sie authentifiziert jedoch alle Anforderungen für unbeaufsichtigte Ausführungszwecke. Sie verwendet stets die Windows-Authentifizierung und authentifiziert Anforderungen mit dem Berichtsserverdienst oder dem Konto für die unbeaufsichtigte Ausführung, falls konfiguriert.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Konfigurieren der Windows-Authentifizierung auf dem Berichtsserver](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
  
-   [Konfigurieren der Standardauthentifizierung auf dem Berichtsserver](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)  
  
-   [Konfigurieren von benutzerdefinierten oder Formularauthentifizierung auf dem Berichtsserver](../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Taskbeschreibungen|Links|  
|-----------------------|-----------|  
|Konfigurieren Sie den integrierte Windows-Authentifizierungstyp.|[Konfigurieren der Windows-Authentifizierung auf dem Berichtsserver](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)|  
|Konfigurieren Sie den Standardauthentifizierungstyp.|[Konfigurieren der Standardauthentifizierung auf dem Berichtsserver](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)|  
|Konfigurieren Sie die formularbasierte Authentifizierung oder andernfalls ein benutzerdefinierten Authentifizierungstyp.|[Konfiguration der benutzerdefinierten oder Formularauthentifizierung auf dem Berichtsserver](../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)|  
|Ermöglichen Sie die [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] im Berichts-Manager, um das benutzerdefinierte Authentifizierungsszenario zu verarbeiten.|[Configure the Web Portal to Pass Custom Authentication Cookies (Konfigurieren des Webportals für die Übergabe von benutzerdefinierten Authentifizierungscookies)](http://msdn.microsoft.com/en-us/91aeb053-149e-4562-ae4c-a688d0e1b2ba)|  

## <a name="next-steps"></a>Nächste Schritte

[Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
[RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Erstellen und Verwalten von Rollenzuweisungen](../../reporting-services/security/create-and-manage-role-assignments.md)   
[Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen-Verbindungen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
[Implementieren von Sicherheitserweiterungen](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)   
[Konfigurieren von SSL-Verbindungen auf einem Berichtsserver im einheitlichen Modus](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)   
[Konfigurieren des Berichts-Generator-Zugriffs](../../reporting-services/report-server/configure-report-builder-access.md)   
[Übersicht über Sicherheitserweiterungen](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
[Authentifizierung in Reporting Services](../../reporting-services/extensions/security-extension/authentication-in-reporting-services.md)   
[Autorisierung in Reporting Services](../../reporting-services/extensions/security-extension/authorization-in-reporting-services.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
