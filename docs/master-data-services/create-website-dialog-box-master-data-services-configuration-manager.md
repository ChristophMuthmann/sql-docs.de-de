---
title: "Erstellen des Dialogfeldes der Website (Konfigurations-Manager für Master Data Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.mds.configmanager.createsite.f1
ms.assetid: 179c9c1e-3b06-421b-b71b-1cb64d104f5e
caps.latest.revision: 10
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 72b03df097b9951384674abbb984636b8999abf7
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="create-website-dialog-box-master-data-services-configuration-manager"></a>Website erstellen (Dialogfeld im Konfigurations-Manager für Master Data Services)
  Verwenden Sie das Dialogfeld **Website erstellen** , um eine neue Website auf dem lokalen Computer zu erstellen. Wenn Sie in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]eine Website erstellen, wird diese den Internetinformationsdiensten (IIS) auf dem lokalen Computer mit einer Stammanwendung hinzugefügt, die als die [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung konfiguriert ist. Darüber hinaus wird ein neuer Anwendungspool erstellt und die Webanwendung in diesen Anwendungspool eingefügt.  
  
## <a name="web-site"></a>Website  
  
|Steuerelementname|Description|  
|------------------|-----------------|  
|**Websitename**|Geben Sie einen Namen für die Website ein, oder verwenden Sie den Standardnamen. Dieser Name ist ein Anzeigename, der nur zur Identifizierung der Website in IIS verwendet wird. Er wird nicht verwendet, um von einem Webbrowser aus auf die Website zuzugreifen.<br /><br /> Der Name muss für alle Websites in IIS auf dem lokalen Computer eindeutig sein.|  
|**Protokoll**|Zeigt **http**an. Verwenden Sie das Hypertext Transfer-Protokoll (HTTP), wenn für die Kommunikation zwischen Client und Server kein verschlüsselter Kanal erforderlich ist.<br /><br /> **Hinweis**: Sie können keine HTTPS-Site in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]erstellen. HTTPS ist das auf SSL (Secure Sockets Layer) basierende HTTP-Protokoll. Es empfiehlt sich beim Austausch vertraulicher oder persönlicher Daten oder wenn Benutzer vor dem Übertragen persönlicher Informationen die Identität des Servers bestätigen sollen. Wenn Ihre Informationen zwischen dem Server und einem Client über einen verschlüsselten Channel übertragen werden sollen, müssen Sie mit einem IIS-Tool wie IIS-Manager die Website mit einer HTTPS-Bindung konfigurieren und die Websitebindung einem Serverzertifikat zuzuordnen. Erst dann können Sie die Website erfolgreich in einem Webbrowser öffnen. Weitere Informationen zu Serverzertifikaten finden Sie unter [Konfigurieren von Serverzertifikaten in IIS 7](http://go.microsoft.com/fwlink/?LinkId=163220) auf [!INCLUDE[msCoName](../includes/msconame-md.md)] TechNet.|  
|**IP-Adresse**|Wählen Sie eine IP-Adresse aus, über die Benutzer auf die Website zugreifen können. Standardmäßig ist **Alle nicht zugewiesenen** ausgewählt. Verwenden Sie den Standardwert, solange kein Grund zur Verwendung einer bestimmten IPv4- oder IPv6-Adresse vorliegt.<br /><br /> Bei **Alle nicht zugewiesenen**antwortet die Website auf Anforderungen, die an alle IP-Adressen auf dem Port und den angegebenen optionalen Hostnamen gerichtet sind. Wenn eine andere Website auf dem Server über eine Bindung auf demselben Port, aber mit einer spezifischen IP-Adresse verfügt, empfängt diese Website HTTP-Anforderungen, die an diesen Port und die spezifische IP-Adresse gerichtet sind. Die Website mit der Einstellung **Alle nicht zugewiesenen** empfängt alle sonstigen HTTP-Anforderungen, die an diesen Port und die übrigen IP-Adressen gerichtet sind.|  
|**Port**|Geben Sie den Port für Anforderungen ein, die an diese Website gerichtet sind. Der Standardport bei ausgewähltem HTTP-Protokoll ist 80. Wenn Sie einen anderen Port als die Standardports angeben, müssen Clients die Portnummer angeben, um eine Verbindung mit der Website herzustellen.<br /><br /> **Hinweis**: Die **Standardwebsite** in IIS ist so konfiguriert, dass das HTTP-Protokoll auf Port 80 für alle nicht zugewiesenen IP-Adressen verwendet wird. Wenn Sie versuchen, die Website in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] mit den Standardbindungsinformationen zu erstellen, erhalten Sie eine Fehlermeldung, dass eine doppelte Bindung vorhanden ist. Sie müssen entweder die Bindungsinformationen für die Website in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]oder die Bindungsinformationen für die Standardwebsite mithilfe eines IIS-Tools, z. B. IIS-Manager, ändern. Alternativ können Sie einen Hostheader angeben, um IIS die eindeutige Identifizierung der Website zu ermöglichen. Die Firewall muss so konfiguriert sein, dass sie den Datenverkehr über den angegebenen Port zulässt.|  
|**Hostheader**|Optionaler Wert. Geben Sie den Namen eines Hostheaders ein. Verwenden Sie diesen Hostheader, wenn Sie einem Computer, der eine einzelne IP-Adresse bzw. einen einzelnen Port verwendet, einen Hostnamen, auch bekannt als Domänenname, zuweisen möchten. Wenn Sie einen Hostnamen angeben, müssen Clients den Namen statt der IP-Adresse verwenden, um auf die Website zuzugreifen. Wenn Sie einen Hostnamen konfigurieren, können Sie die Website erst in einem Webbrowser öffnen, wenn auf dem DNS-Server ein Eintrag für diesen Hostnamen vorhanden ist.<br /><br /> Wenn Benutzer unter `http://www.contoso.com/` auf die Website zugreifen sollen, müssen Sie www.contoso.com als Hostnamen angeben, und der DNS-Server muss einen entsprechenden Eintrag aufweisen.<br /><br /> Wenn die Website in einem Intranet verfügbar ist, müssen Sie keinen Hostnamen angeben, wenn Benutzer den Servernamen, z. B. `http://server_name`, in einem Browser eingeben. Wenn der DNS-Server in der Umgebung jedoch so konfiguriert ist, dass er weitere Namen für diesen Webserver speichert, können Sie eine separate Bindung für jeden Hostnamen erstellen, sodass Benutzer die anderen vom DNS-Server gespeicherten Namen verwenden können. Wenn Sie mehr als einen Hostnamen für die Website konfigurieren müssen, verwenden Sie ein IIS-Tool, z. B. IIS-Manager, um zusätzliche Websitebindungen hinzuzufügen.|  
  
## <a name="application-pool"></a>Anwendungspool  
  
|Steuerelementname|Description|  
|------------------|-----------------|  
|**Name**|Geben Sie einen eindeutigen Anzeigenamen für einen neuen Anwendungspool ein, oder verwenden Sie den bereitgestellten Standardnamen. Die Stammwebanwendung für diese Website wird in diesem Anwendungspool ausgeführt.<br /><br /> Anwendungspools verfügen über immanente Grenzen, durch die Anwendungen in einem Anwendungspool daran gehindert werden, Einfluss auf Anwendungen in einem anderen Anwendungspool zu nehmen.|  
|**Benutzername**|Geben Sie einen Domänen- und Benutzernamen aus Active Directory ein. Dieses Konto entspricht der Identität des Anwendungspools, in dem die Webanwendung ausgeführt wird.<br /><br /> Das Konto wird für den Datenbankzugriff der mds_exec-Datenbankrolle in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Datenbank hinzugefügt. Weitere Informationen finden Sie unter [Datenbankanmeldenamen, -benutzer und -rollen &#40;Master Data Services&#41;](../master-data-services/database-logins-users-and-roles-master-data-services.md). Es wird darüber hinaus einer [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Windows-Gruppe wie **MDS_ServiceAccounts** hinzugefügt. Ihr wurden Berechtigungen auf das temporäre Kompilierungsverzeichnis, **MDSTempDir** im Dateisystem erteilt. Weitere Informationen finden Sie unter [Ordner- und Dateiberechtigungen &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).|  
|**Kennwort**|Geben Sie das Kennwort für das angegebene Benutzerkonto ein.|  
|**Kennwort bestätigen**|Geben Sie das Kennwort für das angegebene Benutzerkonto erneut ein. Die Felder **Kennwort** und **Kennwort bestätigen** müssen das gleiche Kennwort enthalten.|  
  
## <a name="see-also"></a>Siehe auch  
 [Webkonfiguration &#40;Seite im Konfigurations-Manager für Master Data Sevices&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
[Master Data Services – Installation und Konfiguration](../master-data-services/master-data-services-installation-and-configuration.md) [Webanwendungsanforderungen &#40; Master Data Services &#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [Erstellen einer Master Data Manager-Webanwendung &#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
