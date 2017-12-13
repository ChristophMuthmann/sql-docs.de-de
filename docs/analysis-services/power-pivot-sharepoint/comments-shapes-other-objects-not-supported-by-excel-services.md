---
title: "Kommentare, Formen, andere Objekte, die von Excel Services nicht unterstützt | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: ade92e15-dfbf-496b-9378-a00bd83ba750
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7be7712be44114606ec89f89683defeee8e3bd31
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="comments-shapes-other-objects-not-supported-by-excel-services"></a>Kommentare, Formen, andere Objekte, die von Excel Services nicht unterstützt.
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Dieser Fehler tritt auf, wenn Sie Slicer zum Hinzufügen einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Arbeitsmappe aus einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Feldliste.  
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Gilt für|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint|  
|Produktversion|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Ursache|Das Shape-Objekt, mit dem die Positionierung und Formatierung von Slicern gesteuert wird, die einer Arbeitsmappe aus der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Feldliste hinzugefügt wurden, kann von Excel Web Access nicht gerendert werden.|  
|Meldungstext|Die folgenden Funktionen werden von Excel Services nicht unterstützt und möglicherweise nur teilweise oder überhaupt nicht angezeigt:<br /><br /> Kommentare, Formen oder andere Objekte<br /><br /> Einige Funktionen z. B. externe Datenabfragen, zeigen zwischengespeicherte Daten an, die nur in Microsoft Excel aktualisiert werden können.|  
  
## <a name="explanation"></a>Erklärung  
 Excel Web Access zeigt diesen Fehler an, wenn Sie eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe in einem Browser öffnen und in der Meldung **Nicht unterstützte Features. Möglicherweise wird die Arbeitsmappe nicht wie vorgesehen angezeigt** auf die Schaltfläche **Details**klicken.  
  
 Dieser Fehler tritt auf, weil die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe Slicer enthält, deren Layout über ein ausgeblendetes Shape-Objekt in Excel gesteuert wird. Das Shape-Objekt steuert die Formatierung und Positionierung der Slicer in horizontalen und vertikalen Platzierungen.  
  
 Shape-Objekte können von Excel Services nicht gerendert werden, dies ist jedoch kein Problem, weil es sich um ein ausgeblendetes Objekt handelt.  
  
## <a name="user-action"></a>Benutzeraktion  
 Dieser Fehler kann ignoriert werden. Klicken Sie auf **OK** , um die Fehlermeldung zu schließen und die Verwendung von Arbeitsmappe und Slicern ohne Probleme fortzusetzen.  
  
  
