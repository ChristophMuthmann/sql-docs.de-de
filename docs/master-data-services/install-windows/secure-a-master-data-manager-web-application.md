---
title: Sichern einer Master Data Manager-Webanwendung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e360ba3a-e96b-4f85-b588-ed1f767fa973
caps.latest.revision: 9
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 77c7ea1fada6374a7c413b875a9b91b0abec1ce8
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="secure-a-master-data-manager-web-application"></a>Schützen einer Master Data Manager-Webanwendung

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Sie können die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Webanwendung per HTTPS schützen.  
  
> [!NOTE]  
>  Für die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Webanwendung kann entweder HTTP oder HTTPS verwendet werden, jedoch nicht beides.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie die Prozedur aus  
  
-   Sie müssen Administrator auf dem Webserver sein, auf dem [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] installiert ist.  
  
-   Auf dem Webserver muss MDS installiert sein, und es muss eine Webanwendung vorhanden sein. Weitere Informationen finden Sie unter [Installieren von Master Data Services](../../master-data-services/install-windows/install-master-data-services.md) und [Erstellen einer Master Data Manager-Webanwendung &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md).  
  
### <a name="to-secure-the-master-data-manager-web-application-with-https"></a>So schützen Sie die Master Data Manager-Webanwendung per HTTPS  
  
1.  Nachdem Sie sich vergewissert haben, dass die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Webanwendung per HTTP ordnungsgemäß konfiguriert wurde, erstellen Sie in IIS ein Zertifikat. Weitere Informationen finden Sie unter [Konfigurieren von Serverzertifikaten in IIS 7.0](http://technet.microsoft.com/library/cc732230\(WS.10\).aspx).  
  
2.  Klicken Sie im Bereich **Verbindungen** unter **Websites**auf die Website, auf der die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Webanwendung gehostet wird.  
  
3.  Klicken Sie im **Aktionsbereich** auf **Bindungen**.  
  
4.  Klicken Sie auf **Hinzufügen**.  
  
5.  Wählen Sie in der Liste die Option **https**.  
  
6.  Wählen Sie das SSL-Zertifikat aus.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Optional. Um HTTP zu entfernen, damit Benutzer nur per HTTPS auf die Website zugreifen können, klicken Sie in der Liste auf die Zeile mit **http**. Klicken Sie auf **Entfernen** , und klicken Sie im Bestätigungsdialogfeld auf **Ja**.  
  
    > [!IMPORTANT]  
    >  Nachdem HTTP entfernt wurde, müssen die basicHttp- und wsHttpBinding-Konfiguration geändert werden.  
  
9. Klicken Sie zum Schließen des Dialogfelds **Sitebindungen** auf **Schließen**.  
  
10. Öffnen Sie die Datei „web.config“ unter *Laufwerk*:\Programme\Microsoft SQL Server\130\Master Data Services\WebApplication.  
  
11. Suchen Sie nach der Zeichenfolge `<security mode="Message">` , und ändern Sie diese in `<security mode="Transport">`.  
  
12. Speichern und schließen Sie die Datei. Wenn Sie einen Fehler erhalten, kann dies daran liegen, dass Sie die Benutzerkontensteuerung aktiviert haben. Weitere Informationen finden Sie unter [Deaktivieren der Benutzerkontensteuerung](http://technet.microsoft.com/library/cc709691\(WS.10\).aspx). Benutzer sollten jetzt per HTTPS auf die Website zugreifen können.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen einer Master Data Manager-Webanwendung &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
