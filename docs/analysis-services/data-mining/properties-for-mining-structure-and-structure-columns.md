---
title: "Eigenschaften für Miningstrukturen und Strukturspalten | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], column properties
- data mining [Analysis Services], properties
- columns [data mining], properties
- properties [data mining]
ms.assetid: ce90f684-bb8c-4eca-b9e6-000794dbee16
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4b342f6466a757ce2705d97680ed0e0460c0031f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="properties-for-mining-structure-and-structure-columns"></a>Eigenschaften für Miningstrukturen und Strukturspalten
  Sie können mithilfe der Registerkarte **Miningstruktur** des Data Mining-Designers die Eigenschaften für eine Miningstruktur und für die verbundenen Spalten und geschachtelten Tabellen festlegen oder ändern. Eigenschaften, die Sie auf dieser Registerkarte festlegen, werden an alle Miningmodelle weitergegeben, die mit der Struktur verbunden sind.  
  
> [!NOTE]  
>  Wenn Sie den Wert einer beliebigen Eigenschaft in der Miningstruktur ändern, darunter auch Metadaten wie Name oder Beschreibung, müssen die Miningstruktur und zugehörige Modelle neu verarbeitet werden, bevor Sie das Modell anzeigen oder abfragen können.  
  
## <a name="properties-of-mining-structures-and-mining-structure-columns"></a>Eigenschaften von Miningstrukturen und Miningstrukturspalten  
 In der folgenden Tabelle werden die Eigenschaften der für Data Mining spezifischen Miningstruktur und Miningstrukturspalten beschrieben. Diese können auf der Registerkarte **Miningstruktur** angezeigt oder konfiguriert werden. Klicken Sie mit der rechten Maustaste auf ein Element in der Strukturansicht, und klicken Sie anschließend auf **Eigenschaften**, um diese Eigenschaften anzuzeigen oder zu konfigurieren.  
  
-   Klicken Sie auf die Überschrift der Miningstruktur, um die Eigenschaften der Struktur anzuzeigen.  
  
-   Um die Eigenschaften einer Spalte oder einer geschachtelten Tabelle anzuzeigen, klicken Sie auf den Spaltenname.  
  
### <a name="properties-of-the-mining-structure"></a>Eigenschaften der Miningstruktur  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**CacheMode**|Gibt an, ob die beim Trainieren verwendeten Fälle nach Abschluss des Trainings zwischengespeichert oder verworfen werden sollen. **Hinweis:**  Dieses Attribut muss auf **KeepTrainingCases** festgelegt werden, um Drillthroughs und zurückgehaltene Daten zu ermöglichen.|  
|**Sortierung**|Gibt die Standardsortierung für die Spalte an. Wird keine Sortierung angegeben, wird die Sortierung des Servers verwendet.|  
|**Description**|Beschreibt die Miningstruktur. Die Beschreibung sollte den Zweck und die Zusammensetzung der Daten in der Struktur beinhalten.|  
|**ErrorConfiguration (Standard)**|Legt Optionen für die spezielle Behandlung möglicher Fehler fest.|  
|**HoldoutMaxCases**|Gibt die maximale Anzahl von Strukturfällen an, die als Testdataset reserviert werden können.  Werden Werte sowohl für **HoldoutMaxCases** als auch für **HoldoutPercent**angegeben, werden die Bedingungen miteinander kombiniert. **Hinweis:**  Zum Festlegen dieser Eigenschaft muss <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> auf **KeepTrainingCases**, um diese Eigenschaften anzuzeigen oder zu konfigurieren.|  
|**HoldoutPercent**|Gibt die Prozentzahl der Strukturfälle an, die als Testdataset reserviert werden sollen. Werden Werte sowohl für **HoldoutMaxCases** als auch für **HoldoutPercent**angegeben, werden die Bedingungen miteinander kombiniert. **Hinweis:**  Zum Festlegen dieser Eigenschaft muss <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> auf **KeepTrainingCases**, um diese Eigenschaften anzuzeigen oder zu konfigurieren.|  
|**HoldoutSeed**|Gibt einen Ausgangswert zum Initialisieren der Partitionierung des Zurückhaltungstestdatasets an, um sicherzustellen, dass das Dataset erneut erstellt werden kann. **Hinweis:**  Zum Festlegen dieser Eigenschaft muss <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> auf **KeepTrainingCases**, um diese Eigenschaften anzuzeigen oder zu konfigurieren.|  
|**ID**|Zeigt den eindeutigen Bezeichner der Miningstruktur an.<br /><br /> Der Name, den Sie der Miningstruktur bei deren Erstellung zugewiesen haben, wird als ID verwendet. Wenn Sie den Namen später ändern, indem Sie einen neuen Wert für die **Name** -Eigenschaft eingeben, wird der neue Name nur als Alias verwendet. Die ID wird nicht geändert.|  
|**Sprache**|Gibt die Sprache für die Beschriftungen in der Miningstruktur an.|  
|**Name**|Gibt den Namen oder Alias der Miningstruktur an.<br /><br /> Wenn Sie den Wert für die Name-Eigenschaft ändern, wird der neue Name nur als Beschriftung oder Alias verwendet. Der Bezeichner für die Miningstruktur wird nicht geändert.|  
|**Quelle**|Zeigt den Namen und den Typ der Datenquelle an.|  
  
### <a name="properties-of-the-mining-structure-columns"></a>Eigenschaften der Miningstrukturspalten  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**ClassifiedColumns**|Identifiziert die Spalte, die eine klassifizierte Spalte beschreibt.|  
|**Inhalt**|Der Inhaltstyp der Spalte.|  
|**Description**|Beschreibt die Spalte. Die Beschreibung der Spalte sollte Informationen darüber enthalten, wie die Daten in der Spalte für Data Mining abgeleitet oder bearbeitet wurden.|  
|**DiscretizationBucketCount**|Zeigt die Anzahl der Buckets in der diskretisierten Spalte an.<br /><br /> Nur verfügbar, wenn der Inhaltstyp auf **Discretized**festgelegt ist.<br /><br /> Diese Eigenschaft ist schreibgeschützt.|  
|**DiscretizationMethod**|Zeigt die Methode an, die zur Diskretisierung der Spalte verwendet wurde.<br /><br /> Nur verfügbar, wenn der Inhaltstyp auf **Discretized**festgelegt ist.<br /><br /> Diese Eigenschaft ist schreibgeschützt.|  
|**Distribution**|Gibt die Verteilung von Inhalten in der Spalte an.|  
|**ID**|Zeigt den Bezeichner der Spalte an.<br /><br /> Der Wert der ID-Eigenschaft wird beim Ändern des Werts der Name-Eigenschaft für die Spalte nicht beeinflusst.|  
|**IsKey**|Gibt an, ob es sich bei der Spalte um eine Schlüsselspalte handelt.|  
|**KeyColumns**|Enthält die Definition einer Spalte, die der Schlüssel oder Teil eines Schlüssels für ein Attribut ist.|  
|**ModelingFlags**|Legt weitere Parameter fest, die vom Algorithmus verfügbar gemacht werden.|  
|**Name**|Name der Spalte.|  
|**NameColumn**|Identifiziert die Spalte, die den Namen des übergeordneten Elements bereitstellt.|  
|**Quelle**|Zeigt die Quelle der Spalte an.<br /><br /> Für relationale Datenquellen ist der Wert immer **(none)**.<br /><br /> Bei auf einem OLAP-Cube basierenden Strukturen entspricht der Wert der MDX-Anweisung, die den Slice definiert, der als Quelle für die geschachtelte Tabelle verwendet wird.|  
|**SourceMeasureGroup**|Zeigt die Quelle der Measuregruppe an.<br /><br /> Für relationale Datenquellen ist der Wert immer **(none)**.<br /><br /> Bei auf einem OLAP-Cube basierenden Strukturen entspricht der Wert der MDX-Anweisung, die den Slice definiert, der als Quelle für die geschachtelte Tabelle verwendet wird.|  
|**Typ**|Der Datentyp für den Inhalt der Spalte.|  
  
 Weitere Informationen zum Festlegen oder Ändern von Eigenschaften finden Sie unter [Tasks und Anweisungen für Miningstrukturen](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer relationalen Miningstruktur](../../analysis-services/data-mining/create-a-relational-mining-structure.md)   
 [Miningstrukturspalten](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  

