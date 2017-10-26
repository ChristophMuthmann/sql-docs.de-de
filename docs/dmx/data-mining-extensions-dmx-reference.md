---
title: Data Mining-Erweiterungen (DMX)-Referenz | Microsoft Docs
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
- DMX [Analysis Services]
- statements [DMX]
- Data Mining Extensions [Analysis Services], statements
- DMX [Analysis Services], about Data Mining Extensions
- DMX [Analysis Services], statements
- data definition statements [DMX]
- predictions [DMX]
- Data Mining Extensions [Analysis Services]
- SSAS, DMX
- queries [DMX], extensions reference
- SQL Server Analysis Services, DMX
- OLE DB for Data Mining
- data manipulation statements [DMX]
- Data Mining Extensions [Analysis Services], about Data Mining Extensions
- mining models [Analysis Services], DMX
ms.assetid: 6d85ca20-de67-4e20-b3b5-b734c6cfcece
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4f3c7af23a8013d8c194557bfefaab8a2d4019f4
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="data-mining-extensions-dmx-reference"></a>Data Mining-Erweiterungen (DMX) - Referenz
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Data Mining Extensions (DMX) ist eine Programmiersprache, die Sie verwenden können, erstellen und Arbeiten mit Datamining-Modellen in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Mit DMX können Sie die Struktur neuer Data Mining-Modelle erstellen, diese Modelle trainieren sowie die Modelle durchsuchen, verwalten und für Vorhersagen verwenden. DMX besteht aus DDL-Anweisungen (Data Definition Language, Datendefinitionssprache), DML-Anweisungen (Data Manipulation Language, Datenbearbeitungssprache) sowie aus Funktionen und Operatoren.  
  
## <a name="microsoft-ole-db-for-data-mining-specification"></a>Spezifikation von Microsoft OLE DB für Data Mining  
 Die Datamining-Funktionen in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] werden erstellt, um die Einhaltung der [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB für Data Mining-Spezifikation.  
  
 Die [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB für Data Mining-Spezifikation definiert die folgenden:  
  
-   Eine Struktur, die die Informationen aufnimmt, die ein Data Mining-Modell definieren  
  
-   Eine Sprache zum Erstellen und Verwenden von Data Mining-Modellen  
  
 Die Spezifikation definiert die Basis von Data Mining als das virtuelle Data Mining-Modellobjekt. Das Data Mining-Modellobjekt kapselt alle Informationen, die zu einem bestimmten Miningmodell bekannt sind. Das Data Mining-Modellobjekt ist wie eine SQL-Tabelle strukturiert, mit Spalten, Datentypen und Metainformationen, die das Modell beschreiben. Diese Struktur ermöglicht es Ihnen, mit der Sprache DMX, die eine Erweiterung von SQL ist, Modelle zu erstellen und zu verwenden.  
  
 **Weitere Informationen:** [Mining-Strukturen &#40; Analysis Services – Datamining &#41;](../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
##  <a name="BKMK_DMXStatements"></a>DMX-Anweisungen  
 Mit den DMX-Anweisungen können Sie Data Mining-Modelle erstellen, verarbeiten, kopieren, durchsuchen und für Vorhersagen verwenden. Es gibt zwei Arten von Anweisungen in DMX: Datendefinitionsanweisungen und Datenbearbeitungsanweisungen. Sie können jede Art von Anweisung zum Ausführen unterschiedlicher Arten von Aufgaben verwenden.  
  
 In den folgenden Abschnitten finden Sie weitere Informationen zum Verwenden von DMX-Anweisungen:  
  
-   [Datendefinitionsanweisungen](#BKMK_DDL)  
  
-   [Datenbearbeitungsanweisungen](#BKMK_DML)  
  
-   [Grundlegendes zu Abfragen](#BKMK_Queries)  
  
###  <a name="BKMK_DDL"></a>Datendefinitionsanweisungen  
 Datendefinitionsanweisungen verwenden Sie in DMX dazu, neue Miningstrukturen und -modelle zu erstellen und zu definieren, Miningmodelle und Miningstrukturen zu importieren und zu exportieren sowie vorhandene Modelle aus einer Datenbank zu löschen. Datendefinitionsanweisungen in DMX sind Teil der Datendefinitionssprache (Data Definition Language, DDL).  
  
 Mit den Datendefinitionsanweisungen in DMX können Sie folgende Aufgaben ausführen:  
  
-   Erstellen Sie eine Miningstruktur mithilfe der [CREATE MINING STRUCTURE](../dmx/create-mining-structure-dmx.md) -Anweisung und der Miningstruktur ein Miningmodell hinzufügen, mit der [ALTER MINING STRUCTURE](../dmx/alter-mining-structure-dmx.md) Anweisung.  
  
-   Erstellen eines Miningmodells und der zugeordneten Miningstruktur gleichzeitig mithilfe der [CREATE MINING MODEL](../dmx/create-mining-model-dmx.md) Anweisung, um ein leeres Datamining-Modellobjekt zu erstellen.  
  
-   Exportieren eines Miningmodells und der zugeordneten Miningstruktur in eine Datei mithilfe der [EXPORTIEREN](../dmx/export-dmx.md) Anweisung. Importieren eines Miningmodells und der zugeordneten Miningstruktur aus einer Datei, die durch die EXPORT-Anweisung, mithilfe erstellt wird der [IMPORT](../dmx/import-dmx.md) Anweisung.  
  
-   Kopieren Sie die Struktur eines vorhandenen Miningmodells in ein neues Modell und Trainieren mit denselben Daten mithilfe der [SELECT INTO](../dmx/select-into-dmx.md) Anweisung.  
  
-   Vollständiges Entfernen ein Miningmodells aus einer Datenbank mit der [DROP MINING MODEL](../dmx/drop-mining-model-dmx.md) Anweisung. Vollständiges Entfernen einer Miningstruktur und alle ihr zugeordneten Miningmodelle aus der Datenbank mit der [DROP MINING STRUCTURE](../dmx/drop-mining-structure-dmx.md) Anweisung.  
  
 Weitere Informationen zu den Datamining-Tasks, die Sie ausführen können, mithilfe von DMX-Anweisungen finden Sie unter [Data Mining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md).  
  
 [Zurück zu den DMX-Anweisungen](#BKMK_DMXStatements)  
  
###  <a name="BKMK_DML"></a>Datenbearbeitungsanweisungen  
 Mit den Datenbearbeitungsanweisungen in DMX können Sie vorhandene Miningmodelle verwenden, die Modelle durchsuchen sowie Vorhersagen aus ihnen erstellen. Datenbearbeitungsanweisungen in DMX sind Teil der Datenbearbeitungssprache (Data Manipulation Language, DML).  
  
 Mit den Datenbearbeitungsanweisungen in DMX können Sie folgende Aufgaben ausführen:  
  
-   Trainieren ein Miningmodells mit der [INSERT INTO](../dmx/insert-into-dmx.md) Anweisung. Diese Anweisung fügt nicht die tatsächlichen Quelldaten in ein Data Mining-Modellobjekt ein, sondern erstellt eine Abstraktion, die das Miningmodell beschreibt, das der Algorithmus erstellt. Die Quellabfrage für eine INSERT INTO-Anweisung ist in der beschriebenen [ \<quelldatenabfrage >](../dmx/source-data-query.md).  
  
-   Erweitern Sie die SELECT-Anweisung um die Informationen zu suchen, die während des modelltrainings berechnet und in der Datamining-Modell, z. B. Statistiken der Quelldaten gespeichert wird. Im folgenden sind die Klauseln, die Sie einschließen können, um die Leistungsfähigkeit der SELECT-Anweisung zu erweitern:  
  
    -   [SELECT DISTINCT FROM &#60; Modell &#62; &#40; DMX &#41;](../dmx/select-distinct-from-model-dmx.md)  
  
    -   [SELECT FROM &#60; Modell &#62;. Inhalt &#40; DMX &#41;](../dmx/select-from-model-content-dmx.md)  
  
    -   [SELECT FROM &#60; Modell &#62;. Fällen &#40; DMX &#41;](../dmx/select-from-model-cases-dmx.md)  
  
    -   [SELECT FROM &#60; Modell &#62;. SAMPLE_CASES &#40; DMX &#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
    -   [SELECT FROM &#60; Modell &#62;. DIMENSION_CONTENT &#40; DMX &#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
-   Erstellen von Vorhersagen, die auf einem vorhandenen Miningmodell basieren, mit der [PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) -Klausel der SELECT-Anweisung. Die Quellabfrage für eine PREDICTION JOIN-Anweisung ist in der beschriebenen [ \<quelldatenabfrage >](../dmx/source-data-query.md).  
  
-   Entfernen aller trainierten Daten aus einem Modell oder eine Struktur mit den [DELETE &#40; DMX &#41;](../dmx/delete-dmx.md) Anweisung.  
  
 Weitere Informationen zu den Datamining-Tasks, die Sie ausführen können, mithilfe von DMX-Anweisungen finden Sie unter [Data Mining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md).  
  
 [Zurück zu den DMX-Anweisungen](#BKMK_DMXStatements)  
  
###  <a name="BKMK_Queries"></a>Grundlegendes zu DMX-Abfragen  
 Die SELECT-Anweisung bildet die Grundlage für die meisten DMX-Abfragen. Abhängig von den Klauseln, die Sie in der jeweiligen Anweisung verwenden, können Sie Miningmodelle durchsuchen, kopieren oder für Vorhersagen verwenden. Die Vorhersageabfrage verwendet eine Form der Option zum Erstellen von Vorhersagen auf Grundlage vorhandener Miningmodelle erstellen. Funktionen erweitern Ihre Möglichkeiten zum Durchsuchen und Abfragen von Miningmodellen über die systeminternen Möglichkeiten des Data Mining-Modells hinaus.  
  
 Mit DMX-Funktionen können Sie Informationen abrufen, die während des Trainings eines Modells ermittelt wurden, sowie neue Informationen berechnen. Sie können diese Funktionen für viele Zwecke verwenden, so z. B. zum Zurückgeben von Statistiken, die die zugrunde liegenden Daten oder die Genauigkeit einer Vorhersage beschreiben, oder zum Zurückgeben einer erweiterten Erläuterung einer Vorhersage.  
  
 **Weitere****Informationen:** [Verständnis der DMX Select-Anweisung](../dmx/understanding-the-dmx-select-statement.md), [allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md), [Struktur und die Verwendung von DMX-Vorhersageabfragen](../dmx/structure-and-usage-of-dmx-prediction-queries.md), [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz  ](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
 [Zurück zu den DMX-Anweisungen](#BKMK_DMXStatements)  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Funktionsreferenz](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Syntaxkonventionen](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Syntaxelemente](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Allgemeine Vorhersagefunktionen &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struktur und die Verwendung von DMX-Vorhersageabfragen](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Grundlegendes zur Select-Anweisung von DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  

