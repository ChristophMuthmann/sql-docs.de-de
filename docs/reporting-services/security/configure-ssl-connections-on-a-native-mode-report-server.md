---
title: Konfigurieren von SSL-Verbindungen auf einem Berichtsserver im einheitlichen Modus | Microsoft Docs
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Secure Sockets Layer (SSL)
ms.assetid: 212f2042-456a-4c0a-8d76-480b18f02431
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4f973faa65ed34695804de0815331f562b7a24f4
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="configure-ssl-connections-on-a-native-mode-report-server"></a>Konfigurieren von SSL-Verbindungen auf einem Berichtsserver im einheitlichen Modus
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Im einheitlichen Modus wird der HTTP-SSL-Dienst (Secure Sockets Layer, SSL) verwendet, um verschlüsselte Verbindungen mit einem Berichtsserver herzustellen. Wenn in einem lokalen Zertifikatspeicher auf dem Berichtsservercomputer eine Zertifikatsdatei (CER-Datei) installiert ist, können Sie das Zertifikat an eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -URL-Reservierung binden, um Berichtsserververbindungen über einen verschlüsselten Kanal zu unterstützen.  
  
> [!TIP]  
>  Bei Verwendung des SharePoint-Modus von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] finden Sie weitere Informationen in der SharePoint-Dokumentation. Beispielsweise unter [Vorgehensweise: Aktivieren von SSL für eine SharePoint 2010-Webanwendung (http://blogs.msdn.com/b/sowmyancs/archive/2010/02/12/how-to-enable-ssl-on-a-sharepoint-web-application.aspx)](http://blogs.msdn.com/b/sowmyancs/archive/2010/02/12/how-to-enable-ssl-on-a-sharepoint-web-application.aspx).  
  
 Da Internetinformationsdienste (IIS) auch HTTP-SSL verwenden, bestehen signifikante Probleme mit der Interoperabilität, die berücksichtigt werden müssen, wenn IIS und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf demselben Computer ausgeführt werden. Überprüfen Sie im Abschnitt "Interoperabilitätsprobleme mit IIS", wie Sie diese Probleme beheben können.  
  
## <a name="server-certificate-requirements"></a>Anforderungen für Serverzertifikate  
 Auf Ihrem Computer muss ein Serverzertifikat installiert sein (Clientzertifikate werden nicht unterstützt). Reporting Services bietet keine Funktionalität für das Anfordern, Generieren, Herunterladen oder Installieren von Zertifikaten. [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] bietet ein Zertifikate-Snap-in, mit dem Sie ein Zertifikat von einer vertrauenswürdigen Zertifizierungsstelle anfordern können.  
  
 Für Testzwecke können Sie ein Zertifikat lokal generieren. Wenn Sie das Hilfsprogramm **MakeCert** und den Beispielbefehl als Vorlage verwenden, geben Sie Ihren Servernamen als Host an, und entfernen Sie alle Zeilenumbrüche, bevor Sie den Befehl ausführen. Wenn Sie den Befehl in einem DOS-Fenster ausführen, müssen Sie die Puffergröße des Fensters erhöhen, damit der gesamte Befehl aufgenommen werden kann.  
  
 Wenn Sie IIS und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] zusammen auf demselben Computer verwenden, können Sie mit der [!INCLUDE[iismgr](../../includes/iismgr-md.md)] -Konsolenanwendung das auf Ihrem Computer installierte Zertifikat abrufen. [!INCLUDE[iismgr](../../includes/iismgr-md.md)] enthält Optionen, mit denen Sie eine Zertifikatanforderungsdatei (CRT-Datei) erstellen und in ein Paket integrieren können, sodass sie nachfolgend von einer vertrauenswürdigen Zertifizierungsstelle verarbeitet werden kann. Die von Ihnen verwendete Zertifizierungsstelle generiert eine Zertifikatsdatei (CER-Datei), die sie an Sie zurücksendet. Über die IIS-Verwaltungskonsole können Sie die Zertifikatsdatei im lokalen Speicher installieren. Weitere Informationen finden Sie unter [Using SSL to Encrypt Confidential Data](http://go.microsoft.com/fwlink/?LinkId=71123) auf der TechNet-Website.  
  
## <a name="interoperability-issues-with-iis"></a>Interoperabilitätsprobleme mit IIS  
 Wenn IIS auf demselben Computer vorhanden ist wie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , wirkt sich dies entscheidend auf die SSL-Verbindungen zu einem Berichtsserver aus:  
  
-   Wenn IIS installiert ist, muss der World Wide Web-(W3SVC)-Dienst immer ausgeführt werden. Der HTTP-SSL-Dienst stellt eine Abhängigkeit zu IIS her, wenn er erkennt, dass IIS ausgeführt wird. Dies bedeutet, dass der World Wide Web-(W3SVC)-Dienst ausgeführt werden muss, wenn IIS und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf demselben Computer installiert werden und Sie Berichtsserver-URLs für SSL-Verbindungen konfigurieren.  
  
-   Durch das Deinstallieren von IIS kann der Dienst zu einer SSL-gerichteten Berichtsserver-URL vorübergehend unterbrochen werden. Aus diesem Grund wird dringend empfohlen, den Computer neu zu starten, nachdem Sie IIS deinstalliert haben.  
  
     Sie müssen den Computer neu starten, um alle SSL-Sitzungen aus dem Cache zu löschen. Einige Betriebssysteme speichern SSL-Sitzungen bis zu 10 Stunden im Cache. Aus diesem Grund funktioniert eine https://-URL auch, nachdem die SSL-Bindung von der URL-Reservierung in HTTP.SYS entfernt wurde. Durch den Neustart des Computers werden alle geöffneten Verbindungen geschlossen, die den Kanal verwenden.  
  
## <a name="bind-ssl-to-a-reporting-services-url-reservation"></a>Binden von SSL an eine URL-Reservierung für Reporting Services  
 In den folgenden Schritten wird nicht erläutert, wie Sie Zertifikate anfordern, generieren, herunterladen oder installieren. Sie müssen bereits ein Zertifakt installiert haben, das verwendet werden kann. Es bleibt Ihnen überlassen, welche Zertifikatseigenschaften Sie angeben, welche Zertifizierungsstelle Sie verwenden und mit welchen Tools und Hilfsprogrammen Sie das Zertifikat anfordern und installieren.  
  
 Sie können das Zertifikat mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool binden. Wenn das Zertifikat im lokalen Computerspeicher korrekt installiert ist, wird es vom [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool erkannt und in der Liste **SSL-Zertifikate** auf den Seiten **Webdienst-URL** und **Report-Manager-URL** angezeigt.  
  
### <a name="to-configure-a-report-server-url-for-ssl"></a>So konfigurieren Sie eine Berichtsserver-URL für SSL  
  
1.  Starten Sie das Reporting Services-Konfigurationstool, und stellen Sie eine Verbindung mit dem Berichtsserver her.  
  
2.  Klicken Sie auf **Webdienst-URL**.  
  
3.  Erweitern Sie die Liste der SSL-Zertifikate. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] erkennt Serverauthentifizierungszertifikate im lokalen Speicher. Wenn Sie ein Zertifikat installiert haben, das in der Liste nicht angezeigt wird, müssen Sie den Dienst eventuell neu starten. Verwenden Sie die Schaltflächen **Stopp** und **Start** auf der Seite **Berichtsserverstatus** im Konfigurationstool für die Reporting Services, um den Dienst neu zu starten.  
  
4.  Wählen Sie das Zertifikat aus.  
  
5.  Klicken Sie auf **Anwenden**.  
  
6.  Klicken Sie auf die URL, um zu überprüfen, ob sie funktioniert.  
  
 Damit Sie die URL testen können, muss die Berichtsserverdatenbank konfiguriert sein. Erstellen Sie gegebenenfalls die Berichtsserverdatenbank, bevor Sie die URL testen.  
  
 URL-Reservierungen für den Berichts-Manager und den Berichtsserver-Webdienst werden unabhängig konfiguriert. Wenn Sie auch den Zugriff des Berichts-Managers über einen SSL-verschlüsselten Kanal konfigurieren möchten, fahren Sie mit den folgenden Schritten fort:  
  
1.  Klicken Sie auf **Berichts-Manager-URL**.  
  
2.  Klicken Sie auf **Erweitert**.  
  
3.  Klicken Sie unter **Mehrere SSL-Identitäten für Berichts-Manager**auf **Hinzufügen**.  
  
4.  Wählen Sie das gewünschte Zertifikat, klicken Sie auf **OK**, und klicken Sie dann auf **Anwenden**.  
  
5.  Klicken Sie auf die URL, um zu überprüfen, ob sie funktioniert.  
  
## <a name="how-certificate-bindings-are-stored"></a>Speichern von Zertifikatsbindungen  
 Zertifikatsbindungen werden in HTTP.SYS gespeichert. Eine Darstellung der definierten Bindungen wird auch im Abschnitt **URLReservations** der Datei RSReportServer.config gespeichert. Die Einstellungen in der Konfigurationsdatei sind nur eine Darstellung der tatsächlichen, an anderer Stelle gespeicherten Werte. Ändern Sie die Werte in der Konfigurationsdatei nicht direkt. Die Konfigurationseinstellungen werden in der Datei erst angezeigt, wenn Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool oder den Berichtsserver-WMI-Anbieter (Windows Management Instrumentation) verwenden, um ein Zertifikat zu binden.  
  
> [!NOTE]  
>  Wenn Sie eine Bindung mit einem SSL-Zertifikat in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] konfigurieren und das Zertifikat später von dem Computer entfernen möchten, müssen Sie sicherstellen, dass Sie die Bindung aus [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] entfernen, bevor Sie das Zertifikat vom Computer entfernen. Anderenfalls können Sie die Bindung mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool oder WMI nicht mehr entfernen, und die Fehlermeldung "Ungültiger Parameter" wird angezeigt. Wenn Sie das Zertifikat bereits vom Computer entfernt haben, können Sie das Tool Httpcfg.exe verwenden, um die Bindung aus HTTP.SYS zu entfernen. Weitere Informationen zu Httpcfg.exe finden Sie in der Windows-Produktdokumentation.  
  
 SSL-Bindungen stellen in Microsoft Windows eine freigegebene Ressource dar. Die vom Konfigurations-Manager für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] oder anderen Tools wie IIS-Manager vorgenommenen Änderungen können sich auf andere Anwendungen auf demselben Computer auswirken. Es empfiehlt sich, zum Bearbeiten von Bindungen dasselbe Tool zu verwenden, mit dem Sie die Bindungen erstellt haben.  Wenn Sie SSL-Bindungen beispielsweise mit dem Konfigurations-Manager erstellt haben, empfiehlt es sich, den Lebenszyklus der Bindungen mit dem Konfigurations-Manager zu verwalten. Wenn Sie Bindungen mit dem IIS-Manager erstellt haben, empfiehlt es sich, den Lebenszyklus der Bindungen mit dem IIS-Manager zu verwalten. Wenn IIS vor der Installation von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf dem Computer installiert wurde, empfiehlt es sich, die SSL-Konfiguration in IIS vor der Konfiguration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]zu überprüfen.  
  
 Wenn Sie SSL-Bindungen für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] mithilfe des Konfigurations-Managers für Reporting Services entfernen, funktioniert SSL möglicherweise nicht mehr für Websites auf einem Server, auf dem Internetinformationsdienste (IIS) ausgeführt werden, bzw. auf einem anderen HTTP.SYS-Server. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] wird der folgende Registrierungsschlüssel entfernt. Zusammen mit diesem Registrierungsschlüssel wird auch die SSL-Bindung für IIS entfernt. Ohne diese Bindung wird SSL nicht für das HTTPS-Protokoll bereitgestellt. Um dieses Problem zu diagnostizieren, verwenden Sie den IIS-Manager oder das Befehlszeilen-Hilfsprogramm HTTPCFG.exe. Zur Lösung des Problems stellen Sie die SSL-Bindung für die Websites mithilfe des IIS-Managers wieder her. Um das Problem in Zukunft zu vermeiden, entfernen Sie die SSL-Bindungen mit dem IIS-Manager und stellen die Bindung dann mithilfe des IIS-Managers für die gewünschten Websites wieder her. Weitere Informationen finden Sie im Knowledge Base-Artikel [SSL funktioniert nach dem Entfernen einer SSL-Bindung nicht mehr (http://support.microsoft.com/kb/956209/n)](http://support.microsoft.com/kb/956209/n).  
  
## <a name="see-also"></a>Siehe auch  
 [Authentifizierung mit dem Berichtsserver](../../reporting-services/security/authentication-with-the-report-server.md)   
 [Konfigurieren und Verwalten eines Berichtsservers &#40;einheitlicher SSRS-Modus&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Konfigurieren von Berichtsserver-URLs &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
