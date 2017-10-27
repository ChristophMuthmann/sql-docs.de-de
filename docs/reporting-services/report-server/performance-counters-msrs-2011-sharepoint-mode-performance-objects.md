---
title: "Leistungsindikatoren für den MSRS 2011 SharePoint-Modus, Leistungsobjekte | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- performance counters [Reporting Services]
- counters [Reporting Services]
- Report Server Windows service, performance counters
- RS Windows Service performance object
- Scheduling and Delivery Processor performance object [Reporting Services]
- performance [Reporting Services]
ms.assetid: 70bf6980-7845-4ab5-8b2a-ebf526d811a6
caps.latest.revision: 52
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 78bd4357f5e6de5706a536c44bddac7f3e33ade6
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="performance-counters-msrs-2011-sharepoint-mode-performance-objects"></a>Leistungsindikatoren für den MSRS 2011 SharePoint-Modus, Leistungsobjekte
  In diesem Thema werden Leistungsobjekte für den **MSRS 2011-Webdienst im SharePoint Modus** und den **MSRS 2011-Windows-Dienst im SharePoint Modus** beschrieben, die Teil einer [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Bereitstellung im SharePoint-Modus sind.  
  
> [!NOTE]  
>  Mit diesen Leistungsobjekten werden Ereignisse auf dem lokalen Berichtsserver überwacht. Wenn Sie einen Berichtsserver in einer Bereitstellung für horizontales Skalieren ausführen, beziehen sich die Zahlen auf den aktuellen Server, nicht auf die Bereitstellung für horizontales Skalieren insgesamt.  
  
 Die Leistungsobjekte sind im Windows-Systemmonitor (**Perfmon.exe**) verfügbar. Weitere Informationen finden Sie in der Windows-Dokumentation. [Laufzeit-Profilerstellung](http://msdn.microsoft.com/library/w4bz2147.aspx) (http://msdn.microsoft.com/library/w4bz2147.aspx).  
  
 Informationen zu Leistungsindikatoren und Berichtsservern im einheitlichen Modus finden Sie unter [Leistungsindikatoren für den MSRS 2011-Webdienst und den MSRS 2011 Windows Service Leistungsobjekte &#40; Im einheitlichen Modus &#41; ](../../reporting-services/report-server/performance-counters-msrs-2011-web-service-performance-objects.md) [Leistungsindikatoren für den MSRS 2011 Web Service SharePoint Mode und den MSRS 2011 Windows Service SharePoint-Modus, Leistungsobjekte (SharePoint-Modus)](../../reporting-services/report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md).  
  
 In diesem Thema:  
  
-   [Leistungsindikatoren für den MSRS 2011-Webdienst im SharePoint Modus](#bkmk_webservice)  
  
-   [Leistungsindikatoren für den MSRS 2011-Windows-Dienst im SharePoint Modus](#bkmk_windowsservice)  
  
-   [Zurückgeben von Listen mithilfe von PowerShell-Cmdlets](#bkmk_powershell)  
  
##  <a name="bkmk_webservice"></a> Leistungsindikatoren für den MSRS 2011-Webdienst im SharePoint Modus  
 Mit dem **MSRS 2011 Web Service SharePoint Mode** -Leistungsobjekt wird die Berichtsserverleistung überwacht. Dieses Leistungsobjekt enthält eine Reihe von Leistungsindikatoren zum Nachverfolgen der Verarbeitung auf einem Berichtsserver, die in der Regel über interaktive Vorgänge zum Anzeigen von Berichten gestartet wird. Bei der Einrichtung dieses Leistungsindikators können Sie diesen auf alle Instanzen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anwenden oder spezifische Instanzen auswählen. Diese Leistungsindikatoren werden zurückgesetzt, sobald [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] den Berichtsserver-Webdienst beendet.  
  
 In der folgenden Tabelle werden die im **MSRS 2011 Web Service SharePoint Mode** -Leistungsobjekt enthaltenen Leistungsindikatoren aufgelistet.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|**Aktive Sitzungen**|Die Anzahl der aktiven Sitzungen. Dieser Leistungsindikator stellt eine kumulierte Anzahl aller durch Berichtsausführungen generierten Browsersitzungen bereit, unabhängig davon, ob sie noch aktiv sind.<br /><br /> Der Leistungsindikator wird verringert, wenn Sitzungsdatensätze entfernt werden. Standardmäßig werden Sitzungen nach einer Inaktivität von zehn Minuten entfernt.|  
|**Cachetreffer/Sekunde**|Die Anzahl der Anforderungen pro Sekunde nach zwischengespeicherten Berichten. Es handelt sich um Anforderungen für erneut gerenderte Berichte, nicht um Anforderungen für direkt aus dem Cache verarbeitete Berichte. (Siehe **Gesamtanzahl der Cachetreffer** weiter unten in diesem Thema.)|  
|**Cachetreffer/Sekunde (Semantikmodelle)**|Die Anzahl der Anforderungen für ein zwischengespeichertes Modell pro Sekunde. Es handelt sich um Anforderungen für erneut gerenderte Berichte, nicht um Anforderungen für direkt aus dem Cache verarbeitete Berichte.|  
|**Cachefehler/Sekunde**|Die Anzahl der Anforderungen pro Sekunde, bei denen kein Bericht aus dem Cache zurückgegeben werden konnte. Stellen Sie mithilfe dieses Leistungsindikators fest, ob die für die Zwischenspeicherung (Datenträger oder Arbeitsspeicherung) verwendeten Ressourcen ausreichend sind.|  
|**Cachefehler/Sekunde (Semantikmodelle)**|Die Anzahl der Anforderungen pro Sekunde, bei denen kein Modell aus dem Cache zurückgegeben werden konnte. Stellen Sie mithilfe dieses Leistungsindikators fest, ob die für die Zwischenspeicherung (Datenträger oder Arbeitsspeicherung) verwendeten Ressourcen ausreichend sind.|  
|**Erste Sitzung: Anforderungen/Sekunde**|Die Anzahl neuer Benutzersitzungen, die pro Sekunde aus dem Berichtsservercache gestartet werden.|  
|**Arbeitsspeicher-Cachetreffer/Sekunde**|Die Angabe, wie oft pro Sekunde Berichte aus dem In-Memory-Cache abgerufen werden. Der*Arbeitsspeichercache* ist ein Bestandteil des Caches, der Berichte im CPU-Arbeitsspeicher speichert. Wenn der In-Memory-Cache verwendet wird, ruft der Berichtsserver keinen zwischengespeicherten Inhalt von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ab.|  
|**Arbeitsspeicher-Cachefehler/Sekunde**|Die Anzahl, wie oft Berichte pro Sekunde nicht aus dem Arbeitsspeichercache abgerufen werden konnten.|  
|**Nächste Sitzung: Anforderungen/Sekunde**|Die Anzahl der Anforderungen für Berichte, die in einer vorhandenen Sitzung geöffnet sind, pro Sekunde (z. B. Berichte, die aus der Momentaufnahme einer Sitzung gerendert wurden).|  
|**Berichtsanforderungen**|Die Anzahl der Berichte, die derzeit aktiv sind und vom Berichtsserver verarbeitet werden.|  
|**Ausgeführte Berichte/Sekunde**|Die Anzahl der erfolgreichen Berichtsausführungen pro Sekunde. Dieser Leistungsindikator stellt Statistiken zum Berichtsumfang bereit. Verwenden Sie diesen Leistungsindikator zusammen mit **Anforderung/Sekunde** , um die Berichtsausführung mit den Berichtsanforderungen zu vergleichen, die aus dem Cache zurückgegeben werden können.|  
|**Anforderungen/Sekunde**|Die Anzahl der Anforderungen pro Sekunde, die an den Berichtsserver gesendet werden. Dieser Leistungsindikator verfolgt alle Anforderungstypen, die vom Berichtsserver verarbeitet werden.|  
|**Gesamtanzahl der Cachetreffer**|Die Gesamtzahl der Anforderungen nach Berichten aus dem Cache, seit der Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, sobald der Berichtsserver-Webdienst von [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] beendet wird.|  
|**Cachetreffer gesamt (Semantikmodelle)**|Die Gesamtanzahl der Anforderungen für ein Modell aus dem Cache, seit der Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, sobald der Berichtsserver-Webdienst von ASP.NET beendet wird.|  
|**Cachefehler gesamt**|Die Anzahl, wie oft ein Bericht insgesamt nicht aus dem Cache zurückgegeben werden konnte, seit der Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, sobald der Berichtsserver-Webdienst von [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] beendet wird. Mit diesem Leistungsindikator bestimmen Sie, ob ausreichend Speicherplatz und Arbeitsspeicher vorhanden sind.|  
|**Cachefehler gesamt (Semantikmodelle)**|Die Gesamthäufigkeit, mit der ein Modell nicht aus dem Cache zurückgegeben werden konnte, seit der Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, sobald der Berichtsserver-Webdienst von ASP.NET beendet wird. Mit diesem Leistungsindikator bestimmen Sie, ob ausreichend Speicherplatz und Arbeitsspeicher vorhanden sind.|  
|**Arbeitsspeicher-Cachetreffer gesamt**|Die Gesamtzahl der zwischengespeicherten Berichte, die aus dem Arbeitsspeichercache zurückgegeben wurden, seit der Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, sobald der Berichtsserver-Webdienst von [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] beendet wird. Der*In-Memory-Cache* ist ein Bestandteil des Caches, der Berichte im CPU-Speicher speichert. Wenn der In-Memory-Cache verwendet wird, ruft der Berichtsserver keinen zwischengespeicherten Inhalt von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ab.|  
|**Arbeitsspeicher-Cachefehler gesamt**|Die Gesamtzahl der Cachefehlversuche für den In-Memory-Cache, seit der Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, sobald der Berichtsserver-Webdienst von [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] beendet wird.|  
|**Verarbeitungsfehler gesamt**|Die Anzahl der Fehler bei der Anforderungsverarbeitung im Berichtsserver-Webdienst.|  
|**Abgelehnte Threads gesamt**|Die Gesamtanzahl der für die asynchrone Verarbeitung abgelehnten Threads, die anschließend im selben Thread als synchrone Prozesse verarbeitet wurden. Jede Datenquelle wird in einem Thread verarbeitet. Falls die Anzahl der Threads die Kapazität überschreitet, werden Threads für die asynchrone Verarbeitung abgelehnt und seriell verarbeitet.|  
|**Ausgeführte Berichte gesamt**|Die Gesamtzahl der erfolgreich ausgeführten Berichte, seit der Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, sobald der Berichtsserver-Webdienst von [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] beendet wird.|  
|**Anforderungen gesamt**|Die Gesamtzahl der Anforderungen an den Berichtsserver, seit der Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, sobald der Berichtsserver-Webdienst von [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] beendet wird.|  
  
##  <a name="bkmk_windowsservice"></a> Leistungsindikatoren für den MSRS 2011-Windows-Dienst im SharePoint Modus  
 Mit diesem **MSRS 2011 Windows Service SharePoint Mode** -Leistungsobjekt wird der Berichtsserver-Windows-Dienst überwacht. Das Leistungsobjekt enthält eine Reihe von Leistungsindikatoren zum Nachverfolgen der Berichtsverarbeitung, die über geplante Vorgänge gestartet wird. Zu geplanten Vorgängen zählen Abonnierung und Übermittlung, Momentaufnahmen zur Berichtsausführung und der Berichtsverlauf. Bei der Einrichtung dieses Leistungsindikators können Sie diesen auf alle Instanzen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anwenden oder spezifische Instanzen auswählen.  
  
 In der folgenden Tabelle werden die im **MSRS 2011 Windows Service SharePoint mode** -Leistungsobjekt enthaltenen Leistungsindikatoren aufgelistet.  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|**Aktive Sitzungen**|Die Anzahl der aktiven Sitzungen, die in der Berichtsserver-Datenbank gespeichert sind. Dieser Leistungsindikator liefert die Gesamtanzahl aller verfügbaren Browsersitzungen, die aus Berichtsabonnements generiert wurden, unabhängig davon, ob sie noch aktiv sind oder nicht.|  
|**Warnung: Länge der Ereigniswarteschlange**||  
|**Warnung: verarbeitete Ereignisse - CreateSchedule**||  
|**Warnung: verarbeitete Ereignisse - DeleteSchedule**||  
|**Warnung: verarbeitete Ereignisse - DeliverAlert**||  
|**Warnung: verarbeitete Ereignisse - FireAlert**||  
|**Warnung: verarbeitete Ereignisse - FireSchedule**||  
|**Warnung: verarbeitete Ereignisse - GenerateAlert**||  
|**Warnung: verarbeitete Ereignisse - UpdateSchedule**||  
|**Cacheleerungen/Sekunde**|Die Anzahl der Cacheleerungen pro Sekunde.|  
|**Cachetreffer/Sekunde**|Die Anzahl der Anforderungen pro Sekunde nach zwischengespeicherten Berichten. Es handelt sich um Anforderungen für erneut gerenderte Berichte, nicht um Anforderungen für direkt aus dem Cache verarbeitete Berichte. (Siehe **Gesamtanzahl der Cachetreffer** weiter unten in diesem Thema.)|  
|**Cachetreffer/Sekunde (Semantikmodelle)**|Die Anzahl der Anforderungen für zwischengespeicherte Modelle pro Sekunde.|  
|**Cachefehler/Sekunde**|Die Anzahl der Anforderungen pro Sekunde, bei denen kein Bericht aus dem Cache zurückgegeben werden konnte. Stellen Sie mithilfe dieses Leistungsindikators fest, ob die für die Zwischenspeicherung (Datenträger oder Arbeitsspeicherung) verwendeten Ressourcen ausreichend sind.|  
|**Cachefehler/Sekunde (Semantikmodelle)**|Die Anzahl der Anforderungen pro Sekunde, bei denen kein Modell aus dem Cache zurückgegeben werden konnte. Stellen Sie mithilfe dieses Leistungsindikators fest, ob die für die Zwischenspeicherung (Datenträger oder Arbeitsspeicherung) verwendeten Ressourcen ausreichend sind.|  
|**Übermittlungen/Sekunde**|Die Anzahl der Berichtsübermittlungen pro Sekunde, von jeder Übermittlungserweiterung.|  
|**Ereignisse/Sekunde**|Die Anzahl der pro Sekunde verarbeiteten Ereignisse. Zu den überwachten Ereignissen gehören **SnapshotUpdated** und **TimedSubscription**.|  
|**Erste Sitzung: Anforderungen/Sekunde**|Die Anzahl neuer Berichtsausführungssitzungen, die pro Sekunde erstellt wurden.|  
|**Arbeitsspeicher-Cachetreffer/Sekunde**|Die Angabe, wie oft pro Sekunde Berichte aus dem In-Memory-Cache abgerufen werden. Der*Arbeitsspeichercache* ist ein Bestandteil des Caches, der Berichte im CPU-Arbeitsspeicher speichert. Wenn der In-Memory-Cache verwendet wird, ruft der Berichtsserver keinen zwischengespeicherten Inhalt von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ab.|  
|**Arbeitsspeicher-Cachefehler/Sekunde**|Die Angabe, wie oft Berichte pro Sekunde nicht aus dem In-Memory-Cache abgerufen werden können.|  
|**Nächste Sitzung: Anforderungen/Sekunde**|Die Anzahl der Anforderungen für Berichte, die in einer vorhandenen Sitzung geöffnet sind, pro Sekunde (z. B. Berichte, die aus der Momentaufnahme einer Sitzung gerendert wurden).|  
|**Berichtsanforderungen**|Die Anzahl der Berichte, die derzeit aktiv sind und vom Berichtsserver verarbeitet werden. Verwenden Sie diesen Leistungsindikator, um die Zwischenspeicherungsstrategie auszuwerten. Es können u. U. wesentlich mehr Anforderungen als generierte Berichte vorhanden sein.|  
|**Ausgeführte Berichte/Sekunde**|Die Anzahl der erfolgreich generierten Berichte pro Sekunde.|  
|**Anforderungen/Sekunde**|Die Gesamtanzahl erfolgreicher Anforderungen, die vom Berichtsserverdienst pro Sekunde verarbeitet wurden.|  
|**Updates von Momentaufnahmen/Sekunde**|Die Gesamtanzahl der Updates von Berichtsausführungs-Momentaufnahmen pro Sekunde.|  
|**Wiederverwendungen der Anwendungsdomäne gesamt**|Die Gesamtzahl der Anwendungsdomänenzyklen, nachdem der Berichtsserver-Windows-Dienst gestartet wurde.|  
|**Cacheleerungen gesamt**|Die Gesamtzahl der Cacheupdates des Berichtsservers, nachdem der Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, wenn die Anwendungsdomäne wiederverwendet wird. Siehe **Cacheleerungen/Sekunde**.|  
|**Cachetreffer gesamt**|Die Gesamtzahl der Anforderungen nach direkt aus dem Cache verarbeiteten Berichten, nachdem der Berichtsserver-Windows-Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, wenn die Anwendungsdomäne wiederverwendet wird. Siehe **Cachetreffer/Sekunde**.|  
|**Cachetreffer gesamt (Semantikmodelle)**|Die Gesamtanzahl der Modellanforderungen, die direkt aus dem Cache verarbeitet wurden, nachdem der Berichtsserver-Windows-Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, wenn die Anwendungsdomäne wiederverwendet wird.|  
|**Cachefehler gesamt**|Die Gesamtanzahl, wie oft ein Bericht nicht aus dem Cache zurückgegeben werden konnte, nachdem der Berichtsserver-Windows-Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, wenn die Anwendungsdomäne wiederverwendet wird. Siehe **Cachefehler/Sekunde**.|  
|**Cachefehler gesamt (Semantikmodelle)**|Die Gesamthäufigkeit, mit der ein Modell nicht aus dem Cache zurückgegeben werden konnte, nachdem der Berichtsserver-Windows-Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, wenn die Anwendungsdomäne wiederverwendet wird.|  
|**Übermittlungen gesamt**|Die Gesamtzahl der Berichte, die vom Prozessor für Zeitplanung und Übermittlung für alle Übermittlungserweiterungen übermittelt wurden. Dieser Leistungsindikator wird zurückgesetzt, wenn die Anwendungsdomäne wiederverwendet wird.|  
|**Ereignisse insgesamt**|Die Gesamtzahl der Ereignisse, nachdem der Berichtsserver-Windows-Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, wenn die Anwendungsdomäne wiederverwendet wird.|  
|**Arbeitsspeicher-Cachetreffer gesamt**|Die Gesamtzahl der zwischengespeicherten Berichte, die aus dem In-Memory-Cache zurückgegeben wurden, nachdem der Berichtsserver-Windows-Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, wenn die Anwendungsdomäne wiederverwendet wird.|  
|**Arbeitsspeicher-Cachefehler gesamt**|Die Gesamtzahl der Cachefehlversuche für den In-Memory-Cache, seit der Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, wenn die Anwendungsdomäne wiederverwendet wird.|  
|**Verarbeitungsfehler gesamt**|Die Anzahl der Fehler bei der Anforderungsverarbeitung für den Berichtsserver-Windows-Dienst.|  
|**Abgelehnte Threads gesamt**|Die Gesamtanzahl der für die asynchrone Verarbeitung abgelehnten Threads, die anschließend im selben Thread als synchroner Prozess verarbeitet wurden. Bei mittlerer bis starker Auslastung wird dieser Leistungsindikator laufend erhöht.|  
|**Ausgeführte Berichte gesamt**|Die Gesamtzahl der ausgeführten Berichte.|  
|**Anforderungen gesamt**|Die Gesamtzahl der erfolgreich ausgeführten Berichte, seit der Dienst gestartet wurde. Dieser Leistungsindikator wird zurückgesetzt, wenn die Anwendungsdomäne wiederverwendet wird.|  
|**Updates von Momentaufnahmen gesamt**|Die Gesamtanzahl der Updates von Berichtsausführungs-Momentaufnahmen.|  
  
##  <a name="bkmk_powershell"></a> Zurückgeben von Listen mithilfe von PowerShell-Cmdlets  
 ![PowerShell-Inhalt](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell-Inhalt")folgende Windows PowerShell-Skript gibt die Indikatorensätze zurück, in denen countersetname mit "MSR"beginnt.  
  
```  
get-counter -listset msr*  
Returns a list with the following information  
CounterSetName     : MSRS 2011 Windows Service SharePoint Mode  
CounterSetName     : MSRS 2011 Web Service SharePoint Mode  
```  
  
 Das folgende Windows PowerShell-Skript gibt die Liste der Leistungsindikatoren zurück, bei denen für CounterSetName „MSRS 2011 Windows Service SharePoint Mode“ festgelegt ist.  
  
```  
(get-counter -listset "MSRS 2011 Windows Service SharePoint Mode").paths  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Leistung des Berichtsservers](../../reporting-services/report-server/monitoring-report-server-performance.md)   
 [Leistungsindikatoren für den MSRS 2011-Webdienst und den MSRS 2011 Windows Service Leistungsobjekte &#40; Im einheitlichen Modus &#41;](../../reporting-services/report-server/performance-counters-msrs-2011-web-service-performance-objects.md)   
 [Performance Counters for the ReportServer:Service  and ReportServerSharePoint:Service Performance Objects (Leistungsindikatoren für die Leistungsobjekte ReportServer:Service und ReportServerSharePoint:Service)](../../reporting-services/report-server/performance-counters-reportserver-service-performance-objects.md)  
  
  

