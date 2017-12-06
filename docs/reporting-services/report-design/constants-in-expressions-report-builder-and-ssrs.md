---
title: "Konstanten in Ausdrücken (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
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
ms.assetid: b8ae650b-0f46-4848-b62b-15f8a40751b8
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f95f48c7dd8565fd1e0f50b448f6f6c0066ee14d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="constants-in-expressions-report-builder-and-ssrs"></a>Konstanten in Ausdrücken (Berichts-Generator und SSRS)
  Eine Konstante besteht aus Literaltext oder vordefiniertem Text. Der Berichtsprozessor hat Zugriff auf die vordefinierten Konstanten. Wenn Sie die Konstanten in einen Ausdruck einschließen, werden die Werte, die sie darstellen, daher im Ausdruck ersetzt, bevor dieser ausgewertet wird.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="literal-text"></a>Literaltext  
 In einem Ausdruck ist Literaltext Text, der in doppelten Anführungszeichen steht. Sie können Text auch direkt ohne doppelte Anführungszeichen in ein Textfeld eingeben, wenn er nicht Teil eines Ausdrucks ist. Wenn der Textfeldwert nicht mit einem Gleichheitszeichen (=) beginnt, wird der Text als Literaltext behandelt. In der folgenden Tabelle werden mehrere Beispiele für Literaltext in einem Ausdruck angezeigt.  
  
|Konstante|Anzeigetext|Ausdruckstext|  
|--------------|------------------|---------------------|  
|Bericht ausgeführt um:|<\<Expr>>|`="Report run at: " & Globals!ExecutionTime`|  
|Adventure Works Cycles|Adventure Works Cycles|Adventure Works Cycles|  
|[Anzeigetext in Klammern]|\\[Anzeigetext in Klammern\\]|[Anzeigetext in Klammern]|  
  
## <a name="rdl-constants"></a>RDL-Konstanten  
 Sie können in der Berichtsdefinitionssprache (RDL) definierte Konstanten in einem Ausdruck verwenden. Im Dialogfeld **Ausdruck** werden Konstanten angezeigt, wenn Sie einen Ausdruck für eine Berichtseigenschaft erstellen, der nur bestimmte gültige Werte akzeptiert. Diese Werte werden auch als Enumerationstypen bezeichnet. Die folgende Tabelle enthält zwei Beispiele.  
  
|Eigenschaft|Description|Werte|  
|--------------|-----------------|------------|  
|Textausrichtung|Gültige Werte zum Ausrichten von Text in einem Textfeld.|Allgemein, Links, Zentriert, Rechts|  
|Rahmenart|Gültige Werte für eine einem Bericht hinzugefügte Zeile.|Standard, Keine, Gepunktet, Gestrichelt, Einfarbig, Doppelt, Strich-Punkt, Strich-Punkt-Punkt|  
  
## <a name="visual-basic-constants"></a>Visual Basic-Konstanten  
 Sie können in einem Ausdruck in der [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Laufzeitbibliothek definierte Konstanten verwenden. Beispielsweise kann die Konstante **DateInterval.Day**nicht verwendet werden. Für das Datum 10. Januar 2008 gibt der folgende Ausdruck beispielsweise die Zahl 10 zurück:  
  
 `=DatePart("d",Globals!ExecutionTime)`  
  
## <a name="clr-constants"></a>CLR-Konstanten  
 Sie können in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime-Klassen (CLR) definierte Konstanten in einem Ausdruck verwenden. In der folgenden Tabelle wird ein Beispiel für eine systemdefinierte Farbe angezeigt.  
  
|Konstante|Description|  
|--------------|-----------------|  
|MistyRose|Beim Erstellen eines Ausdrucks für eine Berichtseigenschaft, die auf der Hintergrundfarbe basiert, können Sie eine Farbe mit Namen angeben. Gültige Namen werden im Dialogfeld **Ausdruck** aufgelistet.|  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdruck (Dialogfeld)](http://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Datentypen in Ausdrücken (Berichts-Generator und SSRS)](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Dialogfeld „Ausdruck“ (Berichts-Generator)](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  
