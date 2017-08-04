---
title: "--(Kommentar) (DMX)-Übersicht | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- commenting characters
- double hyphens
- -- (comment character)
ms.assetid: 487b580b-5b81-4e52-8868-4fa809e4ef58
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0ab3cef118685094ae96e02dcbf6b994e1157cd0
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="---comment-dmx-summary"></a>--(Kommentar) (DMX)-Zusammenfassung
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Kennzeichnet eine Textzeichenfolge, die [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nicht ausführen soll. Sie können Kommentare in einer DMX-Anweisung (Data Mining-Erweiterungen) schachteln, am Ende einer Codezeile anfügen oder in eine eigene Zeile einfügen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>Parameter  
 *Comment_Text*  
 Die Zeichenfolge, die den Text des Kommentars enthält.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie diesen Operator für einzeilige oder geschachtelte Kommentare. Kommentare, die mithilfe von -- eingefügt werden, werden durch das Neue-Zeile-Zeichen begrenzt.  
  
 Es gibt keine Maximallänge für Kommentare.  
  
 Weitere Informationen zur Verwendung von unterschiedlichen Arten von Kommentaren in DMX finden Sie unter [Kommentare &#40; DMX &#41;](../dmx/comments-dmx.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Schrägstrich-Stern &#40; Kommentar &#41; &#40; DMX &#41;](../dmx/slash-star-comment-dmx.md)   
 [Doppelten Schrägstrich &#40; Kommentar &#41; &#40; DMX &#41;](../dmx/double-slash-comment-dmx.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operatoren &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

