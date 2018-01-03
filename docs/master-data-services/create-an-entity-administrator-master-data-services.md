---
title: "Erstellen eines Entitätsadministrators (Master Data Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 717be1e8-488e-4219-8d1e-ca9084b864cd
caps.latest.revision: "5"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f48a4f1e1ecfbab11ae890a0da8f1aa85edc325
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="create-an-entity-administrator-master-data-services"></a>Erstellen eines Entitätsadministrators (Master Data Services)
  Erstellen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]einen Entitätsadministrator, wenn eine Gruppe oder ein Benutzer über alle Berechtigungen für alle Objekte in mindestens einer Entität oder über die Berechtigung zum Genehmigen ausstehender Changesets verfügen soll.  
  
> [!TIP]  
>  Erstellen Sie zum Vereinfachen der Verwaltung eine Windows-Gruppe oder lokale Gruppe und konfigurieren Sie diese als Entitätsadministrator. Sie können anschließend der Gruppe Benutzer hinzufügen und diese daraus entfernen, ohne auf [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]zuzugreifen.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Benutzer- und Gruppenberechtigungen** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
## <a name="to-create-an-entity-administrator"></a>So erstellen Sie einen Entitätsadministrator  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Benutzer- und Gruppenberechtigungen**.  
  
2.  Wählen Sie die Zeile für den Benutzer oder die Gruppe aus, den bzw. die Sie bearbeiten möchten, und klicken Sie anschließend auf **Ausgewählten Benutzer bearbeiten**.  
  
3.  Klicken Sie auf die Registerkarte **Modelle** , wählen Sie optional ein Modell aus der Liste **Modelle** aus, und klicken Sie anschließend auf **Bearbeiten**.  
  
4.  Klicken Sie auf die Entität, der Sie Berechtigungen erteilen möchten, und klicken Sie anschließend im Menü auf **Admin** .  
  
5.  Führen Sie Schritt 4 für jede Entität aus, für die Sie die Gruppe bzw. den Benutzer als Administrator definieren möchten.  
  
6.  Klicken Sie auf **Speichern**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)   
 [Zuweisen von Berechtigungen für Modellobjekte &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Zuweisen von Hierarchieelementberechtigungen &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Berechtigungen für Modellobjekte &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Berechtigungen für Hierarchieelemente &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
