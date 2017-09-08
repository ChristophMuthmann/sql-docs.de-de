---
title: Filestore (Eigenschaften) | Microsoft Docs
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
- Income property
- InitialBonus property
- PercentScanPerPrice property
- FileStore properties
- BackgroundTrimCost property
- Tax property
- PerformanceTrace property
- MinimumBalance property
- UnbufferedThreshold property
- BackgroundTrimAmount property
- MaximumBalance property
- MemoryLimitMin property
- MemoryLimit property
ms.assetid: 580cf0aa-7425-4d48-aa8d-128f5b488fcd
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 68845b8dc5ff1b025134b227605363607db4b7cf
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="filestore-properties"></a>FileStore (Eigenschaften)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] werden die in den folgenden Tabellen aufgeführten Dateispeicher-Servereigenschaften unterstützt. Hierbei handelt es sich um erweiterte Eigenschaften, die nicht ohne die Unterstützung von [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollten. Weitere Informationen zu zusätzlichen Servereigenschaften und zum Festlegen dieser Eigenschaften finden Sie unter [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Gilt für:** mehrdimensionalen und Tabellenservermodus  
  
## <a name="properties"></a>Eigenschaften  
 **MemoryLimit**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MemoryLimitMin**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **PercentScanPerPrice**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **PerformanceTrace**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **RandomFileAccessMode**  
 Eine boolesche Eigenschaft, die angibt, ob auf Datenbankdateien und zwischengespeicherte Dateien im zufälligen Dateizugriffsmodus zugegriffen wird. Diese Eigenschaft ist standardmäßig deaktiviert. Beim Öffnen von Partitionsdatendateien für den Lesezugriff wird das Flag für den zufälligen Dateizugriff von Analysis Services standardmäßig nicht festgelegt.  
  
 In High-End-Systemen, insbesondere solchen mit umfangreichen Speicherressourcen und mehreren NUMA-Knoten, kann es vorteilhaft sein, zufälligen Dateizugriff zu verwenden. Zur Konfliktverringerung im Cache umgeht Windows im zufälligen Zugriffsmodus Seitenzuordnungsvorgänge, bei denen Daten vom Datenträger in den Systemdateicache eingelesen werden.  
  
 Sie müssen Vergleichstests ausführen, um zu bestimmen, ob die Abfrageleistung durch Ändern dieser Eigenschaft verbessert wird. Best Practices zum Ausführen von Vergleichstests, einschließlich des Löschens des Caches und des Vermeidens von häufigen Fehlern, finden Sie im [SQL Server 2008 R2 Analysis Services-Vorgangshandbuch](http://go.microsoft.com/fwlink/?LinkID=225539). Weitere Informationen zu den Kompromissen bei Verwendung dieser Eigenschaft finden Sie unter [http://support.microsoft.com/kb/2549369](http://support.microsoft.com/kb/2549369).  
  
 Um diese Eigenschaft in Management Studio anzuzeigen oder zu ändern, aktivieren Sie Liste der erweiterten Eigenschaften in der Servereigenschaftenseite. Sie können die Eigenschaft auch in der Datei "msmdsrv.ini" ändern. Nach dem Festlegen dieser Eigenschaft wird empfohlen, den Server erneut zu starten. Andernfalls wird auf bereits geöffnete Dateien weiterhin im bisherigen Modus zugegriffen.  
  
 **UnbufferedThreshold**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
## <a name="memory-model-category"></a>Arbeitsspeichermodell-Kategorie  
 **MemoryModel\Tax**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MemoryModel\Income**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MemoryModel\MaximumBalance**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MemoryModel\MinimumBalance**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MemoryModel\InitialBonus**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
## <a name="see-also"></a>Siehe auch  
 [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
