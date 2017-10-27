---
title: Leistungsindikatoren - ReportServer-Dienst, Leistungsobjekte | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Report Server service, performance counters
ms.assetid: 2bcacab2-3a4f-4aae-b123-19d756b9b9ed
caps.latest.revision: 21
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 92bc628afcaed8a45652e58a6073bd5a53df4012
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="performance-counters---reportserver-service--performance-objects"></a>Leistungsindikatoren - ReportServer-Dienst, Leistungsobjekte für ""
  Unter diesem Thema werden Leistungsindikatoren für die Leistungsobjekte **ReportServer:Service** und **ReportServerSharePoint:Service** beschrieben, die Teil einer [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] -Bereitstellung sind.  
  
> [!NOTE]  
>  Mit den Leistungsobjekten werden Ereignisse auf dem lokalen Berichtsserver überwacht. Wenn Sie einen Berichtsserver in einer Bereitstellung für horizontales Skalieren ausführen, beziehen sich die Zahlen auf den aktuellen Server, nicht auf die Bereitstellung für horizontales Skalieren insgesamt.  
  
 Die Leistungsobjekte sind im Windows-Systemmonitor (**Perfmon.exe**) verfügbar. Weitere Informationen finden Sie in der Windows-Dokumentation. [Laufzeit-Profilerstellung](http://msdn.microsoft.com/library/w4bz2147.aspx) (http://msdn.microsoft.com/library/w4bz2147.aspx).  
  
 In diesem Thema:  
  
-   [ReportServer:Service-Leistungsindikatoren (Berichtsserver im einheitlichen Modus)](#bkmk_ReportServer)  
  
-   [ReportServerSharePoint:Service (Berichtsserver im SharePoint-Modus)](#bkmk_ReportServerSharePoint)  
  
-   [Zurückgeben von Listen mithilfe von PowerShell-Cmdlets](#bkmk_powershell)  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
##  <a name="bkmk_ReportServer"></a> ReportServer:Service-Leistungsindikatoren (Berichtsserver im einheitlichen Modus)  
 Das **ReportServer:Service** -Leistungsobjekt enthält eine Reihe von Leistungsindikatoren zum Nachverfolgen HTTP-bezogener und speicherbezogener Ereignisse für eine Berichtsserverinstanz. Dieses Leistungsobjekt erscheint einmalig pro [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Instanz auf dem Computer, und Sie können für jede Instanz Indikatoren zum Leistungsobjekt hinzufügen oder aus dem Leistungsobjekt löschen. Leistungsindikatoren für die Standardinstanz werden im Format **ReportServer:Service**angezeigt. Leistungsindikatoren für benannte Instanzen werden, in dem Format angezeigt **ReportServer$\<***Instance_name***>: Dienst**.  
  
 Das **ReportServer:Service** -Leistungsobjekt ist neu in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Es bietet eine Teilmenge an Indikatoren, die in IIS (Internetinformationsdienste; Internet Information Services) und [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] in früheren Versionen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]enthalten waren. Diese neuen Leistungsindikatoren sind spezifisch für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], und sie verfolgen HTTP-bezogene Ereignisse für den Berichtsserver nach, wie Anforderungen, Verbindungen und Anmeldeversuche. Darüber hinaus schließt dieses Leistungsobjekt Leistungsindikatoren für die Nachverfolgung von Speicherverwaltungsereignissen ein.  
  
 In der folgenden Tabelle werden die im **ReportServer:Service** -Leistungsobjekt enthaltenen Leistungsindikatoren aufgelistet.  
  
 ![PowerShell-Inhalt](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell-Inhalt") folgende Windows PowerShell-Skript gibt die Liste der Leistungsindikatoren für CounterSetName zurück  
  
```  
(get-counter -listset "ReportServer:Service").paths  
```  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|**Aktive Verbindungen**|Die Anzahl der Verbindungen, die aktuell auf dem Server aktiv sind.|  
|**Gesamtanzahl der empfangenen Bytes**|Die Anzahl der vom Server empfangenen Bytes. Dieser Leistungsindikator zählt die Rohbytes, die insgesamt vom Berichts-Manager und Berichtsserver empfangen wurden.|  
|**Empfangene Bytes/Sekunde**|Die Anzahl der vom Server pro Sekunde empfangenen Bytes. Dieser Leistungsindikator wird nur aktualisiert, wenn eine Übertragung abgeschlossen wird. Dies bedeutet, dass der Leistungsindikator zunächst bei 0 bleibt und sich der Wert nach Abschluss der Übertragung erhöht.|  
|**Gesamtanzahl der gesendeten Bytes**|Die Anzahl der vom Server gesendeten Bytes. Dieser Leistungsindikator zählt die Rohbytes, die insgesamt vom Berichts-Manager und Berichtsserver gesendet wurden.|  
|**Gesendete Byte/Sekunde**|Die Anzahl der vom Server pro Sekunde gesendeten Bytes. Dieser Leistungsindikator wird nur aktualisiert, wenn eine Übertragung abgeschlossen wird. Dies bedeutet, dass der Leistungsindikator zunächst bei 0 bleibt und sich der Wert nach Abschluss der Übertragung erhöht.|  
|**Gesamtanzahl der Fehler**|Die Gesamtanzahl der Fehler, die bei der Verarbeitung von HTTP-Anforderungen aufgetreten sind. Diese Fehler schließen HTTP-Statuscodes in den 400ern und 500ern ein.|  
|**Fehler/Sekunde**|Die Gesamtanzahl der Fehler, die bei der Verarbeitung von HTTP-Anforderungen pro Sekunde aufgetreten sind. Diese Fehler schließen HTTP-Statuscodes in den 400ern und 500ern ein.|  
|**Gesamtanzahl der Anmeldeversuche**|Die Anzahl der Anmeldeversuche, die von RSWindows-Authentifizierungstypen vorgenommen werden. Zu den RSWindows-Authentifizierungstypen gehören RSWindowsNegotiate, RSWindowsNTLM, RSWindowsKerberos und RSWindowsBasic. Der Wert 0 (null) stellt die benutzerdefinierte Authentifizierung dar.|  
|**Anmeldeversuche/Sekunde**|Die Rate der Anmeldeversuche.|  
|**Erfolgreiche Anmeldungen gesamt**|Die Anzahl erfolgreicher Anmeldungen für RSWindows-Authentifizierungstypen. Zu den RSWindows-Authentifizierungstypen gehören RSWindowsNegotiate, RSWindowsNTLM, RSWindowsKerberos und RSWindowsBasic. Der Wert 0 (null) stellt die benutzerdefinierte Authentifizierung dar.|  
|**Erfolgreiche Anmeldungen/Sekunde**|Die Rate erfolgreicher Anmeldungen.|  
|**Auslastungsstatus des Arbeitsspeichers**|Eine der folgenden Zahlen, von 1 bis 5, die den aktuellen Speicherzustand des Servers angeben:<br /><br /> 1: Keine Speicherauslastung<br /><br /> 2: Niedrige Speicherauslastung<br /><br /> 3: Mittlere Speicherauslastung<br /><br /> 4: Hohe Speicherauslastung<br /><br /> 5: Speicherauslastung überschritten|  
|**Umfang der Arbeitsspeicherverringerung**|Die Anzahl der Bytes, die der Server angefordert hat, um den belegten Speicher zu reduzieren.|  
|**Benachrichtigungen zur Verringerung des Arbeitsspeichers/Sekunde**|Die Anzahl der Benachrichtigungen, die der Server in der letzten Sekunde ausgibt, um den belegten Speicher zu reduzieren. Dieser Wert gibt an, wie oft der Server einen Speichermangel erfährt.|  
|**Getrennte Anforderungen**|Die Anzahl der Anforderungen, die aufgrund von Kommunikationsfehlern getrennt sind.|  
|**Ausgeführte Anforderungen**|Die Anzahl der Anforderungen, die gerade verarbeitet werden.|  
|**Nicht autorisierte Anforderungen**|Die Anzahl der Anforderungen, die mit einem HTTP-401-Statuscode fehlschlagen.|  
|**Abgelehnte Anforderungen**|Die Gesamtanzahl der Anforderungen, die aufgrund unzureichender Serverressourcen nicht verarbeitet wurden. Dieser Leistungsindikator gibt die Anzahl der Anforderungen wieder, die einen HTTP 503-Statuscode zurückgeben, der darauf hinweist, dass der Server vollständig ausgelastet ist.|  
|**Anforderungen gesamt**|Die Gesamtanzahl der Anforderungen, die vom Berichtsserverdienst seit dem Start empfangen wurden. Dieser Leistungsindikator zählt Anforderungen, die zum Berichts-Manager gesendet wurden, und Anforderungen, die vom Berichts-Manager zum Berichtsserver gesendet wurden.|  
|**Anforderungen/s**|Die Anzahl der Anforderungen, die pro Sekunde verarbeitet werden. Dieser Wert stellt den aktuellen Durchsatz der Anwendung dar.|  
|**Tasks in Warteschlange**|Die Anzahl der Tasks, die darauf warten, dass ein Thread für die Verarbeitung zur Verfügung steht. Jede Anforderung, die an den Berichtsserver gestellt wird, entspricht einer oder mehreren Tasks. Dieser Leistungsindikator stellt nur die Anzahl an Tasks dar, die für die Verarbeitung bereit sind. Er enthält nicht die Anzahl an Tasks, die derzeit ausgeführt werden.|  
  
##  <a name="bkmk_ReportServerSharePoint"></a> ReportServerSharePoint:Service (Berichtsserver im SharePoint-Modus)  
 Das **ReportServerSharePoint:Service** -Leistungsobjekt wurde in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]hinzugefügt.  
  
 ![PowerShell-Inhalt](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell-Inhalt") folgende Windows PowerShell-Skript gibt die Liste der Leistungsindikatoren für CounterSetName zurück  
  
```  
(get-counter -listset "ReportServerSharePoint:Service").paths  
```  
  
|Leistungsindikator|Description|  
|-------------|-----------------|  
|**Auslastungsstatus des Arbeitsspeichers**||  
|**Umfang der Arbeitsspeicherverringerung**||  
|**Memory Shrink Notifications/Sec**||  
  
##  <a name="bkmk_powershell"></a> Zurückgeben von Listen mithilfe von PowerShell-Cmdlets  
 ![PowerShell-Inhalt](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell-Inhalt") folgende Windows PowerShell-Skript gibt die Liste der Leistungsindikatoren für CounterSetName "Reportserversharepoint: Service" zurück:  
  
```  
(get-counter -listset "ReportServerSharePoint:Service").paths  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Leistung des Berichtsservers](../../reporting-services/report-server/monitoring-report-server-performance.md)   
 [Leistungsindikatoren für den MSRS 2011-Webdienst und den MSRS 2011 Windows Service Leistungsobjekte &#40; Im einheitlichen Modus &#41;](../../reporting-services/report-server/performance-counters-msrs-2011-web-service-performance-objects.md)   
 [Leistungsindikatoren für den MSRS 2011-Webdienst im SharePoint-Modus und den MSRS 2011-Windows-Dienst im SharePoint-Modus, Leistungsobjekte &#40;SharePoint-Modus&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)  
  
  

