---
title: MDX-Datendefinitionsanweisungen (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- MDX [Analysis Services], data manipulation
- data manipulation [MDX]
- data definition statements [MDX]
- Multidimensional Expressions [Analysis Services], data manipulation
ms.assetid: 1f975d7f-8875-43b6-a571-9d5cd7c70217
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7799b80fd5ba847492247f1d52107da4aaf569a1
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition-statements-mdx"></a>MDX-Datendefinitionsanweisungen (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Datendefinitionsanweisungen in MDX (Multidimensional Expressions) dienen zum Erstellen, Löschen und Ändern mehrdimensionaler Objekte. In der folgenden Tabelle sind die verfügbaren Datendefinitionsanweisungen aufgelistet.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[ALTER CUBE-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-alter-cube.md)|Ändert die Struktur eines angegebenen Cubes.|  
|[Erstellen Sie ACTION-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-create-action.md)|Erstellt eine Aktion, die einem Cube, einer Dimension, einer Hierarchie oder einem untergeordneten Objekt zugeordnet werden kann.|  
|[Erstellen Sie CELL CALCULATION-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-create-cell-calculation.md)|Erstellt eine Berechnung, die einen MDX-Ausdruck für eine angegebene Tupelmenge in einem Cube auswertet.|  
|[Erstellen Sie GLOBAL CUBE-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-create-global-cube.md)|Erstellt einen lokal persistenten Cube, der auf einem Teilcube aus einem Cube auf dem Server basiert, und füllt ihn auf. Für die Verbindung mit dem lokal persistenten Cube ist keine Verbindung mit dem Server erforderlich.|  
|[Erstellen Sie MEMBER-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-create-member.md)|Erstellt ein berechnetes Element.|  
|[Erstellen Sie SESSION CUBE-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-create-session-cube.md)|Erstellt einen Cube, der auf Cubes auf dem Server basiert und für alle Abfragen in derselben Sitzung verfügbar ist, und füllt den Cube auf.|  
|[Erstellen Sie die SET-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-create-set.md)|Erstellt eine benannte Menge für einen angegebenen Cube.|  
|[Erstellen Sie SUBCUBE-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-create-subcube.md)|Definiert den Cuberaum eines angegebenen Cubes oder Teilcubes neu zu einem angegebenen Teilcube.|  
|[DROP ACTION-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-drop-action.md)|Löscht eine angegebene Aktion aus einem angegebenen Cube.|  
|[DROP CELL CALCULATION-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-drop-cell-calculation.md)|Entfernt die angegebene Zellenberechnung.|  
|[DROP MEMBER-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-drop-member.md)|Entfernt ein berechnetes Element.|  
|[DROP SET-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-drop-set.md)|Entfernt eine benannte Menge.|  
|[DROP SUBCUBE-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-drop-subcube.md)|Löscht einen angegebenen Teilcube, wobei die zuvor definierte Cube- oder Teilcubedefinition mit dem angegebenen Namen wiederhergestellt wird.|  
|[REFRESH CUBE-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-refresh-cube.md)|Aktualisiert den Clientcache für einen Cube.|  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Anweisungsreferenz &#40; MDX &#41;](../mdx/mdx-statement-reference-mdx.md)   
 [MDX-Datenbearbeitungsanweisungen &#40; MDX &#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [MDX-Skriptanweisungen &#40; MDX &#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  

