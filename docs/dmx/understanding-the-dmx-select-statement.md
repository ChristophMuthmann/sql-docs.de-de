---
title: Grundlegendes zu DMX Select-Anweisung | Microsoft Docs
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
dev_langs: DMX
helpviewer_keywords:
- browsing mining model [Analysis Services]
- Data Mining Extensions [Analysis Services], statements
- DMX [Analysis Services], statements
- predictions [DMX]
- queries [DMX], Select statement
- SELECT statement [DMX]
- statements [DMX], SELECT statement
- copying mining models
ms.assetid: 61e97285-4a06-4434-9a40-38cde5af7c3f
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f8429c48fb398f1d1a9e3f20741c7eecfd0810b5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="understanding-the-dmx-select-statement"></a>Grundlegendes zur SELECT-Anweisung (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Die [wählen](../dmx/select-dmx.md) Anweisung bildet die Grundlage für die meisten Abfragen, die Sie mit Data Mining Extensions (DMX) in erstellen [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Mit dieser Anweisung können Sie viele unterschiedliche Aufgaben ausführen, so z. B. Durchsuchen von Data Mining-Modellen und Erstellen von Vorhersagen für Data Mining-Modelle.  
  
 Folgendes sind die Aufgaben, die Sie mithilfe von abschließen können die **wählen** Anweisung:  
  
-   Durchsuchen eines Data Mining-Modells. Das Schemarowset definiert die Struktur eines Modells.  
  
-   Ermitteln der möglichen Werte einer Miningmodellspalte.  
  
-   Durchsuchen der Fälle, die Knoten in einem Miningmodell zugewiesen sind, oder Abrufen eines repräsentativen Falls.  
  
-   Erstellen von Vorhersagen auf der Basis verschiedener Eingaben.  
  
-   Kopieren von Miningmodellen.  
  
 Jede dieser Aufgaben verwendet einen anderen Satz von Daten, d. h. nennen wir müssen einen *Datendomäne*. Sie definieren die Datendomäne in der **FROM** -Klausel der Anweisung.  
  
-   Sie möchten Objekte im Data Mining-Modell selbst suchen, z. B. die Regel, durch die ein Dataset definiert wird, oder eine Formel für Vorhersagen.  
  
     In diesem Fall müssen Sie die Metadaten untersuchen, die im Modell selbst gespeichert sind. Deshalb besteht die Datendomäne aus den Spalten, die durch das Data Mining-Schemarowset definiert sind.  
  
-   Sie möchten detaillierte Informationen zu den Fällen abrufen, auf deren Grundlage das Modell erstellt wird.  
  
     In diesem Fall müssen Sie einen Drillthrough zur Miningstruktur, d. h. Ihrer Datendomäne, durchführen und die einzelnen Zeilen in den Spalten (Gender, Bike Buyer usw.) untersuchen.  
  
 **Wichtig:** Elemente, die in die Ausdrucksliste oder in der **, in denen** Klausel muss seinen Ursprung der Datendomäne, die von definiert ist die **FROM** Klausel. Datendomänen können nicht gemischt werden.  
  
##  <a name="Select_Types"></a>Wählen Sie Objekttypen aus  
 Die Syntax der **wählen** -Anweisung unterstützt viele verschiedene Aufgaben. Diese Aufgaben führen Sie mithilfe der folgenden Muster aus:  
  
-   [Vorhersagen](#Predicting)  
  
-   [Durchsuchen](#Browsing)  
  
-   [Kopieren](#Copying)  
  
-   [Drillthrough](#Drillthrough)  
  
###  <a name="Predicting"></a>Vorhersagen  
 Mit folgenden Abfragetypen können Sie Vorhersagen ausführen, die auf einem Miningmodell basieren.  
  
 Sie können eine der zum Durchsuchen oder Vorhersagen einschließen **auswählen** Anweisungen innerhalb der **FROM** und **, in dem** einen Prediction Join-Klauseln **wählen Sie** Anweisung.  
  
|Abfragetyp|Description|  
|----------------|-----------------|  
|WÄHLEN SIE AUS DER [NATÜRLICHE] PREDICTION JOIN|Gibt eine Vorhersage zurück, die erstellt wurde, indem die Spalten des Miningmodells mit den Spalten einer internen Datenquelle verknüpft wurden.<br /><br /> Die Datendomäne für diesen Abfragetyp besteht aus den vorhersagbaren Spalten aus dem Modell und den Spalten aus der Eingabedatenquelle.<br /><br /> [SELECT FROM &#60; Modell &#62; PREDICTION JOIN-Abfrage &#40; DMX &#41;](../dmx/select-from-model-prediction-join-dmx.md)<br /><br /> [Vorhersageabfragen &#40; Datamining &#41;](../analysis-services/data-mining/prediction-queries-data-mining.md)|  
|SELECT FROM  *\<Modell >*|Gibt nur auf Basis des Miningmodells den wahrscheinlichsten Status der vorhersagbaren Spalte zurück. Dieser Abfragetyp ist eine Abkürzung für das Erstellen einer Vorhersage mit einem leeren PREDICTION JOIN.<br /><br /> Die Datendomäne für diesen Abfragetyp besteht aus den vorhersagbaren Spalten aus dem Modell.<br /><br /> [SELECT FROM &#60; Modell &#62; &#40; DMX &#41;](../dmx/select-from-model-dmx.md)<br /><br /> [Vorhersageabfragen &#40; Datamining &#41;](../analysis-services/data-mining/prediction-queries-data-mining.md)|  
  
 [Zurück zu Select-Typen](#Select_Types)  
  
###  <a name="Browsing"></a>Durchsuchen  
 Mit folgenden Abfragetypen können Sie die Inhalte eines Miningmodells durchsuchen.  
  
|Abfragetyp|Description|  
|----------------|-----------------|  
|SELECT DISTINCT FROM  *\<Modell >*|Gibt alle Statuswerte vom Miningmodell für die angegebene Spalte zurück.<br /><br /> Die Datendomäne für diesen Abfragetyp entspricht dem Data Mining-Modell.<br /><br /> [SELECT DISTINCT FROM &#60; Modell &#62; &#40; DMX &#41;](../dmx/select-distinct-from-model-dmx.md)<br /><br /> [Inhalt Abfragen &#40; Datamining &#41;](../analysis-services/data-mining/content-queries-data-mining.md)|  
|SELECT FROM  *\<Modell >*. INHALT|Gibt Inhalte mit Beschreibungen zum Miningmodell zurück.<br /><br /> Die Datendomäne für diesen Abfragetyp entspricht dem CONTENT-Schemarowset.<br /><br /> [SELECT FROM &#60; Modell &#62;. Inhalt &#40; DMX &#41;](../dmx/select-from-model-content-dmx.md)<br /><br /> [Inhalt Abfragen &#40; Datamining &#41;](../analysis-services/data-mining/content-queries-data-mining.md)|  
|SELECT FROM  *\<Modell >*. DIMENSION_CONTENT|Gibt Inhalte mit Beschreibungen zum Miningmodell zurück.<br /><br /> Die Datendomäne für diesen Abfragetyp entspricht dem CONTENT-Schemarowset.<br /><br /> [SELECT FROM &#60; Modell &#62;. DIMENSION_CONTENT &#40; DMX &#41;](../dmx/select-from-model-dimension-content-dmx.md)|  
|SELECT FROM  *\<Modell >*. PMML|Gibt für Algorithmen, die diese Funktionalität unterstützen, die PMML-Darstellung (Predictive Model Markup Language) des Miningmodells zurück.<br /><br /> Die Datendomäne für diesen Abfragetyp besteht aus dem PMML-Schemarowset.<br /><br /> [DMSCHEMA_MINING_MODEL_CONTENT_PMML-Rowset](../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)|  
  
 [Zurück zu Select-Typen](#Select_Types)  
  
###  <a name="Copying"></a>Kopieren  
 Sie können ein Miningmodell sowie dessen zugeordnete Miningstruktur in ein neues Modell kopieren und das Modell anschließend innerhalb der Anweisung umbenennen.  
  
|Abfragetyp|Description|  
|----------------|-----------------|  
|SELECT INTO  *\<neues Modell >*|Erstellt eine Kopie des Miningmodells.<br /><br /> Die Datendomäne für diesen Abfragetyp besteht aus dem Data Mining-Modell.<br /><br /> [SELECT INTO &#40; DMX &#41;](../dmx/select-into-dmx.md)|  
  
 [Zurück zu Select-Typen](#Select_Types)  
  
###  <a name="Drillthrough"></a>Drillthrough  
 Mit folgenden Abfragetypen können Sie die Fälle oder eine Darstellung der Fälle durchsuchen, die dazu verwendet wurden, das Modell zu trainieren.  
  
|Abfragetyp|Description|  
|----------------|-----------------|  
|SELECT FROM  *\<Modell >*. FÄLLE|Gibt die Fälle zurück, die zum Trainieren des Miningmodells verwendet werden.<br /><br /> Die Datendomäne für diesen Abfragetyp besteht aus dem Data Mining-Modell.<br /><br /> [SELECT FROM &#60; Modell &#62;. Fällen &#40; DMX &#41;](../dmx/select-from-model-cases-dmx.md)<br /><br /> [Erstellen von Drillthroughabfragen mit der DMX](../analysis-services/data-mining/create-drillthrough-queries-using-dmx.md)|  
|SELECT FROM  *\<Modell >*. SAMPLE_CASES|Gibt einen Beispielfall zurück, der repräsentativ für die Fälle ist, die zum Trainieren des Miningmodells verwendet werden.<br /><br /> Die Datendomäne für diesen Abfragetyp besteht aus dem Data Mining-Modell.<br /><br /> [SELECT FROM &#60; Modell &#62;. SAMPLE_CASES &#40; DMX &#41;](../dmx/select-from-model-sample-cases-dmx.md)|  
|SELECT FROM  *\<Struktur >*. FÄLLE|Gibt die detaillierten Datenzeilen aus der zugrunde liegenden Miningstruktur zurück, auch wenn einige Details nicht zum Trainieren des Miningmodells verwendet wurden.<br /><br /> [SELECT FROM &#60; Struktur &#62;. FÄLLE](../dmx/select-from-structure-cases.md)<br /><br /> [Drillthroughabfragen &#40; Datamining &#41;](../analysis-services/data-mining/drillthrough-queries-data-mining.md)|  
  
 [Zurück zu Select-Typen](#Select_Types)  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Referenz](../dmx/data-mining-extensions-dmx-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Syntaxkonventionen](../dmx/data-mining-extensions-dmx-syntax-conventions.md)  
  
  
