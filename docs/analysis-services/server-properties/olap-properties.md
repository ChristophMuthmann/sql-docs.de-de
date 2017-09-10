---
title: OLAP-Eigenschaften | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- AggregationPerfLog property
- DefaultPageSizeForProp property
- UseSinglePassForDimSecurityAutoExist property
- DeepCompressValue property
- CacheRowsetRows property
- Income property
- AggregationNewAlgo property
- MemoryAdjustFactor property
- DimensionLatencyAccuracy property
- InitialBonus property
- DefaultPageSizeForDataHeader property
- MaxCPUUsage property
- DistinctBuffer property
- PartitionLatencyAccuracy property
- MaxRetries property
- UseDataCacheRegistryMultiplyKey property
- ConvertDeletedToUnknown property
- DatabaseConnectionPoolMax property
- DataFileInitEnabled property
- DefaultPageSizeForHash property
- MaxRolapOrConditions property
- UseDataCacheFreeLastPageMemory property
- OLAP [Analysis Services], properties
- MapHandleAlgorithm property
- IndexBuildEnabled property
- MaxObjectsInParallel property
- IgnoreNullRolapRows property
- DimensionPropertyCacheSize property
- DefaultRefreshInterval property
- CheckDistinctRecordSortOrder property
- BufferMemoryLimit property
- EnableTableGrouping property
- ExpressNonEmptyUseEnabled property
- CopyLinkedDataCacheAndRegistry property
- UseDataSlice property
- MemoryLimitErrorEnabled property
- Enabled property
- EnableRolapOptimization property
- DatabaseConnectionPoolTimeout property
- UseDataCacheRegistryHashTable property
- AggregationsBuildEnabled property
- Tax property
- DatabaseConnectionPoolGeneralTimeout property
- DefaultPageSizeForString property
- DatabaseConnectionPoolConnectTimeout property
- MinimumBalance property
- OptimizeSchema property
- UseCalculationCacheRegistry property
- MaxTableDepth property
- DataSliceInitEnabled property
- PrefetchLowerGranularities property
- UseVBANet property
- BufferRecordLimit property
- DefaultPageSizeForIndexHeader property
- MaximumBalance property
- CalculationCacheRegistryMaxIterations property
- DefaultDrillthroughMaxRows property
- IndexBuildThreshold property
- UseDataCacheRegistry property
- MemoryAdjustConst property
- ApplyIntersect property
- IndexFileInitEnabled property
- CacheRowsetToDisk property
- DataCacheRegistryMaxIterations property
- AllowSEFiltering property
- ForceMultiPass property
- ApplySubtract property
- IndexUseEnabled property
- AggregationsUseEnabled property
- DataPlacementOptimization property
- UseMaterializedIterators property
- CacheRecordLimit property
- ROLAPDimensionProcessingEffort property
- DefaultPageSizeForIndex property
- EnableRolapDimQueryTableGrouping property
- DimensionPropertyKeyCache property
- SleepIntervalSecs property
- DefaultPageSizeForData property
- MapFormatMask property
- CalculationEvaluationPolicy property
- AggregationMemoryLimitMin property
- RecordsReportGranularity property
- MemoryLimit property
- AggregationMemoryLimitMax property
ms.assetid: 06eb0d78-96c0-42ff-b759-f4c794597c8d
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 095706fc60fe06ae2a83969431b390772bee37f2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="olap-properties"></a>OLAP-Eigenschaften
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] unterstützt die in den folgenden Tabellen aufgeführten OLAP-Servereigenschaften. Weitere Informationen zu zusätzlichen Servereigenschaften und zum Festlegen dieser Eigenschaften finden Sie unter [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Gilt für:** Nur mehrdimensionaler Servermodus  
  
## <a name="memory"></a>Speicher  
 **DefaultPageSizeForData**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DefaultPageSizeForDataHeader**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DefaultPageSizeForIndex**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DefaultPageSizeForIndexHeader**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DefaultPageSizeForString**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DefaultPageSizeForHash**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DefaultPageSizeForProp**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
## <a name="lazyprocessing"></a>LazyProcessing  
 **Aktiviert**  
 Eine boolesche Eigenschaft, die angibt, ob die verzögerte Aggregationsverarbeitung aktiviert ist.  
  
 **SleepIntervalSecs**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die das Intervall (in Sekunden) definiert, in dem der Server überprüft, ob Aufträge für eine verzögerte Verarbeitung anstehen.  
  
 **MaxCPUUsage**  
 Eine 64-Bit-Gleitkommazahl mit doppelter Genauigkeit und Vorzeichen, die die maximale CPU-Nutzung für die verzögerte Verarbeitung definiert, ausgedrückt als Prozentsatz. Der Server überwacht die durchschnittliche CPU-Nutzung basierend auf Snapshots. Kurzfristige Überschreitungen dieses Schwellenwerts werden als normales CPU-Verhalten betrachtet.  
  
 Der Standardwert für diese Eigenschaft ist 0,5. Bei dieser Einstellung werden maximal 50 % der CPU für die verzögerte Verarbeitung verwendet.  
  
 **MaxObjectsInParallel**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die die maximale Anzahl von Partitionen angibt, die gleichzeitig verzögert verarbeitet werden können.  
  
 **MaxRetries**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die die Anzahl von Wiederholungen definiert, die bei einem Fehler bei der verzögerten Verarbeitung zulässig sind, bevor ein Fehler ausgelöst wird.  
  
## <a name="processplan"></a>ProcessPlan  
 **CacheRowsetRows**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **CacheRowsetToDisk**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DistinctBuffer**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die die Größe eines für Distinct Count Measures verwendeten internen Puffers definiert. Erhöhen Sie diesen Wert, um die Verarbeitung von Distinct Count Measures zu Lasten der CPU-Nutzung zu beschleunigen.  
  
 **EnableRolapDimQueryTableGrouping**  
 Eine boolesche Eigenschaft, die angibt, ob für ROLAP-Dimensionen die Tabellengruppierung aktiviert ist. Wenn für diese Eigenschaft TRUE festgelegt ist, werden beim Abfragen von ROLAP-Dimensionen zur Laufzeit vollständige ROLAP-Dimensionstabellen auf einmal abgefragt, statt für jedes Attribut eine eigene Abfrage auszuführen.  
  
 **EnableTableGrouping**  
 Eine boolesche Eigenschaft, die angibt, ob die Tabellengruppierung aktiviert ist. Wenn für diese Eigenschaft TRUE festgelegt ist, werden beim Verarbeiten von Dimensionen vollständige Dimensionstabellen auf einmal abgefragt, statt für jedes Attribut eine eigene Abfrage auszuführen.  
  
 **ForceMultiPass**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MaxTableDepth**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MemoryAdjustConst**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MemoryAdjustFactor**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MemoryLimit**  
 Eine 64-Bit-Gleitkommazahl mit doppelter Genauigkeit und Vorzeichen, die die maximale für die Verarbeitung zugeordnete Menge an Arbeitsspeicher definiert, ausgedrückt als Prozentsatz des physischen Arbeitsspeichers.  
  
 Der Standardwert für diese Eigenschaft ist 65. Dies bedeutet, dass 65 % des physischen Arbeitsspeichers für die Cube- und Dimensionsverarbeitung verwendet werden können.  
  
 **MemoryLimitErrorEnabled**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **OptimizeSchema**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
## <a name="proactivecaching"></a>ProactiveCaching  
 **DefaultRefreshInterval**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DimensionLatencyAccuracy**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **PartitionLatencyAccuracy**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
## <a name="process"></a>Verarbeiten  
 **AggregationMemoryLimitMax**  
 Eine 64-Bit-Gleitkommazahl mit doppelter Genauigkeit und Vorzeichen, die die maximale für die Aggregationsverarbeitung zugeordnete Menge an Arbeitsspeicher definiert, ausgedrückt als Prozentsatz des physischen Arbeitsspeichers.  
  
 Der Standardwert für diese Eigenschaft ist 80. Dies bedeutet, dass 80 % des physischen Arbeitsspeichers für die Aggregationsverarbeitung verwendet werden können.  
  
 **AggregationMemoryLimitMin**  
 Eine 64-Bit-Gleitkommazahl mit doppelter Genauigkeit und Vorzeichen, die die minimale für die Aggregationsverarbeitung zugeordnete Menge an Arbeitsspeicher definiert, ausgedrückt als Prozentsatz des physischen Arbeitsspeichers. Mit einem höheren Wert kann die Aggregationsverarbeitung zu Lasten der Speicherauslastung beschleunigt werden.  
  
 Der Standardwert für diese Eigenschaft ist 10. Dies bedeutet, dass mindestens 10 % des physischen Arbeitsspeichers für die Aggregationsverarbeitung verwendet werden.  
  
 **AggregationNewAlgo**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **AggregationPerfLog2**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **AggregationsBuildEnabled**  
 Eine boolesche Eigenschaft, die angibt, ob die Aggregationserstellung aktiviert ist. Hierbei handelt es sich um einen Mechanismus zum Durchführen von Vergleichstests bei der Aggregationserstellung, ohne dass der Aggregationsentwurf geändert werden muss.  
  
 **BufferMemoryLimit**  
 Eine 64-Bit-Gleitkommazahl mit doppelter Genauigkeit und Vorzeichen, die die Arbeitsspeicherbegrenzung für den Verarbeitungspuffer definiert, ausgedrückt als Prozentsatz des physischen Arbeitsspeichers.  
  
 Der Standardwert für diese Eigenschaft ist 60. Dies bedeutet, dass für den Pufferspeicher bis zu 60 % des physischen Arbeitsspeichers verwendet werden können.  
  
 **BufferRecordLimit**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die die Anzahl von Datensätzen definiert, die bei der Verarbeitung gepuffert werden können.  
  
 Der Standardwert dieser Eigenschaft beträgt 1048576 Datensätze.  
  
 **CacheRecordLimit**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **CheckDistinctRecordSortOrder**  
 Eine boolesche Eigenschaft, die definiert, ob beim Verarbeiten von Partitionen die Sortierreihenfolge für die Ergebnisse einer Distinct Count-Abfrage sinnvoll ist. TRUE bedeutet, dass die Sortierreihenfolge nicht sinnvoll ist und vom Server überprüft werden muss. Beim Verarbeiten von Partitionen mit Distinct Count Measure wird eine SQL-Abfrage mit ORDER BY gesendet. Durch Festlegen der Eigenschaft auf FALSE kann die Verarbeitung beschleunigt werden.  
  
 Der Standardwert für diese Eigenschaft ist TRUE. Dies bedeutet, dass die Sortierreihenfolge nicht sinnvoll ist und überprüft werden muss.  
  
 **DatabaseConnectionPoolConnectTimeout**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die den beim Öffnen von neuen Verbindungen zu verwendenden Timeoutwert in Sekunden angibt.  
  
 **DatabaseConnectionPoolGeneralTimeout**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die den Timeoutwert für Datenbankverbindungen bei externen OLE DB-Verbindungen in Sekunden angibt.  
  
 **DatabaseConnectionPoolMax**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die die maximale Anzahl von Datenbankverbindungen in einem Pool angibt.  
  
 Der Standardwert für diese Eigenschaft beträgt 50 Verbindungen.  
  
 **DatabaseConnectionPoolTimeout**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataFileInitEnabled**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataPlacementOptimization**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataSliceInitEnabled**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DeepCompressValue**  
 Eine boolesche Eigenschaft für Measures vom Datentyp Double, die angibt, ob Zahlen komprimiert werden können, wodurch sich ein Verlust bei der numerischen Genauigkeit ergibt. Der Wert FALSE zeigt an, dass keine Komprimierung und kein Genauigkeitsverlust stattfinden.  
  
 Der Standardwert für diese Eigenschaft ist TRUE. Hiermit wird angezeigt, dass die Komprimierung aktiviert ist und ein Genauigkeitsverlust auftreten kann.  
  
 **DimensionPropertyKeyCache**  
 Eine boolesche Eigenschaft, die angibt, ob die Dimensionseigenschaftenschlüssel zwischengespeichert werden. Bei nicht eindeutigen Schlüsseln muss diese Eigenschaft auf TRUE festgelegt werden.  
  
 **IndexBuildEnabled**  
 Eine boolesche Eigenschaft, die angibt, ob nach der Verarbeitung Indizes erstellt werden. Diese Eigenschaft ist für Vergleichstests und Informationszwecke vorgesehen.  
  
 **IndexBuildThreshold**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die einen Schwellenwert für die Zeilenanzahl angibt, unter dem keine Indizes für Partitionen erstellt werden.  
  
 Der Standardwert dieser Eigenschaft beträgt 4096 Zeilen.  
  
 **IndexFileInitEnabled**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MapFormatMask**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **RecordsReportGranularity**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die angibt, wie oft (in Zeilen) der Server während der Verarbeitung Ablaufverfolgungsereignisse aufzeichnet.  
  
 Der Standardwert für diese Eigenschaft ist 1000. Dies bedeutet, dass einmal pro 1000 Zeilen ein Ablaufverfolgungsereignis aufgezeichnet wird.  
  
 **ROLAPDimensionProcessingEffort**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
## <a name="query"></a>Abfrage  
 **AggregationsUseEnabled**  
 Eine boolesche Eigenschaft, die definiert, ob zur Laufzeit gespeicherte Aggregationen verwendet werden. Diese Eigenschaft lässt zu, dass Aggregationen für Informationszwecke oder Vergleichstests ohne Ändern des Aggregationsentwurfs oder erneutes Verarbeiten deaktiviert werden.  
  
 Der Standardwert für diese Eigenschaft ist TRUE. Dies bedeutet, dass Aggregationen aktiviert sind.  
  
 **AllowSEFiltering**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **CalculationCacheRegistryMaxIterations**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **CalculationEvaluationPolicy**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ConvertDeletedToUnknown**  
 Eine boolesche Eigenschaft, die angibt, ob gelöschte Dimensionselemente in Unbekannt konvertiert werden.  
  
 **CopyLinkedDataCacheAndRegistry**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCacheRegistryMaxIterations**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DefaultDrillthroughMaxRows**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die die maximale Anzahl von Zeilen angibt, die von einer Drillthroughabfrage zurückgegeben werden.  
  
 Der Standardwert dieser Eigenschaft beträgt 10000 Zeilen.  
  
 **DimensionPropertyCacheSize**  
 Eine Eigenschaft für eine ganze 32-Bit-Zahl mit Vorzeichen, die den Arbeitsspeicher (in Bytes) angibt, der zum Zwischenspeichern von Dimensionselementen aus einer Abfrage verwendet wird.  
  
 Der Standardwert ist 4.000.000 Bytes (4 MB) pro Attributhierarchie und pro aktiver Abfrage. Der Standardwert gewährleistet eine ausgewogene Cachegröße für Lösungen, die typische Hierarchien enthalten. Dimensionen, die über eine sehr große Anzahl von Elementen (im Millionenbereich) oder über verschachtelte Hierarchien verfügen, erzielen eine bessere Leistung, wenn Sie diesen Wert erhöhen.  
  
 Die Vergrößerung des Cachespeichers kann folgende Auswirkungen haben:  
  
-   Die Kosten der Arbeitsspeichernutzung erhöhen sich, wenn Sie dem Dimensionscache die Nutzung einer größeren Arbeitsspeichermenge erlauben. Die tatsächliche Nutzung hängt von der Abfrageausführung ab. Nicht alle Abfragen verwenden den zulässigen Höchstwert.  
  
     Der von diesen Cachespeichern genutzte Arbeitsspeicher gilt als nicht verkleinerbar und wird bei der Berechnung von **TotalMemoryLimit**berücksichtigt.  
  
-   Wirkt sich auf alle Datenbanken auf dem Server aus. **DimensionPropertyCachesize** ist eine serverweite Eigenschaft. Wenn Sie diese Eigenschaft ändern, wirkt sich dies auf alle Datenbanken aus, die auf der aktuellen Instanz ausgeführt werden.  
  
 Schätzen der Anforderungen für den Dimensionscache:  
  
1.  Beginnen Sie, indem Sie die Größe um einen sehr hohen Wert erhöhen. So stellen Sie fest, ob sich die Vergrößerung des Dimensionscaches vorteilhaft auswirkt. Beispielsweise können Sie den Standardwert in einem ersten Schritt verdoppeln.  
  
2.  Wenn sich eine Leistungsverbesserung abzeichnet, verringern Sie den Wert schrittweise, bis Sie ein ausgewogenes Verhältnis zwischen Leistung und Arbeitsspeicherauslastung erreichen.  
  
 **ExpressNonEmptyUseEnabled**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **IgnoreNullRolapRows**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **IndexUseEnabled**  
 Eine boolesche Eigenschaft, die definiert, ob zur Laufzeit Indizes verwendet werden. Diese Eigenschaft ist für Informationszwecke und zum Durchführen von Vergleichstests vorgesehen.  
  
 **MapHandleAlgorithm**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MaxRolapOrConditions**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **UseCalculationCacheRegistry**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **UseDataCacheFreeLastPageMemory**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **UseDataCacheRegistry**  
 Eine boolesche Eigenschaft, die angibt, ob die Datencacheregistrierung für die Zwischenspeicherung von Abfragergebnissen (jedoch nicht für berechnete Ergebnisse) aktiviert werden soll.  
  
 **UseDataCacheRegistryHashTable**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **UseDataCacheRegistryMultiplyKey**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **UseDataSlice**  
 Eine boolesche Eigenschaft, die definiert, ob zur Laufzeit für die Abfrageoptimierung Datenslices der Partition verwendet werden sollen. Diese Eigenschaft ist für Vergleichstests und Informationszwecke vorgesehen.  
  
 **UseMaterializedIterators**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **UseSinglePassForDimSecurityAutoExist**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **UseVBANet**  
 Eine boolesche Eigenschaft, die definiert, ob für benutzerdefinierte Funktionen die VBA .net-Assembly verwendet werden soll.  
  
 **CalculationPrefetchLocality\ApplyIntersect**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **CalculationPrefetchLocality\ApplySubtract**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **CalculationPrefetchLocality\PrefetchLowerGranularities**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\CachedPageAlloc\Income**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\CachedPageAlloc\InitialBonus**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\CachedPageAlloc\MaximumBalance**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\CachedPageAlloc\MinimumBalance**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\CachedPageAlloc\Tax**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\CellStore\Income**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\CellStore\InitialBonus**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\CellStore\MaximumBalance**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\CellStore\MinimumBalance**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\CellStore\Tax**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\MemoryModel\Income**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\MemoryModel\InitialBonus**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\MemoryModel\MaximumBalance**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\MemoryModel\MinimumBalance**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataCache\MemoryModel\Tax**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
## <a name="jobs"></a>Aufträge  
 **ProcessAggregation\MemoryModel\Income**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ProcessAggregation\MemoryModel\InitialBonus**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ProcessAggregation\MemoryModel\MaximumBalance**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ProcessAggregation\MemoryModel\MinimumBalance**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ProcessAggregation\MemoryModel\Tax**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ProcessAggregation\ProcessPartition\Income**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ProcessAggregation\ProcessPartition\InitialBonus**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ProcessAggregation\ProcessPartition\MaximumBalance**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ProcessAggregation\ProcessPartition\MinimumBalance**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ProcessAggregation\ProcessPartition\Tax**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ProcessAggregation\ProcessProperty\Income**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ProcessAggregation\ProcessProperty\InitialBonus**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ProcessAggregation\ProcessProperty\ MaximumBalance**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ProcessAggregation\ProcessProperty\MinimumBalance**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **ProcessAggregation\ProcessProperty\Tax**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
## <a name="see-also"></a>Siehe auch  
 [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
