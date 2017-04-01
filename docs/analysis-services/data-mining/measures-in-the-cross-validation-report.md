---
title: "Measures im Kreuzvalidierungsbericht | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Wurzel des mittleren Fehlers zum Quadrat [Data Mining]"
  - "Kreuzvalidierung [Data Mining]"
  - "mittlerer absoluter Fehler [Data Mining]"
  - "Protokollergebnis [Data Mining]"
  - "Wahrscheinlichkeit [Data Mining]"
ms.assetid: a07b1665-7f72-4266-82a4-43a91ae2571d
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 28
---
# Measures im Kreuzvalidierungsbericht
  Während der Kreuzvalidierung werden die Daten in einer Miningstruktur von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in mehrere Querschnitte unterteilt. Anschließend werden die Struktur und zugeordnete Miningmodelle iterativ getestet. Auf Grundlage dieser Analyse wird eine Reihe standardmäßiger Genauigkeitsmeasures für die Struktur und jedes Modell ausgegeben.  
  
 Der Bericht enthält einige grundlegende Informationen über die Anzahl der Folds in den Daten sowie die Menge der Daten in jeder Aufteilung sowie einen Satz allgemeiner Metriken zur Beschreibung der Datenverteilung. Sie können die Zuverlässigkeit der Struktur oder des Modells bewerten, indem Sie die allgemeinen Metriken für jeden Querschnitt vergleichen.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] wird auch ein Satz detaillierter Measures für Miningmodelle angezeigt. Diese Measures hängen vom Modelltyp und dem Typ des analysierten Attributs ab, beispielsweise davon, ob es sich um ein diskretes oder kontinuierliches Attribut handelt.  
  
 Dieser Abschnitt enthält eine Liste der im **Kreuzvalidierungsbericht** aufgeführten Measures sowie Erläuterungen zu deren Bedeutung. Ausführliche Informationen zur Berechnung der einzelnen Measures finden Sie unter [Kreuzvalidierungsformeln](../../analysis-services/data-mining/cross-validation-formulas.md).  
  
## Liste der Measures im Kreuzvalidierungsbericht  
 In der folgenden Tabelle sind die Measures aufgelistet, die im Kreuzvalidierungsbericht angezeigt werden. Die Measures werden nach dem *Testtyp* gruppiert, der in der linken Spalte der folgenden Tabelle angegeben ist. In der rechten Spalte ist der Name des Measures, so wie im Bericht angezeigt, und eine kurze Erläuterung zu dessen Bedeutung enthalten.  
  
|Testtyp|Measures und Beschreibungen|  
|---------------|-------------------------------|  
|Clustering|Auf Clustermodelle anwendbare Measures|  
||**Fallwahrscheinlichkeit**:<br />                      Dieses Measure gibt normalerweise an, wie wahrscheinlich es ist, dass ein Fall einem bestimmten Cluster angehört. Bei der Kreuzvalidierung werden die Ergebnisse addiert und dann durch die Anzahl der Fälle dividiert, sodass das Ergebnis in diesem Fall einer durchschnittlichen Fallwahrscheinlichkeit entspricht.|  
|Klassifizierung|Auf Klassifizierungsmodelle anwendbare Measures|  
||**Wahr positiv**/**Falsch positiv**/**Wahr negativ**/**Falsch negativ**:<br /><br /> Anzahl der Zeilen oder Werte in der Partition, in denen der vorhergesagte Status mit dem Zielstatus übereinstimmt und die Vorhersagewahrscheinlichkeit höher als der angegebene Schwellenwert ist.<br /><br /> Fälle mit fehlenden Werten für das Zielattribut werden ausgeschlossen. Dies bedeutet, dass die Anzahl sämtlicher Werte u. U. nicht mit der ursprünglichen Summe übereinstimmt.|  
||**Erfolgreich/Fehler**:<br />                      Anzahl der Zeilen oder Werte in der Partition, in denen der vorhergesagte Status mit dem Zielstatus übereinstimmt und der Vorhersagewahrscheinlichkeitswert größer als 0 ist.|  
|Wahrscheinlichkeit|Wahrscheinlichkeitsmeasures können auf mehrere Modelltypen angewendet werden.|  
||**Lift**:<br />                      Das Verhältnis der tatsächlichen Vorhersagewahrscheinlichkeit zur Randwahrscheinlichkeit in den Testfällen. Zeilen mit fehlenden Werten für das Zielattribut werden ausgeschlossen.<br /><br /> Dieses Measure gibt normalerweise den Grad an, um den sich die Wahrscheinlichkeit des Zielergebnisses verbessert, wenn das Modell verwendet wird.|  
||**Wurzel des mittleren quadratischen Fehlers**:<br />                      Quadratwurzel des mittleren Fehlers für alle Partitionsfälle geteilt durch die Anzahl der Fälle in der Partition ohne die Zeilen mit fehlenden Werten für das Zielattribut.<br /><br /> RMSE ist eine bekannte Schätzfunktion für Vorhersagemodelle. Im Ergebnis werden die Restwerte für jeden Fall gemittelt, wodurch sich ein einzelner Indikator für den Modellfehler ergibt.|  
||**Protokollergebnis**:<br />                      Der Logarithmus der tatsächlichen Wahrscheinlichkeit für jeden Fall, summiert und dann dividiert durch die Anzahl von Zeilen im Eingabedataset, ohne die Zeilen mit fehlenden Werten für das Zielattribut.<br /><br /> Da die Wahrscheinlichkeit als Dezimalbruch dargestellt wird, sind logarithmische Ergebnisse immer negative Zahlen. Eine Zahl, die näher bei 0 liegt, ist ein besseres Ergebnis. Während Rohergebnisse sehr unregelmäßige oder verfälschte Verteilungen aufweisen können, ist ein logarithmisches Ergebnis einem Prozentwert ähnlich.|  
|Schätzung|Measures, die nur auf Schätzungsmodelle angewendet werden, die ein kontinuierliches numerisches Attribut vorhersagen.|  
||**Wurzel des mittleren quadratischen Fehlers**:<br />                      Durchschnittliche Abweichung, wenn der vorhergesagte Wert mit dem Istwert verglichen wird.<br /><br /> RMSE ist eine bekannte Schätzfunktion für Vorhersagemodelle. Im Ergebnis werden die Restwerte für jeden Fall gemittelt, wodurch sich ein einzelner Indikator für den Modellfehler ergibt.|  
||**Mittlerer absoluter Fehler**:<br />                      Durchschnittliche Abweichung, wenn vorhergesagte Werte mit Istwerten verglichen werden, berechnet als Mittelwert der absoluten Summe der Fehler.<br /><br /> Mithilfe des mittleren absoluten Fehlers lässt sich einfacher verdeutlichen, wie nahe die Vorhersagen und die Istwerte insgesamt beieinander liegen. Ein kleineres Ergebnis bedeutet, dass die Vorhersagen genauer waren.|  
||**Protokollergebnis**:<br />                      Der Logarithmus der tatsächlichen Wahrscheinlichkeit für jeden Fall, summiert und dann dividiert durch die Anzahl von Zeilen im Eingabedataset, ohne die Zeilen mit fehlenden Werten für das Zielattribut.<br /><br /> Da die Wahrscheinlichkeit als Dezimalbruch dargestellt wird, sind logarithmische Ergebnisse immer negative Zahlen. Eine Zahl, die näher bei 0 liegt, ist ein besseres Ergebnis. Während Rohergebnisse sehr unregelmäßige oder verfälschte Verteilungen aufweisen können, ist ein logarithmisches Ergebnis einem Prozentwert ähnlich.|  
|Aggregate|Aggregierte Measures geben die Varianz in den Ergebnissen für jede Partition an.|  
||**Mittelwert**:<br />                      Mittelwert der Partitionswerte für ein bestimmtes Measure.|  
||**Standardabweichung**:<br />                      Durchschnitt der Abweichung vom Mittelwert für ein bestimmtes Measure für alle Partitionen in einem Modell.<br /><br /> Bei der Kreuzvalidierung impliziert ein höherer Wert für dieses Ergebnis eine erhebliche Variation zwischen den Folds.|  
  
## Siehe auch  
 [Tests und Überprüfung &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  