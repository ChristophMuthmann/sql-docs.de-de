---
title: "Deaktiviert standardmäßig (Analysis Services)-Funktionen | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a9529edf-337e-4fdd-9a13-99cfe96b4fa1
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: eb06cb663a0a94a0611d95532e80f15e5df2da7d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="features-off-by-default-analysis-services"></a>Standardmäßig deaktivierte Funktionen (Analysis Services)
  Eine Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ist standardmäßig für Sicherheit ausgelegt. Aus diesem Grund sind in der Standardeinstellung alle Funktionen deaktiviert, die sich auf die Sicherheit auswirken können. Die folgenden Funktionen sind bei der Installation deaktiviert und müssen gesondert aktiviert werden, wenn sie verwendet werden sollen:  
  
## <a name="feature-list"></a>Funktionsliste  
 Wenn Sie die folgenden Funktionen aktivieren möchten, stellen Sie eine Verbindung zu [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] über [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]her. Klicken Sie mit der rechten Maustaste auf den Instanznamen, und wählen Sie **Facets**aus. Alternativ können Sie diese Funktionen auch über die Servereigenschaften aktivieren. Dies wird im nächsten Abschnitt beschrieben.  
  
-   Ad-Hoc-Data-Mining-Abfragen (OpenRowset)  
  
-   Verknüpfte Objekte (An)  
  
-   Verknüpfte Objekte (Von)  
  
-   Nur lokale Verbindungen überwachen  
  
-   Benutzerdefinierte Funktionen  
  
## <a name="server-properties"></a>Servereigenschaften  
 Zusätzliche standardmäßig deaktivierte Funktionen können Sie über die Servereigenschaften aktivieren. Stellen Sie eine Verbindung zu [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] über [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]her. Klicken Sie mit der rechten Maustaste auf den Instanznamen, und wählen Sie **Eigenschaften**aus. Klicken Sie auf **Allgemein**, und klicken Sie dann auf **Show Advanced** , um eine umfangreichere Liste mit Eigenschaften anzuzeigen.  
  
-   Ad-Hoc-Data-Mining-Abfragen (OpenRowset)  
  
-   Sitzungsminingmodelle zulassen (Data Mining)  
  
-   Verknüpfte Objekte (An)  
  
-   Verknüpfte Objekte (Von)  
  
-   COM-basierte benutzerdefinierte Funktionen  
  
-   Ablaufverfolgungsdefinitionen (Vorlagen).  
  
-   Abfrageprotokollierung  
  
-   Nur lokale Verbindungen überwachen  
  
-   Binäres XML  
  
-   Komprimierung  
  
-   Gruppenaffinität. Einzelheiten dazu finden Sie unter [Thread Pool Properties](../../analysis-services/server-properties/thread-pool-properties.md) .  
  
  
