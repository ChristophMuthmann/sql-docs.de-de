---
title: Befehle (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- commands [XML for Analysis]
- XML for Analysis, commands
- XMLA, commands
ms.assetid: c8a93ea6-8eb5-4204-b037-69cb442a0082
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 19644de3ba240e417faa3d787360686d7b5c835f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="xml-elements---commands"></a>XML-Elemente - Befehle
  Dieser Referenzabschnitt enthält XML für Analysis (XMLA)-Elemente, die in verwendet werden können die **Befehl** -Element während einer **Execute** -Methodenaufruf.  
  
|Element|Description|  
|-------------|-----------------|  
|[Alter-Element (XMLA)](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)|Enthält Analysis Services Scripting Language (ASSL)-Elementen, die verwendet werden, indem die [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Methode, um Objekte auf einer Instanz von alter [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Backup-Element](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|Sichert eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenbank in einer Sicherungsdatei.|  
|[Batch-Element](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)|Führt eine oder mehrere XML für Analysis (XMLA) Befehle als Batchvorgang ein, sequenziell oder parallel auf einer Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[BeginTransaction-Element](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)|Startet in der aktuellen Sitzung eine Transaktion mit einer Analysis Services-Instanz.|  
|[Cancel-Element](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)|Bricht in einer Analysis Services-Instanz einen gerade ausgeführten Befehl ab.|  
|[ClearCache-Element](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)|Löscht den Arbeitsspeichercache des angegebenen Objekts in einer Analysis Services-Instanz.|  
|[CommitTransaction-Element](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)|Übermittelt in der aktuellen Sitzung eine Transaktion mit einer Analysis Services-Instanz.|  
|[Create-Element](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)|Enthält Analysis Services Scripting Language (ASSL)-Elementen, die verwendet werden, indem die [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Methode zum Erstellen von Objekten auf einer Analysis Services-Instanz.|  
|[Delete-Element](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)|Löscht auf einer Analysis Services-Instanz ein Objekt.|  
|[DesignAggregations-Element](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)|Erstellt Aggregationen für einen Aggregationsentwurf auf einer Analysis Services-Instanz.|  
|[Drop-Element](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|Löscht Attributelemente aus einer Dimension.|  
|[INSERT-Element](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)|Fügt Attributelemente in eine Dimension ein.|  
|[Lock-Element](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)|Sperrt ein bestimmtes Objekt auf einer Analysis Services-Instanz.|  
|[MergePartitions-Element](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)|Führt die Daten von einer oder mehreren Quellpartitionen zu einer Zielpartition zusammen und löscht dann die Quellpartitionen.|  
|[NotifyTableChange-Element](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)|Benachrichtigt eine Analysis Services-Instanz, dass Tabellen in einer bestimmten Datenquelle geändert wurden.|  
|[Process-Element](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|Verarbeitet Objekte auf einer Analysis Services-Instanz.|  
|[Restore-Element](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|Stellt eine Analysis Services-Datenbank aus einer Sicherungsdatei wieder her.|  
|[RollbackTransaction-Element](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)|Führt in der aktuellen Sitzung ein Rollback einer Transaktion mit einer Analysis Services-Instanz durch.|  
|[Statement-Element](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|Enthält eine Abfrage oder Anweisung gesendet werden mithilfe der [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Methode mit einer Instanz von Analysis Services.|  
|[Subscribe-Element](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)|Abonniert eine Ablaufverfolgung und gibt ein Rowset zurück, das die Ablaufverfolgungsereignisse einer Analysis Services-Instanz enthält.|  
|[Synchronize-Element](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|Synchronisiert eine Analysis Services-Datenbank mit einer anderen vorhandenen Datenbank.|  
|[Unlock-Element](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|Entsperrt eine bestimmte Sperre auf einer Analysis Services-Instanz.|  
|[Update-Element](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|Aktualisiert Attributelemente in einer Dimension.|  
|[UpdateCells-Element](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|Aktualisiert Zellen in einem Cube mit aktiviertem Schreibzugriff.|  
  
  
