---
title: "AMO-Klassen für Datamining | Microsoft Docs"
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data mining [AMO]
- AMO, data mining
- Analysis Management Objects, data mining
ms.assetid: e4108825-b722-417c-9647-ab30ce35e549
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a1a5ca970ee22d91b06a945e8a3b600b74892790
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="amo-data-mining-classes"></a>AMO-Klassen für Data Mining
  Mithilfe von Data Mining-Klassen können Sie Data Mining-Objekte erstellen, ändern, löschen und verarbeiten. Das Arbeiten mit Data Mining-Objekten umfasst die Erstellung von Data Mining-Strukturen, die Erstellung von Data Mining-Modellen und die Verarbeitung der Modelle.  
  
 Weitere Informationen zum Einrichten der Umgebung, und ca. <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource>, und <xref:Microsoft.AnalysisServices.DataSourceView> anzuzeigen, [grundlegende AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md).  
  
 Für die Definition von Objekten in Analysis Management Objects (AMO) müssen für jedes Objekt einige Eigenschaften festgelegt werden, um den richtigen Kontext einzurichten. Komplexe Objekte wie OLAP und Data Mining-Objekte erfordern längere und detaillierte Codierung.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [MiningStructure-Objekte](#MiningStructure)  
  
-   [MiningModel-Objekte](#MiningModel)  
  
 Die folgende Abbildung zeigt die Beziehung der in diesem Thema erläuterten Klassen.  
  
 ![AMO-Data Mining-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-dataminingclasses.gif "AMO-Data Mining-Klassen")  
  
##  <a name="MiningStructure">MiningStructure-Objekte</a>  
 Eine Miningstruktur ist der Container für Miningmodelle. Die Struktur definiert alle möglichen Spalten, die von den Miningmodellen verwendet werden können. Jedes Miningmodell definiert seine eigenen Spalten aus dem Satz der definierten Spalten in der Struktur.  
  
 Ein einfaches <xref:Microsoft.AnalysisServices.MiningStructure>-Objekt besteht aus: grundlegenden Informationen, einer Datenquellensicht, mindestens einer <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>, null oder mehr <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> und einer <xref:Microsoft.AnalysisServices.MiningModelCollection>.  
  
 Grundlegende Informationen beinhalten den Namen und die ID (interner Bezeichner) des <xref:Microsoft.AnalysisServices.MiningStructure>-Objekts.  
  
 Das <xref:Microsoft.AnalysisServices.DataSourceView>-Objekt enthält das zugrundeliegende Datenmodell für die Miningstruktur.  
  
 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> sind Spalten oder Attribute, die einzelne Werte besitzen.  
  
 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> sind Spalten oder Attribute, die mehrere Werte für jeden Fall besitzen.  
  
 <xref:Microsoft.AnalysisServices.MiningModelCollection> Enthält alle Miningmodelle, die mit den gleichen Daten erstellt wurden.  
  
 Ein <xref:Microsoft.AnalysisServices.MiningStructure>-Objekt wird erstellt, indem es der <xref:Microsoft.AnalysisServices.MiningStructureCollection> der Datenbank hinzugefügt und das <xref:Microsoft.AnalysisServices.MiningStructure>-Objekt mithilfe der Update-Methode auf dem Server aktualisiert wird.  
  
 Um ein <xref:Microsoft.AnalysisServices.MiningStructure>-Objekt zu entfernen, muss es mithilfe der Drop-Methode des <xref:Microsoft.AnalysisServices.MiningStructure>-Objekts gelöscht werden. Wenn ein <xref:Microsoft.AnalysisServices.MiningStructure>-Objekt aus der Auflistung entfernt wird, wirkt sich dies nicht auf den Server aus.  
  
 Die <xref:Microsoft.AnalysisServices.MiningStructure> kann mithilfe ihrer eigenen Verarbeitungsmethode verarbeitet werden oder wenn sich ein übergeordnetes Objekt selbst mit seiner eigenen Verarbeitungsmethode verarbeitet.  
  
### <a name="columns"></a>Spalten  
 Spalten enthalten die Daten für das Modell und können in Abhängigkeit von der Verwendung von unterschiedlichen Typen sein: Key, Input, Predictable oder InputPredictable. Predictable-Spalten sind das Ziel bei der Erstellung des Miningmodells.  
  
 Einzelwertspalten werden in AMO als <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> bezeichnet. Spalten mit mehreren Werten werden als <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> bezeichnet.  
  
#### <a name="scalarminingstructurecolumn"></a>ScalarMiningStructureColumn  
 Ein einfaches <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>-Objekt besteht aus: grundlegenden Informationen, Typ, Inhalt und Datenbindung.  
  
 Grundlegende Informationen beinhalten den Namen und die ID (interner Bezeichner) der <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
 "Typ" bezeichnet den Datentyp des Werts: LONG, BOOLEAN, TEXT, DOUBLE, DATE.  
  
 "Inhalt" informiert das Modul, wie die Spalte modelliert werden kann. Folgende Werte sind möglich: Discrete, Continuous, Discretized, Ordered, Cyclical, Probability, Variance, StdDev, ProbabilityVariance, ProbabilityStdDev, Support und Key.  
  
 Die Datenbindung verknüpft die Data Mining-Spalte mithilfe des Datenquellensicht-Elements mit dem zugrundeliegenden Datenmodell.  
  
 Eine <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> wird erstellt, indem sie dem übergeordneten <xref:Microsoft.AnalysisServices.MiningStructureCollection> hinzugefügt und das übergeordnete <xref:Microsoft.AnalysisServices.MiningStructure>-Objekt mithilfe der Update-Methode auf dem Server aktualisiert wird.  
  
 So entfernen Sie eine <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>, müssen Sie aus der Auflistung des übergeordneten Elements entfernt werden <xref:Microsoft.AnalysisServices.MiningStructure>, und das übergeordnete Element <xref:Microsoft.AnalysisServices.MiningStructure> Objekt muss mit dem Server mithilfe der Update-Methode aktualisiert werden.  
  
#### <a name="tableminingstructurecolumn"></a>TableMiningStructureColumn  
 Ein einfaches <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>-Objekt besteht aus: grundlegenden Informationen und skalaren Spalten.  
  
 Grundlegende Informationen beinhalten den Namen und die ID (interner Bezeichner) der <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>.  
  
 Skalare Spalten sind <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
 Eine <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> wird erstellt, indem sie der übergeordneten <xref:Microsoft.AnalysisServices.MiningStructure>-Auflistung hinzugefügt und das übergeordnete <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>-Objekt mithilfe der Update-Methode auf dem Server aktualisiert wird.  
  
 Um eine <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> zu entfernen, muss sie aus der Auflistung des übergeordneten <xref:Microsoft.AnalysisServices.MiningStructure> entfernt werden, und das übergeordnete <xref:Microsoft.AnalysisServices.MiningStructure>-Objekt muss mithilfe der Update-Methode auf dem Server aktualisiert werden.  
  
##  <a name="MiningModel">MiningModel-Objekte</a>  
 Ein <xref:Microsoft.AnalysisServices.MiningModel> ist das Objekt, das Ihnen ermöglicht auszuwählen, welche Spalten aus der Struktur verwendet werden sollen und welcher Algorithmus verwendet werden soll, zudem bietet es optionale spezifische Parameter zur Optimierung des Modells. Beispielsweise können mehrere Miningmodelle in der gleichen Miningstruktur definiert werden, die den gleichen Algorithmus verwendet. Es sollen in einem Modell jedoch einige Spalten aus der Miningstruktur ignoriert und diese als Eingabe in einem anderen Modell und als Eingabe und Vorhersage in einem dritten Modell verwendet werden. Dies kann sinnvoll sein, wenn Sie eine Spalte in einem Miningmodell als kontinuierlich, in einem anderen Modell jedoch als diskretisiert behandeln möchten.  
  
 Ein einfaches <xref:Microsoft.AnalysisServices.MiningModel>-Objekt besteht aus: grundlegenden Informationen, Algorithmusdefinition und Spalten.  
  
 Grundlegende Informationen beinhalten den Namen und die ID (interner Bezeichner) des Miningmodells.  
  
 Eine Algorithmusdefinition bezieht sich auf alle in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] bereitgestellten Standardalgorithmen oder alle auf dem Server bereitgestellten benutzerdefinierten Algorithmen.  
  
 "Spalten" ist eine Auflistung der Spalten, die vom Algorithmus und seinen Verwendungsdefinitionen verwendet werden.  
  
 Ein <xref:Microsoft.AnalysisServices.MiningModel> wird erstellt, indem es der <xref:Microsoft.AnalysisServices.MiningModelCollection> der Datenbank hinzugefügt und das <xref:Microsoft.AnalysisServices.MiningModel>-Objekt mithilfe der Update-Methode auf dem Server aktualisiert wird.  
  
 Um ein <xref:Microsoft.AnalysisServices.MiningModel> zu entfernen, muss es mithilfe der Drop-Methode des <xref:Microsoft.AnalysisServices.MiningModel> gelöscht werden. Wenn ein <xref:Microsoft.AnalysisServices.MiningModel> aus der Auflistung entfernt wird, wirkt sich dies nicht auf den Server aus.  
  
 Nach der Erstellung kann das <xref:Microsoft.AnalysisServices.MiningModel> mithilfe seiner eigenen Verarbeitungsmethode verarbeitet werden oder wenn sich ein übergeordnetes Objekt selbst mit seiner eigenen Verarbeitungsmethode verarbeitet.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices>   
 [Grundlegende AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)   
 [Programmieren AMO-Datamining-Objekte](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-data-mining-objects.md)   
 [Einführung in AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Logische Architektur &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Datenbankobjekte &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
