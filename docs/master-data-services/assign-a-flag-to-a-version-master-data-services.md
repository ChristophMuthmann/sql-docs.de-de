---
title: Zuweisen eines Flags zu einer Version (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- version flags [Master Data Services], assigning flags
- versions [Master Data Services], assigning flags
ms.assetid: 6629ec7e-32e7-4a1e-8b31-eb43c5923766
caps.latest.revision: 7
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 74b49ecc3f49ca952e484af32ef98e4dac885655
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="assign-a-flag-to-a-version-master-data-services"></a>Zuweisen eines Flags zu einer Version (Master Data Services)
  Weisen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]ein Flag einer Version zu, um die Version anzugeben, die Benutzer oder abonnierende Systeme verwenden sollten.  
  
> [!NOTE]  
>  Versionsflags können nur jeweils einer Version zugewiesen werden. Wenn Sie ein Flag zuweisen, das einer anderen Version bereits zugewiesen ist, wird das Flag in die Version verschoben, die Sie ausgewählt haben.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Versionsverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Sie müssen ein Versionsflag erstellt haben, um es zuweisen zu können. Weitere Informationen finden Sie unter [Erstellen eines Versionsflags &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md).  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich "Versionsverwaltung" zuzugreifen. Weitere Informationen finden Sie unter [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
### <a name="to-assign-a-flag-to-a-version"></a>So weisen Sie einer Version ein Flag zu  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Versionsverwaltung**.  
  
2.  Doppelklicken Sie auf der Seite **Versionen verwalten** in der Zeile für die Version, der Sie ein Flag zuweisen möchten, auf die Zelle in der Spalte **Flag** .  
  
3.  Wählen Sie aus der Liste das Flag aus, das Sie zuweisen möchten.  
  
    > [!NOTE]  
    >  Wenn das gewünschte Flag nicht verfügbar ist, steht dieses möglicherweise nur für Versionen **Mit ausgeführtem Commit** zur Verfügung. Sie können dies überprüfen, indem Sie die Seite **Versionsflags verwalten** aufrufen und das Feld **Nur Versionen, für die ein Commit ausgeführt wurde** für das Flag anzeigen.  
  
4.  Drücken Sie die EINGABETASTE, um die Änderung zu speichern.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Versionsflags &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md)   
 [Versionen &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)  
  
  

