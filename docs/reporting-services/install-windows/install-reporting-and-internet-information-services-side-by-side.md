---
title: Gleichzeitiges Installieren von Reporting Services und Internetinformationsdiensten | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: deploying [Reporting Services], IIS
ms.assetid: 9b651fa5-f582-4f18-a77d-0dde95d9d211
caps.latest.revision: "40"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 751e6e715cc660cadb66c927d24b63d01361f581
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="install-reporting-and-internet-information-services-side-by-side"></a>Gleichzeitiges Installieren von Reporting Services und Internetinformationsdiensten

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Sie können SQL Server Reporting Services (SSRS) und die Internetinformationsdienste (IIS) auf dem gleichen Computer installieren und ausführen. Je nach IIS-Version treten bestimmte Interoperabilitätsprobleme auf.  
  
|IIS-Version|Probleme|Beschreibung|  
|-----------------|------------|-----------------|  
|8.0, 8.5|Für eine bestimmte Anwendung vorgesehene Anforderungen werden von einer anderen Anwendung angenommen.<br /><br /> HTTP.SYS erzwingt Rangfolgeregeln für URL-Reservierungen. Anforderungen, die an Anwendungen gesendet werden, die den gleichen virtuellen Verzeichnisnamen aufweisen und gemeinsam Port 80 überwachen, erreichen möglicherweise nicht das vorgesehene Ziel, wenn die URL-Reservierung im Vergleich zur URL-Reservierung einer anderen Anwendung schwach ist.|Unter bestimmten Bedingungen empfängt ein registrierter Endpunkt, der einen anderen URL-Endpunkt im URL-Reservierungsschema außer Kraft setzt, HTTP-Anforderungen für die andere Anwendung.<br /><br /> Durch die Verwendung eindeutiger Namen für die virtuellen Verzeichnisse des Berichtsserver-Webdiensts und des [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] s kann dieser Konflikt vermieden werden.<br /><br /> Detaillierte Informationen über dieses Szenario sind in diesem Thema enthalten.|  
  
## <a name="precedence-rules-for-url-reservations"></a>Rangfolgeregeln für URL-Reservierungen  
 Um die Interoperabilitätsprobleme zwischen IIS und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]lösen zu können, müssen Sie zunächst die URL-Reservierungsrangfolgeregeln verstehen. Rangfolgeregeln können folgendermaßen beschrieben werden: Je expliziter eine URL-Reservierung definiert ist, umso eher erhält sie die Anforderungen für diese URL.  
  
-   Eine URL-Reservierung, die ein virtuelles Verzeichnis angibt, ist expliziter als eine URL-Reservierung ohne virtuelles Verzeichnis.  
  
-   Eine URL-Reservierung, die eine einzige Adresse angibt (mittels einer IP-Adresse, eines vollqualifizierten Domänennamens, eines Computernamens im Netzwerk oder eines Hostnamens) ist expliziter als ein Platzhalter.  
  
-   Eine URL-Reservierung, die einen starken Platzhalter angibt, ist expliziter als eine URL-Reservierung mit einem schwachen Platzhalter.  
  
 In den folgenden Beispielen werden verschiedene URL-Reservierungen gezeigt. Als Erste steht die URL-Reservierung mit der höchsten Explizität, als Letzte die mit der geringsten Explizität:  
  
|Beispiel|Anforderung|  
|-------------|-------------|  
|`http://123.234.345.456:80/reports`|Empfängt alle Anforderungen, die an `http://123.234.345.456/reports` oder `http://\<computername>/reports` gesendet werden, wenn ein Domain Name Service die IP-Adresse in diesen Hostnamen auflösen kann.|  
|`http://+:80/reports`|Empfängt alle Anforderungen, die an eine IP-Adresse oder einen Hostnamen gesendet werden, die bzw. der gültig für diesen Computer ist, sofern die URL den Namen des virtuellen Verzeichnisses "reports" enthält.|  
|`http://123.234.345.456:80`|Empfängt alle Anforderungen, die `http://123.234.345.456` oder `http://\<computername>` angeben, wenn ein Domain Name Service die IP-Adresse in diesen Hostnamen auflösen kann.|  
|`http://+:80`|Empfängt für alle Anwendungsendpunkte, die **Alle zugewiesenen**zugeordnet sind, Anforderungen, die nicht bereits von anderen Anwendungen empfangen wurden.|  
|`http://*:80`|Empfängt für Anwendungsendpunkte, die **Alle nicht zugewiesenen**zugeordnet sind, Anforderungen, die nicht bereits von anderen Anwendungen empfangen wurden.|  
  
 Ein Zeichen für einen Portkonflikt ist die folgende Fehlermeldung: 'System.IO.FileLoadException: Der Prozess kann nicht auf die Datei zugreifen, da sie von einem anderen Prozess verwendet wird. (Ausnahme von HRESULT: 0x80070020).  
  
## <a name="url-reservations-for-iis-80-85-with-sql-server-reporting-services"></a>URL-Reservierungen für IIS 8.0, 8.5 mit SQL Server Reporting Services  
 Anhand der im vorherigen Abschnitt beschriebenen Rangfolgeregeln wird deutlich, wie die für Reporting Services und IIS definierten URL-Reservierungen zur Interoperabilität beitragen. Reporting Services empfängt Anforderungen, die die Namen der virtuellen Verzeichnisse seiner Anwendungen explizit angeben; IIS empfängt alle verbleibenden Anforderungen, die dann an Anwendungen umgeleitet werden können, die innerhalb des IIS-Verarbeitungsmodells ausgeführt werden.  
  
|Application|URL-Reservierung|Beschreibung|Anforderungsempfang|  
|-----------------|---------------------|-----------------|---------------------|  
|Berichtsserver|`http://+:80/ReportServer`|Starker Platzhalter an Port 80, mit virtuellem Verzeichnis "ReportServer".|Empfängt alle Anforderungen an Port 80, die das virtuelle Verzeichnis "ReportServer" angeben. Der Berichtsserver-Webdienst empfängt alle Anforderungen an http://\<Computername>/reportserver.|  
|Webportal|`http://+:80/Reports`|Starker Platzhalter an Port 80, mit virtuellem Verzeichnis "Reports".|Empfängt alle Anforderungen an Port 80, die das virtuelle Verzeichnis "reports" angeben. Das [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] empfängt alle Anforderungen an http://\<Computername>/reports.|  
|IIS|`http://*:80/`|Schwacher Platzhalter an Port 80.|Empfängt an Port 80 alle verbleibenden Anforderungen, die nicht von einer anderen Anwendung empfangen wurden.|  

## <a name="side-by-side-deployments-of-sql-server-reporting-services-on-iis-80-85"></a>Parallele Bereitstellungen von SQL Server Reporting Services in IIS 8.0, 8.5

 Interoperabilitätsprobleme zwischen IIS und Reporting Services treten auf, wenn IIS-Websites und Reporting Services identische Namen virtueller Verzeichnisse aufweisen. Gehen wir beispielsweise von folgender Konfiguration aus:  
  
-   Eine Website in IIS, die Port 80 und einem virtuellen Verzeichnis mit dem Namen "Reports" zugewiesen ist.  
  
-   Eine in der Standardkonfiguration installierte Berichtsserverinstanz, bei der die URL-Reservierung auch Port 80 angibt und die [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]-Anwendung auch „Reports“ als Namen des virtuellen Verzeichnisses verwendet.  
  
 Bei dieser Konfiguration wird eine an http://\<Computername>:80/reports gesendete Anforderung vom [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] empfangen. Die Anwendung, auf die über das virtuelle Verzeichnis „Reports“ in IIS zugegriffen wird, empfängt nach der Installation der Berichtsserverinstanz keine Anforderungen mehr.  
  
 Wenn Sie die Bereitstellungen älterer und neuerer Versionen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]gleichzeitig ausführen, tritt unter Umständen das gerade beschriebene Routingproblem auf. Dies liegt daran, dass alle [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Versionen „ReportServer“ und „Reports“ als Namen der virtuellen Verzeichnisse für den Berichtsserver und die [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] anwendungen verwenden und damit die Wahrscheinlichkeit erhöht wird, dass in IIS die virtuellen Verzeichnisse „reports“ und „reportserver“ vorhanden sind.  
  
 Um sicherzustellen, dass alle Anwendungen Anforderungen empfangen, sollten Sie diesen Richtlinien folgen:  
  
-   In Reporting Services-Installationen sollten Sie Namen für virtuelle Verzeichnisse angeben, die nicht bereits von einer IIS-Website an dem Port verwendet werden, den auch Reporting Services verwendet. Wenn ein Konflikt auftritt, müssen Sie Reporting Services im Dateimodus installieren (über die Option Server installieren, jedoch nicht konfigurieren im Installations-Assistenten), sodass Sie die virtuellen Verzeichnisse nach dem Setup konfigurieren können. Ein Zeichen für einen Konflikt in Ihrer Konfiguration ist die folgende Fehlermeldung: 'System.IO.FileLoadException: Der Prozess kann nicht auf die Datei zugreifen, da sie von einem anderen Prozess verwendet wird. (Ausnahme von HRESULT: 0x80070020).  
  
-   Übernehmen Sie für Installationen, die Sie manuell konfigurieren, die Standardnamenskonventionen in den URLs. Wenn Sie [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] als benannte Instanz installieren, müssen Sie beim Erstellen eines virtuellen Verzeichnisses den Instanznamen angeben.  

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren von Berichtsserver-URLs](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[Konfigurieren einer URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Installieren des Reporting Services-Berichtsservers im einheitlichen Modus](../../reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
