---
title: Konfigurieren eines Berichtsservers in einem Netzwerklastenausgleichcluster | Microsoft-Dokumentation
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
helpviewer_keywords: report servers [Reporting Services], network load balancing
ms.assetid: 6bfa5698-de65-43c3-b940-044f41c162d3
caps.latest.revision: "10"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: cd081a235bf3a816c211f7a94dd122fc3cf01bf0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="configure-a-report-server-on-a-network-load-balancing-cluster"></a>Konfigurieren eines Berichtsservers in einem NLB-Cluster (Network Load Balancing, Netzwerklastenausgleich)
  Wenn Sie einen Berichtsserver für horizontales Skalieren für die Ausführung in einem NLB-Cluster (Network Load Balancing, Netzwerklastenausgleich) konfigurieren möchten, müssen Sie folgende Schritte ausführen:  
  
-   Stellen Sie sicher, dass der Zugriff auf den NLB-Cluster über den Namen eines virtuellen Servers möglich ist, der der IP-Adresse des virtuellen Servers zugeordnet ist. Der Name eines virtuellen Servers ist erforderlich, damit Sie einen einzelnen Zugriffspunkt für den NLB-Cluster konfigurieren können. Wenn Sie für jede Berichtsserverinstanz eine URL konfigurieren, geben Sie den Namen des virtuellen Servers als Host an.  
  
-   Konfigurieren Sie die Anzeigestatusüberprüfung, um das Anzeigen interaktiver Berichte zu unterstützen. Interaktive Berichte werden i. d. R. in einer Benutzersitzung mehrfach gerendert, um als Reaktion auf Benutzeraktionen neue oder andere Daten anzuzeigen. Durch das Konfigurieren der Anzeigestatusüberprüfung wird die Kontinuität in Benutzersitzungen unabhängig davon gewahrt, welcher Berichtsserver die Anforderung tatsächlich bearbeitet.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] bietet keine Funktionalität für den Lastenausgleich einer Bereitstellung für horizontales Skalieren oder zum Definieren eines einzelnen Zugriffspunkts über eine freigegebene URL. Sie müssen eine separate Software oder eine Hardware-NLB-Clusterlösung implementieren, um eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bereitstellung für horizontales Skalieren zu unterstützen.  
  
 Sie können [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf Knoten installieren, die bereits zu einem NLB-Cluster gehören, oder Sie können eine Bereitstellung für horizontales Skalieren konfigurieren und anschließend die Clustersoftware installieren.  
  
## <a name="steps-for-report-server-deployment-on-an-nlb-cluster"></a>Schritte zur Berichtsserverbereitstellung in einem NLB-Cluster  
 Beachten Sie beim Installieren und Konfigurieren der Bereitstellung die folgenden Richtlinien:  
  
|Schritt|Description|Weitere Informationen|  
|----------|-----------------|----------------------|  
|1|Überprüfen Sie vor der Installation von Reporting Services auf Serverknoten in einem NLB-Cluster die Anforderungen für die Bereitstellung für horizontales Skalieren.|[Bereitstellung für horizontales Skalieren (Berichtsserver im einheitlichen Modus)](http://msdn.microsoft.com/library/4df38294-6f9d-4b40-9f03-1f01c1f0700c) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation|  
|2|Konfigurieren Sie den NLB-Cluster, und überprüfen Sie, ob er ordnungsgemäß arbeitet.<br /><br /> Ordnen Sie unbedingt der virtuellen Server-IP-Adresse des NLB-Clusters einen Hostheadernamen zu. Der Hostheadername wird in der Berichtsserver-URL verwendet, und er ist leichter zu behalten als eine IP-Adresse.|Weitere Informationen finden Sie in der Windows Server-Produktdokumentation für die Version des verwendeten Windows-Betriebssystems.|  
|3|Fügen Sie den NetBIOS-Namen und den vollqualifizierten Domänennamen (Fully Qualified Domain Name oder FQDN) für den Hostheader der in der Windows-Registrierung gespeicherten Liste **BackConnectionHostNames** hinzu. Führen Sie die Schritte in **Methode 2: Angeben von Hostnamen** im [Knowledge Base-Artikel 896861](http://support.microsoft.com/kb/896861) (http://support.microsoft.com/kb/896861), mit der folgenden Anpassung aus. **Schritt 7** des Knowledge Base-Artikels lautet wie folgt: "Beenden Sie den Registrierungs-Editor, und starten Sie den IISAdmin-Dienst anschließend neu." Starten Sie stattdessen den Computer neu, damit die Änderungen wirksam werden.<br /><br /> Wenn z.B. der Hostheadername \<MyServer> ein virtueller Name für den Windows-Computernamen „contoso“ ist, können Sie wahrscheinlich mit „contoso.domain.com“ auf das FQDN-Formular verweisen. Sie müssen sowohl den Hostheadernamen (MyServer ) als auch den FQDN-Namen (contoso.domain.com) zur Liste in **BackConnectionHostNames**hinzufügen.|Dieser Schritt ist erforderlich, wenn Ihre Serverumgebung die NTLM-Authentifizierung auf dem lokalen Computer verwendet und eine Loopbackverbindung erstellt.<br /><br /> In diesem Fall tritt bei Anforderungen zwischen dem Berichts-Manager und dem Berichtsserver der Fehler 401 (Nicht autorisiert) auf.|  
|4|Installieren Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im Dateimodus auf Knoten, die bereits zu einem NLB-Cluster gehören, oder konfigurieren Sie die Berichtsserverinstanzen für die Bereitstellung für horizontales Skalieren.<br /><br /> Die konfigurierte Bereitstellung für horizontales Skalieren antwortet möglicherweise nicht auf Anforderungen, die an die IP des virtuellen Servers gerichtet sind. Sie wird erst in einem späteren Schritt so konfiguriert, dass die IP des virtuellen Servers verwendet wird, und zwar nach dem Konfigurieren der Anzeigestatusüberprüfung.|[Konfigurieren eines Berichtsservers im einheitlichen Modus für Bereitstellungen für horizontales Skalieren &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)|  
|5|Konfigurieren der Anzeigestatusüberprüfung<br /><br /> Optimale Ergebnisse erzielen Sie, wenn Sie diesen Schritt nach dem Konfigurieren der Bereitstellung für horizontales Skalieren und vor dem Konfigurieren der Berichtsserverinstanzen für die Verwendung der virtuellen Server-IP-Adresse ausführen. Indem Sie zuerst die Anzeigestatusüberprüfung konfigurieren, können Sie Ausnahmen für fehlgeschlagene Statusüberprüfungen vermeiden, wenn Benutzer versuchen, auf interaktive Berichte zuzugreifen.|[Vorgehensweise: Konfigurieren der Anzeigestatusüberprüfung](#ViewState) in diesem Thema|  
|6|Konfigurieren Sie **Hostname** und **UrlRoot** so, dass die IP des virtuellen Servers des NLB-Clusters verwendet wird.|[So konfigurieren Sie HostName und UrlRoot](#SpecifyingVirtualServerName) in diesem Thema.|  
|7|Überprüfen Sie, ob der Zugriff auf die Server mit dem angegebenen Hostnamen möglich ist.|[Überprüfen des Zugriffs auf Berichtsserver](#Verify) in diesem Thema.|  
  
##  <a name="ViewState"></a> Vorgehensweise: Konfigurieren der Anzeigestatusüberprüfung  
 Zum Ausführen einer Bereitstellung für horizontales Skalieren in einem NLB-Cluster müssen Sie die Anzeigestatusüberprüfung konfigurieren, sodass Benutzer interaktive HTML-Berichte anzeigen können. Sie müssen dies für den Berichtsserver und den Berichts-Manager ausführen.  
  
 Die Anzeigestatusüberprüfung wird von ASP.NET gesteuert. Sie ist standardmäßig aktiviert und verwendet die Identitätsinformationen des Webdiensts zum Ausführen der Überprüfung. In einem Szenario mit NLB-Cluster sind jedoch mehrere Dienstinstanzen und Webdienstidentitäten, die auf unterschiedlichen Computern ausgeführt werden, vorhanden. Da die Dienstidentität von Knoten zu Knoten variiert, können Sie die Überprüfung nicht nur anhand einer einzigen Prozessidentität ausführen.  
  
 Zum Umgehen dieses Problems können Sie einen willkürlichen Validierungsschlüssel generieren, um die Anzeigestatusüberprüfung zu unterstützen, und anschließend jeden Berichtsserverknoten zum Verwenden desselben Schlüssels manuell konfigurieren. Sie können eine beliebige nach dem Zufallsprinzip generierte hexadezimale Sequenz verwenden. Der Überprüfungsalgorithmus (z. B. SHA1) bestimmt, wie lang die hexadezimale Sequenz sein muss.  
  
1.  Generieren Sie mithilfe der von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]bereitgestellten Funktionalität zum automatischen Generieren einen Überprüfungsschlüssel und einen Entschlüsselungsschlüssel. Letztlich benötigen Sie einen einzigen \<**machineKey**>-Eintrag, den Sie für jede Berichts-Manager-Instanz in der Bereitstellung für horizontales Skalieren in die Datei „Web.config“ einfügen können.  
  
     Das folgende Beispiel zeigt den Wert, den Sie benötigen. Kopieren Sie das Beispiel nicht in die Konfigurationsdateien, denn die Schlüsselwerte sind ungültig.  
  
    ```  
    <machineKey validationKey="123455555" decryptionKey="678999999" validation="SHA1" decryption="AES"/>  
    ```  
  
2.  Öffnen Sie die Datei „Web.config“ für den Berichts-Manager, und fügen Sie im Abschnitt \<**system.web**> das \<**machineKey**>-Element ein, das Sie generiert haben. Standardmäßig befindet sich die Datei Web.config für den Berichts-Manager unter \Programme\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportManager\Web.config.  
  
3.  Speichern Sie die Datei.  
  
4.  Wiederholen Sie den vorherigen Schritt für alle Berichtsserver in der Bereitstellung für horizontales Skalieren.  
  
5.  Überprüfen Sie, ob alle „Web.Config“-Dateien in den \Reporting Services\Report Manager-Ordnern identische \<**machineKey**>-Elemente im Abschnitt \<**system.web**> enthalten.  
  
##  <a name="SpecifyingVirtualServerName"></a> So konfigurieren Sie HostName und UrlRoot  
 Wenn Sie eine Berichtsserverbereitstellung für horizontales Skalieren in einem NLB-Cluster konfigurieren möchten, müssen Sie den Namen eines einzelnen virtuellen Servers definieren, der einen einzelnen Zugriffspunkt für den Servercluster bietet. Registrieren Sie den Namen dieses virtuellen Servers dann beim DNS-Server in der Umgebung.  
  
 Nachdem Sie den Namen des virtuellen Servers definiert haben, können Sie die **Hostname** -Eigenschaft und die **UrlRoot** -Eigenschaft in der Datei RSReportServer.config so konfigurieren, dass sie den Namen des virtuellen Servers in der Berichtsserver-URL enthalten.  
  
 Konfigurieren Sie die **Hostname** -Eigenschaft, wenn Sie Platzhalter-URL-Reservierungen in der Berichtsumgebung verwenden. Wenn Sie in der **Hostname** -Eigenschaft den virtuellen Servernamen des NLB-Servers angeben, dann wird der Netzwerkverkehr für die Berichtsumgebung an den NLB-Server geleitet. Der NLB verteilt die Anforderungen dann an die Berichtsserverknoten.  
  
 Konfigurieren Sie außerdem die **UrlRoot** -Eigenschaft, damit Berichtslinks in Berichten funktionieren, die in statische Berichte, z.B. in das Excel- oder PDF-Format, exportiert wurden, oder in Berichten, die von Abonnements erzeugt werden, beispielsweise E-Mail-Abonnements.  
  
 Wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 oder [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 integrieren oder Ihre Berichte in einer benutzerdefinierten Webanwendung hosten, müssen Sie unter Umständen nur die **UrlRoot** -Eigenschaft konfigurieren. In diesem Fall legen Sie die **UrlRoot** -Eigenschaft auf die URL der SharePoint-Site oder Webanwendung fest. Damit wird der Netzwerkverkehr für die Berichtsumgebung an die Anwendung geleitet, welche die Berichte handhabt, statt an den Berichtsserver oder NLB-Cluster.  
  
 Ändern Sie **ReportServerUrl**nicht. Wenn Sie diese URL ändern, führt dies dazu, dass jedes Mal, wenn eine interne Anforderungen verarbeitet wird, ein zusätzlicher Roundtrip über den virtuellen Server ausgeführt wird. Weitere Informationen zu finden Sie unter [URLs in Konfigurationsdateien (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md). Weitere Informationen zum Bearbeiten von Konfigurationsdateien finden Sie unter [Ändern einer Reporting Services-Konfigurationsdatei (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
1.  Öffnen Sie RSReportServer.config in einem Text-Editor.  
  
2.  Suchen Sie nach dem **\<Service>**-Abschnitt, und fügen Sie der Konfigurationsdatei die folgenden Informationen hinzu, womit der **Hostname**-Wert durch den Namen des virtuellen Servers für den NLB-Server ersetzt wird:  
  
    ```  
    <Hostname>virtual_server</Hostname>  
    ```  
  
3.  Suchen Sie **UrlRoot**. Das Element ist in der Konfigurationsdatei nicht angegeben, aber als Standardwert wird eine URL in folgendem Format verwendet: http:// oder `https://<computername>/<reportserver>`, wobei \<*reportserver*> der Name des virtuellen Verzeichnisses des Berichtsserver-Webdiensts ist.  
  
4.  Geben Sie für **UrlRoot** einen Wert ein, der den virtuellen Namen des Clusters im folgenden Format enthält: http:// oder `https://<virtual_server>/<reportserver>`.  
  
5.  Speichern Sie die Datei.  
  
6.  Wiederholen Sie diese Schritte jeweils in der Datei RSReportServer.config für alle Berichtsserver in der Bereitstellung für horizontales Skalieren.  
  
##  <a name="Verify"></a> Überprüfen des Zugriffs auf Berichtsserver  
 Überprüfen Sie, ob Sie auf die Bereitstellung für horizontales Skalieren über den Namen des virtuellen Servers (z.B. `https://MyVirtualServerName/reportserver` und `https://MyVirtualServerName/reports`) zugreifen können.  
  
 Sie können überprüfen, welcher Knoten tatsächlich Berichte verarbeitet, indem Sie die Berichtsserver-Protokolldateien untersuchen oder indem Sie das RS-Ausführungsprotokoll überprüfen (die Ausführungsprotokolltabelle enthält eine Spalte namens **InstanceName** , die anzeigt, welche Instanz eine bestimmte Anforderung verarbeitet hat). Weitere Informationen finden Sie unter [Reporting Services-Protokolldateien und Quellen](../../reporting-services/report-server/reporting-services-log-files-and-sources.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinebibliothek.  
  
 Wenn keine Verbindung mit dem Berichtsserver hergestellt werden kann, überprüfen Sie den NLB, um sicherzustellen, dass Anforderungen an den Berichtsserver gesendet werden, und zeigen Sie die HTTP-Protokolldatei des Berichtsservers an, um sich davon zu überzeugen, dass der Server die Anforderungen empfängt.  
  
#### <a name="troubleshooting-failed-requests"></a>Problembehandlung bei fehlgeschlagenen Anforderungen  
 Wenn Anforderungen die Berichtsserverinstanzen nicht erreichen, überprüfen Sie die Datei RSReportServer.config, um festzustellen, ob der Name des virtuellen Servers als Hostname für die Berichtsserver-URLs angegeben wurde:  
  
1.  Öffnen Sie die Datei RSReportServer.config in einem Text-Editor.  
  
2.  Suchen Sie \<**Hostname**>, \<**ReportServerUrl**>, und \<**UrlRoot**>, und überprüfen Sie den Hostnamen jeder Einstellung. Wenn der Wert nicht dem erwarteten Hostnamen entspricht, ersetzen Sie ihn durch den richtigen Hostnamen.  
  
 Wenn Sie das Reporting Services-Konfigurationstool starten, nachdem Sie diese Änderungen vorgenommen haben, ändert das Tool möglicherweise die Einstellungen für \<**ReportServerUrl**> auf den Standardwert. Bewahren Sie immer eine Sicherungskopie der Konfigurationsdateien für den Fall auf, dass Sie diese durch die Version ersetzen müssen, die die gewünschten Einstellungen enthält.  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Konfigurations-Manager &#40;einheitlicher Modus&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Konfigurieren einer URL &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Konfigurieren eines Berichtsservers im einheitlichen Modus für Bereitstellungen für horizontales Skalieren (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)   
 [Manage a Reporting Services Native Mode Report Server (Verwalten eines Berichtsservers von Reporting Services im einheitlichen Modus)](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
