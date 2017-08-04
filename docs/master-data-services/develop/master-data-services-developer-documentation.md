---
title: Master Data Services-Entwicklerdokumentation | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 067b1f69-84eb-4a13-b220-120cd63704b4
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 46b9d4302eb2ba1133fb1840c29112aaebad22b4
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="master-data-services-developer-documentation"></a>Master Data Services Developer Documentation
  Erfahren Sie mehr über das Schreiben von Code aus, um die Darstellung anpassen, wie Sie und Ihre Benutzer interagieren mit [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Vorgehensweise:  
  
-   Schreiben Sie ein Programm, die greift auf die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Webdienst aufzurufen. Die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Webdienst ist ein Windows Communication Foundation (WCF)-Dienst, mit denen Entwickler steuern [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] -Funktionen durch Code.  
  
-   Integrieren Sie [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Funktionen in vorhandene Anwendungen.  
  
-   Schreiben Sie Code, um wiederkehrende oder komplexe Aktionen auszuführen, die sich über die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]-Benutzeroberfläche nur schwer oder gar nicht ausführen lassen.  
  
-   Erstellen Sie einen benutzerdefinierten Workflow, der als Reaktion auf eine von Ihnen angegebene Geschäftsregel ausgeführt wird. Ein benutzerdefinierter Workflow ruft von Ihnen geschriebenen Code auf, durch den jede zum Verarbeiten des Workflows erforderliche Aktion ausgeführt werden kann.  
  
## <a name="master-data-manager-web-service"></a>Master Data Manager-Webdienst  
 Der [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]-Webdienst ermöglicht die programmgesteuerte Verwendung der Funktionen von [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] an jedem Computer, der auf die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]-Website zugreifen kann. Bevor Sie Code für den Zugriff auf den Webdienst schreiben können, müssen Sie Proxyklassen generieren, die in einem von Ihnen angegebenen Namespace enthalten sind. In dieser Dokumentation wird <xref:Microsoft.MasterDataServices> als Proxynamespace verwendet. Die hauptproxyklasse, mit der Sie Webdienstvorgänge auszuführen, ist die <xref:Microsoft.MasterDataServices.ServiceClient> Klasse implementiert die <xref:Microsoft.MasterDataServices.IService> Schnittstelle. Rufen Sie über Ihren Code Methoden der der <xref:Microsoft.MasterDataServices.ServiceClient> -Klasse für den Zugriff auf die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Webdienst aufzurufen. Die übrigen Klassen im Namespace werden von den Webdienstvorgängen verwendet.  
  
### <a name="web-service-content"></a>Webdienstinhalt  
 [Erstellen von Master Data Manager Web Service Proxy Classes](../../master-data-services/develop/create-master-data-manager-web-service-proxy-classes.md)  
 Beschreibt die Aktivierung der Veröffentlichung von Metadaten über die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]-Website sowie die Erstellung von Proxyklassen für den programmgesteuerten Zugriff auf Webdienstvorgänge.  
  
 [Kategorisierte Webdienstvorgänge &#40; Master Data Services &#41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
 Eine nach Kategorien unterteilte Liste der Webdienstvorgänge der der <xref:Microsoft.MasterDataServices.ServiceClient> Klasse.  
  
## <a name="custom-workflows"></a>Benutzerdefinierte Workflows  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] verwendet Geschäftsregeln, um grundlegende Workflowlösungen zu erstellen. Sie können Daten automatisch aktualisieren und validieren und E-Mail-Benachrichtigungen auf Basis von Bedingungen senden, die Sie angeben. Geschäftsregeln in [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] dienen zur Verwaltung der häufigsten workflowszenarien. Erfordert Ihr Workflow eine komplexere Ereignisverarbeitung wie Genehmigungen mit mehreren Ebenen oder komplexe Entscheidungsstrukturen, können Sie [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] so konfigurieren, dass Daten an eine von Ihnen erstellte benutzerdefinierte Assembly gesendet werden. Zur Handhabung von benutzerdefinierten Workflows müssen Sie konfigurieren und starten Sie SQL Server MDS Workflow Integration Service über den webanwendungscomputer, und erstellen Sie eine Assembly, implementiert die <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender> Schnittstelle.  
  
### <a name="custom-workflow-content"></a>Benutzerdefinierter Workflowinhalt  
 [Erstellen Sie einen benutzerdefinierten Workflow &#40; Master Data Services &#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
 Anleitungen zum Erstellen einer workflowhandlerassembly, zum Konfigurieren und starten SQL Server MDS Workflow Integration Service und zum Erstellen einer Geschäftsregel in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , die einen benutzerdefinierten Workflow startet.  
  
## <a name="web-server-namespaces"></a>Webserver-Namespaces  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]wird eine Reihe von Assemblys auf dem Webservercomputer installiert. Diese Assemblys enthalten Namespaces, die für erweiterte Szenarien verwendet werden können, in denen das Verhalten des Webservercomputers angepasst wird. In der folgenden Tabelle werden diese Namespaces beschrieben.  
  
|Namespace|Beschreibung|  
|---------------|-----------------|  
|<xref:Microsoft.MasterDataServices.Deployment>|Enthält Klassen, die zu verwendenden zum Erstellen eines Bereitstellungspakets aus einem Modell und zum Bereitstellen eines Pakets in einer [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Datenbank.|  
|<xref:Microsoft.MasterDataServices.Services>|Enthält eine Klasse, die empfangen und Verarbeiten von Webdienstvorgängen, die versucht, den Webservercomputer über die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Webanwendung.|  
|<xref:Microsoft.MasterDataServices.Services.DataContracts>|Enthält Klassen, mit denen definiert wird, wie Daten vom Clientcomputer über die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]-Webanwendung an den Webservercomputer übergeben werden.|  
|<xref:Microsoft.MasterDataServices.Services.MessageContracts>|Enthält Klassen, mit denen definiert wird, wie Anforderungen und Antworten vom Clientcomputer über die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]-Webanwendung an den Webservercomputer übergeben werden.|  
|<xref:Microsoft.MasterDataServices.Services.ServiceContracts>|Enthält die Schnittstelle, mit der die Vorgänge definiert werden, die durch den [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]-Webdienst aufgerufen werden können.|  
  
  
