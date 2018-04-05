---
title: Arbeiten mit Analysis Services-Projekten und Datenbanken in Entwicklung | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Analysis Services, projects
ms.assetid: 39cf9166-fa92-40fe-9962-210a52461257
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2315a46f017758da30f2973154bcd2fe451e1748
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="work-with-analysis-services-projects-and-databases-in-development"></a>Arbeiten mit Analysis Services-Projekten und Datenbanken in der Entwicklung
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Entwickeln Sie ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] her, indem [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] im Projektmodus oder im Onlinemodus.  
  
## <a name="single-developer"></a>Einzelner Entwickler  
 Wenn nur ein einzelner Entwickler die gesamte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank und alle Objekte entwickelt, aus denen sie besteht, kann [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] während des Entwicklungszyklus der Business Intelligence-Lösung jederzeit entweder im Projektmodus oder im Onlinemodus verwendet werden. Bei einem einzelnen Entwickler ist die Wahl des Modus nicht von besonderer Bedeutung. Die Wartung einer Offlineprojektdatei unter Einbeziehung eines Quellcodeverwaltungssystems weist viele Vorteile auf, z. B. Archivierung und Rollback. Ein einzelner Entwickler muss sich jedoch nicht damit befassen, Änderungen mit anderen Entwicklern abzustimmen.  
  
## <a name="multiple-developers"></a>Mehrere Entwickler  
 Wenn mehrere Entwickler an einer Business Intelligence-Lösung arbeiten, wird es zu Problemen kommen, falls die Entwickler nicht vorwiegend, oder sogar immer, im Projektmodus mit Quellcodeverwaltung arbeiten. Durch die Quellcodeverwaltung wird sichergestellt, dass zwei Entwickler nicht gleichzeitig Änderungen an demselben Objekt vornehmen.  
  
 Nehmen Sie z. B. an, ein Entwickler arbeitet im Projektmodus und nimmt Änderungen an ausgewählten Objekten vor. Nehmen Sie weiterhin an, dass, während der Entwickler diese Änderungen vornimmt, ein anderer Entwickler im Onlinemodus eine Änderung an der bereitgestellten Datenbank vornimmt. Ein Problem tritt auf, wenn der erste Entwickler versucht, das geänderte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt bereitzustellen. In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] wird nämlich erkannt, dass Objekte innerhalb der bereitgestellten Datenbank geändert wurden, und der Entwickler wird aufgefordert, die gesamte Datenbank zu überschreiben, wodurch auch die Änderungen des zweiten Entwicklers überschrieben werden. Da [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nicht in der Lage ist, die Änderungen zwischen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankinstanz und den Objekten im Projekt, das überschrieben werden soll, aufzulösen, hat der erste Entwickler genau genommen nur die Möglichkeit, alle eigenen Änderungen zu verwerfen und die Änderungen erneut an einem neuen Projekt vorzunehmen, das auf der aktuellen Version der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank basiert.  
  
  
