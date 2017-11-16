---
title: Entwickeln mit XMLA in Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XML for Analysis, data mining
- commands [XML for Analysis]
- data mining [XML for Analysis]
- XMLA, data mining
- XML for Analysis, Analysis Services tasks
- XMLA, Analysis Services tasks
ms.assetid: 54445ee7-720c-4683-99a6-e75b3dcca904
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e66b7b47c25412bf52fe296461c4993d2a533632
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="developing-with-xmla-in-analysis-services"></a>Entwickeln mit XMLA in Analysis Services
  XML for Analysis (XMLA) ist ein SOAP-basiertes (Simple Object Access Protocol) XML-Protokoll, das speziell auf den universellen Datenzugriff für jede standardmäßige, mehrdimensionale Datenquelle ausgerichtet ist, auf die mit einer HTTP-Verbindung zugegriffen werden kann. Beim Kommunizieren mit Clientanwendungen wird XMLA als einziges Protokoll von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwendet. Im Grunde formulieren alle von Analysis Services unterstützten Clientbibliotheken Anforderungen und Antworten in XMLA.  
  
 Als Entwickler können Sie eine Clientanwendung mithilfe von XMLA in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] integrieren, und zwar ohne Abhängigkeiten von .NET Framework oder COM-Schnittstellen. Anwendungsanforderungen, die das Hosten auf vielen Plattformen einschließen, können mit XMLA und einer HTTP-Verbindung zu [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erfüllt werden.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erfüllt vollständig die 1.1-Spezifikation von XMLA, aber erweitert sie auch, um Datendefinition, Datenbearbeitung und Datensteuerelementunterstützung zu ermöglichen. Analysis Services-Erweiterungen werden als Analysis Services Scripting Language (ASSL) bezeichnet. Die gemeinsame Verwendung von XMLA und ASSL ermöglicht einen größeren Satz an Funktionalitäten und bietet damit mehr Möglichkeiten als XMLA. Weitere Informationen über ASSL finden Sie unter [Entwickeln mit Analysis Services Scripting Language &#40; ASSL &#41; ](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Verwalten von Verbindungen und Sitzungen &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)|Beschreibt, wie eine Verbindung mit einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz hergestellt wird und wie Sitzungen und Statusbehaftung in XMLA verwaltet werden.|  
|[Behandeln von Fehlern und Warnungen &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/handling-errors-and-warnings-xmla.md)|Beschreibt, wie [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Fehler und Warninformationen für Methoden und Befehle in XMLA zurückgibt.|  
|[Definieren und Identifizieren von Objekten &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)|Beschreibt Objektbezeichner und Objektverweise und erläutert, wie Bezeichner und Verweise innerhalb von XMLA-Befehlen verwendet werden.|  
|[Verwalten von Transaktionen &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-transactions-xmla.md)|Erläutert, wie die [BeginTransaction](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [CommitTransaction](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), und [RollbackTransaction](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md) Befehle aus, um explizit zu definieren und verwalten eine Transaktion für die aktuelle XMLA Sitzung.|  
|[Abbrechen von Befehlen &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/canceling-commands-xmla.md)|Beschreibt, wie die ["Abbrechen"](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)Befehl aus, um Befehle, Sitzungen und Verbindungen in XMLA abzubrechen.|  
|[Ausführen von Batchvorgängen &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)|Beschreibt, wie die [Batch](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) Befehl aus, um mehrere XMLA führen Befehle seriell oder parallel, entweder innerhalb derselben Transaktion oder als separate Transaktionen, die mit einer einzigen XMLA- [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) Methode.|  
|[Erstellen und Ändern von Objekten &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/creating-and-altering-objects-xmla.md)|Beschreibt, wie die [erstellen](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md), [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), und [löschen](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md) Befehle zusammen mit Analysis Services Scripting Language (ASSL)-Elemente zum definieren, ändern oder entfernen Objekte aus einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz.|  
|[Sperren und entsperren Datenbanken &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/locking-and-unlocking-databases-xmla.md)|Erläutert, wie die [Sperre](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) und [Unlock](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md) Befehle zum Sperren und Entsperren einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank.|  
|[Verarbeitung von Objekten &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md)|Beschreibt, wie die [Prozess](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) Befehl Prozess ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Objekt.|  
|[Zusammenführen von Partitionen &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md)|Beschreibt, wie die [MergePartitions](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md) Befehl zum Zusammenführen von Partitionen auf einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz.|  
|[Entwerfen von Aggregationen &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/designing-aggregations-xmla.md)|Beschreibt, wie die [DesignAggregations](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md) -Befehl entweder im iterativen oder im Batchmodus verwendet, um Aggregationen zu entwerfen für einen Aggregationsentwurf in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Sichern, Wiederherstellen und Synchronisieren von Datenbanken &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)|Beschreibt, wie die [Backup](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) und [wiederherstellen](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) Befehle zum Sichern und Wiederherstellen einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank aus einer Sicherungsdatei.<br /><br /> Außerdem beschreibt, wie die [Synchronize](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) Befehls zum Synchronisieren einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenbank mit einer vorhandenen Datenbank auf derselben Instanz oder auf einer anderen Instanz.|  
|[Einfügen, aktualisieren und Löschen von Elementen &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)|Beschreibt, wie die [einfügen](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [Update](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), und [löschen](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) Befehle hinzufügen, ändern oder Löschen von Elementen aus einer Dimension mit aktiviertem Schreibzugriff.|  
|[Aktualisieren von Zellen &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)|Beschreibt, wie die [UpdateCells](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md) Befehl aus, um die Werte der Zellen in einer Partition mit aktiviertem Schreibzugriff zu ändern.|  
|[Verwalten von Caches &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-caches-xmla.md)|Erläutert, wie die [ClearCache](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md) Befehl zum Löschen des Caches [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Objekte.|  
|[Überwachen von Ablaufverfolgungen &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/monitoring-traces-xmla.md)|Beschreibt, wie die [abonnieren](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md) Befehl abonnieren und Überwachen eine vorhandene Ablaufverfolgung auf einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz.|  
  
## <a name="data-mining-with-xmla"></a>Data Mining mit XMLA  
 XML for Analysis bietet vollständige Unterstützung für Data Mining-Schemarowsets. Diese Rowsets finden Sie Informationen zum Abfragen von Datamining-Modelle, die mithilfe der [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) Methode. Weitere Informationen zu Datamining-Schemarowsets finden Sie unter [Data Mining-Schemarowsets](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
 Weitere Informationen zu DMX finden Sie unter [Data Mining-Erweiterungen &#40; DMX &#41; Verweis](../../dmx/data-mining-extensions-dmx-reference.md).  
  
## <a name="namespace-and-schema"></a>Namespace und Schema  
  
### <a name="namespace"></a>Namespace  
 In dieser Spezifikation definierte Schema verwendet den XML-Namespace `http://schemas.microsoft.com/AnalysisServices/2003/Engine` und die standardabkürzung "DDL".  
  
### <a name="schema"></a>Schema  
 Die Definition eines XSD-Schemas (XML Schema Definition) für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Objektdefinitionssprache basiert auf der Definition der Schemaelemente und Hierarchie in diesem Abschnitt.  
  
## <a name="extensibility"></a>Erweiterbarkeit  
 Erweiterbarkeit der das Schema der objektdefinitionssprache wird bereitgestellt, von der ein **Anmerkung** Element, das auf alle Objekte enthalten ist. Dieses Element kann gemäß den folgenden Regeln jeglichen gültigen XML-Code aus jedem XML-Namespace (außer dem Zielnamespace, der den DDL definiert) enthalten:  
  
-   XML kann nur Elemente enthalten.  
  
-   Jedes Element muss einen eindeutigen Namen haben. Es wird empfohlen, den Wert der **Namen** auf den Zielnamespace verweist.  
  
 Diese Regeln werden auferlegt, damit der Inhalt von der **Anmerkung** Tag als eine Reihe von Name/Wert-Paaren über Decision Support Objects (DSO) 9.0 verfügbar gemacht werden kann.  
  
 Kommentare und Leerzeichen innerhalb der **Anmerkung** Tag, die nicht mit einem untergeordneten Element eingeschlossen sind möglicherweise nicht beibehalten. Darüber hinaus müssen alle Elemente Lese-/ Schreibzugriff sein; Schreibgeschützte Elemente werden ignoriert.  
  
 Das Schema der Objektdefinitionssprache ist insofern geschlossen, dass der Server nicht zulässt, dass abgeleitete Typen durch im Schema definierte Elemente ersetzt werden. Daher akzeptiert der Server nur die hier definierte Gruppe an Elementen und keine anderen Elemente oder Attribute. Unbekannte Elemente bewirken, dass das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Modul einen Fehler auslöst.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln mit Analysis Services Scripting Language &#40; ASSL &#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Grundlegendes zur Microsoft OLAP-Architektur](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  

