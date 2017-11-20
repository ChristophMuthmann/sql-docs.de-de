---
title: Kommentare (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- comments [DMX]
- Data Mining Extensions [Analysis Services], comments
- double forward slashes
- commenting characters
- text strings [SQL Server]
- remarks [DMX]
- forward slash-asterisk character pairs
- DMX [Analysis Services], comments
- /*...*/ (comment)
- double hyphens
- // (comment)
- -- (comment character)
ms.assetid: 64d10eb5-4fe8-42c6-b387-eff336315e56
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 012feb6b830b18151708a85259a0d52ba195788f
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="comments-dmx"></a>Kommentare (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Kommentare in Data Mining Extensions (DMX) sind Textzeichenfolgen in Programmcode Codes, [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] wird nicht ausgeführt. Kommentare werden auch als Anmerkungen bezeichnet. Mit Kommentaren können Sie Code dokumentieren oder Teile einer DMX-Anweisung oder eines DMX-Skripts deaktivieren, wenn Sie den Code untersuchen.  
  
 Wenn Sie Programmcode mit Kommentaren dokumentieren, lässt sich der Code später einfacher pflegen. Mit Kommentaren können Sie bestimmte Informationen festhalten, so z. B. den Namen des Programms, den Namen des Entwicklers, der den Code geschrieben hat, und die Datumsangaben für wesentliche Codeänderungen. Außerdem können Sie Kommentare dazu verwenden, komplizierte Berechnungen oder eine Programmiermethode zu beschreiben.  
  
 Die folgenden Aussagen sind grundsätzliche Richtlinien für das Schreiben von Kommentaren:  
  
-   In Kommentaren können Sie sämtliche alphanumerischen Zeichen oder Symbole verwenden. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ignoriert alle Zeichen in Kommentaren.  
  
-   Es gibt keine Längenbeschränkung für einen Kommentar innerhalb einer Anweisung oder eines Skripts. Ein Kommentar kann aus einer oder mehreren Zeilen bestehen.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] unterstützt die folgenden Zeichenkombinationen als Kommentarzeichen:  
  
-   **(doppelte Schrägstriche).** Verwenden Sie diese Kommentarzeichen, um einen Kommentar auf der gleichen Zeile wie auszuführender Code oder auch einen Kommentar auf einer eigenen Zeile zu schreiben. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] wertet den gesamten Text von den doppelten Schrägstrichen bis zum Ende der Zeile als Kommentar aus. Wenn Sie einen mehrzeiligen Kommentar erstellen möchten, verwenden Sie die doppelten Schrägstriche am Anfang jeder Kommentarzeile. Weitere Informationen zu diesen Kommentarzeichen finden Sie unter [doppelten Schrägstrich &#40; Kommentar &#41; &#40; DMX &#41; ](../dmx/double-slash-comment-dmx.md).  
  
-   **--(doppelte Bindestriche).** Verwenden Sie diese Kommentarzeichen, um einen Kommentar auf der gleichen Zeile wie auszuführender Code oder auch einen Kommentar auf einer eigenen Zeile zu schreiben. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] wertet den gesamten Text von den doppelten Bindestrichen bis zum Ende der Zeile als Kommentar aus. Wenn Sie einen mehrzeiligen Kommentar erstellen möchten, verwenden Sie die doppelten Bindestriche am Anfang jeder Kommentarzeile. Weitere Informationen zu diesen Kommentarzeichen finden Sie unter [--&#40; Kommentar &#41; &#40; DMX &#41; Zusammenfassung](../dmx/comment-dmx-summary.md).  
  
-   **/\*... \*/ (Schrägstrich/Sternchen-Zeichenpaare).** Verwenden Sie diese Kommentarzeichen, um einen Kommentar auf der gleichen Zeile wie der auszuführende Code, einen Kommentar auf einer eigenen Zeile oder Kommentare innerhalb des ausführbaren Codes zu schreiben. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]Wertet den gesamten Text aus dem öffnenden kommentarzeichenpaar (/ *), zum schließenden kommentarzeichenpaar (\*/) als Teil des Kommentars. Um einen mehrzeiligen Kommentar erstellen möchten, starten Sie den Kommentar mit dem Öffnen Kommentarzeichen (/\*), und beenden Sie den Kommentar mit dem Schließen Kommentarzeichen (\*/). Die Zeilen des Kommentars sollten keine anderen Kommentarzeichen enthalten. Weitere Informationen zu diesen Kommentarzeichen finden Sie unter [Schrägstrich Stern &#40; Kommentar &#41; &#40; DMX &#41; ](../dmx/slash-star-comment-dmx.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Referenz](../dmx/data-mining-extensions-dmx-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Syntaxkonventionen](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Syntaxelemente](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struktur und die Verwendung von DMX-Vorhersageabfragen](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Grundlegendes zur Select-Anweisung von DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  

