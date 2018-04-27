---
title: Erstellen des Dialogfeldes der Webanwendung (Konfigurations-Manager für Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.mds.configmanager.createapp.f1
ms.assetid: e045b41a-4836-47f6-8e78-2b09494b461f
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aef55f518c666c08e853e22608167e851be4914f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="create-web-application-dialog-box-master-data-services-configuration-manager"></a>Webanwendung erstellen (Dialogfeld im Konfigurations-Manager für Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Im Dialogfeld **Webanwendung erstellen** können Sie die [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung erstellen. Diese Webanwendung wird auf der Website erstellt, die Sie auf der Seite **Webkonfiguration** ausgewählt haben.  
  
## <a name="web-application"></a>Webanwendung  
 Der Webserver stellt den Inhalt für diese Webanwendung aus dem Ordner [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] **WebApplication** im Dateisystem bereit. Dieser Speicherort wird beim Setup angegeben. Der Standardpfad lautet: *Laufwerk*:\Programme\Microsoft SQL Server\130\Master Data Services\WebApplication.  
  
|Steuerelementname|Description|  
|------------------|-----------------|  
|Virtueller Pfad|Wählen Sie den virtuellen Pfad aus, unter dem Sie die [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung erstellen möchten. Ein virtueller Pfad ist Teil der URL, die für den Zugriff auf eine Webanwendung verwendet wird.<br /><br /> Diese Liste wird nach den virtuellen Anwendungspfaden gefiltert, unter denen die [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung erstellt werden kann. Sie können keine [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung unter einer anderen [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung erstellen.|  
|Alias|Geben Sie einen Namen für die [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung ein, oder verwenden Sie den Standardnamen. Dieser Name wird in einer URL verwendet, um von einem Webbrowser aus auf die Webanwendung zuzugreifen.|  
  
## <a name="application-pool"></a>Anwendungspool  
  
|Steuerelementname|Description|  
|------------------|-----------------|  
|**Name**|Geben Sie einen eindeutigen Anzeigenamen für einen neuen Anwendungspool ein, oder verwenden Sie den Standardnamen. Diesem Anwendungspool wird die [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung hinzugefügt.<br /><br /> Anwendungspools verfügen über immanente Grenzen, durch die Anwendungen in einem Anwendungspool daran gehindert werden, Einfluss auf Anwendungen in einem anderen Anwendungspool zu nehmen.|  
|**User name**|Geben Sie einen Domänen- und Benutzernamen aus Active Directory ein. Dieses Konto entspricht der Identität des Anwendungspools, in dem die Webanwendung ausgeführt wird. Dieses Konto sollte mit dem Konto identisch sein, das Sie beim Erstellen der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank als Dienstkonto angegeben haben.<br /><br /> Das Konto wird für den Datenbankzugriff der mds_exec-Datenbankrolle in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Datenbank hinzugefügt. Weitere Informationen finden Sie unter [Datenbankanmeldenamen, -benutzer und -rollen &#40;Master Data Services&#41;](../master-data-services/database-logins-users-and-roles-master-data-services.md). Es wird darüber hinaus einer [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Windows-Gruppe wie **MDS_ServiceAccounts** hinzugefügt. Ihr wurden Berechtigungen auf das temporäre Kompilierungsverzeichnis, **MDSTempDir** im Dateisystem erteilt. Weitere Informationen finden Sie unter [Ordner- und Dateiberechtigungen &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).|  
|**Kennwort**|Geben Sie das Kennwort für das angegebene Benutzerkonto ein.|  
|**Kennwort bestätigen**|Geben Sie das Kennwort für das angegebene Benutzerkonto erneut ein. Die Felder **Kennwort** und **Kennwort bestätigen** müssen das gleiche Kennwort enthalten.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Webkonfiguration &#40;Seite im Konfigurations-Manager für Master Data Sevices&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
[Master Data Services – Installation und Konfiguration](../master-data-services/master-data-services-installation-and-configuration.md) [Webanwendungsanforderungen & #40; Master Data Services & #41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [Erstellen einer Master Data Manager-Webanwendung &#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
