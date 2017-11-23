---
title: Plug-in-Algorithmen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- third-party algorithms [Analysis Services]
- algorithms [data mining], creating
- plugin algorithms [Analysis Services]
ms.assetid: fe364ddc-576e-42fc-9ced-baa399992f92
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6af94e43b03b75765f7e84903dbadee1341d31a6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="plugin-algorithms"></a>Plug-In-Algorithmen
  Neben den Algorithmen, die in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitgestellt werden, gibt es viele andere Algorithmen, die für Data Mining verwendet werden können. Entsprechend stellt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] einen Mechanismus bereit, um von Drittanbietern erstellte Algorithmen als Plug-Ins zu integrieren. Vorausgesetzt, die Algorithmen erfüllen bestimmte Standards, können Sie diese in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genauso verwenden, wie die [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Algorithmen. Plug-In-Algorithmen verfügen über die gleichen Funktionen, wie die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitgestellten Algorithmen.  
  
 Eine vollständige Beschreibung der Schnittstellen, die von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwendet werden, um mit Plug-In-Algorithmen zu kommunizieren, finden Sie in den Beispielen für die Erstellung eines benutzerdefinierten Algorithmus und für benutzerdefinierte Modell-Viewer auf der [CodePlex-](http://go.microsoft.com/fwlink/?LinkID=87843) Website.  
  
## <a name="algorithm-requirements"></a>Anforderungen für Algorithmen  
 Damit ein Algorithmus als Plug-In in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]integriert werden kann, müssen Sie die folgenden COM-Schnittstellen implementieren:  
  
 **IDMAlgorithm**  
 Implementiert einen Algorithmus, der Modelle erstellt und implementiert die Vorhersagevorgänge der resultierenden Modelle.  
  
 **IDMAlgorithmNavigation**  
 Ermöglicht Browsern den Zugriff auf die Inhalte von Modellen.  
  
 **IDMPersist**  
 Ermöglicht [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]das Laden und Speichern der vom Algorithmus trainierten Modelle.  
  
 **IDMAlgorithmMetadata**  
 Beschreibt die Funktionen und Eingabeparameter des Algorithmus.  
  
 **IDMAlgorithmFactory**  
 Erstellt Instanzen der Objekte, die die Algorithmusschnittstelle implementieren und stellt für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] einen Zugriff auf die Schnittstelle der Algorithmusmetadaten bereit.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwendet diese COM-Schnittstellen zum Kommunizieren mit den Plug-In-Algorithmen. Obwohl die verwendeten Plug-In-Algorithmen die [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Spezifikation OLE DB für Data Mining unterstützen müssen, müssen Sie nicht alle Data Mining-Optionen in der Spezifikation unterstützen. Mit dem [MINING_SERVICES](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md) -Schemarowset können Sie die Funktionen eines Algorithmus ermitteln. Dieses Schemarowset führt die unterstützten Data Mining-Optionen für jeden Anbieter von Plug-In-Algorithmen auf.  
  
 Sie müssen neue Algorithmen registrieren, bevor Sie sie mit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]verwenden können. Fügen Sie die folgenden Informationen in die INI-Datei der Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ein, in die die Algorithmen integriert werden sollen, um einen Algorithmus zu registrieren:  
  
-   Der Algorithmusname  
  
-   ProgID (dies ist optional und wird nur für Plug-In-Algorithmen eingefügt)  
  
-   Ein Flag, das angibt, ob der Algorithmus aktiviert ist oder nicht  
  
 Das folgende Codebeispiel illustriert die Registrierung eines neuen Algorithmus:  
  
 `<ConfigurationSettings>`  
  
 `...`  
  
 `<DataMining>`  
  
 `...`  
  
 `<Algorithms>`  
  
 `...`  
  
 `<Sample_Plugin_Algorithm>`  
  
 `<Enabled>1</Enabled>`  
  
 `<ProgID>Microsoft.DataMining.SamplePlugInAlgorithm.Factory</ProgID>`  
  
 `</Sample_PlugIn_Algorithm>`  
  
 `...`  
  
 `</Algorithms>`  
  
 `...`  
  
 `</DataMining>`  
  
 `...`  
  
 `</ConfigurationSettings>`  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [DMSCHEMA_MINING_SERVICES-Rowset](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)  
  
  
