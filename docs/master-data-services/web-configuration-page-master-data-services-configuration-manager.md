---
title: "Webkonfiguration (Seite im Konfigurations-Manager f&#252;r Master Data Sevices) | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.mds.configmanager.webconfigpg.f1"
ms.assetid: 7b900778-0169-4e42-9faf-98dc1c01313e
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# Webkonfiguration (Seite im Konfigurations-Manager f&#252;r Master Data Sevices)
  Verwenden Sie die Seite **Webkonfiguration** , um eine Website und eine Webanwendung zu konfigurieren. Sie können ferner die Data Quality Services aktivieren.  
  
## Konfigurieren der Webanwendung  
  
|Steuerelementname|Description|  
|------------------|-----------------|  
|**Website**|Erstellen Sie eine neue Website, wählen Sie die Standardwebsite aus oder wählen Sie eine andere verfügbare Website aus (wenn aufgelistet). Diese Liste zeigt die Websites an, die in Internet Information Services (IIS) auf dem lokalen Computer definiert sind. Wenn Sie eine neue Website erstellen, wird automatisch eine neue Webanwendung erstellt. Wenn Sie den Standard oder eine andere vorhandene Website auswählen, müssen Sie manuell eine Anwendung erstellen.|  
|**Webanwendung**|Wählen Sie eine [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung zur Konfiguration aus. In diesem Feld werden nur die [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendungen in der ausgewählten Website angezeigt.<br /><br /> Wenn nichts angezeigt wird, klicken Sie auf **Erstellen**, um eine Website zu erstellen.|  
|**Create**|Öffnet das Dialogfeld **Webanwendung erstellen** , in dem Sie eine [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung in der ausgewählten Website erstellen. Diese Schaltfläche wird nur aktiviert, wenn die ausgewählte Website über keine Stammwebanwendung verfügt, die als [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung konfiguriert ist.|  
  
## Zuordnen einer Anwendung zu einer Datenbank  
  
|Steuerelementname|Description|  
|------------------|-----------------|  
|**Select**|Öffnet das Dialogfeld **Verbindung mit Server herstellen** , in dem Sie eine Verbindung mit einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz herstellen und eine [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank auswählen, die mit der ausgewählten [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung verknüpft werden soll.|  
|**SQL Server-Instanz**|Zeigt den Namen der ausgewählten [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz an, auf der die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank gehostet wird. Es wird erst ein Eintrag angezeigt, nachdem Sie eine Verbindung mit einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz hergestellt und eine Datenbank ausgewählt haben.|  
|**Datenbank**|Zeigt den Namen der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank an, die der ausgewählten [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung zugeordnet ist. Es wird erst ein Eintrag angezeigt, nachdem Sie eine Verbindung mit einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz hergestellt und eine Datenbank ausgewählt haben.|  
  
## Aktivieren der DQS-Integration  
  
|Steuerelementname|Description|  
|------------------|-----------------|  
|**Integration in Data Quality Services aktivieren**|Aktivieren Sie diese Option, um die in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]. Weitere Informationen finden Sie unter [Enable Data Quality Services Integration with Master Data Services](../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md).|  
  
## Siehe auch  
 [Erste Schritte mit Master Data Services &#40;SQL Server 2016&#41;](../Topic/Get%20Started%20with%20Master%20Data%20Services%20\(SQL%20Server%202016\).md)   
 [Anforderungen für die Webanwendung &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [Erstellen einer Master Data Manager-Webanwendung &#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  