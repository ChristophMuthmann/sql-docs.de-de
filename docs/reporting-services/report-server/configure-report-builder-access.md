---
title: Konfigurieren des Berichts-Generatorzugriffs | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Reporting Services, Report Builder
- Report Builder 1.0, configuring access
- configuring servers [Reporting Services]
ms.assetid: a79003d0-c905-4d4c-9560-93a7cc1e1dd4
caps.latest.revision: "47"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 2018c910537ea73bc36d1a41f074d9aeae0e9a37
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="configure-report-builder-access"></a>Konfigurieren des Berichts-Generator-Zugriffs
  Der Berichts-Generator ist ein Tool für die Ad-hoc-Berichterstellung, das mit einem für den einheitlichen oder den integrierten SharePoint-Modus konfigurierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver zusammen installiert wird.  
  
 Der Zugriff auf den Berichts-Generator ist von den folgenden Faktoren abhängig:  
  
-   Servereigenschaften, mit denen bestimmt wird, ob der Berichts-Generator auf dem Berichtsserver verfügbar ist.  
  
-   Rollenzuweisungen oder Berechtigungen, mit denen der Berichts-Generator einzelnen Benutzern oder Gruppen zur Verfügung gestellt wird.  
  
-   Authentifizierungseinstellungen, die bestimmten, ob Benutzeranmeldeinformationen an den Berichtsserver weitergegeben werden können oder anonymer Zugriff für die Anwendungsdateien konfiguriert wird.  
  
 Es muss ein veröffentlichtes Berichtsmodell vorliegen, das bearbeitet werden kann, um den Berichts-Generator verwenden zu können.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 Der Berichts-Generator ist nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Auf dem Clientcomputer muss [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 installiert sein. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] stellt die Infrastruktur zum Ausführen von [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] -Anwendungen bereit.  
  
 Sie müssen [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 6.0 oder höher verwenden.  
  
 Der Berichts-Generator wird immer im Modus für volle Vertrauenswürdigkeit ausgeführt; Sie können ihn nicht so konfigurieren, dass er im Modus für teilweise Vertrauenswürdigkeit ausgeführt wird. In früheren Versionen war es möglich, den Berichts-Generator im Modus für partielle Vertrauenswürdigkeit auszuführen, aber diese Option wird in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höheren Versionen nicht unterstützt.  
  
## <a name="enabling-and-disabling-report-builder"></a>Aktivieren und Deaktivieren des Berichts-Generators  
 Der Berichts-Generator ist in der Standardeinstellung aktiviert. Die Berichtsserveradministratoren können den Berichts-Generator deaktivieren, indem sie die Berichtsserver-Systemeigenschaft **EnableReportDesignClientDownload** auf **false**festlegen. Durch Festlegen dieser Eigenschaft werden Downloads des Berichts-Generators für diesen Berichtsserver deaktiviert.  
  
 Zum Festlegen der Berichtsserver-Systemeigenschaften können Sie Management Studio oder ein Skript verwenden:  
  
-   Wenn Sie Management Studio verwenden möchten, stellen Sie eine Verbindung mit dem Berichtsserver her und legen auf der Seite mit den erweiterten Servereigenschaften die Eigenschaft **EnableReportDesignClientDownload** auf **false**fest. Weitere Informationen zum Öffnen dieser Seite finden Sie unter [Festlegen von Berichtsservereigenschaften (Management Studio)](../../reporting-services/tools/set-report-server-properties-management-studio.md).  
  
-   Ein Beispielskript, das eine Berichtsservereigenschaft festlegt, finden Sie unter [Skripts für Bereitstellungs- und Verwaltungsaufgaben](../../reporting-services/tools/script-deployment-and-administrative-tasks.md).  
  
## <a name="role-assignments-granting-report-builder-access-on-a-native-mode-report-server"></a>Rollenzuweisungen, die auf einem Berichtsserver im einheitlichen Modus Zugriff auf den Berichts-Generator gewähren  
 Erstellen Sie auf einem Berichtsserver im einheitlichen Modus Benutzerrollenzuweisungen, die Tasks zum Verwenden des Berichts-Generators einschließen. Sie müssen Inhalts-Manager und Systemadministrator sein, um Rollendefinitionen und Rollenzuweisungen auf der Element- und Websiteebene erstellen oder ändern zu können.  
  
 Die folgenden Anweisungen gehen davon aus, dass Sie vordefinierte Rollen verwenden. Wenn Sie die Rollendefinitionen abgeändert oder von SQL Server 2000 aktualisiert haben, überprüfen Sie die Rollen, um sicherzustellen, dass sie die erforderlichen Tasks enthalten. Weitere Informationen zum Erstellen von Rollenzuweisungen finden Sie unter [Gewähren von Benutzerzugriff auf einen Berichtsserver (Berichts-Manager)](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md).  
  
 Nachdem Sie die Rollenzuweisungen erstellt haben, sind die Benutzer zu Folgendem berechtigt:  
  
-   Benutzer, denen die Rollen Systembenutzer und Browser zugewiesen wurden, können veröffentlichte Berichts-Generator-Berichte auf einem Berichtsserver anzeigen, ohne den Berichts-Generator starten zu müssen.  
  
-   Benutzer, denen die Rollen Systembenutzer und Berichts-Generator zugewiesen wurden, können Modelle erzeugen, den Berichts-Generator starten und Berichte erstellen sowie Berichte auf dem Berichtsserver speichern.  
  
-   Benutzer, denen die Rollen Systembenutzer und Verleger zugewiesen wurden, können Modelle aus dem Modell-Designer auf dem Berichtsserver veröffentlichen. Modelle werden im Berichts-Generator als Datenquellen verwendet.  
  
-   Benutzer, denen die Rollen Systemadministrator und Inhalts-Manager zugewiesen wurden, verfügen über sämtliche Berechtigungen zum Erstellen, Anzeigen und Verwalten von Berichts-Generator-Berichten.  
  
#### <a name="to-verify-required-tasks-are-in-the-role-definitions"></a>So überprüfen Sie, ob die Rollendefinitionen die erforderlichen Tasks enthalten  
  
1.  Starten Sie Management Studio, und stellen Sie eine Verbindung mit dem Berichtsserver her.  
  
2.  Öffnen Sie den Ordner **Sicherheit** .  
  
3.  Öffnen Sie den Ordner **Systemrollen** .  
  
4.  Klicken Sie mit der rechten Maustaste auf **Systemadministrator**, und wählen Sie **Eigenschaften**aus.  
  
5.  Wählen Sie **Berichtsdefinitionen ausführen** aus, und klicken Sie auf **OK**.  
  
6.  Klicken Sie mit der rechten Maustaste auf **Systembenutzer**, und wählen Sie **Eigenschaften**aus.  
  
7.  Wählen Sie **Berichtsdefinitionen ausführen** aus, und klicken Sie auf **OK**.  
  
8.  Öffnen Sie den Ordner **Rollen** .  
  
9. Klicken Sie mit der rechten Maustaste auf **Browser**, und wählen Sie **Eigenschaften**aus.  
  
10. Wählen Sie **Modelle anzeigen** aus, und klicken Sie auf **OK**.  
  
11. Klicken Sie mit der rechten Maustaste auf **Inhalts-Manager**, und wählen Sie **Eigenschaften**aus.  
  
12. Wählen Sie **Modelle anzeigen**, **Modelle verwalten**und **Berichte lesen**aus, und klicken Sie auf **OK**.  
  
13. Klicken Sie mit der rechten Maustaste auf **Verleger**, und wählen Sie **Eigenschaften**aus.  
  
14. Wählen Sie **Modelle verwalten** aus, und klicken Sie auf **OK**.  
  
15. Erstellen Sie die Berichts-Generator-Rolle, wenn sie nicht vorhanden ist:  
  
    1.  Öffnen Sie den Ordner **Sicherheit** .  
  
    2.  Klicken Sie mit der rechten Maustaste auf **Rollen**, und wählen Sie **Neue Rolle**aus.  
  
    3.  Geben Sie im Feld Name den Namen **Berichts-Generator**ein.  
  
    4.  Geben Sie im Feld Beschreibung eine Rollenbeschreibung ein, damit die Benutzer im Berichts-Manager wissen, wozu ihre Rolle dient.  
  
    5.  Fügen Sie die folgenden Aufgaben hinzu: **Berichte lesen**, **Berichte anzeigen**, **Modelle anzeigen**, **Ressourcen anzeigen**, **Ordner anzeigen**und **Einzelne Abonnements verwalten**.  
  
    6.  Klicken Sie auf **OK** , um die Rolle zu speichern.  
  
#### <a name="to-create-role-assignments-that-grant-access-to-report-builder"></a>So erstellen Sie Rollenzuweisungen, die Zugriff auf den Berichts-Generator gewähren  
  
1.  Starten Sie den Berichts-Manager.  
  
2.  Klicken Sie auf **Siteeinstellungen**.  
  
3.  Klicken Sie auf **Sicherheit**.  
  
4.  Wenn für den Benutzer oder die Gruppe, für den bzw. die Sie den Zugriff auf den Berichts-Generator konfigurieren möchten, klicken Sie auf **Bearbeiten**.  
  
     Andernfalls klicken Sie auf **Neue Rollenzuweisung**. Geben Sie unter Gruppe oder Benutzer ein Windows-Domänenbenutzer- oder -Gruppenkonto im folgenden Format ein: \<Domäne>\\<Konto\>. Wenn Sie die Formularauthentifizierung oder die benutzerdefinierte Sicherheit verwenden, geben Sie das Benutzer- oder Gruppenkonto in dem für Ihre Bereitstellung richtigen Format an.  
  
5.  Wählen Sie **Systembenutzer**aus, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie auf **Startseite**.  
  
7.  Klicken Sie auf die Registerkarte **Ordnereinstellungen** .  
  
8.  Klicken Sie auf die Registerkarte **Sicherheit** .  
  
9. Wenn für den Benutzer oder die Gruppe, für den bzw. die Sie den Zugriff auf den Berichts-Generator konfigurieren möchten, klicken Sie auf **Bearbeiten**.  
  
     Andernfalls klicken Sie auf **Neue Rollenzuweisung**. Geben Sie unter Gruppe oder Benutzer ein Windows-Domänenbenutzer- oder -Gruppenkonto im folgenden Format ein: \<Domäne>\\<Konto\>. Wenn Sie die Formularauthentifizierung oder die benutzerdefinierte Sicherheit verwenden, geben Sie das Benutzer- oder Gruppenkonto in dem für Ihre Bereitstellung richtigen Format an.  
  
10. Wählen Sie **Berichts-Generator**aus, und klicken Sie dann auf **Anwenden**.  
  
11. Wiederholen Sie den Vorgang, um Rollenzuweisungen für weitere Benutzer oder Gruppen zu erstellen oder ändern.  
  
## <a name="permissions-granting-report-builder-access-on-a-sharepoint-integrated-mode-report-server"></a>Berechtigungen, die auf einem Berichtsserver im integrierten SharePoint-Modus Zugriff auf den Berichts-Generator gewähren  
 Auf einem Berichtsserver im integrierten SharePoint-Modus wird SharePoint-Benutzern, die über die Berechtigungsstufen Teilnehmen oder Vollzugriff verfügen, Zugriff auf den Berichts-Generator gewährt.  
  
 Wenn Sie benutzerdefinierte Berechtigungsstufen verwenden, müssen Sie Elemente hinzufügen und Elemente bearbeiten in die Berechtigungsstufe aufnehmen. Weitere Informationen zum Zugriff auf den Berichts-Generator über integrierte Berechtigungsstufen finden Sie unter [Verwenden der integrierten Sicherheit in Windows SharePoint Services für Berichtsserverelemente](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md). Weitere Informationen zu Berechtigungsanforderungen für benutzerdefinierte Berechtigungsstufen finden Sie unter [Festlegen von Berechtigungen für Berichtsservervorgänge in einer SharePoint-Webanwendung](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md).  
  
## <a name="authentication-considerations-and-credential-reuse"></a>Authentifizierungsüberlegungen und Wiederverwendung von Anmeldeinformationen  
 Der Berichts-Generator verwendet ClickOnce-Technologie, um seine Anwendungsdateien auf einen Clientcomputer herunterzuladen und dort zu installieren. Die ClickOnce-Technologie ist für die unidirektionale Anwendungsbereitstellung vorgesehen, bei der Programmdateien auf einem Clientcomputer platziert werden und die Anwendung als separater Prozess unter der Identität des Standardbenutzers ausgeführt wird. Weil der Berichts-Generator eine Verbindung mit dem Berichtsserver herstellen muss, um Anwendungsdateien und Berichtsserverdaten abzurufen, ist es wichtig, zu verstehen wie die ClickOnce-Technologie den Sicherheitskontext festlegt und in verschiedenen Szenarien Anforderungen an Remotecomputer ausgibt:  
  
-   ClickOnce wird immer als separater Prozess auf dem Clientcomputer ausgeführt. Die Prozessidentität entspricht den Standard-Windows-Benutzeranmeldeinformationen. ClickOnce nutzt weder die Sitzungsdaten mit Internet Explorer gemeinsam noch bezieht ClickOnce den Benutzersicherheitskontext von Internet Explorer.  
  
-   ClickOnce sendet Anforderungen, deren Authentifizierungsheader die integrierte Sicherheit von Windows angeben. Wenn ein Server für einen anderen Authentifizierungstyp konfiguriert wurde, reagiert dieser Server mit einem Authentifizierungsfehler auf Anforderungen von ClickOnce. Um dieses Problem zu umgehen, müssen Sie entweder einen Server für die integrierte Sicherheit von Windows konfigurieren, oder Sie müssen anonyme Zugriffe zulassen, damit die Authentifizierungsprüfung entfällt.  
  
-   Der Berichts-Generator stellt eine eigene Verbindung mit einem Berichtsserver her. Wenn Sie nicht die integrierte Sicherheit von Windows mit einmaliger Anmeldung verwenden, müssen die Benutzer die Anmeldeinformationen für die Verbindung zwischen Berichts-Generator und Berichtsserver erneut eingeben.  
  
 In der folgenden Tabelle werden die vom Berichtsserver unterstützten Authentifizierungstypen beschrieben, und es wird angegeben, ob zusätzliche Konfigurationsschritte für den Zugriff auf den Berichts-Generator erforderlich sind.  
  
|Authentifizierungstyp des Berichtsservers|Reaktion von Berichts-Generator und ClickOnce-Anwendungsstartprogramm|  
|---------------------------------------|--------------------------------------------------------------------|  
|Negotiate (Standard)<br /><br /> NTLM (Standard)|Bei Verwendung der integrierten Sicherheit von Windows sind authentifizierte Anforderungen von ClickOnce und Berichts-Generator in der Regel erfolgreich, wenn Client und Server in der gleichen Domäne bereitgestellt wurden, wenn der Benutzer sich beim Clientcomputer unter einem Domänenkonto angemeldet hat, das zum Zugriff auf den Berichts-Generator berechtigt ist, und wenn der Berichtsserver für die Windows-Authentifizierung konfiguriert wurde.<br /><br /> Die Anforderungen sind erfolgreich, da ClickOnce und die Browserverbindung mit dem Berichtsserver über die gleiche Benutzeridentität verfügen.<br /><br /> Anforderungen schlagen fehl, wenn der Benutzer Internet Explorer mit der Option Ausführen als geöffnet und keine Standardanmeldeinformationen angegeben hat. Falls die Benutzersitzung auf dem Berichtsserver unter einem bestimmten Konto eingerichtet und ClickOnce unter einem anderen Konto ausgeführt wird, dann verweigert der Berichtsserver den Zugriff auf die Dateien.|  
|Kerberos|Internet Explorer, der für den Einsatz des Berichts-Generators erforderlich ist, unterstützt Kerberos nicht direkt.|  
|Standardauthentifizierung|ClickOnce unterstützt die Standardauthentifizierung nicht. Es werden keine Anforderungen formuliert, die die Standardauthentifizierung im Authentifizierungsheader angeben. Es werden keine Anmeldeinformationen übergeben oder Benutzer zur Angabe von Anmeldeinformationen aufgefordert. Sie können diese Probleme umgehen, indem Sie den anonymen Zugriff auf die Anwendungsdateien des Berichts-Generators aktivieren.<br /><br /> Anforderungen sind erfolgreich, wenn Sie anonyme Zugriffe auf die Anwendungsdateien des Berichts-Generators zulassen, weil der Berichtsserver den Authentifizierungsheader ignoriert. Weitere Informationen zum Aktivieren des anonymen Zugriffs auf den Berichts-Generator finden Sie unter [Konfigurieren der Standardauthentifizierung auf dem Berichtsserver](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md).<br /><br /> Nachdem ClickOnce die Anwendungsdateien abgerufen hat, öffnet der Berichts-Generator eine separate Verbindung mit einem Berichtsserver. Die Benutzer müssen ihre Anmeldeinformationen erneut eingeben, damit die Verbindung zwischen Berichts-Generator und Berichtsserver hergestellt werden kann. Der Berichts-Generator erfasst keine Anmeldeinformationen von Internet Explorer oder ClickOnce.<br /><br /> Anforderungen schlagen fehl, wenn der Berichtsserver für die Standardauthentifizierung konfiguriert wurde und der anonyme Zugriff auf die Programmdateien des Berichts-Generators nicht aktiviert wurde. Die Anforderung schlägt fehl, da in ClickOnce-Anforderungen die integrierte Sicherheit von Windows angegeben wird. Wenn Sie einen Berichtsserver für die Standardauthentifizierung konfigurieren, weist der Server die Anforderung zurück, weil darin ein unzulässiges Sicherheitspaket angegeben wird und weil sie nicht die vom Server erwarteten Anmeldeinformationen enthält.<br /><br /> Falls der Berichtsserver für die Verwendung von SharePoint im integrierten Modul konfiguriert ist und die SharePoint-Site die grundlegende Authentifizierung verwendet, erhalten Benutzer zudem die Fehlermeldung 401, wenn Sie versuchen, den Berichts-Generator mithilfe von ClickOnce auf ihren Clientcomputern zu installieren. Der Grund hierfür liegt darin, dass SharePoint ein Cookie verwendet, um eine Benutzerauthentifizierung für die Dauer der Sitzung beizubehalten, ClickOnce dieses Cookie jedoch nicht unterstützt. Wenn ein Benutzer eine ClickOnce-Anwendung wie den Berichts-Generator startet, leitet die Anwendung das Cookie nicht an SharePoint weiter, weshalb SharePoint den Zugriff verweigert und den Fehler 401 zurückgibt.<br /><br /> Sie können dieses Problem umgehen, indem Sie eine der folgenden Optionen ausprobieren:<br /><br /> – Aktivieren Sie die Option **Kennwort speichern** , wenn Sie die Benutzeranmeldeinformationen bereitstellen.<br /><br /> –Aktivieren Sie den anonymen Zugriff auf die SharePoint-Websiteauflistung.<br /><br /> –Konfigurieren Sie die Umgebung so, dass der Benutzer keine Anmeldeinformationen bereitstellen muss. Beispielsweise können Sie den SharePoint-Server in einer Intranetumgebung so konfigurieren, dass er Teil einer Arbeitsgruppe ist. Anschließend können Sie Benutzerkonten auf den lokalen Computern erstellen.|  
|Benutzerdefiniert|Wenn Sie einen Berichtsserver für die Verwendung einer benutzerdefinierten Authentifizierung konfigurieren, wird der anonyme Zugriff auf dem Berichtsserver aktiviert, und die Anforderungen werden ohne Authentifizierungsprüfung akzeptiert.<br /><br /> Nachdem ClickOnce die Anwendungsdateien abgerufen hat, öffnet der Berichts-Generator eine separate Verbindung mit einem Berichtsserver. Die Benutzer müssen ihre Anmeldeinformationen erneut eingeben, damit die Verbindung zwischen Berichts-Generator und Berichtsserver hergestellt werden kann. Der Berichts-Generator erfasst keine Anmeldeinformationen von Internet Explorer oder ClickOnce.|  
  
## <a name="see-also"></a>Siehe auch  
 [Authentifizierung mit dem Berichtsserver](../../reporting-services/security/authentication-with-the-report-server.md)   
 [Browserunterstützung für Reporting Services und Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)   
 [Starten des Berichts-Generators](../../reporting-services/report-builder/start-report-builder.md)   
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Vorgehensweise: Herstellen einer Verbindung mit einem Berichtsserver in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Berichtsserver-Systemeigenschaften](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)  
  
  
