---
title: Überprüfen einer Version anhand von Geschäftsregeln (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- validating versions [Master Data Services]
- validating versions [Master Data Services], about validating versions
- versions [Master Data Services], validating
- business rules [Master Data Services], applying to all members
ms.assetid: 5aee7901-6d05-41d4-8bbb-c6f26791d1df
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b606e815107bcaf30365c9656d6b3bf123d3012
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="validate-a-version-against-business-rules-master-data-services"></a>Überprüfen einer Version anhand von Geschäftsregeln (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Überprüfen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]eine Version, um Geschäftsregeln auf alle Elemente in der Modellversion anzuwenden.  
  
 Im folgenden Verfahren wird erklärt, wie Daten mit der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung überprüft werden. Wenn Sie über die Berechtigung in der MDS-Datenbank verfügen, können Sie stattdessen eine gespeicherte Prozedur verwenden. Weitere Informationen finden Sie unter [Gespeicherte Überprüfungsprozedur &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md).  
  
> [!NOTE]  
>  Damit ein Commit für eine Version ausgeführt werden kann, müssen alle Elemente die Überprüfung bestehen.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Versionsverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
-   Der Status der Version muss **Öffnen** oder **Gesperrt**sein.  
  
-   Auf der Seite **Versionen überprüfen** müssen Elemente mit einem anderen Status als **Überprüfung erfolgreich**vorhanden sein.  
  
### <a name="to-validate-a-version"></a>So überprüfen Sie eine Version  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Versionsverwaltung**.  
  
2.  Klicken Sie auf der Seite **Versionen verwalten** auf der Menüleiste auf **Version überprüfen**.  
  
3.  Wählen Sie auf der Seite **Versionen überprüfen** das Modell und die Version aus, die Sie überprüfen möchten.  
  
4.  Klicken Sie auf **Überprüfen**.  
  
5.  Klicken Sie im Bestätigungsdialogfeld auf **OK**.  
  
    > [!NOTE]  
    >  Wenn die Statusanzeige nicht mehr angezeigt wird, hat die Version die Überprüfung beendet.  
  
## <a name="next-steps"></a>Next Steps  
  
-   [Sperren einer Version &#40;Master Data Services&#41;](../master-data-services/lock-a-version-master-data-services.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überprüfungsstatus &#40;Master Data Services&#41;](../master-data-services/validation-statuses-master-data-services.md)   
 [Gespeicherte Überprüfungsprozedur &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)   
 [Versionen &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Überprüfen von bestimmten Elementen auf Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
  
