---
title: "Syntax für URL-Reservierungen (SSRS-Konfigurations-Manager) | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- URL reservations
ms.assetid: 30e4be2e-e65d-462c-895a-5a0a636d042f
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d18adbfb6ce7a50b458ac1f8197c197281e9d81e
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="url-reservation-syntax--ssrs-configuration-manager"></a>Syntax für URL-Reservierungen (SSRS-Konfigurations-Manager)
  Dieses Thema beschreibt die Komponenten der URL-Zeichenfolge für den Report Server-Webdienst und den Berichts-Manager. Die intern gespeicherte URL-Zeichenfolge verfügt über eine andere Struktur als eine URL, die Sie in die Adressleiste eines Browserfensters eingeben. Die Zeichenfolge für die URL-Reservierung erscheint im Fenster Ergebnisse des Reporting Services-Konfigurationstools, wenn Sie eine URL konfigurieren, sowie in der Datei RSReportServer.config. Zu wissen, wie die URL-Zeichenfolge definiert wird, kann sich als nützlich erweisen, wenn Sie URL-Reservierungsprobleme beheben oder http.SYS abfragen, um die auf Ihrem Server definierten internen URL-Reservierungen anzuzeigen.  
  
## <a name="url-syntax"></a>URL-Syntax  
 Die Berichtsserver-URL wird im **UrlString** -Element und im **VirtualDirectory** -Element gespeichert. Der Grund für die Trennung von **UrlString** und **VirtualDirectory** in separate Elemente besteht darin, dass für jede [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Anwendung mehrere URL-Zeichenfolgen angegeben werden können, jedoch nur ein virtueller Verzeichnisname zulässig ist.  
  
 In HTTP.SYS schließt die URL-Reservierung sowohl **UrlString** als auch **VirtualDirectory**ein. Die Syntax für eine URL-Reservierung besteht aus den folgenden Komponenten:  
  
 \<Schema > ://\<Hostname >:\<Port > /\<Virtualdirectory >  
  
 In der folgenden Tabelle werden die einzelnen Eigenschaften sowie die jeweils gültigen Werte beschrieben.  
  
|Eigenschaft|Gültige Werte|Beschreibung|  
|--------------|------------------|-----------------|  
|Schema|http oder https|Präfixe für Nicht-SSL- und SSL-Verbindungen.|  
|Hostname|(+) Starker Platzhalter, entspricht dem Wert **(Alle zugewiesenen)** für die IP-Adresse.<br /><br /> (\*) Schwacher Platzhalter, entspricht einer IP-Adresse von **(Alle nicht zugewiesenen)**.<br /><br /> Vollqualifizierter Domänenname<br /><br /> Computername<br /><br /> IP-Adresse (IPV4)<br /><br /> IP-Adresse (IPV6)|Identifiziert den Server auf dem Netzwerk.<br /><br /> (+) Starker Platzhalter ist der Standard. HTTP.SYS akzeptiert alle Anforderungen auf allen Netzwerkadaptern für eine bestimmte Kombination aus Port und virtuellem Verzeichnis. Der Berichtsserver akzeptiert jede Anforderung auf dem Port.<br /><br /> (\*) Schwacher Platzhalter. HTTP.SYS akzeptiert alle Anforderungen, die nicht von anderen URL-Reservierungen auf allen Netzwerkadaptern für eine bestimmte Kombination aus Port und virtuellem Verzeichnis verarbeitet werden.<br /><br /> Der Computername ist der NETBIOS-Name des Computers im Netzwerk.<br /><br /> Der vollqualifizierte Domänenname umfasst die Domänenadresse und den Servernamen, wie bei einem Domänencontroller oder öffentlichen DNS-Server registriert.<br /><br /> Die IP-Adresse (IPV4) ist die IP-Adresse eines Netzwerkadapters auf dem Computer im IPV4-Format: *nnn.nnn.nnn.nnn*.<br /><br /> IP-Adresse (IPV6) ist die IP-Adresse eines Netzwerkadapters auf dem Computer im IPV6-Format: \<Header >:\<Header >:*nnn.nnn.nnn.nnn*.|  
|Port|80<br /><br /> 443<br /><br /> \<Benutzerdefinierte >|Port 80 ist der Standardport für HTTP-Anforderungen an und von einem Server.<br /><br /> Port 443 ist der Standardport für SSL-Verbindungen.<br /><br /> Sie können jeden Port verwenden, der nicht bereits von einer anderen Anwendung reserviert ist.|  
|VirtualDirectory|ReportServer*[_Instanzname]*<br /><br /> Reports*[_Instanzname]*<br /><br /> \<Benutzerdefinierte >|Gibt den Namen der Anwendung an. Dabei handelt es sich um einen Zeichenfolgewert. Standardmäßig verwendet [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ReportServer und Reports als Anwendungsnamen für den Report Server-Webdienst und die Berichts-Manager-Anwendungen. Sie können andere Namen verwenden, wenn Sie es vorziehen.<br /><br /> Dieser Wert ist erforderlich. Er identifiziert die Anwendung.<br /><br /> Geben Sie nur ein virtuelles Verzeichnis für jede Anwendungsinstanz an. Um in der gleichen Instanz mehrere URLs für dieselbe Anwendung zu definieren, erstellen Sie mehrere Versionen von **UrlString**. Um eindeutige Namen für das virtuelle Verzeichnis für mehrere Anwendungsinstanzen zu erstellen, nehmen Sie den Instanznamen ggf. in den Namen des virtuellen Verzeichnisses auf. Verwenden Sie dazu den Unterstrich (_), um den Instanznamen anzuhängen. *InstanceName* ist optional, wird jedoch empfohlen, wenn Sie mehrere Instanzen auf dem gleichen Computer installiert haben. Weitere Informationen dazu, wie Sie URL-Reservierungen für benannte Instanzen festlegen, finden Sie unter [URL-Reservierungen für Berichtsserver-Bereitstellungen mit mehreren Instanzen &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md).<br /><br /> Beim Wert für das virtuelle Verzeichnis wird die Groß-/Kleinschreibung nicht beachtet. Sie können jede beliebige Zeichenfolge verwenden, vorausgesetzt sie enthält keine URL-Trennzeichen oder URL-Codierung.|  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Berichtsserver-URLs &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Konfigurieren einer URL &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  

