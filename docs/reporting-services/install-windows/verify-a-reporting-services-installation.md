---
title: "Überprüfen einer Installation von Reporting Services | Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/03/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- checking report server installations
- verifying report server installations
- Report Designer [Reporting Services], verifying installations
- installing Reporting Services, verifying installations
- Report Manager [Reporting Services], verifying installations
- report servers [Reporting Services], verifying installations
- Setup [Reporting Services], verifying installations
ms.assetid: 82a51a99-66f0-4b0c-b05b-07d22387adb0
caps.latest.revision: "45"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: b7135112da1536af6b279b8f0de55bfcb646e4b4
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="verify-a-reporting-services-installation"></a>Überprüfen einer Installation von Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver können in zwei Modi installiert werden: einheitlich oder SharePoint. Die Schritte, die Sie zum Überprüfen der Installation ausführen sollten, hängen vom Berichtsservermodus ab.  
  
##  <a name="bkmk_sharepointmode"></a> Überprüfen der SharePoint-Modus-Installation  
  
### <a name="to-verify-the-reporting-services-service"></a>So überprüfen Sie Reporting Services  
  
1.  Klicken Sie in der SharePoint-Zentraladministration in der Gruppe **Systemeinstellungen** auf **Dienste auf dem Server verwalten** .  
  
2.  Überprüfen Sie, ob der **SQL Server Reporting Services-Dienst** installiert ist und den Status **Wird ausgeführt** aufweist.  
  
     Wird der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst nicht in der Liste aufgeführt, überprüfen Sie, ob der Dienst installiert ist. Weitere Informationen finden Sie unter [Installieren des ersten Berichtsservers im SharePoint-Modus](http://msdn.microsoft.com/en-us/b29d0f45-0068-4c84-bd7e-5b8a9cd1b538).  
  
### <a name="to-verify-the-service-application"></a>So überprüfen Sie die Dienstanwendung  
  
1.  Um in der Zentraladministration zu überprüfen, ob mindestens eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung vorhanden ist, klicken Sie in der Gruppe **Anwendungsverwaltung** auf **Dienstanwendungen verwalten** .  
  
2.  Stellen Sie sicher, dass eine Dienstanwendung des Typs **SQL Server Reporting Services-Dienstanwendung** und ein entsprechender Anwendungsproxy vorhanden ist.  
  
3.  Klicken Sie auf eine Stelle **in der Nähe** des Namens der Dienstanwendung, und klicken Sie dann auf der SharePoint-Symbolleiste auf **Eigenschaften** .  Wenn Sie direkt auf den Namen der Dienstanwendung klicken, werden die Verwaltungsseiten der Dienstanwendung und nicht die Eigenschaftenseite geöffnet.  
  
4.  Überprüfen Sie, ob die **Zuordnung der Webanwendung** so konfiguriert ist, dass sie auf die gewünschte Webanwendung verweist.  
  
### <a name="to-verify-the-site-collection-feature"></a>So überprüfen Sie die Websitesammlungsfunktion  
  
1.  Klicken Sie in den Websiteeinstellungen auf **Websitesammlungsfunktionen** in der Gruppe **Websitesammlungsverwaltung** .  
  
2.  Überprüfen Sie, dass die **Berichtsserver-Integrationsfunktion** aktiviert ist.  
  
### <a name="to-verify-reporting-server-content-types"></a>So überprüfen Sie Berichtsserverinhaltstypen  
  
1.  Informationen zum Überprüfen oder Hinzufügen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver-Inhaltstypen finden Sie unter [Hinzufügen von Reporting Services-Inhaltstypen zu einer SharePoint-Bibliothek](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
### <a name="to-verify-you-can-launch-report-builder"></a>So überprüfen Sie, dass Sie der Berichts-Generator gestartet werden kann  
  
1.  Klicken Sie von einer Dokumentbibliothek auf **Dokumente** im SharePoint-Menüband.  
  
2.  Klicken Sie auf **Neues Dokument** und anschließend auf **Berichts-Generator-Bericht**. Wenn Sie diese Option nicht sehen, überprüfen Sie die vorherige Prozedur über das Hinzufügen der Berichtsserverinhaltstypen zu einer Bibliothek.  
  
### <a name="create-a-basic-report"></a>Erstellen eines einfachen Berichts  
  
1.  Erstellen Sie in einer SharePoint-Dokumentbibliothek einen grundlegenden [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht, der nur ein Textfeld enthält, z. B. einen Titel. Der Bericht enthält keine Datenquellen oder Datasets. Ziel ist es, zu überprüfen, ob Sie den Berichts-Generator öffnen und einen grundlegenden Bericht in der Vorschau anzeigen können.  
  
2.  Speichern Sie den Bericht in der Dokumentbibliothek, und führen Sie den Bericht dann aus der Bibliothek heraus aus. Weitere Informationen zum Erstellen von Berichten mit dem Berichts-Generator finden Sie unter [Starten des Berichts-Generators](http://msdn.microsoft.com/en-us/8c8c7d2e-b315-418d-bf65-90e7685e4259).  
  
### <a name="reporting-services-samples"></a>Reporting Services-Beispiele  
  
1.  Führen Sie eines der Lernprogramme zu Reporting Services durch. Weitere Informationen finden Sie unter [Reporting Services-Tutorials (SSRS)](../../reporting-services/reporting-services-tutorials-ssrs.md).  
  
2.  Laden Sie die Adventure Works-Beispieldatenbank und die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Beispielberichte von GitHub herunter. Weitere Informationen finden Sie in den [AdventureWorks-Beispieldatenbanken](https://github.com/Microsoft/sql-server-samples/releases).  
  
##  <a name="bkmk_nativemode"></a> Überprüfen einer Installation im einheitlichen Modus  
 Wenn Sie einen Berichtsserver im einheitlichen Modus anhand der Standardkonfiguration installieren, wird der Server durch das Setup installiert und bereitgestellt. Um festzustellen, ob der Berichtsserver durch das Setup bereitgestellt wurde, führen Sie einige wenige einfache Tests aus. Um diese Schritte ausführen zu können, müssen Sie ein lokaler Administrator sein. Um weitere Benutzer für das Ausführen der Tests zu aktivieren, konfigurieren Sie für diese Benutzer den Berichtsserverzugriff.  
  
### <a name="to-verify-that-the-report-server-is-installed-and-running"></a>So überprüfen Sie, ob der Berichtsserver installiert ist und ausgeführt wird  
  
1.  Führen Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool aus, und stellen Sie eine Verbindung mit der soeben installierten Berichtsserverinstanz her. Auf der Seite Webdienst-URL finden Sie einen Link zum Report Server-Webdienst. Klicken Sie auf den Link, um zu überprüfen, ob Sie auf den Server zugreifen können. Wenn die Berichtsserver-Datenbank noch nicht konfiguriert ist, holen Sie dies nach, bevor Sie auf den Link klicken.  
  
2.  Öffnen Sie Konsolenanwendungen für die Dienste, und überprüfen Sie, ob der Berichtsserver-Dienst ausgeführt wird. Um den Status des Berichtsserver-Diensts anzuzeigen, klicken Sie auf **Start**, zeigen Sie auf **Systemsteuerung**, doppelklicken Sie auf **Verwaltung**, und doppelklicken Sie anschließend auf **Dienste**. Führen Sie in der Liste mit den Diensten einen Bildlauf zu **Berichtsserver (MSSQLSERVER)**durch. Der Status sollte **Gestartet**lauten.  
  
3.  Öffnen Sie einen Browser, und geben Sie die Berichtsserver-URL in der Adressleiste ein. Die Adresse besteht aus dem Servernamen und dem Namen des virtuellen Verzeichnisses, das Sie bei beim Setup für den Berichtsserver angegeben haben. Standardmäßig lautet das virtuelle Verzeichnis des Berichtsservers **ReportServer**. Mit der folgenden URL können Sie die Berichtsserverinstallation überprüfen: http://*\<Computername>*/ReportServer*\<_Instanzname>*. Wenn der Berichtsserver als eine benannte Instanz installiert wurde, lautet die URL anders. Weitere Informationen zum URL-Format finden Sie unter [Konfigurieren von Berichtsserver-URLs (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md). Informationen für lokale Administratoren unter Windows Vista oder Windows Server 2008 finden Sie unter [Konfigurieren eines Berichtsservers im einheitlichen Modus für die lokale Verwaltung (SSRS)](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
4.  Führen Sie Berichte aus, um die Berichtsservervorgänge zu testen. Für diesen Schritt können Sie einen Beispielbericht aus einem Lernprogramm erstellen. Weitere Informationen finden Sie unter [Erstellen eines einfachen Tabellenberichts (SSRS-Tutorial)](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md).  
  
### <a name="to-verify-that-the-includessrswebportalincludesssrswebportalmd-is-installed-and-running"></a>So überprüfen Sie, ob der [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] installiert ist und ausgeführt wird  
  
1.  Öffnen Sie einen Browser, und geben Sie die Webportal-URL in der Adressleiste ein. Die Adresse besteht aus dem Servernamen und dem Namen des virtuellen Verzeichnisses, das Sie beim Setup für den [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] oder im Konfigurations-Manager für Reporting Services auf der Seite „Webportal-URL“ angegeben haben. Standardmäßig ist das virtuelle [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] -Verzeichnis entsprechend **Reports**. Mit der folgenden URL können Sie die [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] -Installation überprüfen:  
  
     http://*\<Computername>*/Reports*\<_Instanzname>*.  
  
2.  Verwenden Sie den [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] , um einen neuen Ordner zu erstellen, oder laden Sie eine Datei hoch, um zu testen, ob Definitionen an die Berichtsserver-Datenbank zurückgegeben werden. Falls diese Vorgänge erfolgreich sind, ist die Verbindung einsatzbereit.  
  
     Weitere Informationen finden Sie unter [Webportal (einheitlicher SSRS-Modus)](http://msdn.microsoft.com/en-us/7349e626-6ed5-4d21-b05f-cf042ad9ad70).  
  
### <a name="to-verify-that-report-designer-is-installed-and-running"></a>So überprüfen Sie, ob der Berichts-Designer installiert ist und ausgeführt wird  
  
1.  Öffnen Sie [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], und erstellen Sie auf Grundlage eines Berichtsserverprojekttyps ein neues Projekt. Weitere Informationen zum Verwenden des Berichtsserverprojekt-Assistenten finden Sie in der SQL Server-Onlinedokumentation unter [Reporting Services in SQL Server-Datentools (SSDT)](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md).  
  
2.  Wenn Sie Berichtsbeispiele installiert haben, öffnen Sie die Beispielberichts-Projektdateien, und veröffentlichen Sie die Berichte auf einem Berichtsserver.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Problembehandlung für eine Reporting Services-Installation](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
 [Cause and Resolution of Reporting Services Errors (Ursachen und Lösungen für Reporting Services-Fehler)](../../reporting-services/troubleshooting/cause-and-resolution-of-reporting-services-errors.md)  
  
  
