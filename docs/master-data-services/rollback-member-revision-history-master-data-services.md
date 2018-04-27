---
title: Zurücksetzen des Elementrevisionsverlaufs (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
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
ms.assetid: d39d3474-20e7-429f-9c8d-fcc4eb0854fc
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a7cbc4600fefd64b4dd58c7c6e5481340ff0c8f7
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="rollback-member-revision-history-master-data-services"></a>Zurücksetzen des Elementrevisionsverlaufs (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Ein Elementrevisionsverlauf wird jedes Mal aufgezeichnet, wenn ein Element geändert wird. Sie können einen Elementrevisionsverlauf auf eine frühere Version zurücksetzen.  
  
## <a name="prerequisites"></a>Voraussetzungen  
  
-   Sie benötigen die Berechtigung, mindestens eines der Attribute des ausgewählten Elements zu aktualisieren. Wenn Sie einen Revisionsverlauf zurücksetzen, werden alle Attributwerte, die aktualisiert werden können, auf die vorherigen Versionswerte zurückgesetzt.  
  
-   Der Revisionsverlauf steht nur dann zur Verfügung, wenn der Transaktionsprotokolltyp der Entität "Element" ist.  
  
 **Zurücksetzen eines Elementrevisionsverlaufs**  
  
1.  Klicken Sie in Master Data Manager auf "Explorer".  
  
2.  Wählen Sie die Entität und das Element aus, das zurückgesetzt werden soll.  
  
3.  Klicken Sie auf **Verlauf anzeigen**.  
  
4.  Wählen Sie die Revision aus, die zurückgesetzt werden soll, und klicken Sie anschließend auf **Zurücksetzen**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Elementrevisionsverlauf &#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md)   
 [Ändern des Transaktionsprotokolltyps von Entitäten &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
  
