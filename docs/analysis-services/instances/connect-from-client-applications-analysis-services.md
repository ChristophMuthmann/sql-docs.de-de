---
title: Herstellen einer Verbindung von Clientanwendungen (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connection.login.analysisserver.f1
- sql13.swb.connecttoas.connectionproperties.f1
- sql13.swb.connecttoas.login.f1
ms.assetid: b1e0f1d4-0b87-4ad3-8172-f746fe2f16a2
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 20302da167c1ba1d19fb1b65ab871d81f7170591
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="connect-from-client-applications-analysis-services"></a>Herstellen einer Verbindung von Clientanwendungen (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Wenn Sie mit Analysis Services nicht vertraut sind, können Sie die Informationen in diesem Thema verwenden, für die Verbindung mit einer vorhandenen Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mithilfe der gängigen Tools und Anwendungen. In diesem Thema wird auch erläutert, wie Sie zu Testzwecken eine Verbindung unter verschiedenen Benutzeridentitäten herstellen.  
  
-   [Herstellen einer Verbindung mithilfe von SQL Server Management Studio (SSMS)](#bkmk_SSMS)  
  
-   [Herstellen einer Verbindung mithilfe von Excel](#bkmk_excel)  
  
-   [Herstellen einer Verbindung mithilfe von SQL Server Data Tools](#bkmk_SSDT)  
  
-   [Testen von Verbindungen](#bkmk_tshoot)  
  
 Die Referenzdokumentation zu Verbindungszeichenfolgen wird getrennt bereitgestellt. Weitere Informationen finden Sie unter [Verbindungszeichenfolgen-Eigenschaften &#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md).  
  
 Erfolgreiche Verbindungen sind von einer gültigen Portkonfiguration und entsprechenden Benutzerberechtigungen abhängig. Klicken Sie auf die folgenden Links, um mehr über die einzelnen Anforderungen zu erfahren.  
  
-   [Konfigurieren der Windows-Firewall, um den Zugriff auf Analysis Services zuzulassen](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
  
-   [Autorisieren des Zugriffs auf Objekte und Vorgänge &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
##  <a name="bkmk_SSMS"></a> Herstellen einer Verbindung mithilfe von SQL Server Management Studio (SSMS)  
 Stellen Sie eine Verbindung mit Analysis Services in SSMS her, um Serverinstanzen und Datenbanken interaktiv zu verwalten. Sie können auch XMLA- oder MDX-Abfragen ausführen, um Verwaltungsaufgaben auszuführen oder Daten abzurufen. Im Unterschied zu anderen Tools und Anwendungen, von denen Datenbanken nur beim Senden einer Abfrage geladen werden, lädt SSMS alle Datenbanken, sobald eine Verbindung mit dem Server hergestellt wird. Dies setzt allerdings voraus, dass Sie zur Anzeige der Datenbank berechtigt sind. Wenn Sie also über viele tabellarische Datenbanken auf dem Server verfügen, werden alle Datenbanken in den Systemarbeitsspeicher geladen, sobald Sie über SSMS eine Verbindung herstellen.  
  
 Sie können Berechtigungen testen, indem Sie SSMS unter einer bestimmten Benutzeridentität ausführen und dann unter Verwendung dieser Identität eine Verbindung mit Analysis Services herstellen.  
  
 Halten Sie die UMSCHALTTASTE gedrückt, und klicken Sie mit der rechten Maustaste auf die Verknüpfung **SQL Server Management Studio** , um auf die Option **Als anderer Benutzer ausführen** zuzugreifen.  
  
1.  Starten Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Wählen Sie im Dialogfeld **Verbindung mit Server herstellen** den [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Servertyp aus.  
  
2.  Geben Sie auf der Registerkarte Anmeldung den Servernamen ein, indem Sie den Namen des Computers angeben, auf dem der Server ausgeführt wird. Sie können den Server mithilfe seines Netzwerknamens oder mithilfe eines vollqualifizierten Domänennamens angeben.  
  
     Bei einer benannten Instanz muss der Servername in folgendem Format angegeben werden: Servername\Instanzname. Ein Beispiel für diese Namenskonvention könnte ADV-SRV062-\Finance für einen Server sein, der den Netzwerknamen ADV-SRV062 hat, wo Analysis Services als benannte Instanz mit der Bezeichnung Finance installiert war.  
  
     Bei Servern, die in einem Failovercluster bereitgestellt werden, stellen Sie die Verbindung über den Netzwerknamen des SSAS-Clusters her. Dieser Name wird beim SQL Server-Setup als **Name des SQL Server-Netzwerks**angegeben. Wenn Sie SSAS als benannte Instanz auf einem Windows Server-Failovercluster (WSFC) installiert haben, wird der Instanzname der Verbindung niemals hinzugefügt. Diese Vorgehensweise ist charakteristisch für SSAS. Bei einer benannten Instanz eines gruppierten relationalen Datenbankmoduls ist der Instanzname im Gegensatz dazu enthalten. Wenn Sie z. B. sowohl SSAS als auch das Datenbankmodul als benannte Instanz (Contoso-Accounting) mit dem SQL Server-Netzwerknamen "SQL-CLU" installiert haben, würden Sie die Verbindung mit SSAS mit "SQL-CLU" und die Verbindung mit dem Datenbankmodul mit "SQL-CLU\Contoso-Accounting" herstellen. Weitere Informationen und Beispiele finden Sie unter [Verwenden von SQL Server Analysis Services in einem Cluster](http://go.microsoft.com/fwlink/p/?LinkId=396548) .  
  
     Bei Servern, die in einem Cluster mit Netzwerklastenausgleich bereitgestellt werden, stellen Sie mithilfe des virtuellen Netzwerknamens des NLB-Servers eine Verbindung her.  
  
3.  Als Authentifizierung wird immer die Windows-Authentifizierung verwendet, und die Benutzeridentität entspricht immer dem Windows-Benutzer, der über Management Studio eine Verbindung herstellt.  
  
     Damit die Verbindung erfolgreich hergestellt werden kann, müssen Sie über die Berechtigung verfügen, auf den Server oder auf eine Datenbank auf dem Server zuzugreifen. Für die meisten Aufgaben, die Sie in Management Studio ausführen, sind Administratorberechtigungen erforderlich. Stellen Sie sicher, dass das Konto, unter dem Sie eine Verbindung herstellen, Mitglied der Serveradministratorrolle ist. Weitere Informationen finden Sie unter [Erteilen von serverweiten Administratorrechten für eine Analysis Services-Instanz](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
4.  Klicken Sie auf **Verbindungseigenschaften** , um eine bestimmte Datenbank anzugeben und Timeoutwerte oder Verschlüsselungsoptionen festzulegen. Optionale Verbindungsinformationen sind Verbindungseigenschaften, die nur für die aktuelle Verbindung verwendet werden.  
  
5.  Klicken Sie auf die Registerkarte **Zusätzliche Verbindungsparameter** , um Verbindungseigenschaften festzulegen, die im Dialogfeld Verbindung mit Server herstellen nicht verfügbar sind. Beispielsweise können Sie `Roles=Reader` in das Textfeld eingeben.  
  
     Indem Sie eine Verbindung über eine Rolle mit weniger Berechtigungen herstellen, können Sie das Datenbankverhalten testen, wenn diese Rolle wirksam ist.  
  
    ```  
    Provider=MSOLAP; Data Source=SERVERNAME; Initial Catalog=AdventureWorks2012; Roles=READER  
    ```  
  
##  <a name="bkmk_excel"></a> Herstellen einer Verbindung mithilfe von Excel  
 Microsoft Excel wird häufig zum Analysieren von Geschäftsdaten verwendet. Als Bestandteil einer Excel-Installation installiert Office den OLE DB-Anbieter für Analysis Services (MSOLAP.DLL), ADOMD.NET und andere Datenanbieter, damit Sie die Daten bequemer auf Netzwerkservern verwenden können. Wenn Sie eine neuere Version von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mit einer früheren Version von Excel verwenden, müssen Sie wahrscheinlich neuere Datenanbieter auf jeder Arbeitsstation installieren, die eine Verbindung mit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]herstellt. Weitere Informationen finden Sie unter [Für Analysis Services-Verbindungen verwendete Datenanbieter](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md) .  
  
 Wenn Sie eine Verbindung mit einem Analysis Services-Cube oder einer Datenbank für tabellarische Modelle einrichten, speichert Excel die Verbindungsinformationen zur zukünftigen Verwendung in einer ODC-Datei. Die Verbindung wird im Sicherheitskontext des aktuellen Windows-Benutzers hergestellt. Das Benutzerkonto muss über Leseberechtigungen für die Datenbank verfügen, damit die Verbindung erfolgreich hergestellt werden kann.  
  
 Wenn Sie [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Daten in einer Excel-Arbeitsmappe verwenden, werden Verbindungen für die Dauer einer Abfrageanforderung aufrechterhalten. Wenn Sie die Abfragearbeitsauslastung von Excel überwachen, werden Sie daher wahrscheinlich pro Sitzung eine Vielzahl von Verbindungen sehen, die jeweils für eine sehr kurze Dauer aufrechterhalten werden.  
  
 Sie können Berechtigungen testen, indem Sie Excel unter einer bestimmten Benutzeridentität starten.  
  
 Halten Sie die UMSCHALTTASTE gedrückt, und klicken Sie mit der rechten Maustaste auf die Verknüpfung **Excel** , um auf die Option **Als anderer Benutzer ausführen** zuzugreifen.  
  
1.  Klicken Sie auf der Registerkarte **Daten**in Excel auf **Aus anderen Quellen**, und klicken Sie dann auf Von Analysis Services. Geben Sie den Servernamen ein, und wählen Sie dann einen Cube oder eine Perspektive für die Abfrage aus.  
  
     Bei Servern, die in einem Cluster mit Lastenausgleich bereitgestellt werden, verwenden Sie den Namen des virtuellen Servers, der dem Cluster zugewiesen ist.  
  
2.  Wenn Sie eine Verbindung in Excel herstellen, können Sie auf der letzten Seite des Datenverbindungs-Assistenten Authentifizierungseinstellungen für Excel Services angeben. Diese Einstellungen werden verwendet, um Eigenschaften auf der Arbeitsmappe festzulegen, wenn Sie sie auf einen SharePoint-Server hochladen sollten, der über Excel Services verfügt. Die Einstellungen werden in Datenaktualisierungsvorgängen verwendet. Zu den Optionen zählen **Windows-Authentifizierung**, **Secure Store Service (SSS)** und **Keine**.  
  
     Vermeiden Sie, **Keine**zu verwenden. Mit Analysis Services können Sie auf der Verbindungszeichenfolge weder einen Benutzernamen und noch ein Kennwort angeben, außer wenn Sie eine Verbindung mit einem Server herstellen, der für den HTTP-Zugriff konfiguriert wurde. Verwenden Sie auch nicht "SSS", außer wenn Sie bereits wissen, dass einem Satz von Windows-Benutzeranmeldeinformationen, die über Benutzerzugriff auf die Analysis Services-Datenbanken verfügen, die SSS-Zielanwendungs-ID zugeordnet ist. Für die meisten Szenarien ist die Verwendung der Standardoption für die Windows-Authentifizierung die beste Wahl für eine Analysis Services-Verbindung in Excel.  
  
 Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit oder Importieren von Daten aus SQL Server Analysis Services](http://go.microsoft.com/fwlink/?linkID=215150).  
  
##  <a name="bkmk_SSDT"></a> Herstellen einer Verbindung mithilfe von SQL Server Data Tools  
 SQL Server Data Tools wird zum Erstellen von BI-Lösungen, einschließlich Analysis Services-Modelle, Reporting Services-Berichte und SSIS-Pakete, verwendet. Beim Erstellen von Berichten oder Paketen müssen Sie möglicherweise eine Verbindung mit Analysis Services angeben.  
  
 Unter den folgenden Links wird erläutert, wie eine Verbindung mit Analysis Services aus einem Berichtsserverprojekt oder einem Integration Services-Projekt hergestellt wird:  
  
-   [Analysis Services-Verbindungstyp für MDX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)  
  
-   [Analysis Services-Verbindungs-Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
> [!NOTE]  
>  Bei der Bearbeitung eines vorhandenen Analysis Services-Projekts mit SQL Server Data Tools sollten Sie beachten, dass Sie mit einem lokalen Projekt bzw. einem Projekt, das der Versionskontrolle unterliegt, eine Offlineverbindung herstellen können. Alternativ können Sie eine Verbindung im Onlinemodus herstellen, um Analysis Services-Objekte bei laufender Datenbank zu aktualisieren. Weitere Informationen finden Sie unter [Connect in Online Mode to an Analysis Services Database](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md). Im Allgemeinen befinden sich Verbindungen von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] im Projektmodus, in dem Änderungen nur für die Datenbank bereitgestellt werden, wenn Sie das Projekt explizit bereitstellen.  
  
##  <a name="bkmk_tshoot"></a> Testen von Verbindungen  
 Mithilfe von SQL Server Profiler können Sie Verbindungen mit Analysis Services überwachen. Die Ereignisse Audit Login und Audit Logout liefern Details zu einer Verbindung. In der Identitätsspalte ist der Sicherheitskontext angegeben, unter dem die Verbindung hergestellt wird.  
  
1.  Starten Sie erst **SQL Server Profiler** für die Analysis Services-Instanz und dann eine neue Ablaufverfolgung.  
  
2.  Überprüfen Sie in der Ereignisauswahl, ob **Audit Login** und **Audit Logout** im Abschnitt Sicherheitsüberwachung aktiviert sind.  
  
3.  Stellen Sie von einem Remoteclientcomputer über einen Anwendungsdienst (z. B. SharePoint oder Reporting Services) eine Verbindung mit Analysis Services her. Das Audit Login-Ereignis zeigt die Identität des Benutzers an, der eine Verbindung mit Analysis Services herstellt.  
  
 Verbindungsfehler sind häufig auf eine unvollständige oder ungültige Serverkonfiguration zurückzuführen. Überprüfen Sie zunächst immer die Serverkonfiguration:  
  
-   Pingen Sie den Server von einem Remotecomputer, um sicherzustellen, dass er Remoteverbindungen zulässt.  
  
-   **Firewallregeln auf dem Server lassen eingehende Verbindungen von Clients in derselben Domäne zu**  
  
     Mit Ausnahme von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint ist für alle Verbindungen mit einem Remoteserver die Konfiguration der Firewall erforderlich, sodass der Zugriff auf den Port möglich ist, an dem von Analysis Services gelauscht wird. Wenn Verbindungsfehler angezeigt werden, überprüfen Sie, ob auf den Port zugegriffen werden kann und dass Benutzerberechtigungen den entsprechenden Datenbanken zugeordnet sind.  
  
     Verwenden Sie zum Testen Excel oder SSMS auf einem Remotecomputer, und geben Sie die IP-Adresse und den Port an, die von der Analysis Services-Instanz verwendet werden. Wenn Sie eine Verbindung herstellen können, sind die Firewallregeln für die Instanz gültig, und die Instanz lässt Remoteverbindungen zu.  
  
     Wenn Sie TCP/IP für das Verbindungsprotokoll verwenden, sollten Sie zusätzlich beachten, dass für Analysis Services Clientverbindungen erforderlich sind, die von derselben Domäne oder einer vertrauenswürdigen Domäne stammen. Bei Verbindungen, die sich über Sicherheitsgrenzen erstrecken, müssen Sie wahrscheinlich den HTTP-Zugriff konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von HTTP-Zugriff auf Analysis Services unter Internetinformationsdienste &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
-   Können Sie mithilfe einiger Tools eine Verbindung herstellen, mit anderen jedoch nicht? Das Problem kann auf eine falsche Clientbibliotheksversion zurückzuführen sein. Sie können Clientbibliotheken von der Downloadseite für das SQL Server Feature Pack herunterladen.  
  
 Folgende Ressourcen können beim Beheben von Verbindungsfehlern hilfreich sein:  
  
 [Lösen allgemeiner Verbindungsprobleme in SQL Server 2005 Analysis Services – Verbindungsszenarien](http://technet.microsoft.com/library/cc917670.aspx). Obwohl dieses Dokument bereits einige Jahre älter ist, sind die enthaltenen Informationen und Methoden weiterhin gültig.  
  
## <a name="see-also"></a>Siehe auch  
 [Verbindung mit Analysis Services herstellen](../../analysis-services/instances/connect-to-analysis-services.md)   
 [Von Analysis Services unterstützte Authentifizierungsmethoden](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)   
 [Identitätswechsel &#40; SSAS – tabellarisch &#41;](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   
 [Erstellen einer Datenquelle &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
  
