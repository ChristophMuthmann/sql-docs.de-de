---
title: Benutzerdefiniertes Element Architektur | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, architecture
ms.assetid: 2a88ea46-c9f8-4dd7-aad1-16de11da4f06
caps.latest.revision: 16
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 6ebe0c967ffac1057773dee7d423492371542cee
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="custom-report-item-architecture"></a>Architektur des benutzerdefinierten Berichtselements
  Ein benutzerdefiniertes Berichtselement ist eine Erweiterung von RDL (Report Definition Language), mit dem Entwickler Funktionen hinzufügen können, die ursprünglich nicht in RDL unterstützt werden oder mit denen die Funktionen bestehender Steuerelemente erweitert werden. Es gibt zwei Hauptkomponenten in einem benutzerdefinierten Berichtselement: die Laufzeitkomponente und die Entwurfszeitkomponente. Diese Komponenten sind als [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Assemblys implementiert und können in jeder CLS-kompatiblen Sprache geschrieben werden.  
  
## <a name="the-run-time-component"></a>Die Laufzeitkomponente  
 Die Laufzeitkomponente für ein benutzerdefiniertes Berichtselement wird vom Berichtsprozessor zur Laufzeit aufgerufen. Die Laufzeitkomponente akzeptiert Daten, die vom Berichtsprozessor zur Laufzeit übergeben werden, verarbeitet diese Daten und gibt ein Bild zurück, das das gerenderte, benutzerdefinierte Berichtselement enthält.  
  
 ![Benutzerdefiniertes Element Laufzeitkomponente](../../reporting-services/custom-report-items/media/customreportitemrun-timecomponentarchitecture.gif "Custom Report Item-Laufzeitkomponente")  
  
## <a name="the-design-time-component"></a>Die Entwurfszeitkomponente  
 Über die Entwurfszeitkomponente kann das benutzerdefinierte Berichtselement in der Berichts-Designer-Schnittstelle in [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] definiert und bearbeitet werden. Die Entwurfszeitkomponente besteht aus mehreren Untersteuerungselementen, die das Aussehen und die Eigenschaften des benutzerdefinierten Berichtselements in der Entwurfsumgebung steuern.  
  
 ![Benutzerdefiniertes Element Entwurfszeitkomponente](../../reporting-services/custom-report-items/media/customreportitemdesign-timecomponentarchitecture.gif "benutzerdefinierte Element-Entwurfszeitkomponenten")  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen ein benutzerdefiniertes Element-Laufzeitkomponente](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Erstellen einer benutzerdefinierten Bericht Element zur Entwurfszeit-Komponente](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [Vorgehensweise: Bereitstellen eines benutzerdefinierten Berichtselements](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  
