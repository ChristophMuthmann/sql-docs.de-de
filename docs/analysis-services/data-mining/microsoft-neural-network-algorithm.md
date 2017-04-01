---
title: "Microsoft Neural Network-Algorithmus | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Schulen neuronaler Netzwerke"
  - "Ausgabeneuronen [Analysis Services]"
  - "Algorithmen [Data Mining]"
  - "Neural Network-Algorithmen [Analysis Services]"
  - "Neuronen [Analysis Services]"
  - "Klassifikationsalgorithmen [Analysis Services]"
  - "Neuronale Netzwerke"
  - "Mehrschichtiges Perzeptronnetzwerk von Neuronen [Analysis Services]"
  - "Verborgene Neuronen"
  - "Deltaregelnetzwerk mit Rückpropagierung"
  - "Eingabeneuronen [Analysis Services]"
  - "Regressionsalgorithmen [Analysis Services]"
ms.assetid: 61eb4861-8a6a-4214-a4b8-1dd278ad7a68
caps.latest.revision: 46
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 46
---
# Microsoft Neural Network-Algorithmus
  Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus ist eine Implementierung der beliebten und anpassbaren Architektur für neuronale Netzwerke für das Machine Learning.  Der Algorithmus testet jeden möglichen Status des Eingabeattributs mit jedem möglichen Status des vorhersagbaren Attributs und nutzt die Trainingsdaten für die Berechnung der Wahrscheinlichkeiten für jede Kombination. Sie können diese Wahrscheinlichkeiten später für Klassifizierungs- oder Regressionstasks und für die Vorhersage eines Ergebnisses auf Basis einiger Eingabeattribute verwenden. Ein neuronales Netzwerk kann auch für die Zuordnungsanalyse verwendet werden.  
  
 Beim Erstellen eines Miningmodells mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus können Sie mehrere Ausgaben einschließen – der Algorithmus erstellt dann mehrere Netzwerke. Die Anzahl der Netzwerke in einem einzelnen Miningmodell ist abhängig von der Anzahl der Status (oder Attributwerte) in den Eingabespalten sowie die Anzahl der vorhersagbaren Spalten, die das Miningmodell verwendet, und der Anzahl der Status in diesen Spalten.  
  
## Beispiel  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus ist hilfreich zum Analysieren komplexer Eingabedaten, z. B. die eines Produktions- oder Handelsprozesses oder von Geschäftsproblemen. Für diese Daten sind zwar bedeutende Trainingsdatenmengen verfügbar, jedoch können für diese Daten Regeln mithilfe anderer Algorithmen nicht einfach abgeleitet werden.  
  
 Das Verwenden des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus wird in folgenden Szenarien empfohlen:  
  
-   Marketing- und Werbeanalysen, z.B. zur Erfolgsermittlung einer direkten Werbung oder einer Radiowerbekampagne  
  
-   Vorhersagen von Kursschwankungen, Währungsveränderungen oder anderen stark veränderlichen Finanzinformationen aus Verlaufsdaten  
  
-   Analysieren von Produktions- und Industrieprozessen  
  
-   Textmining  
  
-   Jedes Vorhersagemodell, das komplexe Beziehungen zwischen vielen Eingaben und relativ wenigen Ausgaben analysiert  
  
## Funktionsweise des Algorithmus  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus erstellt ein Netzwerk, das aus bis zu drei Knotenebenen besteht (die auch als *Neuronen* bezeichnet werden). Zu diesen Ebenen gehört eine *Eingabeebene*, die *verborgene Ebene* und eine *Ausgabeebene*.  
  
 **Eingabeebene:** Eingabeknoten definieren alle Eingabeattributwerte für das Data Mining-Modell und deren Wahrscheinlichkeiten.  
  
 **Verborgene Ebene:** Verborgene Knoten empfangen die von Eingabeknoten bereitgestellten Eingaben und stellen Ausgabeknoten die empfangenen Ausgaben zur Verfügung. In der verborgenen Ebene werden den verschiedenen Wahrscheinlichkeiten der Eingaben Gewichtungen zugewiesen. Eine Gewichtung beschreibt die Relevanz oder Wichtigkeit einer bestimmten Eingabe zum verborgenen Knoten. Je größer die Gewichtung ist, die einer Eingabe zugewiesen wird, desto wichtiger ist der Wert dieser Eingabe. Gewichtungen können negativ sein, was bedeutet, dass ein bestimmtes Ergebnis durch die Eingabe eher unterdrückt als begünstigt werden kann.  
  
 **Ausgabeebene:** Ausgabeknoten stellen vorhersagbare Attributwerte des Data Mining-Modells dar.  
  
 Eine ausführliche Erklärung dazu, wie die Eingabeebene, die verborgene Ebene und die Ausgabeebene erstellt und eingestuft werden, finden Sie unter [Technische Referenz für den Microsoft Neural Network-Algorithmus](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md).  
  
## Erforderliche Daten für neuronale Netzwerkmodelle  
 Ein neuronales Netzwerkmodell muss eine Schlüsselspalte, mindestens eine Eingabespalte und mindestens eine vorhersagbare Spalte enthalten.  
  
 Data Mining-Modelle, die den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network-Algorithmus verwenden, hängen stark von den Werten ab, die Sie für die im Algorithmus verfügbaren Parameter festlegen. Die Parameter legen fest, wie Daten als Stichprobe genommen werden, wie die Daten in jeder Spalte verteilt werden oder werden sollen und wann die Funktionsauswahl aufgerufen wird, um die im endgültigen Modell zu verwendenden Werte einzugrenzen.  
  
 Weitere Informationen zum Festlegen der Parameter für das Anpassen des Modellverhaltens finden Sie unter [Technische Referenz für den Microsoft Neural Network-Algorithmus](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md).  
  
## Anzeigen eines neuronalen Netzwerkmodells  
 Um mit den Daten zu arbeiten und zu sehen, wie das Modell Eingaben mit Ausgaben korreliert, können Sie den **Microsoft-Viewer für neuronale Netzwerke**verwenden. Über diesen benutzerdefinierten Viewer können Sie Eingabeattribute und deren Werte filtern und Diagramme einsehen, die darstellen, welche Auswirkungen diese auf die Ausgaben haben. Die QuickInfos im Viewer zeigen die Wahrscheinlichkeit und Prognose für jedes Paar an Eingabe- und Ausgabewerten an. Weitere Informationen finden Sie unter [Modell mit dem Microsoft-Viewer für neuronale Netzwerke durchsuchen](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md).  
  
 Die einfachste Art und Weise, die Struktur des Modells zu durchsuchen, erfolgt über den **Microsoft Generic Content Tree-Viewer**. Hier können Sie die Eingaben, Ausgaben und Netzwerke einsehen, die vom Modell erstellt wurden, und auf jeden beliebigen Knoten klicken, um diesen zu erweitern und Statistiken in Bezug auf die Knoten der Eingabe-, Ausgabeebene und der verborgenen Ebene einzusehen. Weitere Informationen finden Sie unter [Durchsuchen eines Modells mit dem Microsoft Generic Content Tree Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
## Erstellen von Vorhersagen  
 Nachdem das Modell verarbeitet wurde, können Sie das Netzwerk und die innerhalb eines jeden Knotens gespeicherten Gewichtungen verwenden, um Vorhersagen zu erstellen. Ein neuronales Netzwerkmodell unterstützt Regression, Zuordnung und Klassifikationsanalyse. Daher können die Bedeutungen der einzelnen Vorhersagen unterschiedlich sein. Darüber hinaus können Sie das Modell selbst abfragen, um die gefundenen Korrelationen zu prüfen und die entsprechenden Statistiken abzurufen. Beispiele dazu, wie Abfragen für ein Modell für ein neuronales Netzwerk erstellt werden, finden Sie unter [Abfragebeispiele für neuronale Netzwerkmodelle](../../analysis-services/data-mining/neural-network-model-query-examples.md).  
  
 Allgemeine Informationen zur Erstellung von Abfragen für ein Data Mining-Modell finden Sie unter [Data Mining-Abfragen](../../analysis-services/data-mining/data-mining-queries.md).  
  
## Hinweise  
  
-   Unterstützt nicht Drillthrough oder Data Mining-Dimensionen. Grund hierfür ist, dass die Struktur der Knoten im Miningmodell nicht zwangsläufig den zugrunde liegenden Daten direkt entspricht.  
  
-   Unterstützt nicht die Erstellung von Modellen im PMML-Format (Predictive Model Markup Language).  
  
-   Unterstützt die Verwendung von OLAP-Miningmodellen.  
  
-   Unterstützt nicht die Erstellung von Data Mining-Dimensionen.  
  
## Siehe auch  
 [Technische Referenz für den Microsoft Neural Network-Algorithmus](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [Miningmodellinhalt von neuronalen Netzwerkmodellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Neuronale Beispiele für Netzwerkmodellabfragen](../../analysis-services/data-mining/neural-network-model-query-examples.md)   
 [Microsoft Logistic Regression-Algorithmus](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)  
  
  