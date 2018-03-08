---
title: Command Events Data Columns | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: Command Events event category
ms.assetid: 7169f1e2-c6be-4d8c-b147-25719b84bc2c
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7f3c3be311e1f0ce7b53bd35b90fb94dfc03f07b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="command-events-data-columns"></a>Datenspalten für Befehlsereignisse
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]In der folgenden Tabelle sind die Datenspalten für jede Ereignisklasse in der **Befehlsereignisse** (Ereigniskategorie).  
  
 Die **Befehlsereignisse** -Ereigniskategorie weist folgende Ereignisklassen auf:  
  
-   [Command Begin-Klasse](#bkmk_1)  
  
-   [Command End-Klasse](#bkmk_2)  
  
 In den folgenden Tabellen sind die Datenspalten für jede dieser Ereignisklassen aufgeführt.  
  
##  <a name="bkmk_1"></a> Command Begin-Klasse – Datenspalten  
  
|Datenspalte|Description|  
|-----------------|-----------------|  
|ConnectionID|Enthält die eindeutige Verbindungs-ID, die dem Befehlsereignis zugeordnet ist.|  
|TextData|Enthält die eindeutigen Textdaten, die dem Befehlsereignis zugeordnet sind.|  
|ServerName|Enthält den Namen der Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , in der das Befehlsereignis aufgetreten ist.|  
|CurrentTime|Enthält die aktuelle Zeit des Befehlsereignisses.|  
|DatabaseName|Enthält den Namen der Datenbank, in der der Befehl ausgeführt wird.|  
|EventSubclass|Enthält die Ereignisklasse innerhalb des Befehlsereignisses. Diese Werte werden unterstützt:<br /><br /> 0: Create<br /><br /> 1: Alter<br /><br /> 2: Delete<br /><br /> 3: Process<br /><br /> 4: DesignAggregations<br /><br /> 5: WBInsert<br /><br /> 6: WBUpdate<br /><br /> 7: WBDelete<br /><br /> 8: Backup<br /><br /> 9: Restore<br /><br /> 10: MergePartitions<br /><br /> 11: Subscribe<br /><br /> 12: Batch<br /><br /> 13: BeginTransaction<br /><br /> 14: CommitTransaction<br /><br /> 15: RollbackTransaction<br /><br /> 16: GetTransactionState<br /><br /> 17: Cancel<br /><br /> 18: Synchronize<br /><br /> 19: Import80MiningModels<br /><br /> 20: Attach<br /><br /> 21: Detach<br /><br /> 22: SetAuthContext<br /><br /> 23: ImageLoad<br /><br /> 24: ImageSave<br /><br /> 10000: Other|  
|NTUserName|Enthält den Windows-Benutzernamen, der dem Befehlsereignis zugeordnet ist. Der Benutzername liegt im kanonischen Format vor. Beispiel: engineering.microsoft.com/software/user.|  
|RequestProperties|Enthält die XMLA-Anforderungseigenschaften (XML for Analysis), die dem Befehlsereignis zugeordnet sind.|  
|SPID|Enthält die Serverprozess-ID (SPID), mit der die Benutzersitzung eindeutig identifiziert wird, die dem Befehlsereignis zugeordnet ist. Die SPID entspricht direkt dem von XMLA verwendeten Sitzungs-GUID.|  
|StartTime|Enthält die Zeit, zu der das Befehlsereignis gestartet wurde, falls verfügbar.|  
|SessionType|Enthält die Entität, die den Vorgang verursacht hat.|  
|NTDomainName|Enthält das Windows-Domänenkonto, das dem Objektberechtigungsereignis zugeordnet ist.|  
|ClientProcessID|Enthält die eindeutige Clientprozess-ID, die dem Befehlsereignis zugeordnet ist.|  
  
##  <a name="bkmk_2"></a> Command End-Klasse – Datenspalten  
  
|Datenspalte|Description|  
|-----------------|-----------------|  
|ConnectionID|Enthält die eindeutige Verbindungs-ID, die dem Befehlsereignis zugeordnet ist.|  
|TextData|Enthält die eindeutigen Textdaten, die dem Befehlsereignis zugeordnet sind.|  
|ServerName|Enthält den Namen der Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , in der das Befehlsereignis aufgetreten ist.|  
|CurrentTime|Enthält die aktuelle Zeit des Befehlsereignisses. Für das Filtern stehen die Formate *JJJJ*-*MM*-*TT* und *JJJJ*-*MM*-*TT HH*:*MM*:*SS*zur Verfügung.|  
|DatabaseName|Enthält den Namen der Datenbank, in der der Befehl ausgeführt wird.|  
|Duration|Enthält die ungefähre Dauer zwischen dem Command Begin- und dem Command End-Ereignis.|  
|EndTime|Enthält die Zeit, zu der das Befehlsereignis endete. Für das Filtern stehen die Formate *JJJJ*-*MM*-*TT* und *JJJJ*-*MM*-*TT HH*:*MM*:*SS*zur Verfügung.|  
|EventSubclass|Enthält die Ereignisklasse innerhalb des Befehlsereignisses. Diese Werte werden unterstützt:<br /><br /> 0: Create<br /><br /> 1: Alter<br /><br /> 2: Delete<br /><br /> 3: Process<br /><br /> 4: DesignAggregations<br /><br /> 5: WBInsert<br /><br /> 6: WBUpdate<br /><br /> 7: WBDelete<br /><br /> 8: Backup<br /><br /> 9: Restore<br /><br /> 10: MergePartitions<br /><br /> 11: Subscribe<br /><br /> 12: Batch<br /><br /> 13: BeginTransaction<br /><br /> 14: CommitTransaction<br /><br /> 15: RollbackTransaction<br /><br /> 16: GetTransactionState<br /><br /> 17: Cancel<br /><br /> 18: Synchronize<br /><br /> 19: Import80MiningModels<br /><br /> 20: Attach<br /><br /> 21: Detach<br /><br /> 22: SetAuthContext<br /><br /> 23: ImageLoad<br /><br /> 24: ImageSave<br /><br /> 10000: Other|  
|NTCanonicalUserName|Enthält den Windows-Benutzernamen, der dem Befehlsereignis zugeordnet ist. Der Benutzername liegt im kanonischen Format vor. Beispiel: engineering.microsoft.com/software/user.|  
|NTUserName|Enthält das Windows-Benutzerkonto, das dem Befehlsereignis zugeordnet ist.|  
|SPID|Enthält die Serverprozess-ID (SPID), mit der die Benutzersitzung eindeutig identifiziert wird, die dem Befehlsereignis zugeordnet ist. Die SPID entspricht direkt dem von XMLA verwendeten Sitzungs-GUID.|  
|StartTime|Enthält die Zeit, zu der das End-Befehlsereignis gestartet wurde, falls verfügbar.|  
|CPUTime|Enthält die CPU-Zeit (in Millisekunden), die vom Prozess zwischen dem Begin-Befehlsereignis und dem End-Befehlsereignis verwendet wurde.|  
|Fehler|Enthält die Fehlernummer jedes Fehlers, der dem Befehlsereignis zugeordnet ist.|  
|Schweregrad|Enthält den Schweregrad einer Ausnahme, die dem Befehlsereignis zugeordnet ist. Die Werte sind:<br /><br /> 0 = Erfolg<br /><br /> 1 = Information<br /><br /> 2 = Warnung<br /><br /> 3 = Fehler|  
|Success|Enthält die Erfolgs- bzw. Fehlschlagsinformation des Befehlsereignisses. Die Werte sind:<br /><br /> 0 = Fehler<br /><br /> 1 = Erfolg|  
|SessionType|Enthält die Entität, die die Operation verursacht hat, die dem End-Befehlsereignis zugeordnet ist.|  
|NTDomainName|Enthält das Windows-Domänenkonto, das dem Befehlsereignis zugeordnet ist.|  
|ClientProcessID|Enthält die eindeutige Clientprozess-ID, die dem Befehlsereignis zugeordnet ist.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Command Events Event Category](../../analysis-services/trace-events/command-events-event-category.md)  
  
  
