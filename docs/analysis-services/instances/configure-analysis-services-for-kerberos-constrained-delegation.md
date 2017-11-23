---
title: "Analysis Services für die eingeschränkte Kerberos-Delegierung konfigurieren | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6d751477-6bf1-48b4-8833-5a631bbe7650
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 60e56d6d5643afee56cf5d30a548a90ebd5ff7f1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configure-analysis-services-for-kerberos-constrained-delegation"></a>Konfigurieren von Analysis Services für die eingeschränkte Kerberos-Delegierung
  Wenn Sie Analysis Services für die Kerberos-Authentifizierung konfigurieren, verfolgen Sie damit wahrscheinlich eines oder beide der folgenden Ziele: Analysis Services soll bei der Abfrage von Daten eine Benutzeridentität annehmen, oder eine Benutzeridentität soll von Analysis Services an einen untergeordneten Dienst delegiert werden. Für die Szenarien gelten leicht abweichende Konfigurationsanforderungen. Bei beiden Szenarien muss überprüft werden, ob die Konfiguration ordnungsgemäß ausgeführt wurde.  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos-Konfigurations-Manager für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** ist ein Diagnosetool zur Behebung Kerberos-bezogener Verbindungsprobleme bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [Microsoft Kerberos-Konfigurations-Manager für SQL Server](http://www.microsoft.com/download/details.aspx?id=39046).  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Zulassen, dass Analysis Services eine Benutzeridentität annimmt](#bkmk_impersonate)  
  
-   [Konfigurieren von Analysis Services für die vertrauenswürdige Delegierung](#bkmk_delegate)  
  
-   [Prüfen, ob eine Identität angenommen oder delegiert wurde](#bkmk_test)  
  
> [!NOTE]  
>  Die Delegierung ist nicht erforderlich, wenn die Verbindung mit Analysis Services eine Single-Hop-Verbindung ist oder wenn die Lösung gespeicherte Anmeldeinformationen verwendet, die von SharePoint "Einmaliges Anmelden" oder Reporting Services bereitgestellt werden. Wenn alle Verbindungen direkte Verbindungen von Excel mit einer Analysis Services-Datenbank sind oder auf gespeicherten Anmeldeinformationen basieren, können Sie Kerberos (oder NTLM) verwenden, ohne eine eingeschränkte Delegierung konfigurieren zu müssen.  
>   
>  Die eingeschränkte Kerberos-Delegierung ist erforderlich, wenn die Benutzeridentität über mehrere Computerverbindungen verwendet werden muss (auch bekannt als "Doppelhop"). Wenn der Analysis Services-Datenzugriff von der Benutzeridentität abhängig ist und die Verbindungsanforderung von einem delegierenden Dienst stammt, verwenden Sie die Checkliste im nächsten Abschnitt, um sicherzustellen, dass Analysis Services die Identität des ursprünglichen Aufrufers annehmen kann. Weitere Informationen zu Analysis Services-Authentifizierungsabläufen finden Sie unter [Microsoft BI-Authentifizierung und Identitätsdelegierung](http://go.microsoft.com/fwlink/?LinkID=286576).  
>   
>  Als bewährte Sicherheitsmethode empfiehlt Microsoft immer eher die eingeschränkte als die uneingeschränkte Delegierung. Die uneingeschränkte Delegierung ist ein großes Sicherheitsrisiko, da sie der Dienstidentität ermöglicht, die Identität eines anderen Benutzers auf *beliebigen* Downstreamcomputern, -diensten oder -anwendungen zu übernehmen (im Gegensatz zu nur den Diensten, die über eine eingeschränkte Delegierung ausdrücklich definiert werden).  
  
##  <a name="bkmk_impersonate"></a> Zulassen, dass Analysis Services eine Benutzeridentität annimmt  
 Um übergeordneten Diensten wie Reporting Services, IIS oder SharePoint zu ermöglichen, eine Benutzeridentität für Analysis Services anzunehmen, müssen Sie die eingeschränkte Kerberos-Delegierung für diese Dienste konfigurieren. In diesem Szenario nimmt Analysis Services die Identität des aktuellen Benutzers an, indem die vom delegierenden Dienst bereitgestellte Identität angenommen wird. Die daraufhin zurückgegebenen Ergebnisse basieren auf der Rollenmitgliedschaft dieser Benutzeridentität.  
  
|Task|Description|  
|----------|-----------------|  
|Schritt 1: Überprüfen, ob die Konten für die Delegierung geeignet sind|Stellen Sie sicher, dass die Konten, unter denen Sie die Dienste ausführen, über die entsprechenden Eigenschaften in Active Directory verfügen. Dienstkonten in Active Directory dürfen nicht als vertrauliche Konten gekennzeichnet oder ausdrücklich aus Delegierungsszenarien ausgeschlossen werden. Weitere Informationen finden Sie unter [Grundlegendes zu Benutzerkonten](http://go.microsoft.com/fwlink/?LinkId=235818).<br /><br /> Hinweis: Im Allgemeinen müssen alle Konten und Server derselben Active Directory-Domäne oder vertrauenswürdigen Domänen in derselben Gesamtstruktur angehören. Da Windows Server 2012 jedoch die Delegierung über Domänengrenzen hinweg unterstützt, können Sie eingeschränkte Kerberos-Delegierung über eine Domänengrenze hinweg konfigurieren, wenn die Domänenfunktionsebene Windows Server 2012 ist. Eine andere Möglichkeit besteht darin, Analysis Services für den HTTP-Zugriff zu konfigurieren und IIS-Authentifizierungsmethoden für die Clientverbindung zu verwenden. Weitere Informationen finden Sie unter [Konfigurieren von HTTP-Zugriff auf Analysis Services unter Internetinformationsdienste &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).|  
|Schritt 2: Registrieren des SPN|Vor dem Einrichten der eingeschränkten Delegierung müssen Sie einen Dienstprinzipalnamen (SPN) für die Analysis Services-Instanz registrieren. Sie benötigen den Analysis Services-SPN, wenn Sie die eingeschränkte Kerberos-Delegierung für Dienste der mittleren Ebene konfigurieren. Anweisungen dazu finden Sie unter [SPN registration for an Analysis Services instance](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md) .<br /><br /> Ein Dienstprinzipalname (Service Principal Name, SPN) gibt die eindeutige Identität eines Diensts in einer Domäne an, die für die Kerberos-Authentifizierung konfiguriert wurde. Clientverbindungen mit integrierter Sicherheit erfordern im Rahmen der SSPI-Authentifizierung häufig einen SPN. Die Anforderung wird an einen Active Directory-Domänencontroller (DC) weitergeleitet. Dabei stellt KDC ein Ticket bereit, wenn für den vom Client angegebenen SPN in Active Directory eine entsprechende SPN-Registrierung vorhanden ist.|  
|Schritt 3: Konfigurieren der eingeschränkten Delegierung|Nachdem Sie die zu verwendenden Konten überprüft und SPNs dafür registriert haben, konfigurieren Sie im nächsten Schritt übergeordnete Dienste wie IIS, Reporting Services oder SharePoint-Webdienste für die eingeschränkte Delegierung, und geben Sie dabei die Analysis Services-SPN als spezifischen Dienst an, für den die Delegierung erlaubt ist.<br /><br /> Unter SharePoint ausgeführte Dienste wie Excel Services oder Reporting Services im SharePoint-Modus hosten häufig Arbeitsmappen und Berichte, die mehrdimensionale oder tabellarische Analysis Services-Daten nutzen. Die Konfiguration der eingeschränkten Delegierung für diese Dienste ist eine allgemeine Konfigurationsaufgabe, die ausgeführt werden muss, damit die Datenaktualisierung von Excel Services unterstützt wird. Über die folgenden Links erhalten Sie Anweisungen für SharePoint Services und andere Dienste, die Downstream-Verbindungsanforderungen für Analysis Services-Daten ausgeben können:<br /><br /> [Identitätsdelegierung für Excel Services (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=299826) oder [Konfigurieren von Excel Services in SharePoint Server 2010 für Kerberos-Authentifizierung](http://support.microsoft.com/kb/2466519)<br /><br /> [Identitätsdelegierung für PerformancePoint-Dienste (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=299827)<br /><br /> [Identitätsdelegierung für SQL Server Reporting Services (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=299828)<br /><br /> Informationen zu IIS 7.0 finden Sie unter [Konfigurieren der Windows-Authentifizierung (IIS 7.0)](http://technet.microsoft.com/library/cc754628\(v=ws.10\).aspx) oder [Konfigurieren von SQL Server 2008 Analysis Services und SQL Server 2005 Analysis Services, um Kerberos-Authentifizierung zu verwenden](http://support.microsoft.com/kb/917409).|  
|Schritt 4: Testen von Verbindungen|Stellen Sie beim Testen Verbindungen von Remotecomputern unter verschiedenen Identitäten her, und fragen Sie Analysis Services mit den gleichen Anwendungen ab, die von Benutzern im geschäftlichen Bereich verwendet werden. Mithilfe von SQL Server Profiler können Sie die Verbindung überwachen. Die Benutzeridentität für die Anforderung sollte angezeigt werden. Weitere Informationen finden Sie unter [Prüfen, ob eine Identität angenommen oder delegiert wurde](#bkmk_test) in diesem Abschnitt.|  
  
##  <a name="bkmk_delegate"></a> Konfigurieren von Analysis Services für die vertrauenswürdige Delegierung  
 Indem Sie Analysis Services für die eingeschränkte Kerberos-Delegierung konfigurieren, ermöglichen Sie dem Dienst, eine Clientidentität für einen untergeordneten Dienst, z. B. das relationale Datenbankmodul, anzunehmen. Daraufhin können die Daten so abgefragt werden, als wäre der Client direkt verbunden.  
  
 Delegierungsszenarien für Analysis Services sind auf tabellarische Modelle beschränkt, die für den **DirectQuery** -Modus konfiguriert sind. Dies ist das einzige Szenario, bei dem Analysis Services delegierte Anmeldeinformationen an einen anderen Dienst übergeben kann. In allen anderen Szenarien wie den im vorherigen Abschnitt erwähnten SharePoint-Szenarien ist Analysis Services am empfangenden Ende der Delegierungskette. Weitere Informationen zu DirectQuery finden Sie unter [DirectQuery-Modus &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).  
  
> [!NOTE]  
>  Ein typisches Missverständnis ist, dass ROLAP-Speicher, -Verarbeitungsvorgänge oder -Zugriff auf Remotepartitionen auf irgendeine Weise eine eingeschränkte Delegierung erforderlich machen. Das ist nicht der Fall. Alle diese Vorgänge werden direkt vom Dienstkonto (das auch als Verarbeitungskonto bezeichnet wird) im eigenen Namen ausgeführt. Die Delegierung ist für diese Vorgänge in Analysis Services nicht erforderlich, da die Berechtigungen für solche Vorgänge direkt dem Dienstkonto gewährt werden (beispielsweise das Gewähren der db_datareader-Berechtigungen für die relationale Datenbank, damit der Dienst Daten verarbeiten kann). Weitere Informationen zu Servervorgängen und -berechtigungen finden Sie unter [Konfigurieren von Dienstkonten &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md).  
  
 In diesem Abschnitt wird erläutert, wie Sie Analysis Services für die vertrauenswürdige Delegierung einrichten. Nachdem Sie diese Aufgabe abgeschlossen haben, kann Analysis Services delegierte Anmeldeinformationen zur Unterstützung des in tabellarischen Lösungen verwendeten DirectQuery-Modus an SQL Server übergeben.  
  
 Vorbereitungen:  
  
-   Überprüfen Sie, ob Analysis Services gestartet wurde.  
  
-   Überprüfen Sie, ob der für Analysis Services registrierte SPN gültig ist. Anweisungen finden Sie unter [SPN registration for an Analysis Services instance](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md).  
  
 Wenn beide Voraussetzungen erfüllt sind, fahren Sie mit den folgenden Schritten fort. Beachten Sie, dass Sie Domänenadministrator sein müssen, um die eingeschränkte Delegierung einzurichten.  
  
1.  Suchen Sie unter Active Directory-Benutzer und -Computer das Dienstkonto, unter dem Analysis Services ausgeführt wird. Klicken Sie mit der rechten Maustaste auf das Dienstkonto, und wählen Sie **Eigenschaften**aus.  
  
     Zur Veranschaulichung werden in den folgenden Screenshots "OlapSvc" und "SQLSvc" verwendet, um Analysis Services und SQL Server darzustellen.  
  
     "OlapSvc" ist das Konto, das für die eingeschränkte Delegierung an "SQLSvc" konfiguriert wird. Nachdem Sie diese Aufgabe abgeschlossen haben, ist "OlapSvc" berechtigt, delegierte Anmeldeinformationen für ein Dienstticket an "SQLSvc" zu übergeben. Dadurch wird beim Anfordern von Daten die Identität des ursprünglichen Aufrufers angenommen.  
  
2.  Wählen Sie auf der Registerkarte Delegierung die Option **Benutzer bei Delegierungen angegebener Dienste vertrauen**und dann **Nur Kerberos verwenden**aus. Klicken Sie auf **Hinzufügen** , um anzugeben, an welchen Dienst Anmeldeinformationen von Analysis Services delegiert werden dürfen.  
  
     Die Registerkarte Delegierung wird nur angezeigt, wenn das Dienstkonto (OlapSvc) einem Dienst (Analysis Services) zugewiesen ist und für den Dienst ein SPN registriert wurde. Die SPN-Registrierung setzt voraus, dass der Dienst ausgeführt wird.  
  
     ![SSAS_Kerberos_1_AccountProperties](../../analysis-services/instances/media/ssas-kerberos-1-accountproperties.gif "SSAS_Kerberos_1_AccountProperties")  
  
3.  Klicken Sie auf der Seite Dienste hinzufügen auf **Benutzer oder Computer**.  
  
     ![SSAS_Kerberos_2_](../../analysis-services/instances/media/ssas-kerberos-2.gif "SSAS_Kerberos_2_")  
  
4.  Geben Sie auf der Seite zum Auswählen von Benutzern oder Computern das Konto ein, das zur Ausführung der SQL Server-Instanz verwendet wird, die Daten für tabellarische Analysis Services-Modelldatenbanken bereitstellt. Klicken Sie auf **OK** , um das Dienstkonto zu übernehmen.  
  
     Wenn Sie das gewünschte Konto nicht auswählen können, überprüfen Sie, ob SQL Server ausgeführt wird und ob ein SPN für das Konto registriert wurde. Weitere Informationen zu SPNs für das Datenbankmodul finden Sie unter [Register a Service Principal Name for Kerberos Connections](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  
  
     ![SSAS_Kerberos_3_SelectUsers](../../analysis-services/instances/media/ssas-kerberos-3-selectusers.gif "SSAS_Kerberos_3_SelectUsers")  
  
5.  Die SQL Server-Instanz sollte jetzt in Dienste hinzufügen angezeigt werden. Darüber hinaus wird jeder Dienst, der dieses Konto verwendet, in der Liste angezeigt. Wählen Sie die SQL Server-Instanz aus, die Sie verwenden möchten. Klicken Sie auf **OK** , um die Instanz zu übernehmen.  
  
     ![SSAS_Kerberos_4_](../../analysis-services/instances/media/ssas-kerberos-4.gif "SSAS_Kerberos_4_")  
  
6.  Die Eigenschaftenseite des Analysis Services-Dienstkontos sollte jetzt dem folgenden Screenshot entsprechen. Klicken Sie auf **OK** , um die Änderungen zu speichern.  
  
     ![SSAS_Kerberos_5_Finished](../../analysis-services/instances/media/ssas-kerberos-5-finished.gif "SSAS_Kerberos_5_Finished")  
  
7.  Überprüfen Sie, ob die Delegierung erfolgreich war, indem Sie vom Remoteclientcomputer unter einer anderen Identität eine Verbindung herstellen und eine Abfrage an das tabellarische Modell senden. Die Benutzeridentität für die Anforderung sollte im SQL Server Profiler angezeigt werden.  
  
##  <a name="bkmk_test"></a> Prüfen, ob eine Identität angenommen oder delegiert wurde  
 Überwachen Sie mit SQL Server Profiler die Identität des Benutzers, der die Daten abfragt.  
  
1.  Starten Sie erst **SQL Server Profiler** für die Analysis Services-Instanz und dann eine neue Ablaufverfolgung.  
  
2.  Überprüfen Sie in der Ereignisauswahl, ob **Audit Login** und **Audit Logout** im Abschnitt Sicherheitsüberwachung aktiviert sind.  
  
3.  Stellen Sie von einem Remoteclientcomputer über einen Anwendungsdienst (z. B. SharePoint oder Reporting Services) eine Verbindung mit Analysis Services her. Das Audit Login-Ereignis zeigt die Identität des Benutzers an, der eine Verbindung mit Analysis Services herstellt.  
  
 Gründliche Tests erfordern den Einsatz von Netzwerküberwachungstools, die Kerberos-Anforderungen und -Antworten im Netzwerk erfassen können. Für diese Aufgabe kann das Netzwerkmonitor-Hilfsprogramm (netmon.exe) mit Kerberos-Filter verwendet werden. Weitere Informationen zur Verwendung von Netmon 3.4 und anderen Tools zum Testen der Kerberos-Authentifizierung finden Sie unter [Konfigurieren der Kerberos-Authentifizierung: Kernkonfiguration (SharePoint Server 2010)](http://technet.microsoft.com/library/gg502602\(v=office.14\).aspx).  
  
 Eine ausführliche Beschreibung der einzelnen Optionen auf der Registerkarte "Delegierung" des Active Directory-Dialogfelds mit den Objekteigenschaften finden Sie unter [Das komplizierteste Dialogfeld Active Directory](http://windowsitpro.com/windows/most-confusing-dialog-box-active-directory) . In diesem Artikel wird auch erläutert, wie Sie LDP zum Testen und Interpretieren der Testergebnisse verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft-BI-Authentifizierung und Identitätsdelegierung](http://go.microsoft.com/fwlink/?LinkID=286576)   
 [Gegenseitige Authentifizierung mithilfe von Kerberos](http://go.microsoft.com/fwlink/?LinkId=299283)   
 [Verbindung mit Analysis Services herstellen](../../analysis-services/instances/connect-to-analysis-services.md)   
 [SPN-Registrierung für Analysis Services-Instanz](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)   
 [Verbindungszeichenfolgen-Eigenschaften &#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)  
  
  
