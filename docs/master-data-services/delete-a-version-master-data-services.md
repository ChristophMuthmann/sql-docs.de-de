---
title: "Löschen einer Version (Master Data Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- versions [Master Data Services], deleting
- deleting versions [Master Data Services]
ms.assetid: 2a4eeffe-8379-4744-ad44-c27d8c8ac9a8
caps.latest.revision: "6"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a1d01182cb0a7e28d711e090a8f82fa01239a41
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="delete-a-version-master-data-services"></a>Löschen einer Version (Master Data Services)
  Löschen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]eine Version, wenn Sie sicher sind, dass Sie die der Version zugeordneten Masterdaten nicht mehr benötigen. Nachdem Sie eine Version gelöscht haben, können Sie die zugeordneten Masterdaten nicht abrufen.  
  
> [!WARNING]  
>  Wenn ein Modell nur über eine Version verfügt, und Sie diese löschen, wird das Modell unbrauchbar.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen berechtigt sein, die mdm.viw_SYSTEM_SCHEMA_VERSION-Sicht anzuzeigen und die gespeicherte Prozedur mds.udpVersionDelete in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Datenbank auszuführen. Weitere Informationen finden Sie unter [Sicherheit von Datenbankobjekten &#40;Master Data Services&#41;](../master-data-services/database-object-security-master-data-services.md).  
  
### <a name="to-delete-a-version"></a>So löschen Sie eine Version  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , und stellen Sie eine Verbindung mit der [!INCLUDE[ssDE](../includes/ssde-md.md)] -Instanz für die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank her.  
  
2.  Öffnen Sie die mdm.viw_SYSTEM_SCHEMA_VERSION-Sicht.  
  
3.  Suchen Sie die Version des Modells, die Sie löschen möchten, und kopieren Sie den Wert im Feld **ID** .  
  
4.  Erstellen Sie eine neue Abfrage.  
  
5.  Geben Sie den folgenden Text ein, indem Sie *version_ID* durch den in Schritt 2 kopierten Wert ersetzen.  
  
    ```  
    EXEC [mdm].[udpVersionDelete] @Version_ID='version_ID'  
    ```  
  
6.  Führen Sie die Abfrage aus.  
  
    > [!NOTE]  
    >  Es kann einige Minuten dauern, bis die Änderung in der Webanwendung angezeigt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Versionen &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [Kopieren einer Version &#40;Master Data Services&#41;](../master-data-services/copy-a-version-master-data-services.md)  
  
  
