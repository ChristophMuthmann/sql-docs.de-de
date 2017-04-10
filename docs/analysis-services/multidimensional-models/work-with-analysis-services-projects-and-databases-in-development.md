---
title: "Arbeiten mit Analysis Services-Projekten und -Datenbanken w&#228;hrend der Entwicklungsphase | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Analysis Services, Projekte"
ms.assetid: 39cf9166-fa92-40fe-9962-210a52461257
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 16
---
# Arbeiten mit Analysis Services-Projekten und -Datenbanken w&#228;hrend der Entwicklungsphase
  Sie können eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank entwickeln, indem Sie [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] entweder im Projektmodus oder im Onlinemodus verwenden.  
  
## Einzelner Entwickler  
 Wenn nur ein einzelner Entwickler die gesamte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank und alle Objekte entwickelt, aus denen sie besteht, kann [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] während des Entwicklungszyklus der Business Intelligence-Lösung jederzeit entweder im Projektmodus oder im Onlinemodus verwendet werden. Bei einem einzelnen Entwickler ist die Wahl des Modus nicht von besonderer Bedeutung. Die Wartung einer Offlineprojektdatei unter Einbeziehung eines Quellcodeverwaltungssystems weist viele Vorteile auf, z. B. Archivierung und Rollback. Ein einzelner Entwickler muss sich jedoch nicht damit befassen, Änderungen mit anderen Entwicklern abzustimmen.  
  
## Mehrere Entwickler  
 Wenn mehrere Entwickler an einer Business Intelligence-Lösung arbeiten, wird es zu Problemen kommen, falls die Entwickler nicht vorwiegend, oder sogar immer, im Projektmodus mit Quellcodeverwaltung arbeiten. Durch die Quellcodeverwaltung wird sichergestellt, dass zwei Entwickler nicht gleichzeitig Änderungen an demselben Objekt vornehmen.  
  
 Nehmen Sie z. B. an, ein Entwickler arbeitet im Projektmodus und nimmt Änderungen an ausgewählten Objekten vor. Nehmen Sie weiterhin an, dass, während der Entwickler diese Änderungen vornimmt, ein anderer Entwickler im Onlinemodus eine Änderung an der bereitgestellten Datenbank vornimmt. Ein Problem tritt auf, wenn der erste Entwickler versucht, das geänderte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt bereitzustellen. In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] wird nämlich erkannt, dass Objekte innerhalb der bereitgestellten Datenbank geändert wurden, und der Entwickler wird aufgefordert, die gesamte Datenbank zu überschreiben, wodurch auch die Änderungen des zweiten Entwicklers überschrieben werden. Da [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nicht in der Lage ist, die Änderungen zwischen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankinstanz und den Objekten im Projekt, das überschrieben werden soll, aufzulösen, hat der erste Entwickler genau genommen nur die Möglichkeit, alle eigenen Änderungen zu verwerfen und die Änderungen erneut an einem neuen Projekt vorzunehmen, das auf der aktuellen Version der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank basiert.  
  
  