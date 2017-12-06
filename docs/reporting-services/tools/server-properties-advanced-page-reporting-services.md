---
title: "Servereigenschaften (Seite Erweitert) – Reporting Services | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/09/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.reportserver.serverproperties.advanced.f1
ms.assetid: 07b78a84-a6aa-4502-861d-349720ef790e
caps.latest.revision: "18"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 4b993a3e2c45709e1095bfeb54919f5261bf6a12
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="server-properties-advanced-page---reporting-services"></a>Servereigenschaften (Seite Erweitert) – Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Verwenden Sie diese Seite, um Systemeigenschaften auf dem Berichtsserver festzulegen. Es gibt eine Anzahl von Möglichkeiten, Systemeigenschaften festzulegen. Dieses Tool stellt eine grafische Benutzeroberfläche bereit, so dass Sie Eigenschaften festlegen können, ohne Code schreiben zu müssen.

Öffnen Sie diese Seite, indem Sie SQL Server Management Studio starten und eine Verbindung mit einer Berichtsserverinstanz herstellen. Klicken Sie mit der rechten Maustaste auf den Namen des Berichtsservers, und klicken Sie anschließend auf **Eigenschaften**. Klicken Sie auf **Erweitert**, um diese Seite zu öffnen.

## <a name="options"></a>enthalten

**EnableMyReports**  
Gibt an, ob die Funktion <legacyBold>Meine Berichte</legacyBold> aktiviert ist. Der Wert **true** gibt an, dass die Funktion aktiviert ist.  

**MyReportsRole**  
Der Name der Rolle, die beim Erstellen von Sicherheitsrichtlinien für die Ordner <legacyBold>Meine Berichte</legacyBold> des Benutzers verwendet wird. Der Standardwert lautet **My Reports Role**.  

**EnableClientPrinting**  
Bestimmt, ob das RSClientPrint-ActiveX-Steuerelement zum Herunterladen vom Berichtsserver verfügbar ist. Gültige Werte sind **true** und **false**. Der Standardwert ist **true**. Weitere Informationen zu zusätzlichen Einstellungen, die für dieses Steuerelement erforderlich sind, finden Sie unter [Aktivieren und Deaktivieren des clientseitigen Drucks für Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  

**EnableExecutionLogging**  
Gibt an, ob die Protokollierung der Berichtsausführung aktiviert ist. Der Standardwert ist **true**. Weitere Informationen zum Berichtsserver-Ausführungsprotokoll finden Sie unter [Berichtsserver-Ausführungsprotokoll und die ExecutionLog3-Ansicht](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  

**ExecutionLogDaysKept**  
Die Anzahl von Tagen, in denen die Berichtsausführungsdaten im Ausführungsprotokoll verbleiben. Gültige Werte für diese Eigenschaft sind **-1** bis **2**,**147**,**483**,**647**. Wenn der Wert **-1** ist, werden Einträge nicht aus der Ausführungsprotokolltabelle gelöscht. Der Standardwert lautet **60**.  

> [!NOTE] 
> Wenn Sie den Wert auf **0** (null) festlegen, werden alle Einträge aus dem Ausführungsprotokoll *gelöscht*. Bei einem Wert von **-1** werden die Einträge im Ausführungsprotokoll nicht gelöscht.

**SessionTimeout**  
Der Zeitraum in Sekunden, in dem die Sitzung aktiv bleibt. Der Standardwert lautet **600**.  

**SharePointIntegratedMode**  
Dies ist eine schreibgeschützte Eigenschaft, die den Servermodus angibt. Wenn dieser Wert False ist, wird der Berichtsserver im einheitlichen Modus ausgeführt.  

**SiteName**  
Der Name der Berichtsserversite, der im Seitentitel des Webportals angezeigt wird. Der Standardwert lautet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Diese Eigenschaft kann eine leere Zeichenfolge sein. Die maximale Länge beträgt 8,000 Zeichen.  

**StoredParametersLifetime**  
Gibt die maximale Anzahl von Tagen an, während derer ein gespeicherter Parameter gespeichert werden kann. Gültige Werte sind **-1**, **+1** bis **2.147.483.647**. Der Standardwert ist **180** Tage.  

**StoredParametersThreshold**  
Gibt die maximale Anzahl von Parameterwerten an, die von dem Berichtsserver gespeichert werden können. Gültige Werte sind **-1**, **+1** bis **2.147.483.647**. Der Standardwert lautet **1500**.  

**UseSessionCookies**  
Gibt an, ob der Berichtsserver beim Kommunizieren mit Clientbrowsern Sitzungscookies verwenden soll. Der Standardwert ist **true**.  

**ExternalImagesTimeout**  
Legt den Zeitraum fest, innerhalb dessen eine externe Bilddatei abgerufen werden muss, bevor bei der Verbindung ein Timeout auftritt. Der Standardwert ist **600** Sekunden.  

**SnapshotCompression**  
Definiert, wie Momentaufnahmen komprimiert werden. Der Standardwert lautet **SQL**. Die folgenden Werte sind gültig:

|Werte|Description|
|---------|---------|
|**location**|Momentaufnahmen werden komprimiert, wenn sie in der Berichtsserver-Datenbank gespeichert werden. Dies ist das aktuelle Verhalten.|
|**Keine**|Momentaufnahmen werden nicht komprimiert.|
|**Alle**|Momentaufnahmen werden bei allen Speicheroptionen komprimiert. Dazu gehören auch die Berichtsserver-Datenbank oder das Dateisystem.|

**SystemReportTimeout**  
Der Standard-Timeoutwert für die Berichtsverarbeitung in Sekunden für alle im Berichtsserver-Namespace verwalteten Berichte. Dieser Wert kann auf Berichtsebene überschrieben werden. Ist diese Eigenschaft festgelegt, versucht der Berichtsserver, die Verarbeitung eines Berichts zu beenden, sobald der angegebene Zeitraum überschritten wird. Gültige Werte sind **-1** bis **2**.**147**.**483**.**647**. Wenn der Wert **-1**ist, tritt bei Berichten im Namespace während der Verarbeitung kein Timeout auf. Der Standardwert lautet **1800**.  

**SystemSnapshotLimit**  
Die maximale Anzahl an Momentaufnahmen, die für einen Bericht gespeichert werden. Gültige Werte sind **-1** bis **2**.**147**.**483**.**647**. Lautet der Wert **-1**, so ist die Anzahl von Momentaufnahmen nicht einschränkt.  

**EnableIntegratedSecurity**  
Bestimmt, ob die integrierte Sicherheit von Windows für Berichtsdatenquellen-Verbindungen unterstützt wird. Der Standardwert ist **True**. Die folgenden Werte sind gültig:

|Werte|Description|
|---------|---------|
|**Wahr**|Die integrierte Sicherheit von Windows ist aktiviert.|
|**False**|Die integrierte Sicherheit von Windows ist nicht aktiviert. Berichtsdatenquellen, die für die Verwendung der integrierten Sicherheit von Windows konfiguriert sind, werden nicht ausgeführt.|

**EnableLoadReportDefinition**  
Wählen Sie diese Option um anzugeben, ob Benutzer eine Ad-hoc-Berichtsausführung von einem Bericht des Berichts-Generators ausführen können. Durch Festlegen dieser Option wird der Wert der **EnableLoadReportDefinition** -Eigenschaft auf dem Berichtsserver bestimmt.  

Wenn Sie diese Option deaktivieren, wird die Eigenschaft auf False festgelegt, und der Berichtsserver generiert keine Berichte mit Durchklicken für Berichte, die ein Berichtsmodell als Datenquelle verwenden. Alle Aufrufe der LoadReportDefinition-Methode werden blockiert.  

Die Deaktivierung dieser Option führt zu einem Sicherheitsrisiko, weil böswillige Benutzer einen Denial-of-Service-Angriff ausführen können, bei dem der Berichtsserver mit LoadReportDefinition-Anforderungen überlastet wird.  

**EnableRemoteErrors**  
Nimmt externe Fehlerinformationen (beispielsweise Fehlerinformationen zu Berichtsdatenquellen) in die Fehlermeldungen auf, die für Benutzer zurückgegeben werden, die Berichte von Remotecomputern anfordern. Gültige Werte sind **true** und **false**. Der Standardwert ist **false**. Weitere Informationen finden Sie unter [Aktivieren von Remotefehlern &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md).  

**EnableReportDesignClientDownload**  
Gibt an, ob das Berichts-Generator-Installationspaket vom Berichtsserver heruntergeladen werden kann. Wenn Sie diese Einstellung deaktivieren, funktioniert die URL zum Berichts-Generator nicht. Weitere Informationen finden Sie unter [Konfigurieren des Berichts-Generator-Zugriffs](../../reporting-services/report-server/configure-report-builder-access.md).  

**EditSessionCacheLimit**  
Gibt die Anzahl von Datencacheeinträgen an, die in einer Berichtsbearbeitungssitzung aktiv sein können. Die Standardanzahl ist 5.  

**EditSessionTimeout**  
Gibt die Anzahl der Sekunden bis zum Timeout einer Berichtsbearbeitungssitzung an. Der Standardwert ist 7.200 Sekunden (2 Stunden).  

**EnableCustomVisuals** ***(nur für Power BI-Berichtsserver)***  
Legt fest, ob Power BI-Berichtsserver die Anzeige von Power BI-Visualisierungselementen ermöglicht. Die Werte sind TRUE und FALSE.  Der Standardwert lautet "True".  

**EnablePowerBIReportExportData** ***(nur für Power BI-Berichtsserver)***  
Ob Power BI-Berichtsserver den Export von Daten aus Power BI-Visualisierungselementen ermöglicht. Die Werte sind TRUE und FALSE.  Der Standardwert lautet "True".  

**ScheduleRefreshTimeoutMinutes** ***(nur für Power BI-Berichtsserver)***  
Timeout bei der Datenaktualisierung in Minuten für die geplante Aktualisierung von Power BI-Berichten mit eingebetteten AS-Modellen. Der Standardwert ist 120 Minuten.

**EnableTestConnectionDetailedErrors**  
Gibt an, ob ausführliche Fehlermeldungen an den Clientcomputer gesendet werden, wenn Benutzer Datenquellverbindungen mit dem Berichtsserver testen. Der Standardwert ist **true**. Wenn die Option auf **false**festgelegt wird, werden nur generische Fehlermeldungen gesendet.

**AccessControlAllowCredentials**  
Gibt an, ob die Antwort auf die Client-Anforderung verfügbar gemacht werden kann, wenn das Kennzeichen „Anmeldeinformationen“ auf TRUE festgelegt ist. Der Standardwert ist **false**.

**AccessControlAllowHeaders** Eine durch Kommas abgetrennte Liste von Headern, die der Server zulässt, wenn ein Client eine Anforderung stellt. Diese Eigenschaft kann aus einer leeren Zeichenfolge bestehen, wobei * angibt, dass alle Header zulässig sind.

**AccessControlAllowMethods** Eine durch Kommas abgetrennte Liste von HTTP-Methoden, die der Server zulässt, wenn ein Client eine Anforderung stellt. Die Standardwerte sind GET, PUT, POST, PATCH, DELETE, wobei * angibt, dass alle Methoden zulässig sind.

**AccessControlAllowOrigin** Eine durch Kommas abgetrennte Liste von Headern, die der Server zulässt, wenn ein Client eine Anforderung stellt. Der Standardwert ist leer, wodurch sämtliche Anforderungen verhindert werden. Wenn * angegeben wird, sind alle Ursprünge zulässig, wenn keine Anmeldeinformationen festgelegt sind. Wenn hingegen Anmeldeinformationen festgelegt sind, muss eine explizite Liste von Ursprüngen angegeben werden.

**AccessControlExposeHeaders** Eine durch Kommas abgetrennte Liste von Headern, die der Server den Clients verfügbar macht. Für diese Einstellung gibt es keinen Standardwert.

**AccessControlMaxAge** Gibt die Anzahl der Sekunden an, für die Ergebnisse einer Preflightanforderung im Cache gespeichert werden können. Der Standardwert ist 600 (10 Minuten).

## <a name="see-also"></a>Siehe auch

[Festlegen von Berichtsservereigenschaften &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Vorgehensweise: Herstellen einer Verbindung mit einem Berichtsserver in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Eigenschaften von Reporting Services](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Berichtsserver im Management Studio (F1-Hilfe)](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[Berichtsserver-Systemeigenschaften](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[Skripts für Bereitstellungs- und Verwaltungsaufgaben](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[Aktivieren und Deaktivieren von "Meine Berichte"](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
