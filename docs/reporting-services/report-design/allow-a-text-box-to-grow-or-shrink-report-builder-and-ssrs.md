---
title: "Zulassen, dass Textfelder vergrößert oder verkleinert werden (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dbc01e78-5993-47e5-af04-34f9e3bbcee1
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 821458f2eac2a87cd05a4070b60983957c745bd0
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs"></a>Zulassen, dass Textfelder vergrößert oder verkleinert werden (Berichts-Generator und SSRS)
  In einem paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Bericht sind Textfelder nicht nur eigenständige Kästchen auf der Berichtsentwurfsoberfläche. Jede Zelle in einer Tabelle oder Matrix (einem Tablix-Datenbereich) enthält auch ein Textfeld, das auf dieselbe Weise formatiert werden kann wie eigenständige Textfelder. In der Standardeinstellung haben Textfelder eine feste Größe. Sie können Optionen festlegen, durch die ein Textfeld in Anpassung an seinen Inhalt vergrößert oder verkleinert wird. Diese Optionen entsprechen der **CanGrow** -Eigenschaft bzw. der **CanShrink** -Eigenschaft im Bereich Eigenschaften.  
  
## <a name="to-allow-a-text-box-to-grow-or-shrink"></a>So lassen Sie zu, dass ein Textfeld vergrößert oder verkleinert wird  
  
1.  Klicken Sie mit der rechten Maustaste auf das Textfeld, und klicken Sie dann auf **Textfeldeigenschaften**.  
  
2.  Klicken Sie auf die Registerkarte **Allgemein** .  
  
    -   Wenn ein Textfeld basierend auf dem Inhalt vertikal erweitert werden soll, wählen Sie **Vergrößern der Höhe zulassen**.  
  
    -   Wenn ein Textfeld basierend auf dem Inhalt verkleinert werden soll, wählen Sie **Verringern der Höhe zulassen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Textfelder &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)  
  
  
