---
title: Erstellen von Master Data Manager Web Service Proxy Classes | Microsoft Docs
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
ms.assetid: 8bdab026-a0c0-41f3-9d36-f3919c23247f
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a45cd15ced90aef95feb03f8fbaafd5aa70cb746
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>Erstellen von Proxyklassen für den Master Data Manager-Webdienst
  Der [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]-Webdienst ermöglicht die programmgesteuerte Verwendung der Funktionen von [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] an jedem Computer, der auf die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]-Website zugreifen kann. Vor dem Schreiben des Codes für den Zugriff auf den Webdienst sind Proxyklassen zu erstellen. Die hauptproxyklasse, mit der Sie Webdienstvorgänge auszuführen, ist die <xref:Microsoft.MasterDataServices.ServiceClient> Klasse implementiert die <xref:Microsoft.MasterDataServices.IService> Schnittstelle.  
  
## <a name="enable-web-service-metadata-publishing"></a>Aktivieren der Veröffentlichung von Webdienst-Metadaten  
 Bevor Sie Proxyklassen generieren können, ist die Veröffentlichung der Webdienst-Metadaten zu aktivieren. Gehen Sie dazu folgendermaßen vor:  
  
1.  Öffnen der [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Datei "Web.config" in einem Text-Editor. Diese Datei befindet sich im Ordner "WebApplication" des [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Installationspfads.  
  
2.  Suchen der **MdsWsHttpBehavior** Handlerbereich unter dem  **\<ServiceBehaviors >**. Für die  **\<ServiceMetadata >** -Elementgruppe, **HttpGetEnabled** auf **"true"**.  
  
    > [!NOTE]  
    >  Wenn Sie Webdienste über Secure Sockets Layer (SSL) aktivieren möchten, legen Sie **HttpsGetEnabled** auf **"true"** in der **MdsWsHttpBehavior** Abschnitt der Datei "Web.config". Sie müssen auch ändern **MdsWsHTTPBinding** , damit sie für SSL, ebenfalls, und kommentieren Sie den Abschnitt "nicht-SSL" konfiguriert ist.  
  
3.  Speichern Sie die an der Datei vorgenommenen Änderungen.  
  
4.  Testen Sie die Veröffentlichung von Metadaten durch Navigieren zur Dienst-URL, z. B.: `http://yourserver/MDS/service/service.svc`. Ist die Metadaten-Veröffentlichung aktiviert, wird eine Seite angezeigt. Diese beginnt mit:   
    "Sie haben einen Dienst erstellt."  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>Erstellen von Proxyklassen mit Visual Studio  
 Wenn Sie Visual Studio 2010 installiert haben, ist die einfachste Methode zum Generieren von Proxyklassen Hinzufügen einer **Dienstverweis** zu Ihrem Projekt. Die Adresse des Dienstverweises ist die URL der [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]-Webanwendung, wobei "/service/service.svc" angefügt wird. Beispiel: `http://yourserver/MDS/service/service.svc` Weitere Informationen finden Sie unter [wie: hinzufügen, aktualisieren oder Entfernen eines Dienstverweises](http://go.microsoft.com/fwlink/?LinkId=221167).  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>Erstellen von Proxyklassen mit "Svcutil.exe"  
 Benötigen Sie entweder [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows SDK installiert, um Svcutil.exe auf Ihrem Computer verfügen. Wenn Sie [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] verwenden, müssen Sie den Befehl über die [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]-Eingabeaufforderung ausführen. Weitere Informationen finden Sie unter [ServiceModel Metadata Utility Tool (Svcutil.exe)](http://go.microsoft.com/fwlink/?LinkId=165027) und [Generieren eines WCF-Clients aus Dienstmetadaten](http://go.microsoft.com/fwlink/?LinkId=164821).  
  
 Verwenden Sie zum Erstellen mehrerer C#-Proxyklassen mit "Svcutil.exe" einen Befehl wie folgt:  
  
```  
svcutil.exe http://<server_name:port>/<virtual_path>/Service/Service.svc   
/out:<proxy_name>.cs /messageContract /tcv:Version35   
/noconfig /ct:System.Collections.ObjectModel.Collection`1   
/namespace:*,Microsoft.MasterDataServices  
```  
  
 Erläuterungen:  
  
-   *Servername*:*Port* dem Computernamen und die Portnummer des Computers, auf dem gehostet [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].  
  
-   *Virtual_path* ist der virtuelle Pfad der [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] in Internet Information Services (IIS).  
  
-   *Proxy_name* ist der Name für die generierte Proxydatei.  
  
## <a name="see-also"></a>Siehe auch  
 [Kategorisierte Webdienstvorgänge &#40; Master Data Services &#41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
  
  
