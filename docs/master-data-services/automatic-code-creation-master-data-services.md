---
title: Automatische Codeerstellung (Master Data Services) | Microsoft-Dokumentation
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
ms.assetid: 9adbd5e1-f28c-4fb5-afa7-082de2831f3e
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82b145eb8a947c9320b4c4cb261d3a83e623d094
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="automatic-code-creation-master-data-services"></a>Automatische Codeerstellung (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können numerische Werte für das Codeattribut oder andere numerische Attributwerte automatisch generiert werden. Wenn Codes automatisch generiert werden, können Sie trotzdem andere Werte für Codes eingeben; es wird nur ein Anfangswert automatisch festgelegt.  
  
## <a name="generating-code-values"></a>Generieren von Codewerten  
 Administratoren können automatisch generierte Werte für das Code-Attribut konfigurieren, indem sie die Eigenschaften der zugeordneten Entität bearbeiten. Sie können einen Anfangswert angeben, und jeder nachfolgende Wert wird um 1 erhöht.  
  
 Wenn Sie Codewerte in MDS entweder in einem der Tools oder mit dem Stagingprozess eingeben, können Sie den Code-Wert leer lassen und ein Code-Wert wird automatisch generiert. Oder Sie können einen Codewert Ihrer Wahl angeben.  
  
## <a name="generating-other-attribute-values"></a>Generieren von anderen Attributwerten  
 Administratoren können Werte für andere Attribute als Code automatisch generieren, indem sie Geschäftsregeln erstellen. Sie können einen Anfangswert angeben und die Zahl angeben, um die jeder nachfolgende Wert inkrementiert wird.  
  
 Wenn Sie Attributwerte in MDS entweder in einem der Tools oder mit dem Stagingprozess eingeben, können Sie den Attributwert leer lassen. Wenn Geschäftsregeln angewendet werden, werden die Werte auf Grundlage des höchsten vorhandenen Werts inkrementiert. Wenn die Regel z. B. "Standardattribut für einen generierten Wert, der bei 1 startet und um 4 inkrementiert wird" lautet und der höchste aktuelle Wert für das Attribut 700 ist, beträgt der Wert für das nächste Element, das hinzugefügt wird, 704.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Automatisches Generieren von Werten für das Codeattribut.|[Automatisches Generieren von Codeattributwerten &#40;Master Data Services&#41;](../master-data-services/automatically-generate-code-attribute-values-master-data-services.md)|  
|Generieren Sie automatisch Werte für andere Attribute.|[Automatisches Generieren von anderen Attributwerten als Code &#40;Master Data Services&#41;](../master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)|  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   [Übersicht über Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
-   [Entitäten &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  
