---
title: Kreuzvalidierungsformeln | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
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
ms.topic: article
ms.assetid: fd1ea582-29a1-4154-8de2-47bab3539b4d
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 041206471791fe8be8b06e407854f96fc021eedd
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="cross-validation-formulas"></a>Kreuzvalidierungsformeln
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Wenn Sie einen kreuzvalidierungsbericht generieren, enthält es genauigkeitsmeasures für jedes Modell in Abhängigkeit von den Typ des Miningmodells (d. h. der Algorithmus, der zum Erstellen des Modells verwendet wurde), der den Datentyp des vorhersagbaren Attributs und dem vorhersagbaren Attribut Wert, falls vorhanden.  
  
 In diesem Abschnitt werden die im Kreuzvalidierungsbericht verwendeten Measures aufgeführt und die Berechnungsmethode beschrieben.  
  
 Eine Aufschlüsselung der Genauigkeitsmeasures nach Modelltyp finden Sie unter [Measures im Kreuzvalidierungsbericht](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).  
  
## <a name="formulas-used-for-cross-validation-measures"></a>Für Kreuzvalidierungsmeasures verwendete Formeln  
  
> [!NOTE]  
>  **Wichtig:** Diese Genauigkeitsmeasures werden für jedes Zielattribut berechnet. Sie können für jedes Attribut einen Zielwert bestimmen oder weglassen. Wenn ein Fall in einem Dataset über keinen Wert für das Zielattribut verfügt, wird der Fall so behandelt, als hätte er einen Spezialwert, der als *fehlender Wert*bezeichnet wird. Zeilen, die fehlende Werte aufweisen, werden beim Berechnen des Genauigkeitsmeasures für ein bestimmtes Zielattribut nicht gezählt. Da die Ergebnisse für jedes Attribut einzeln berechnet werden, wird das Ergebnis für das Zielattribut nicht beeinflusst, wenn Werte für das Zielattribut, jedoch nicht für andere Attribute vorhanden sind.  
  
|Measure|Gilt für|Implementierung|  
|-------------|----------------|--------------------|  
|**Richtig positiv**|Diskretes Attribut, Wert wird angegeben|Anzahl der Fälle, die diese Bedingungen erfüllen:<br /><br /> Fall enthält den Zielwert.<br /><br /> Modell hat vorhergesagt, dass der Fall den Zielwert enthält.|  
|**Wahr negativ**|Diskretes Attribut, Wert wird angegeben|Anzahl der Fälle, die diese Bedingungen erfüllen:<br /><br /> Fall enthält den Zielwert nicht.<br /><br /> Modell hat vorhergesagt, dass der Fall den Zielwert nicht enthält.|  
|**Falsch positiv**|Diskretes Attribut, Wert wird angegeben|Anzahl der Fälle, die diese Bedingungen erfüllen:<br /><br /> Tatsächlicher Wert ist gleich dem Zielwert.<br /><br /> Modell hat vorhergesagt, dass der Fall den Zielwert enthält.|  
|**Falsch negativ**|Diskretes Attribut, Wert wird angegeben|Anzahl der Fälle, die diese Bedingungen erfüllen:<br /><br /> Tatsächlicher Wert ist ungleich dem Zielwert.<br /><br /> Modell hat vorhergesagt, dass der Fall den Zielwert nicht enthält.|  
|**Erfolgreich/Fehler**|Diskretes Attribut, kein festgelegtes Ziel|Anzahl der Fälle, die diese Bedingungen erfüllen:<br /><br /> Erfolgreich, wenn der vorhergesagte Status mit der höchsten Wahrscheinlichkeit gleich dem Eingabestatus ist und die Wahrscheinlichkeit größer als der Wert von **Statusschwellenwert**ist.<br /><br /> Andernfalls fehlgeschlagen.|  
|**Lift**|Diskretes Attribut. Zielwert kann angegeben werden, ist aber nicht erforderlich.|Die mittlere logarithmische Wahrscheinlichkeit für alle Zeilen mit Werten für das Zielattribut, wobei die logarithmische Wahrscheinlichkeit pro Fall als Log(ActualProbability/MarginalProbability) berechnet wird. Um den Mittelwert zu berechnen, wird die Summe der Protokollierungswahrscheinlichkeitswerte durch die Anzahl der Zeilen im Eingabedataset dividiert, wobei Zeilen mit fehlenden Werten für das Zielattribut ausgeschlossen werden.<br /><br /> Als Prognosegüte kann ein negativer oder ein positiver Wert angegeben werden. Ein positiver Wert steht für ein effektives Modell, das die Zufallsvorhersage übertrifft.|  
|**Logarithmisches Ergebnis**|Diskretes Attribut. Zielwert kann angegeben werden, ist aber nicht erforderlich.|Logarithmus der tatsächlichen Wahrscheinlichkeit für jeden Fall, summiert und dann dividiert durch die Anzahl von Zeilen im Eingabedataset, ohne die Zeilen mit fehlenden Werten für das Zielattribut.<br /><br /> Da die Wahrscheinlichkeit als Dezimalbruch dargestellt wird, sind logarithmische Ergebnisse immer negative Zahlen. Je näher das Ergebnis an 0 liegt, desto besser ist es.|  
|**Fallwahrscheinlichkeit**|Cluster|Summe der Clusterwahrscheinlichkeitsergebnisse für alle Fälle, dividiert durch die Anzahl der Fälle in der Partition, ohne die Zeilen mit fehlenden Werten für das Zielattribut.|  
|**Mittlerer absoluter Fehler**|Kontinuierliches Attribut|Summe der absoluten Fehler für alle Fälle in der Partition, dividiert durch die Anzahl der Fälle in der Partition.|  
|**Wurzel des mittleren quadratischen Fehlers**|Kontinuierliches Attribut|Quadratwurzel des mittleren Fehlers für die Partition zum Quadrat.|  
|**Wurzel des mittleren Fehlers zum Quadrat**|Diskretes Attribut. Zielwert kann angegeben werden, ist aber nicht erforderlich.|Quadratwurzel des Mittelwerts der quadrierten Komplemente des Wahrscheinlichkeitsergebnisses, dividiert durch die Anzahl der Fälle in der Partition, ohne die Zeilen mit fehlenden Werten für das Zielattribut.|  
|**Wurzel des mittleren Fehlers zum Quadrat**|Diskretes Attribut, kein festgelegtes Ziel|Quadratwurzel des Mittelwerts der quadrierten Komplemente des Wahrscheinlichkeitsergebnisses, dividiert durch die Anzahl der Fälle in der Partition, ohne die Fälle mit fehlenden Werten für das Zielattribut.|  
  
## <a name="see-also"></a>Siehe auch  
 [Tests und Überprüfung &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)   
 [Kreuzvalidierung &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)  
  
  
