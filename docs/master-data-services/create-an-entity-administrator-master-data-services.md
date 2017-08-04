---
title: "Erstellen eines Entitätsadministrators (Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 717be1e8-488e-4219-8d1e-ca9084b864cd
caps.latest.revision: 5
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e26187fb7d92fcbae23646b92d6cf02ee5511f5e
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="create-an-entity-administrator-master-data-services"></a>Erstellen eines Entitätsadministrators (Master Data Services)
  Erstellen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]einen Entitätsadministrator, wenn eine Gruppe oder ein Benutzer über alle Berechtigungen für alle Objekte in mindestens einer Entität oder über die Berechtigung zum Genehmigen ausstehender Changesets verfügen soll.  
  
> [!TIP]  
>  Erstellen Sie zum Vereinfachen der Verwaltung eine Windows-Gruppe oder lokale Gruppe und konfigurieren Sie diese als Entitätsadministrator. Sie können anschließend der Gruppe Benutzer hinzufügen und diese daraus entfernen, ohne auf [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]zuzugreifen.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
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
  
## <a name="see-also"></a>Siehe auch  
 [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)   
 [Weisen Sie Modellobjektberechtigungen &#40; Master Data Services &#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Zuweisen von Berechtigungen für Hierarchieelemente &#40; Master Data Services &#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Modellierung von Objektberechtigungen &#40; Master Data Services &#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Berechtigungen für Hierarchieelemente &#40; Master Data Services &#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
