---
title: Benennungsregeln (Analysis Services)-Objekt | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- objects [Analysis Services], naming
ms.assetid: b338a60d-4802-4b68-862a-6dc6a3f75e48
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9b489ecceb4d8aeb5716708ae680999a296b5d14
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="object-naming-rules-analysis-services"></a>Objektbenennungsregeln (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]In diesem Thema wird beschrieben, Benennungskonventionen für Objekte sowie reservierte Wörter und Zeichen in einem nicht verwendet werden, Objektnamen, im Code oder Skripts in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
##  <a name="bkmk_Names"></a>Benennungskonventionen  
 Jedes Objekt verfügt über eine **Namen** und **ID** -Eigenschaft, die innerhalb des Bereichs der übergeordneten Auflistung eindeutig sein muss. Beispielsweise können zwei Dimensionen denselben Namen haben, solange sich beide in unterschiedlichen Datenbanken befinden.  
  
 Obwohl Sie manuell angeben können die **ID** ist in der Regel automatisch generiert, wenn das Objekt erstellt wurde. Sie sollten keine Änderung der **ID** , sobald Sie mit dem Erstellen eines Modells begonnen haben. Alle Objektverweise im gesamten Modell basieren auf der **ID**. Daher kann die Änderung einer **ID** können führen, dass das Modell beschädigt.  
  
 **DataSource** und **DataSourceView** Objekte gelten keine nennenswerten Ausnahmen Benennungskonventionen. **DataSource** ID auf einen einzelnen Punkt (.), die nicht eindeutig sind, als Verweis auf die aktuelle Datenbank festgelegt werden kann. Eine zweite Ausnahme bildet **DataSourceView**, dem unterliegen der Benennungskonventionen für definiert **DataSet** Objekte in .NET Framework, in dem die **Namen** dient als die Der Bezeichner.  
  
 Die folgenden Regeln gelten für **Namen** und **ID** Eigenschaften.  
  
-   Bei den Namen wird die Groß-/Kleinschreibung nicht berücksichtigt. Ein Cube mit dem Namen "sales" und ein anderer mit dem Namen "Sales" können nicht gleichzeitig in derselben Datenbank vorhanden sein.  
  
-   Führende oder nachfolgende Leerzeichen sind in Objektnamen nicht zulässig. Innerhalb des Namens können Leerzeichen verwendet werden. Führende und nachfolgende Leerzeichen werden implizit abgeschnitten. Dies gilt für die **Namen** und **ID** eines Objekts.  
  
-   Es können maximal 100 Zeichen eingegeben werden.  
  
-   Es gibt keine besondere Anforderung für das erste Zeichen eines Bezeichners. Das erste Zeichen kann jedes gültige Zeichen sein.  
  
##  <a name="bkmk_reserved"></a>Reservierte Wörter und Zeichen  
 Reservierte Wörter sind auf Englisch und gelten für Objektnamen, nicht für Beschriftungen. Wenn Sie versehentlich ein reserviertes Wort in einem Objektnamen verwenden, tritt ein Überprüfungsfehler auf. Bei mehrdimensionalen und Data Mining-Modellen können die unten beschriebenen reservierten Wörter in Objektnamen nicht verwendet werden.  
  
 Bei tabellarischen Modellen, deren Datenbankkompatibilität auf 1103 festgelegt ist, wurden die Überprüfungsregeln für bestimmte Objekte gelockert, um Kompatibilität mit den erweiterten Zeichenanforderungen und Benennungskonventionen bestimmter Clientanwendungen zu gewährleisten. Datenbanken, die diese Kriterien erfüllen, unterliegen weniger strengen Überprüfungsregeln. In diesem Fall ist die Überprüfung eines Objektnamens auch dann erfolgreich, wenn er reserviertes Zeichen enthält.  
  
 **Reservierte Wörter**  
  
-   AUX  
  
-   CLOCK$  
  
-   COM1 bis COM9 (COM1, COM2, COM3 usw.)  
  
-   CON  
  
-   LPT1 bis LPT9 (LPT1, LPT2, LPT3 usw.)  
  
-   NUL  
  
-   PRN  
  
-   NULL ist in XML in keiner Zeichenfolge als Zeichen zulässig.  
  
 **Reservierte Zeichen**  
  
 In der folgenden Tabelle werden die ungültigen Zeichen für bestimmte Objekte aufgeführt.  
  
|Objekt|Ungültige Zeichen|  
|------------|------------------------|  
|**Server**|Beachten Sie die Windows-Serverbenennungskonventionen, wenn Sie ein Serverobjekt benennen. Finden Sie unter [Benennungskonventionen (Windows)](http://msdn.microsoft.com/library/windows/desktop/ms682856\(v=vs.85\).aspx) für Details.|  
|**DataSource**|: / \ * &#124; ? " () [] {} <>|  
|**Ebene** oder **Attribut**|zugreifen. , ; ' ` : / \ * &#124; ? " & % $ ! + = [] {} < >|  
|**Dimension** oder **Hierarchie**|zugreifen. , ; ' ` : / \ * &#124; ? " & % $ ! + = () [] {} \<,>|  
|Alle anderen Objekte|zugreifen. , ; ' ` : / \ * &#124; ? " & % $ ! + = () [] {} < >|  
  
 **Ausnahmen: Wenn reservierte Zeichen zulässig sind**  
  
 Wie bereits erwähnt, können in Datenbanken mit einer bestimmten Modalität und einem bestimmten Kompatibilitätsgrad Objektnamen verwendet werden, die reservierte Zeichen enthalten. Dimensionsattribut-, Hierarchie-, Ebenen-, Measure- und KPI-Objektnamen für tabellarische Datenbanken (1103 oder höher) können reservierte Zeichen enthalten, wenn diese Datenbanken die Verwendung erweiterter Zeichen zulassen:  
  
|Servermodus und Datenbank-Kompatibilitätsgrad|Reservierte Zeichen zulässig?|  
|--------------------------------------------------|----------------------------------|  
|MOLAP (alle Versionen)|nein|  
|Tabellarischer Modus - 1050|nein|  
|Tabellarischer Modus - 1100|nein|  
|Tabellarischer Modus – 1130 und höher|ja|  
  
 Für Datenbanken kann als ModelType Default angegeben sein. 
          Default ist äquivalent zu Multidimensional, und die Verwendung von reservierten Zeichen in Spaltennamen wird in diesem Fall nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
 [Reservierte Wörter in MDX](../../../mdx/mdx-reserved-words.md)   
 [Unterstützung für Übersetzungen in Analysis Services](../../../analysis-services/translation-support-in-analysis-services.md)   
 [XML for Analysis-Kompatibilität &#40; XMLA &#41;](../../../analysis-services/xmla/xml-for-analysis-compliance-xmla.md)  
  
  
