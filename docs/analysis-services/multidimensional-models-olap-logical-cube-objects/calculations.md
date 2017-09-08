---
title: Berechnungen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- calculations [Analysis Services]
- OLAP objects [Analysis Services], calculations
- MDX [Analysis Services], calculations
- calculations [Analysis Services], about calculations
- cubes [Analysis Services], calculations
ms.assetid: 6be84916-fd05-4efc-ab98-6adbbad80154
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6fa38369b12c07a47a2501bc906535b0263db2e5
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="calculations"></a>Berechnungen
  Eine Berechnung ist ein Ausdruck (Multidimensional Expressions) oder ein Skript, das verwendet wird, definieren Sie ein berechnetes Element, eine benannte Menge oder eine Zuweisung mit definiertem Bereich in einem Cube in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Mithilfe von Berechnungen können Sie einem Cube Objekte hinzufügen, die nicht durch die Daten des Cubes definiert sind, sondern über Ausdrücke, die auf andere Teile des Cubes, andere Cubes oder auch auf Informationen außerhalb der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbank verweisen können. Mithilfe von Berechnungen können Sie die Funktionen eines Cubes erweitern, wodurch Business Intelligence-Anwendungen flexibler und leistungsfähiger werden. Weitere Informationen zu skripterstellungsberechnungen finden Sie unter [Introduction to MDX Scripting in Microsoft SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81892). Weitere Informationen zu Leistungsproblemen im Zusammenhang mit MDX-Abfragen und-Berechnungen finden Sie unter der [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621).  
  
## <a name="calculated-members"></a>Berechnete Elemente  
 Bei einem berechneten Element handelt es sich um ein Element, dessen Wert zur Laufzeit mithilfe eines MDX-Ausdrucks (Multidimensional Expressions) berechnet wird, den Sie beim Definieren des berechneten Elements angeben. Ein berechnetes Element ist für Business Intelligence-Anwendungen in gleicher Weise wie andere Elemente auch verfügbar. Durch berechnete Elemente wird die Größe des Cubes nicht erhöht, da nur die Definitionen im Cube gespeichert werden. Die Werte werden im Arbeitsspeicher berechnet, wenn sie zur Beantwortung einer Abfrage benötigt werden.  
  
 Berechnete Elemente können für eine beliebige Dimension, einschließlich der Measuredimension, definiert werden. Berechnete Elemente, die auf der Measuredimension erstellt wurden, werden als berechnete Measures bezeichnet.  
  
 Obwohl berechnete Elemente normalerweise auf Daten basieren, die bereits im Cube vorhanden sind, können Sie komplexe Ausdrücke erstellen, indem Sie Daten mit arithmetischen Operatoren, Zahlen und Funktionen kombinieren. Mit MDX-Funktionen wie LookupCube können Sie auch auf Daten in anderen Cubes in der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbank zugreifen. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] enthält standardisierte Visual Studio-Funktionsbibliotheken, und mit gespeicherten Prozeduren können Sie Daten aus anderen Quellen als der aktuellen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbank abrufen. Weitere Informationen zu gespeicherten Prozeduren finden Sie unter [gespeicherte Prozeduren definieren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md).  
  
 Angenommen, die leitenden Mitarbeiter eines Transportunternehmens möchten ermitteln, welcher Frachttyp, ausgehend vom Gewinn pro Mengeneinheit, rentabler versendet werden kann. Sie verwenden dazu einen Shipments-Cube, der die Dimensionen Cargo, Fleet und Time sowie die Measures Price_to_Ship, Cost_to_Ship und Volume_in_Cubic_Meters enthält; der Cube enthält jedoch kein Measure für die Rentabilität. Sie können in dem Cube ein berechnetes Element als Measure mit dem Namen Profit_per_Cubic_Meter erstellen, wobei Sie die vorhandenen Measures im folgenden Ausdruck verwenden:  
  
```  
([Measures].[Price_to_Ship] - [Measures].[Cost_to_Ship]) /  
[Measures].[Volume_in_Cubic_Meters]  
```  
  
 Nachdem Sie das berechnete Element erstellt haben, wird Profit_per_Cubic_Meter zusammen mit den anderen Measures angezeigt, wenn Sie den Shipments-Cube das nächste Mal durchsuchen.  
  
 Verwenden Sie zum Erstellen berechneter Elemente der **Berechnung**Registerkarte im Cube-Designer. Weitere Informationen finden Sie unter [berechnete Elemente erstellen](../../analysis-services/multidimensional-models/create-calculated-members.md)  
  
## <a name="named-sets"></a>Benannte Mengen  
 Eine benannte Menge ist ein CREATE SET MDX-Anweisungsausdruck, der eine Menge zurückgibt. Der MDX-Ausdruck wird als Teil der Definition eines Cubes in gespeichert [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Eine benannte Menge wird zum Wiederverwenden in MDX-Abfragen (Multidimensional Expressions) erstellt. Mithilfe einer benannten Menge können Anwender des Produkts im geschäftlichen Bereich Abfragen vereinfachen und für komplexe, häufig verwendete Mengenausdrücke einen Mengennamen anstelle eines Mengenausdrucks verwenden. **Verwandtes Thema:** [benannten Mengen erstellen](../../analysis-services/multidimensional-models/create-named-sets.md)  
  
## <a name="script-commands"></a>Skriptbefehle  
 Ein Skriptbefehl ist ein MDX-Skript, das in der Cubedefinition enthalten ist. Mithilfe von Skriptbefehlen können Sie nahezu jede Aktion ausführen, die von MDX auf einem Cube unterstützt wird, wie etwa eine Berechnung mit einem definierten Bereich, die nur auf einen Teil des Cubes angewendet wird. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], MDX-Skripts können entweder den gesamten Cube oder auf bestimmte Abschnitte des Cubes an bestimmten Punkten während der gesamten Ausführung des Skripts anwenden. Der Standardskriptbefehl, die CALCULATE-Anweisung, füllt Zellen im Cube mit aggregierten Daten auf, die auf dem Standardbereich basieren.  
  
 Der Standardbereich ist der gesamte Cube, aber Sie können auch einen begrenzteren Bereich angeben, einen so genannten Teilcube, und ein MDX-Skript dann nur auf diesen bestimmten Cubebereich anwenden. Die SCOPE-Anweisung definiert den Bereich aller nachfolgenden MDX-Ausdrücke und -Anweisungen im Berechnungsskript, bis der Bereich beendet oder erneut definiert wird. Dann wird die THIS-Anweisung verwendet, um einen MDX-Ausdruck auf den aktuellen Bereich anzuwenden. Sie können die BACK_COLOR-Anweisung verwenden, um eine Hintergrundzellenfarbe für die Zellen im aktuellen Bereich festzulegen. Dies ist beim Debuggen sehr hilfreich.  
  
 Sie können einen Skriptbefehl z. B. verwenden, um Mitarbeitern für einen gewissen Zeitraum Sollvorgaben und ein Vertriebsgebiet auf der Grundlage der gewichteten Verkaufszahlen für einen früheren Zeitraum zuzuordnen.  
  
## <a name="see-also"></a>Siehe auch  
 [Berechnungen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
