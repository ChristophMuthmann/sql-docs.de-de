---
title: "Verwalten eines ausgeführten Prozesses | Microsoft Docs"
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
- report processing [Reporting Services], status information
- jobs [Reporting Services]
- viewing jobs
- canceling jobs
- user jobs [Reporting Services]
- system jobs [Reporting Services]
- report processing [Reporting Services], managing running processes
- processes [Reporting Services]
- scanning processes [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services]
- canceling subscriptions
- report servers [Reporting Services], jobs
- data-driven subscriptions
- displaying jobs
- subscriptions [Reporting Services], running processes
ms.assetid: 473e574e-f1ff-4ef9-bda6-7028b357ac42
caps.latest.revision: 53
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 103472f5003235e0e08c65c40999545ff4d864ee
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="manage-a-running-process"></a>Verwalten eines ausgeführten Prozesses
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] überwacht den Status von Aufträgen, die auf dem Berichtsserver ausgeführt werden. Die in Bearbeitung befindlichen Aufträge werden in regelmäßigen Abständen vom Berichtsserver gescannt und die Statusinformationen in die Berichtsserver-Datenbank bzw. bei Verwendung des SharePoint-Modus in die Dienstanwendungs-Datenbanken geschrieben. Ein Auftrag wird verarbeitet, wenn alle folgenden Prozesse ausgeführt werden: Abfrageausführung auf einem Remote- oder auf einem lokalen Datenbankserver, Berichtsverarbeitung und Berichtsrendering.  
  
 Sie können sowohl *Benutzeraufträge* als auch *Systemaufträge*verwalten.  
  
-   Benutzeraufträge werden durch einen einzelnen Benutzer oder durch ein Abonnement initiiert. Dazu gehört das Ausführen eines Berichts bei Bedarf, das Anfordern einer Momentaufnahme zum Berichtsverlauf, das manuelle Erstellen einer Berichtsmomentaufnahme sowie das Verarbeiten eines Standardabonnements.  
  
-   Systemaufträge werden durch den Berichtsserver initiiert. Zu Systemaufträgen zählen geplante Momentaufnahmen zur Berichtsausführung, geplante Momentaufnahmen zum Berichtsverlauf sowie datengesteuerte Abonnements.  
  
 Die Berichtsverarbeitungszeit und die Ressourcenverwendung können je nach Bericht, Komplexität der Abfrage, Datenmenge und Renderingformat für den Bericht sehr unterschiedlich sein. Berichte mit einfachen Abfragen für eine lokale Datenquelle sind oft in Millisekunden abgeschlossen und müssen nie verwaltet oder optimiert werden. Im Gegensatz dazu erfordert ein großer Bericht, der in PDF oder Excel gerendert wird, je nach Hardwareressourcen, Übermittlungsoptionen und gleichzeitig ausgeführten Prozessen unter Umständen eine beträchtliche Verarbeitungszeit. Bei den meisten lang andauernden Prozessen auf einem Berichtsserver handelt es sich um Renderingvorgänge für Berichte sowie um Prozesse, die auf den Abschluss der Abfrageverarbeitung warten. Gelegentlich müssen Sie möglicherweise einen Berichtsprozess abbrechen, wenn Sie einen Computer offline schalten möchten, oder einen gerade ausgeführten Auftrag beenden, dessen Abschluss zu lange dauert.  
  
 Die folgenden Prozesse können abgebrochen werden:  
  
-   Bedarfsgesteuerte Berichtsverarbeitung.  
  
-   Geplante Berichtsverarbeitung.  
  
-   Standardabonnements von einzelnen Benutzern.  
  
 Durch das Abbrechen eines Auftrags werden nur die Prozesse beendet, die auf dem Berichtsserver ausgeführt werden. Da der Berichtsserver keine Datenverarbeitung auf anderen Computern verwaltet, müssen Sie Abfrageprozesse, die anschließend auf anderen Systemen verwaist sind, manuell abbrechen. Geben Sie möglichst Timeoutwerte an, um Abfragen automatisch zu beenden, deren Ausführung zu lange dauert. Weitere Informationen finden Sie unter [Festlegen von Timeoutwerten für die Verarbeitung von Berichten und freigegebenen Datasets &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md). Weitere Informationen zum vorübergehenden Anhalten eines Berichts finden Sie unter [Deaktivieren oder Anhalten der Berichts- und Abonnementverarbeitung](../../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md).  
  
> [!NOTE]  
>  In seltenen Fällen müssen Sie den Server neu starten, um einen Prozess abzubrechen. Im SharePoint-Modus muss der Anwendungspool, in dem die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung gehostet wird, u. U. neu gestartet werden. Weitere Informationen finden Sie unter [Starten und Beenden des Berichtsserverdiensts](../../reporting-services/report-server/start-and-stop-the-report-server-service.md).  
  
 In diesem Thema:  
  
-   [Anzeigen und Abbrechen von Aufträgen (einheitlicher Modus)](#bkmk_native)  
  
-   [Anzeigen und Abbrechen von Aufträgen (SharePoint-Modus)](#bkmk_sharepoint)  
  
-   [Programmgesteuertes Verwalten von Aufträgen](#bkmk_programmatically)  
  
##  <a name="bkmk_native"></a> Anzeigen und Abbrechen von Aufträgen (einheitlicher Modus)  
 Sie können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] zum Anzeigen oder Abbrechen eines auf dem Berichtsserver ausgeführten Auftrags verwenden. Zum Abrufen einer Liste mit Aufträgen, die aktuell ausgeführt werden, oder zum Abrufen des aktuellen Auftragsstatus aus der Berichtsserver-Datenbank müssen Sie die Seite aktualisieren. Wenn Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung zum Berichtsserver herstellen, können Sie einen Auftragsordner öffnen, um eine Liste der Berichte anzuzeigen, die aktuell auf dem Berichtsservercomputer bearbeitet werden. Statusinformationen zu jedem Auftrag werden auf der Seite Auftragseigenschaften angezeigt. Sie können Statusinformationen für alle Aufträge anzeigen lassen, indem Sie das Dialogfeld Berichtsserveraufträge abbrechen öffnen.  
  
 Sie können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] zum Anzeigen oder Abbrechen eines auf dem Berichtsserver ausgeführten Auftrags verwenden. Zum Abrufen einer Liste mit Aufträgen, die aktuell ausgeführt werden, oder zum Abrufen des aktuellen Auftragsstatus aus der Berichtsserver-Datenbank müssen Sie die Seite aktualisieren. Wenn Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung zum Berichtsserver herstellen, können Sie einen Auftragsordner öffnen, um eine Liste der Berichte anzuzeigen, die aktuell auf dem Berichtsservercomputer bearbeitet werden. Statusinformationen zu jedem Auftrag werden auf der Seite Auftragseigenschaften angezeigt. Sie können Statusinformationen für alle Aufträge anzeigen lassen, indem Sie das Dialogfeld Berichtsserveraufträge abbrechen öffnen.  
  
 Mit [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] können Sie die Modellgenerierung, die Modellverarbeitung oder datengesteuerte Abonnements nicht auflisten oder abbrechen. Reporting Services bietet keine Möglichkeit zum Abbrechen der Modellgenerierung bzw. -verarbeitung. Sie können jedoch datengesteuerte Abonnements mit den unter diesem Thema aufgeführten Anweisungen abbrechen.  
  
### <a name="how-to-cancel-report-processing-or-subscription"></a>So brechen Sie Berichtsverarbeitung oder -abonnements ab  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Berichtsserver her. Anweisungen finden Sie unter [Herstellen einer Verbindung zu einem Berichtsserver in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md).  
  
2.  Öffnen Sie den Ordner **Aufträge** .  
  
3.  Klicken Sie mit der rechten Maustaste auf den Bericht, und klicken Sie anschließend auf **Aufträge abbrechen**.  
  
### <a name="how-to-cancel-a-data-driven-subscription"></a>So brechen Sie ein datengesteuertes Abonnement ab  
  
1.  Öffnen Sie die Datei RSReportServer.config in einem Text-Editor.  
  
2.  Suchen Sie **IsNotificationService**.  
  
3.  Legen Sie hierfür **False**fest.  
  
4.  Speichern Sie die Datei.  
  
5.  Löschen Sie im Berichts-Manager das datengesteuerte Abonnement aus der Registerkarte Abonnements des Berichts oder aus **Meine Abonnements**.  
  
6.  Nachdem Sie das Abonnement gelöscht haben, suchen Sie in der Datei RSReportServer.config **IsNotificationService** , und legen Sie dafür **True**fest.  
  
7.  Speichern Sie die Datei.  
  
### <a name="configuring-frequency-settings-for-retrieving-job-status"></a>Konfigurieren von Frequenzeinstellungen für den Abruf des Auftragsstatus  
 Ein Auftrag, der gerade ausgeführt wird, wird in der temporären Datenbank des Berichtsservers gespeichert. Durch Ändern der Konfigurationseinstellungen in der Datei RSReportServer.config können Sie steuern, wie oft der Berichtsserver nach Aufträgen, die verarbeitet werden, scannt, sowie das Intervall festlegen, nach dem der Status eines ausgeführten Auftrags von Neu in Wird ausgeführt geändert wird. Die Einstellung **RunningRequestsDbCycle** gibt an, wie oft der Berichtsserver nach ausgeführten Prozessen scannt. Standardmäßig werden die Statusinformationen alle 60 Sekunden aufgezeichnet. Die Einstellung **RunningRequestsAge** gibt das Intervall an, nach dem der Status eines Auftrags von "Neu" in "Wird ausgeführt" geändert wird.  
  
##  <a name="bkmk_sharepoint"></a> Anzeigen und Abbrechen von Aufträgen (SharePoint-Modus)  
 Die Verwaltung von Aufträgen in einer SharePoint-Modusbereitstellung wird für jede [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung abgeschlossen, indem die SharePoint-Zentraladministration verwendet wird.  
  
#### <a name="to-manage-jobs-in-sharepoint-mode"></a>So verwalten Sie Aufträge im SharePoint-Modus  
  
1.  Klicken Sie in der Sharepoint-Zentraladministration auf **Dienstanwendungen verwalten**.  
  
2.  Suchen und klicken Sie auf den Namen Ihrer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung, um die Seite für die Verwaltung von Anwendungen zu öffnen.  
  
3.  Klicken Sie auf **Aufträge verwalten**.  
  
4.  Klicken Sie auf die **Auftrag-ID** , um die Details des Auftrags anzuzeigen.  
  
5.  Klicken Sie alternativ auf das Feld für den Auftrag, und klicken Sie auf **Löschen** , um den Auftrag abzubrechen. Durch das Löschen des Auftrags wird nicht das Abonnement gelöscht.  
  
##  <a name="bkmk_programmatically"></a> Programmgesteuertes Verwalten von Aufträgen  
 Sie können Aufträge programmgesteuert oder mit einem Skript verwalten. Weitere Informationen finden Sie unter <xref:ReportService2010.ReportingService2010.ListJobs%2A>, <xref:ReportService2010.ReportingService2010.CancelJob%2A>.  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsserveraufträge abbrechen &#40;Management Studio&#41;](../../reporting-services/tools/cancel-report-server-jobs-management-studio.md)   
 [Auftragseigenschaften &#40;Management Studio&#41;](../../reporting-services/tools/job-properties-management-studio.md)   
 [Ändern einer Reporting Services-Konfigurationsdatei &#40;rsreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Überwachen der Leistung des Berichtsservers](../../reporting-services/report-server/monitoring-report-server-performance.md)  
  
  
