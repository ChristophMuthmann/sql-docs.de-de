---
title: Reporting Services-Datenwarnungen | Microsoft Docs
ms.custom: 
ms.date: 07/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8c234077-b670-45c0-803f-51c5a5e0866e
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 27956feca3ad15233943a447422e2260bd61c913
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="reporting-services-data-alerts"></a>Reporting Services-Datenwarnungen

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

SQL Server Reporting Services-datenwarnungen sind eine datengesteuerte warnungslösung, mit denen die über Berichtsdaten informiert werden, die interessante oder wichtige und zu einem relevanten Zeitpunkt. Mithilfe von Datenwarnungen müssen Sie nicht mehr nach Informationen suchen – diese werden Ihnen bereitgestellt.

Datenwarnmeldungen werden per E-Mail gesendet. Sie können festlegen, dass Meldungen je nach Wichtigkeit der Informationen mehr oder weniger häufig oder nur im Fall von Ergebnisänderungen zu senden sind. Sie können mehrere E-Mail-Empfänger festlegen und somit andere Benutzer informieren, um die Effizienz und Zusammenarbeit verbessern.

> [!NOTE]
> Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.

##  <a name="AlertingWF"></a> Datenwarnungsarchitektur und Workflow

Im Folgenden werden die wichtigsten Bereiche der [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Datenwarnungen zusammengefasst:

-   **Festlegen und Speichern von Datenwarnungsdefinitionen**: Sie führen einen Bericht aus, erstellen Regeln, die interessante Datenwerte kennzeichnen, definieren ein Serienmuster zum Senden der Datenwarnmeldung und legen die Empfänger der Warnmeldung fest.  
  
-   **Ausführen von Datenwarnungsdefinitionen**: Der Warndienst verarbeitet Warnungsdefinitionen zu einem geplanten Zeitpunkt, ruft Berichtsdaten ab und erstellt Datenwarnungsinstanzen auf Basis von Regeln in der Warnungsdefinition.  
  
-   **Senden von Datenwarnmeldungen an Empfänger**: Der Warndienst erstellt eine Warnungsinstanz und sendet per E-Mail eine Warnmeldung an Empfänger.  
  
 Außerdem können Sie als Datenwarnungseigentümer die Informationen zu Ihren Datenwarnungen anzeigen und die Datenwarnungsdefinitionen löschen und bearbeiten. Eine Warnung hat nur einen Eigentümer (Ersteller der Warnung).  
  
 Warnungsadministratoren, also Benutzer mit der SharePoint-Berechtigung zum Verwalten von Warnungen, können Datenwarnungen auf Websiteebene verwalten. Sie können Listen von Warnungen von jedem Websitebenutzer anzeigen und Warnungen löschen.  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Datenwarnungen unterscheiden sich von SharePoint-Warnungen. Sie können SharePoint-Warnungen auf jedem Dokumenttyp, einschließlich Berichten, definieren. SharePoint-Warnungen werden gesendet, wenn das Dokument geändert wird. Sie fügen z. B. einer Tabelle in einem Bericht eine Spalte hinzu. Im Gegensatz dazu werden Datenwarnungen gesendet, wenn die in einem Bericht angezeigten Daten den Regeln der Warnungsdefinitionen entsprechen. Die Regeln verweisen normalerweise auf die Daten, die in einem Bericht angezeigt werden.  
  
 Durch Erstellen von Datenwarnungen für Berichte lassen sich Änderungen an Berichtsdaten überwachen und mit für Ihre Geschäftsanforderungen geeigneten Zeitintervallen Datenwarnungen per E-Mail versenden, wenn Berichtsdaten den Regeln entsprechen, die für Sie und andere Benutzer interessante Daten definieren. Sie können Datenwarnungen auch bedarfsgesteuert ausführen. Wenn Sie die SharePoint-Berechtigung "Warnung erstellen" besitzen, können Sie Warnungen in jedem Bericht erstellen, für den Sie über die Berechtigung zum Anzeigen verfügen. Sie können mehrere Warnungen in einem Bericht erstellen. Mehrere Benutzer können dieselben oder andere Warnungen in einem Bericht erstellen. Um mit anderen Personen zusammenzuarbeiten, können Sie diese als Empfänger von Warnmeldungen in Datenwarnungsdefinitionen angeben, die Sie erstellen.  
  
 Das folgende Diagramm zeigt den Workflow zum Erstellen und Speichern einer Datenwarnungsdefinition und zum Erstellen eines SQL-Agent-Auftrags, um mit der Verarbeitung der Instanz der Datenwarnung und dem Senden von Datenwarnmeldungen per E-Mail zu beginnen, die die Berichtsdaten enthalten, die die Warnung für mindestens einen Empfänger ausgelöst haben.  
  
 ![Workflows in einer Reporting Services-Warnungen](../reporting-services/media/rs-alertingworkflow.gif "Workflow in Reporting Services-Warnungen")  
  
### <a name="reports-supported-by-data-alerts"></a>Von Datenwarnungen unterstützte Berichte  
 Sie können Datenwarnungen für alle Typen von professionellen Berichten erstellen, die in der Berichtsdefinitionssprache (RDL) geschrieben und im Berichts-Designer oder Berichts-Generator erstellt wurden. Berichte, die Datenbereiche wie z. B. Tabellen und Diagramme enthalten, Berichte mit Unterberichten und komplexe Berichte mit mehreren parallelen Spaltengruppen und geschachtelten Datenbereichen. Die einzige Voraussetzung ist, dass der Bericht mindestens einen Datenbereich beliebigen Typs beinhaltet und die Berichtsdatenquelle so konfiguriert ist, dass entweder gespeicherte Anmeldeinformationen oder keine Anmeldeinformationen verwendet werden. Wenn der Bericht keine Datenbereiche aufweist, können Sie keine Warnung dafür erstellen.  
  
 Sie können keine Datenwarnungen in mit [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]erstellten Berichten erstellen.  
  
 Wenn Sie [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] im einheitlichen Modus oder im SharePoint-Modus installieren oder die eigenständige Version des Berichts-Generators verwenden, können Sie Berichte auf einem Berichtsserver, dem Computer oder in einer SharePoint-Bibliothek speichern. Um Datenwarnungen zu Berichten zu erstellen, müssen die Berichte gespeichert oder in eine SharePoint-Bibliothek hochgeladen werden. Das bedeutet, dass Sie keine Warnungen zu Berichten erstellen können, die auf einem Berichtsserver im einheitlichen Modus oder dem Computer gespeichert sind. Zudem können Sie keine in benutzerdefinierten Anwendungen eingebetteten Warnungen erstellen.  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] unterstützt zahlreiche Typen von Anmeldeinformationen in Berichten. Sie können Datenwarnungen für Berichte mit Datenquellen erstellen, die so konfiguriert sind, dass gespeicherte Anmeldeinformationen oder keine Anmeldeinformationen verwendet werden. Sie können keine Warnungen für Berichte erstellen, die zur Verwendung der Anmeldeinformationen mit integrierter Sicherheit oder der Eingabeaufforderung für Anmeldeinformationen konfiguriert wurden. Der Bericht wird als Teil der Verarbeitung der Warnungsdefinition ausgeführt, und die Verarbeitung schlägt ohne Anmeldeinformationen fehl. Weitere Informationen finden Sie unter den folgenden Links:  
  
-   [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
-   [Rollen und Berechtigungen &#40;Reporting Services&#41;](../reporting-services/security/roles-and-permissions-reporting-services.md)  
  
-   [Authentifizierung mit dem Berichtsserver](../reporting-services/security/authentication-with-the-report-server.md)  
  
### <a name="run-reports"></a>Ausführen von Berichten  
 Der erste Schritt zum Erstellen einer Datenwarnungsdefinition umfasst das Suchen des gewünschten Berichts in der SharePoint-Bibliothek und das anschließende Ausführen des Berichts. Wenn ein Bericht bei der Ausführung keine Daten enthält, können Sie zu diesem Zeitpunkt keine Warnung für den Bericht erstellen.  
  
 Geben Sie im Fall eines parametrisierten Berichts die beim Ausführen des Berichts zu verwendenden Parameterwerte an. Die Parameterwerte werden in den Datenwarnungsdefinitionen gespeichert, die Sie für einen Bericht erstellen. Die Werte werden beim erneuten Ausführen des Berichts als Schritt der Verarbeitung der Datenwarnungsdefinition verwendet. Wenn Sie die Parameterwerte ändern, ist der Bericht mit diesen Parameterwerten erneut auszuführen, und Sie müssen eine Warnungsdefinition für die neue Berichtsversion erstellen.  
  
### <a name="create-data-alert-definitions"></a>Erstellen von Datenwarnungsdefinitionen  
 Die [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Datenwarnungsfunktionen umfassen den Datenwarnungs-Designer, der zum Erstellen von Datenwarnungsdefinitionen dient.  
  
 Um eine Datenwarnungsdefinition zu erstellen, führen Sie den Bericht aus, und öffnen Sie den Datenwarnungs-Designer über das SharePoint-Berichts-Viewer-Menü **Aktionen** . Die Berichtsdaten-Feeds für den Bericht werden generiert. Zudem werden die ersten 100 Zeilen im Datenfeed in einer Datenvorschautabelle im Datenwarnungs-Designer angezeigt. Alle Datenfeeds aus einem Bericht werden so lange zwischengespeichert, wie Sie im Datenwarnungs-Designer an der Warnungsdefinition arbeiten. Das Zwischenspeichern ermöglicht schnelles Umschalten zwischen Datenfeeds. Wenn Sie im Datenwarnungs-Designer eine Warnungsdefinition erneut öffnen, werden die Datenfeeds aktualisiert.  
  
 Datenwarnungsdefinitionen bestehen aus Regeln und Klauseln, denen Berichtsdaten entsprechen müssen, damit eine Datenwarnmeldung ausgelöst wird. Zudem umfassen sie einen Plan mit der Definition der Häufigkeit zum Senden der Warnmeldung, optional die Datumsangaben zum Starten und Beenden des Sendevorgangs für die Warnmeldung sowie Informationen (z. B. die Betreffzeile und eine Beschreibung für die Warnmeldung) und die Empfänger der Meldung. Nach dem Erstellen einer Warnungsdefinition speichern Sie diese in der SQL Server-Warnungsdatenbank.  
  
### <a name="save-data-alert-definitions-and-alerting-metadata"></a>Speichern von Datenwarnungsdefinitionen und Warnungsmetadaten  
 Wenn Sie [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] im SharePoint-Modus installieren, wird die SQL Server-Warnungsdatenbank automatisch erstellt.  
  
 Datenwarnungsdefinitionen und Warnungsmetadaten werden in der Warnungsdatenbank gespeichert. Standardmäßig heißt diese Datenbank ReportingServices\<GUID > _Alerting.  
  
 Wenn Sie die Datenwarnungsdefinition speichern, erstellt der Warnungsdienst einen SQL Server-Agent-Auftrag für die Warnungsdefinition. Der Auftrag beinhaltet einen Auftragszeitplan. Der Zeitplan basiert auf dem Serienmuster, das Sie mit der Warnungsdefinition definieren. Durch die Ausführung des Auftrags wird die Verarbeitung der Datenwarnungsdefinition initiiert.  
  
### <a name="process-data-alert-definitions"></a>Verarbeiten von Datenwarnungsdefinitionen  
 Wenn der Zeitplan für den Auftrag des SQL Server-Agent die Verarbeitung der Warnungsdefinition startet, wird der Bericht ausgeführt, um die Berichtsdatenfeeds zu aktualisieren. Der Warndienst liest die Datenfeeds und wendet die in den Datenwarnungsdefinitionen angegebenen Regeln auf die Datenwerte an. Entspricht mindestens ein Datenwert den Regeln, wird eine Datenwarnungsinstanz erstellt und eine Datenwarnmeldung mit den Warnungsergebnissen per E-Mail an alle Empfänger gesendet. Die Ergebnisse entsprechen Zeilen mit Berichtsdaten, die zum Zeitpunkt der Erstellung der Warnungsinstanz alle Regeln erfüllt haben. Um mehrere Warnmeldungen mit den gleichen Ergebnissen zu unterbinden, können Sie angeben, dass Meldungen nur gesendet werden, wenn sich die Ergebnisse ändern. In diesem Fall wird eine Warnungsinstanz erstellt und in der Warnungsdatenbank gespeichert. Eine Warnmeldung wird jedoch nicht generiert. Tritt ein Fehler auf, wird die Warnungsinstanz ebenfalls in der Warnungsdatenbank gespeichert und eine Warnmeldung mit den Fehlerdetails an die Empfänger gesendet. Der Abschnitt "Diagnose und Protokollierung" weiter unten in diesem Thema bietet weitere Informationen zur Protokollierung und Problembehandlung.  
  
### <a name="send-data-alert-messages"></a>Senden von Datenwarnmeldungen  
 Datenwarnmeldungen werden per E-Mail gesendet.  
  
 Die Zeile **Von** enthält einen von der [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -E-Mail-Übermittlungskonfiguration bereitgestellten Wert. In der Zeile **An** sind die Empfänger aufgelistet, die Sie angegeben haben, als Sie die Warnung im Datenwarnungs-Designer erstellt haben.  
  
 Abgesehen von der E-Mail-Betreffzeile, die Sie im Datenwarnungs-Designer angeben, enthält die Datenwarnmeldung die folgenden Informationen:  
  
-   Der Name der Person, die die Datenwarnungsdefinition erstellt hat.  
  
-   Wenn Sie in der Warnungsdefinition eine Beschreibung angegeben haben, wird diese am oberen Rand des E-Mail-Texts angezeigt.  
  
-   Die Warnungsergebnisse, die aus den Zeilen im Berichtsdatenfeed bestehen und die in der Warnungsdefinition angegebenen Regeln erfüllen.  
  
-   Ein Link zum Bericht, auf dem die Warnungsdefinition basiert.  
  
-   Die Regeln für die Warnungsdefinition.  
  
-   Die Parameter und Werte, mit denen Sie den Bericht ausgeführt haben.  
  
-   Die Kontextwerte von Berichtselementen, die außerhalb der Berichtsdatenbereiche liegen.  
  
 Wenn keine Datenwarnungsinstanz oder Datenwarnmeldung erstellt werden kann, wird an alle Empfänger eine Fehlermeldung gesendet. Anstelle der Warnungsergebnisse beinhaltet die Meldung eine Fehlerbeschreibung.  
  
 Weitere Informationen finden Sie unter [Data Alert Messages](../reporting-services/data-alert-messages.md).  
  
##  <a name="InstallAlerting"></a> Installieren von Datenwarnungen  
 Die Datenwarnungsfunktion ist nur verfügbar, wenn [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] im SharePoint-Modus installiert ist. Wenn Sie [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] im SharePoint-Modus installieren, erstellt das Setup automatisch die Warnungsdatenbank, in der Datenwarnungsdefinitionen und Warnungsmetadaten gespeichert werden, sowie zwei SharePoint-Seiten zum Verwalten von Warnungen. Zudem wird der SharePoint-Website der Datenwarnungs-Designer hinzugefügt. Für Warnungen während der Installation müssen keine besonderen Schritte ausgeführt oder Optionen festgelegt werden.  
  
 Weitere Informationen zum Installieren von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] im SharePoint-Modus, einschließlich des gemeinsamen Diensts von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , der in der [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] - und [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Dienstanwendung neu ist und die Sie vor der Verwendung der [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Funktionen erstellen und konfigurieren müssen, finden Sie unter [Installieren des SharePoint-Modus von Reporting Services für SharePoint 2010](http://msdn.microsoft.com/en-us/47efa72e-1735-4387-8485-f8994fb08c8c) in der MSDN Library.  
  
 Gemäß des zuvor in diesem Thema gezeigten Diagramms verwenden Datenwarnungen SQL Server-Agent-Aufträge. Zum Erstellen des Auftrags muss der SQL Server-Agent ausgeführt werden. Unter Umständen haben Sie den SQL Server-Agent bei der Installation von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]so konfiguriert, dass er automatisch startet. Andernfalls lässt sich der SQL Server-Agent manuell starten. Weitere Informationen finden Sie unter [Konfigurieren des SQL Server-Agents](http://msdn.microsoft.com/library/2e361a62-9e92-4fcd-80d7-d6960f127900) und [Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agents oder des SQL Server-Browsers](../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
 Sie können in der SharePoint-Zentraladministration mithilfe der Seite **Abonnements und Warnungen bereitstellen** herausfinden, ob der SQL Server-Agent ausgeführt wird, und benutzerdefinierte [!INCLUDE[tsql](../includes/tsql-md.md)] -Skripts erstellen und herunterladen, die Sie dann ausführen, um dem SQL Server-Agent Berechtigungen zu gewähren. Erstellen Sie die [!INCLUDE[tsql](../includes/tsql-md.md)] -Skripts alternativ mithilfe von PowerShell. Weitere Informationen finden Sie unter [Provision Subscriptions and Alerts for SSRS Service Applications](../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
##  <a name="ConfigAlert"></a> Konfigurieren von Datenwarnungen  
 Ab [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] werden die Einstellungen für [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Funktionen, einschließlich Datenwarnungen, zwischen der Konfigurationsdatei des Berichtsservers (rsreportserver.config) und einer SharePoint-Konfigurationsdatenbank verteilt, wenn Sie [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] im SharePoint-Modus installieren. Wenn Sie die Dienstanwendung als Schritt der Installation und Konfiguration von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]erstellen, wird die SharePoint-Konfigurationsdatenbank automatisch erstellt. Weitere Informationen finden Sie unter [RsReportServer.config-Konfigurationsdatei](../reporting-services/report-server/rsreportserver-config-configuration-file.md) und [Reporting Services-Konfigurationsdateien](../reporting-services/report-server/reporting-services-configuration-files.md).  
  
 Die Einstellungen für [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Datenwarnungen beinhalten die Intervalle zum Bereinigen von Warndaten und -metadaten sowie die Anzahl an erneuten Versuchen beim Senden von Datenwarnmeldungen per E-Mail. Sie können die Konfigurationsdatei und Konfigurationsdatenbank aktualisieren, um andere Werte für Datenwarneinstellungen zu verwenden.  
  
 Die Konfigurationsdatei des Berichtsservers lässt sich direkt aktualisieren. Die SharePoint-Konfigurationsdatenbank wird mit Windows PowerShell-Cmdlets aktualisiert.  
  
 In der folgenden Tabelle sind die Konfigurationselemente für Datenwarnungen, ihre Standardwerte, Beschreibungen und Speicherorte aufgeführt.  
  
|Einstellung|Standardwert|Description|Speicherort|  
|-------------|-------------------|-----------------|--------------|  
|AlertingCleanupCycleMinutes|20|Zeit zwischen Starts des Cleanupzyklus in Minuten.|Konfigurationsdatei des Berichtsservers|  
|AlertingExecutionLogCleanupMinutes|10080|Zeit für die Aufbewahrung von Ausführungsprotokolleinträgen in Minuten.|Konfigurationsdatei des Berichtsservers|  
|AlertingDataCleanupMinutes|360|Zeit für die Aufbewahrung temporärer Daten in Minuten.|Konfigurationsdatei des Berichtsservers|  
|AlertingMaxDataRetentionDays|180|Zeit bis zum Löschen von Warnungsausführungsmetadaten, Warnungsinstanzen und Ausführungsergebnissen in Tagen.|Konfigurationsdatei des Berichtsservers|  
|MaxRetries|3|Anzahl der erneuten Versuche zum Verarbeiten von Datenwarnungen.|Dienstkonfigurationsdatenbank|  
|SecondsBeforeRetry|900|Anzahl an Sekunden des Wartens vor jedem Neuversuch.|Dienstkonfigurationsdatenbank|  
  
 Standardmäßig gelten die MaxRetries- und SecondsBeforeRetry-Einstellungen für alle Ereignisse von Datenwarnungen. Wenn Sie eine genauere Steuerung der Neuversuche und Verzögerungen bei Neuversuchen wünschen, fügen Sie Elemente für alle Ereignishandler hinzu, die verschiedene Werte für MaxRetries und SecondsBeforeRetry angeben.  
  
### <a name="event-handlers-and-retry"></a>Ereignishandler und Wiederholung  
 Die Ereignishandler sind:  
  
|Ereignishandler|Description|  
|-------------------|-----------------|  
|FireAlert|Klicken Sie im Datenwarnungs-Manager auf **Ausführen**  , um die unmittelbare Verarbeitung einer Warnungsdefinition zu initiieren.|  
|FireSchedule|Der SQL Server-Agent startet den Auftragszeitplan für eine Warnungsdefinition.|  
|CreateSchedule|Sie erstellen eine Datenwarnungsdefinition, und ein SQL Server-Agent-Auftragszeitplan wird auf Basis des in der Warnungsdefinition angegebenen Häufigkeitsintervalls erstellt.|  
|UpdateSchedule|Sie aktualisieren das Häufigkeitsintervall der Datenwarnungsdefinition, und der SQL Server-Agent-Auftragszeitplan wird aktualisiert.|  
|DeleteSchedule|Sie löschen die Datenwarnungsdefinition, und der zugehörige SQL Server-Agent-Auftragszeitplan wird gelöscht.|  
|GenerateAlert|Die Warnungslaufzeit verarbeitet den Berichtsdatenfeed, wendet die in der Datenwarnungsdefinition angegebenen Regeln an, bestimmt, ob eine Instanz der Datenwarnung zu erstellen ist, und erstellt nach Bedarf eine Instanz der Datenwarnung.|  
|DeliverAlert|Die Laufzeit erstellt die Datenwarnmeldung und sendet sie an alle Empfänger per E-Mail.|  
  
 Die folgende Tabelle bietet eine Übersicht über die Ereignishandler und die Fehler, bei denen eine Wiederholung ausgelöst wird:  
  
|Fehlerkategorie|<|\<|Ereignistyp||>|>|>|  
|--------------------|--------|--------|----------------|-|--------|--------|--------|  
||**FireAlert**|**FireSchedule**|**CreateSchedule**|**UpdateSchedule**|**DeleteSchedule**|**GenerateAlert**|**DeliverAlert**|  
|Nicht genügend Arbeitsspeicher.|X|X|X|X|X|X|X|  
|Threadabbruch|X|X|X|X|X|X|X|  
|SQL-Agent wird nicht ausgeführt|X||X|X|X|||  
|Vorübergehend. Meistens aufgrund von Verbindungsproblemen, Timeouts und Sperren.|X|X|X|X|X|X|X|  
|IOException|||||||X|  
|WebException|||||||X|  
|SocketException|||||||X|  
|SMTPException **(\*)**|||||||X|  
  
 **(\*)** SMTP-Fehler, die eine Wiederholung auslösen:  
  
-   SmtpStatusCode.ServiceNotAvailable  
  
-   SmtpStatusCode.MailboxBusy  
  
-   SmtpStatusCode.MailboxUnavailable  
  
###  <a name="bkmk_disablealerts"></a> Deaktivieren von Datenwarnungen  
 Wenn Sie die Datenwarnungsfunktion deaktivieren möchten, aktualisieren Sie den Abschnitt "Dienst" der Konfigurationsdatei. Im folgenden Code wird der Abschnitt "Dienst" der Konfigurationsdatei gezeigt.  
  
 `<Service>`  
  
 `<IsSchedulingService>True</IsSchedulingService>`  
  
 `<IsNotificationService>True</IsNotificationService>`  
  
 `<IsEventService>True</IsEventService>`  
  
 `<IsAlertingService>True</IsAlertingService>`  
  
 `…`  
  
 `</Service>`  
  
 Zum Deaktivieren des Warndiensts ändern Sie unter `<IsAlertingService>True</IsAlertingService>`True in False.  
  
##  <a name="Permissions"></a> Berechtigungen für Datenwarnungen  
 Vor dem Erstellen von Datenwarnungen in Berichten müssen Sie die Berechtigung zum Ausführen des Berichts und zum Erstellen von Warnungen auf der SharePoint-Website besitzen. Im Folgenden finden Sie weitere Informationen zu Berichtsberechtigungen.  
  
-   [Generieren von Datenfeeds aus Berichten &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)  
  
-   [Festlegen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Datenwarndienst unterstützt zwei Berechtigungsstufen: Information Worker und Warnungsadministrator. In der folgenden Tabelle sind die verwandten SharePoint-Berechtigungen und die Benutzeraufgaben aufgeführt.  
  
|Benutzertyp|SharePoint-Berechtigung|Taskbeschreibung|  
|---------------|---------------------------|----------------------|  
|Information Worker|Elemente anzeigen<br /><br /> Warnungen erstellen|Zeigen Sie Elemente wie z. B. Berichte an, und erstellen Sie Datenwarnungen in den Berichten. Bearbeiten und löschen Sie Warnungen.|  
|Warnungsadministrator|Benachrichtigungen verwalten|Zeigen Sie eine Liste aller Datenwarnungen an, die auf der SharePoint-Website gespeichert wurden, und löschen Sie die Warnungen.|  
  
##  <a name="DiagnosticsLogging"></a> Diagnose und Protokollierung  
 Datenwarnungen bieten zahlreiche Möglichkeiten zur Unterstützung von Information Workern und Administratoren beim Nachverfolgen von Warnungen und Verstehen der Ursachen von Fehlern bei Warnungen und helfen Administratoren bei der Verwendung von Protokollen, um zu erfahren, welche Warnmeldungen an wen gesendet wurden, und um die Anzahl der gesendeten Warnungsinstanzen usw. herauszufinden.  
  
### <a name="data-alert-manager"></a>Datenwarnungs-Manager  
 Der Datenwarnungs-Manager listet Warnungsdefinitionen und Fehlerinformationen auf, die Information Worker und Administratoren beim Ermitteln von Fehlerursachen unterstützen. Einige häufige Ursachen für Fehler:  
  
-   Der Berichtsdatenfeed wurde geändert, und Spalten, die in Regeln für Datenwarnungsdefinitionen verwendet werden, sind nicht mehr im Datenfeed enthalten.  
  
-   Die Berechtigung zum Anzeigen des Berichts wurde widerrufen.  
  
-   Der Datentyp in der zugrunde liegenden Datenquelle wurde geändert, und die Warnungsdefinition ist nicht mehr gültig.  
  
### <a name="logs"></a>Protokolle  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] bietet eine Reihe von Protokollen, mit denen Sie einen besseren Einblick in die bei der Verarbeitung von Datenwarnungsdefinitionen ausgeführten Berichte, in die erstellten Datenwarnungsinstanzen usw. erhalten. Drei Protokolle sind besonders nützlich: das Warnungsausführungsprotokoll sowie das Ausführungsprotokoll und das Ablaufverfolgungsprotokoll des Berichtsservers.  
  
 Weitere Informationen zu anderen [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Protokollen finden Sie unter [Reporting Services-Protokolldateien und Quellen](../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
#### <a name="alerting-execution-log"></a>Warnungsausführungsprotokoll  
 Der Warnungslaufzeitdienst schreibt Einträge in die Tabelle ExecutionLogView in der Warnungsdatenbank. Sie können die Tabelle abfragen oder die folgenden gespeicherten Prozeduren ausführen, um umfangreichere Diagnoseinformationen zu den in der Warnungsdatenbank gespeicherten Datenwarnungen abzurufen.  
  
-   ReadAlertData  
  
-   ReadAlertHistory  
  
-   ReadAlertInstances  
  
-   ReadEventHistory  
  
-   ReadFeedPollHistory  
  
-   ReadFeedPools  
  
-   ReadPollData  
  
-   ReadSentAlerts  
  
 Sie können die gespeicherte Prozedur mithilfe von SQL-Agents nach einem Zeitplan ausführen. Weitere Informationen finden Sie unter [SQL Server Agent](http://msdn.microsoft.com/library/8d1dc600-aabb-416f-b3af-fbc9fccfd0ec).  
  
#### <a name="report-server-execution-log"></a>Berichtsserver-Ausführungsprotokoll  
 Berichte werden ausgeführt, um die Datenfeeds zu generieren, auf denen Datenwarnungsdefinitionen basieren. Das Ausführungsprotokoll des Berichtsservers in der zugehörigen Datenbank erfasst bei jeder Ausführung des Berichts Informationen. Fragen Sie die ExecutionLog2-Sicht in der Datenbank ab, um ausführliche Informationen zu erhalten. Weitere Informationen finden Sie unter [Berichtsserver-Ausführungsprotokoll und die ExecutionLog3-Sicht](../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
#### <a name="report-server-trace-log"></a>Ablaufverfolgungsprotokoll des Berichtsservers  
 Das Ablaufverfolgungsprotokoll des Berichtsservers enthält sehr detaillierte Informationen für Berichtsserver-Dienstvorgänge, einschließlich der vom Berichtsserver-Webdienst und der Hintergrundverarbeitung ausgeführten Vorgänge. Ablaufverfolgungsinformationen können beispielsweise zum Debuggen einer Anwendung, die einen Berichtsserver enthält, oder zum Analysieren eines bestimmten Problems, das ins Ereignis- oder Ausführungsprotokoll geschrieben wurde, nützlich sein. Weitere Informationen finden Sie unter [Report Server Service Trace Log](../reporting-services/report-server/report-server-service-trace-log.md).  
  
##  <a name="PerformanceCounters"></a> Performance Counters  
 Datenwarnungen stellen eigene Leistungsindikatoren bereit. Alle außer ein Leistungsindikator beziehen sich auf ein Ereignis, das ein Teil des Warnungslaufzeitdiensts ist. Der Leistungsindikator, der auf die Ereigniswarteschlange bezogen ist, gibt die Länge der Warteschlange für alle aktiven Ereignisse an.  
  
|Ereignis oder Ereigniswarteschlange|Leistungsindikator|  
|--------------------------|-------------------------|  
|ALERTINGQUEUESIZE|Warnung: Länge der Ereigniswarteschlange|  
|FireAlert|Warnung: verarbeitete Ereignisse - FireAlert|  
|FireSchedule|Warnung: verarbeitete Ereignisse - FireSchedule|  
|CreateSchedule|Warnung: verarbeitete Ereignisse - CreateSchedule|  
|UpdateSchedule|Warnung: verarbeitete Ereignisse - UpdateSchedule|  
|DeleteSchedule|Warnung: verarbeitete Ereignisse - DeleteSchedule|  
|GenerateAlert|Warnung: verarbeitete Ereignisse - GenerateAlert|  
|DeliverAlert|Warnung: verarbeitete Ereignisse - DeliverAlert|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] stellt Leistungsindikatoren für weitere [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Funktionen bereit. Weitere Informationen finden Sie unter [Leistungsindikatoren für die Leistungsobjekte „ReportServer:Service“ und „ReportServerSharePoint:Service“](../reporting-services/report-server/performance-counters-reportserver-service-performance-objects.md), [Leistungsindikatoren für den MSRS 2011-Webdienst und den MSRS 2011-Windows-Dienst, Leistungsobjekte &#40;einheitlicher Modus&#41;](../reporting-services/report-server/performance-counters-msrs-2011-web-service-performance-objects.md) und [Leistungsindikatoren für den MSRS 2011-Webdienst im SharePoint-Modus und den MSRS 2011-Windows-Dienst im SharePoint-Modus, Leistungsobjekte &#40;SharePoint-Modus&#41;](../reporting-services/report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md).  
  
##  <a name="SupportForSSL"></a> Unterstützung für SSL  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] kann den HTTP-SSL-Dienst (Secure Sockets Layer) verwenden, um verschlüsselte Verbindungen zu einem Berichtsserver oder einer SharePoint-Website herzustellen.  
  
 Die Benutzeroberfläche für den Warnungslaufzeitdienst und die Datenwarnungen unterstützt SSL und funktioniert unabhängig von der Verwendung von SSL oder HTTP ähnlich. Es gibt jedoch einige feine Unterschiede. Wenn die Datenwarnungsdefinition mit einer SSL-Verbindung erstellt wird, verwendet die URL, die zurück auf die SharePoint-Bibliothek von der Datenwarnmeldung verweist, auch SSL. Sie können die SSL-Verbindung identifizieren, da sie in der URL HTTPS anstelle von HTTP verwendet. Ebenso verwendet der Link zurück zur SharePoint-Website HTTP, wenn die Datenwarnungsdefinition mit einer HTTP-Verbindung erstellt wurde. Unabhängig davon, ob die Warnungsdefinition mit SSL oder HTTP erstellt wurde, ist die Erfahrung für Benutzer und Warnungsadministratoren bei der Verwendung des Datenwarnungs-Designers oder Datenwarnungs-Managers identisch. Wenn das Protokoll (HTTP oder SSL) zwischen dem Zeitpunkt der Warnungsdefinitionserstellung, dem anschließenden Update und der erneuten Speicherung geändert wird, wird das ursprüngliche Protokoll beibehalten und in Link-URLs verwendet.  
  
 Wenn Sie eine Datenwarnung für eine SharePoint-Website erstellen, die für die Verwendung von SSL konfiguriert ist, und dann die SSL-Anforderung entfernen, ist die Warnung auf der Website weiterhin funktionsfähig. Wenn die Website gelöscht wird, wird stattdessen die Standardzonenwebsite verwendet.  
  
##  <a name="UserInterface"></a> Benutzeroberfläche für Datenwarnungen  
 Datenwarnungen enthalten SharePoint-Seiten zum Verwalten von Warnungen sowie einen Designer zum Erstellen und Bearbeiten von Datenwarnungsdefinitionen.  
  
-   **Datenwarnungs-Designer** , mit dem Sie Datenwarnungsdefinitionen erstellen oder bearbeiten. Weitere Informationen finden Sie unter [Datenwarnungs-Designer](../reporting-services/data-alert-designer.md), [Erstellen einer Datenwarnung im Datenwarnungs-Designer](../reporting-services/create-a-data-alert-in-data-alert-designer.md) und [Bearbeiten einer Datenwarnung im Warnungs-Designer](../reporting-services/edit-a-data-alert-in-alert-designer.md).  
  
-   **Datenwarnungs-Manager** , mit dem Sie Listen der Datenwarnungen anzeigen, Warnungen löschen und Warnungen zur Bearbeitung öffnen. Der Datenwarnungs-Manager steht in zwei Versionen zur Verfügung: eine für Benutzer zur Verwaltung der Warnungen, die sie erstellt haben, und eine für Administratoren zur Verwaltung der Warnungen, die zu Websitebenutzern gehören.  
  
     Weitere Informationen zum Verwalten der von Ihnen erstellen Datenwarnungen finden Sie unter [Datenwarnungs-Manager für SharePoint-Benutzer](../reporting-services/data-alert-manager-for-sharepoint-users.md) und [Verwalten meiner Datenwarnungen im Datenwarnungs-Manager](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md).  
  
     Weitere Informationen zum Verwalten aller Datenwarnungen auf einer Website finden Sie unter [Datenwarnungs-Manager für Warnungsadministratoren](../reporting-services/data-alert-manager-for-alerting-administrators.md) und [Verwalten aller Datenwarnungen auf einer SharePoint-Website im Datenwarnungs-Manager](../reporting-services/manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md).  
  
-   Stellen Sie**Abonnements und Datenwarnungen** bereit, mit denen Sie herausfinden, ob Reporting Services den SQL Server-Agent für Datenwarnungen verwenden und Skripts herunterladen kann, die den Zugriff auf den SQL Server-Agent ermöglichen. Weitere Informationen finden Sie unter [Provision Subscriptions and Alerts for SSRS Service Applications](../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
##  <a name="Globalization"></a> Globalisierung der Datenwarnungen  
 Bestimmte Schriften wie Arabisch und Hebräisch werden von rechts nach links geschrieben. Datenwarnungen unterstützen Schriften mit Schreibrichtung von rechts nach links und umgekehrt. Datenwarnungen erkennen die Kultur und ändern die Darstellung und das Verhalten der Benutzeroberfläche und des Layouts von Datenwarnmeldungen entsprechend. Die Kultur wird von der regionalen Einstellung des Betriebssystems auf dem Computer des Benutzers abgeleitet. Der Kultur wird bei jedem Update und erneuten Speicherung der Datenwarnungsdefinition gespeichert.  
  
 Ob Daten die Regeln in der Warnungsdefinition erfüllen, kann von der Kultur in der Warnungsdefinition beeinflusst werden. Zeichenfolgenvergleiche werden am häufigsten von kulturspezifischen Regeln beeinflusst.  
  
 Das Ermitteln, ob Daten die Regeln in der Warnungsdefinition erfüllen, kann von der Kultur in der Warnungsdefinition beeinflusst werden. Dies tritt am häufigsten bei Zeichenfolgen auf. Beispielsweise wird in einer Warnungsdefinition mit deutscher Kultur die Regel, die den englischen Buchstaben "o" mit dem deutschen Buchstaben "ö" vergleicht, nicht erfüllt. In der gleichen Warnungsdefinition mit englischer Kultur wird die Regel jedoch erfüllt.  
  
 Die Datenformatierung basiert auch auf der Kultur der Warnungsdefinition. Wenn die Kultur einen Punkt als Dezimalsymbol verwendet, wird zum Beispiel ein Wert als 45.67 angezeigt. Dahingegen wird bei einer Kultur, die ein Komma als Dezimalsymbol verwendet, der Wert 45,67 angezeigt.  
  
 Je nach verwendeter Benutzeroberfläche für Datenwarnungen variiert die Unterstützung für die Schreibrichtung von rechts nach links. Der Datenwarnungs-Designer unterstützt Schriften mit Schreibrichtung von rechts nach links in Textfeldern, aber das Layout des Designers ist nicht von rechts nach links orientiert. Das zugehörige Layout ist wie andere Tools von links nach rechts ausgerichtet. Wenn eine Warnungsdefinition, die mit Textausrichtung von rechts nach links erstellt wurde, in einer Umgebung mit Ausrichtung von links nach rechts bearbeitet wird, wird beim Speichern der Warnungsdefinition die Textausrichtung von rechts nach links beibehalten. Der Datenwarnungs-Manager verhält sich auf die gleiche Weise wie eine SharePoint-Seite. Das zugehörige Layout ist von rechts nach links orientiert – wie andere SharePoint-Seiten auch. Datenwarnmeldungen, die auf Datenwarnungsdefinitionen mit Ausrichtung von rechts nach links basieren, zeigen den Meldungstext von rechts nach links an, und das Meldungslayout ist von links nach rechts ausgerichtet.  
  
##  <a name="HowTo"></a> Verwandte Aufgaben  
  
-   [Speichern eines Berichts in einer SharePoint-Bibliothek &#40;Berichts-Generator&#41;](../reporting-services/report-builder/save-a-report-to-a-sharepoint-library-report-builder.md)  
  
-   [Erstellen einer Datenwarnung im Datenwarnungs-Designer](../reporting-services/create-a-data-alert-in-data-alert-designer.md)  
  
-   [Bearbeiten einer Datenwarnung im Warnungs-Designer](../reporting-services/edit-a-data-alert-in-alert-designer.md)  
  
-   [Verwalten meiner Datenwarnungen im Datenwarnungs-Manager](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md)  
  
-   [Verwalten aller Datenwarnungen auf einer SharePoint-Website im Datenwarnungs-Manager](../reporting-services/manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager.md)  
  
-   [Gewähren von Berechtigungen an Benutzer und Warnungsadministratoren](../reporting-services/grant-permissions-to-users-and-alerting-administrators.md)  
  
## <a name="see-also"></a>Siehe auch

[Datenwarnungs-Designer](../reporting-services/data-alert-designer.md)   
[Datenwarnungs-Manager für Warnungsadministratoren](../reporting-services/data-alert-manager-for-alerting-administrators.md)   
[Datenwarnungs-Manager für SharePoint-Benutzer](../reporting-services/data-alert-manager-for-sharepoint-users.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
