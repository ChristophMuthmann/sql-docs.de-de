---
title: "Anwendungsdomänen für Berichtsserveranwendungen | Microsoft Docs"
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
- application domains [Reporting Services]
- recycling application domains
ms.assetid: a455e2e6-8764-493d-a1bc-abe80829f543
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0cec89b68c69b5e5ae6875d5d5d5e721008844cd
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="application-domains-for-report-server-applications"></a>Anwendungsdomänen für Berichtsserveranwendungen
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]wird der Berichtsserver als einzelner Dienst implementiert, der den Report Server-Webdienst, den Berichts-Manager und eine Hintergrundverarbeitungsanwendung umfasst. Jede Anwendung wird in einer eigenen Anwendungsdomäne innerhalb des einzelnen Berichtsserverprozesses ausgeführt. Größtenteils werden Anwendungsdomänen intern erstellt, konfiguriert und verwaltet. Es ist jedoch nützlich zu wissen, wie Wiederverwendungsvorgänge für Berichtsserver-Anwendungsdomänen auftreten, wenn Sie Leistungs- oder Speicherprobleme untersuchen oder Dienstausfälle beheben müssen.  
  
> [!NOTE]  
>  Wenn Sie den Zugriff des Berichts-Generators auf einen Berichtsserver konfigurieren, der mit der Standardauthentifizierung arbeitet, wird der Berichts-Generator in seiner eigenen Anwendungsdomäne ausgeführt. Diese Anwendungsdomäne unterscheidet sich von anderen im Serverprozess ausgeführten Anwendungsdomänen. Sie wird vom Service Controller verwaltet und unterliegt nicht den Funktionen zur Speicherverwaltung, die die Speicherbelegung als Reaktion auf Speicherengpässe auf dem Berichtsserver neu anpassen.  
  
 In der folgenden Liste werden die Ereignisse, die Anwendungsdomänen-Wiederverwendungsvorgänge für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Anwendungen verursachen, beschrieben:  
  
-   Geplante Wiederverwendungsvorgänge, die in vordefinierten Intervallen auftreten.  
  
-   Konfigurationsänderungen des Berichtsservers.  
  
-   [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] -Konfigurationsänderungen.  
  
-   Fehler bei der Speicherbelegung.  
  
 In der folgenden Tabelle wird das Anwendungsdomänen-Wiederverwendungsverhalten als Reaktion auf diese Ereignisse zusammengefasst:  
  
|Ereignis|Ereignisbeschreibung|Gilt für|Konfigurierbar|Beschreibung des Wiederverwendungsvorgangs|  
|-----------|-----------------------|----------------|------------------|-----------------------------------|  
|Geplante Wiederverwendungsvorgänge, die in vordefinierten Intervallen auftreten|Standardmäßig werden Anwendungsdomänen alle 12 Stunden wiederverwendet.<br /><br /> Geplante Wiederverwendungsvorgänge finden in [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] -Anwendungen, die dem Gesamtprozesszustand dienen, sehr häufig statt.|Report Server-Webdienst<br /><br /> Berichts-Manager<br /><br /> Hintergrundverarbeitungsanwendung|Ja. Das Wiederverwendungsintervall wird durch die Konfigurationseinstellung**RecycleTime** in der Datei RSReportServer.config festgelegt.<br /><br /> **MaxAppDomainUnloadTime** legt die Wartezeit fest, während der die Hintergrundverarbeitung abgeschlossen werden kann.|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] verwaltet den Wiederverwendungsvorgang für den Webdienst und den Berichts-Manager.<br /><br /> Für die Hintergrundverarbeitungsanwendung erstellt der Berichtsserver eine neue Anwendungsdomäne für neue Aufträge, die durch Zeitpläne initialisiert werden. Bereits ausgeführte Aufträge können in der aktuellen Anwendungsdomäne zu Ende verarbeitet werden, bis die Wartezeit abläuft.|  
|Konfigurationsänderungen des Berichtsservers|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwendet Anwendungsdomänen als Reaktion auf Änderungen in der Datei RSReportServer.config wieder.|Report Server-Webdienst<br /><br /> Berichts-Manager<br /><br /> Hintergrundverarbeitungsanwendung|Nein.|Sie können das Auftreten von Wiederverwendungsvorgängen nicht verhindern. Wiederverwendungsvorgänge, die als Reaktion auf Änderungen der Konfigurationseinstellungen auftreten, werden jedoch auf die gleiche Weise behandelt wie geplante Wiederverwendungsvorgänge. Für neue Anforderungen werden neue Anwendungsdomänen erstellt, während aktuelle Anforderungen und Aufträge in der aktuellen Anwendungsdomäne abgeschlossen werden.|  
|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] -Konfigurationsänderungen|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] verwendet Anwendungsdomänen dann wieder, wenn Änderungen der überwachten Dateien auftreten (z.B. „machine.config“- und „Web.config“-Dateien sowie [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] -Programmdateien).|Report Server-Webdienst<br /><br /> Berichts-Manager|Nein.|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] verwaltet den Vorgang.<br /><br /> Wiederverwendungsvorgänge, die von [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] initiiert werden, beeinflussen die Hintergrundverarbeitungs-Anwendungsdomäne nicht.|  
|Ungenügender Arbeitsspeicher und Fehler bei der Speicherbelegung|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR verwendet Anwendungsdomänen sofort wieder, wenn es zu Fehlern bei der Speicherbelegung kommt oder der Arbeitsspeicher des Servers extrem ausgelastet ist.|Report Server-Webdienst<br /><br /> Berichts-Manager<br /><br /> Hintergrundverarbeitungsanwendung|Nein.|Bei hoher Arbeitsspeicherauslastung akzeptiert der Berichtsserver keine neuen Anforderungen in der aktuellen Anwendungsdomäne. Während des Zeitraums, in dem der Server neue Anforderungen verweigert, treten HTTP 503-Fehler auf. Neue Anwendungsdomänen werden erst dann erstellt, wenn die alte Anwendungsdomäne entladen wird. Wenn Sie daher bei einer hohen Arbeitsspeicherauslastung des Servers Änderungen an Konfigurationsdateien vornehmen, werden ausgeführte Anforderungen und Aufträge möglicherweise nicht gestartet oder abgeschlossen.<br /><br /> Im Fall eines Fehlers bei der Speicherbelegung werden alle Anwendungsdomänen sofort neu gestartet. Gerade ausgeführte Aufträge und Anforderungen werden gelöscht. Sie müssen diese Aufträge und Anforderungen manuell neu starten.|  
  
## <a name="planned-and-unplanned-recycle-operations"></a>Geplante und ungeplante Wiederverwendungsvorgänge  
 Wiederverwendungsvorgänge sind entweder geplant oder ungeplant, je nachdem, wie der jeweilige Vorgang herbeigeführt wird:  
  
-   Geplante Wiederverwendungsvorgänge treten in regelmäßigen Abständen auf, die in der Datei RSReportServer.config definiert sind. Das Standardintervall beträgt 12 Stunden. Dies ist eine bewährte Vorgehensweise für [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] -Anwendungen, die dem Gesamtprozesszustand dienen. Bei geplanten Wiederverwendungsvorgängen erstellt der Berichtsserver zusätzliche Anwendungsdomänen für neue Anforderungen. Bereits ausgeführte Anforderungen können in der aktuellen Anwendungsdomäne zu Ende verarbeitet werden, bis die Wartezeit abläuft. Konfigurationseinstellungen, die geplante Wiederverwendungsvorgänge steuern, werden für den gesamten Server festgelegt. Sie können keine unterschiedlichen Wiederverwendungszeitpläne oder Speicherschwellenwerte für die einzelnen Anwendungen konfigurieren.  
  
-   Nicht geplante Wiederverwendungsvorgänge treten willkürlich als Reaktion auf Konfigurationsänderungen, Speicherauslastung und Speicherbelegungsfehler auf:  
  
    -   Bei Konfigurationsänderungen versucht der Berichtsserver, eine "weiche" Wiederverwendung, bei der neue Anforderungen an eine neue Instanz der Anwendungsdomäne weitergeleitet werden. Wenn dies fehlschlägt, initiiert der Server eine "harte" Anwendungsdomänen-Wiederverwendung, bei der alle gerade ausgeführten Anforderungen abgebrochen, die aktuellen Anwendungsdomänen geschlossen und die Anwendungsdomänen neu gestartet werden.  
  
    -   Fehler bei der Speicherbelegung deuten darauf hin, dass keine ausreichenden Systemressourcen für die vom Server durchgeführte Berichtsverarbeitung verfügbar sind. Ein "harter" Wiederverwendungsvorgang für alle Anwendungsdomänen tritt als Reaktion auf einen Speicherbelegungsfehler auf. Alle Anforderungswarteschlangen werden gelöscht. Abgebrochene Anforderungen werden nicht neu gestartet. Benutzer, die einen Bericht interaktiv angezeigt haben, müssen eine Aktualisierung vornehmen oder den Bericht erneut öffnen. Die geplante Verarbeitung wird zum nächsten geplanten Zeitpunkt durchgeführt. Wenn die Verzögerung nicht akzeptabel ist, können Sie eine Berichtsmomentaufnahme manuell aktualisieren, einen Abonnementzeitplan oder einen Berichtsmomentaufnahme-Zeitplan ändern, damit er sofort ausgeführt wird.  
  
 Die Anwendungsdomänen für den Report Server-Webdienst, den Berichts-Manager und die Hintergrundverarbeitungsanwendung werden entweder zusammen oder einzeln wiederverwendet, je nachdem wodurch die Wiederverwendung ausgelöst wird:  
  
-   Wiederverwendungsvorgänge, die von [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] initiiert werden, wirken sich nur auf folgende [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] -Anwendungen aus: Report Server-Webdienst und Berichts-Manager. [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] verwendet zugrunde liegende Anwendungsdomänen wieder, wenn Änderungen an den überwachten Dateien vorgenommen werden. Wiederverwendungsvorgänge, die von [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] initiiert werden, sind in der Regel unabhängig von Wiederverwendungsvorgängen für die Hintergrundverarbeitungsanwendung.  
  
-   Vom Berichtsserver initiierte Wiederverwendungsvorgänge wirken sich in der Regel auf den Report Server-Webdienst, den Berichts-Manager und die Hintergrundverarbeitungsanwendung aus. Wiederverwendungsvorgänge treten als Reaktion auf Änderungen an den Konfigurationseinstellungen und Neustart von Diensten auf.  
  
## <a name="rsreportserver-configuration-settings-for-application-domains"></a>RSReportServer-Konfigurationseinstellungen für Anwendungsdomänen  
 Die Konfigurationseinstellungen werden in der Datei [RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)angegeben. Im folgenden Beispiel werden die Standardkonfigurationseinstellungen für das geplante Anwendungsdomänen-Wiederverwendungsverhalten veranschaulicht.  
  
 `<RecycleTime>720</RecycleTime>`  
  
 `<MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>`  
  
 In der folgenden Tabelle sind diese Elemente beschrieben.  
  
|Element|Gilt für|Definition|  
|-------------|----------------|----------------|  
|**RecycleTime**|Alle drei [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Anwendungsdomänen|Gibt an, wie oft die Anwendungsdomänen wiederverwendet werden. Der standardmäßige Wiederverwendungszeitplan entspricht dem 12-Stunden-Muster, das in der Regel für die [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] -Anwendungsdomänen-Wiederverwendung gilt. Zum geplanten Zeitpunkt werden alle neuen Anforderungen an die neue Instanz der Anwendungsdomäne weitergeleitet. Zurzeit in der ursprünglichen Instanz ausgeführte Anforderungen werden abgeschlossen. Nach Abschluss aller Prozesse wird die ursprünglichen Instanz gelöscht, und die neue Instanz wird zur einzig aktiven Instanz der Anwendungsdomäne.<br /><br /> Der Standardwert ist 720 Minuten.|  
|**MaxAppDomainUnloadTime**|Nur Hintergrundverarbeitungs-Anwendungsdomäne|Ein Berichtsserver ordnet standardmäßig eine Wartezeit von 30 Minuten zu, in der eine Anwendungsdomäne während eines Wiederverwendungsvorgangs heruntergefahren werden kann. Können die zurzeit ausgeführten Aufträge nicht in der vorgesehenen Zeit abgeschlossen werden (oder dauert ein Auftrag länger, als es die Wartezeit zulässt), wird die Instanz der Anwendungsdomäne sofort neu gestartet. Alle nicht abgeschlossenen Aufträge werden beendet.<br /><br /> Weitere Informationen zum Anzeigen des Status oder Abbrechen von Aufträgen, die auf dem Berichtsserver ausgeführt werden, finden Sie unter [Berichtsserveraufträge abbrechen &#40;Management Studio&#41;](../../reporting-services/tools/cancel-report-server-jobs-management-studio.md).|  
  
> [!NOTE]  
>  Obwohl der Report Server-Webdienst und der Berichts-Manager [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]-Anwendungen sind, reagiert keine dieser Anwendungen auf eine geplante Anwendungsdomänen-Wiederverwendung, die möglicherweise in der Datei machine.config für in IIS gehostete [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]-Anwendungen festgelegt ist.  
  
## <a name="see-also"></a>Siehe auch  
 [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Ändern einer Reporting Services-Konfigurationsdatei &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Konfigurieren von verfügbarem Speicher für Berichtsserveranwendungen](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)  
  
  
