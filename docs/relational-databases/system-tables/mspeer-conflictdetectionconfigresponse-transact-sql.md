---
title: MSpeer_conflictdetectionconfigresponse (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSpeer_conflictdetectionconfigresponse
- MSpeer_conflictdetectionconfigresponse_TSQL
dev_langs: TSQL
helpviewer_keywords: MSpeer_conflictdetectionconfigureresponse
ms.assetid: 2685fb66-731d-40f7-af4b-596b9222c5d4
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb96eb44f44e3a7a0d1e1e4bcd0b1ce8dc00cf5e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mspeerconflictdetectionconfigresponse-transact-sql"></a>MSpeer_conflictdetectionconfigresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wird in der Peer-zu-Peer-Replikation verwendet, um die Antwort jedes Knotens auf eine topologieübergreifende Konfigurationsanforderung zu speichern. Diese Tabelle wird in der Veröffentlichungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|request_id|**int**|Identifiziert einen konfliktkonfigurationsanforderungseintrag in der [MSpeer_conflictdetectionconfigrequest](../../relational-databases/system-tables/mspeer-conflictdetectionconfigrequest-transact-sql.md) Tabelle.|  
|peer_node|**sysname**|Name der Serverinstanz, die die Antwort generiert hat.|  
|peer_db|**sysname**|Abonnementdatenbank auf dem Peer, der die Antwort generiert hat.|  
|peer_version|**sysname**|Kennzeichnet die Versionsnummer des Verlegers|  
|peer_db_version|**sysname**|Kennzeichnet die Versionsnummer der Peer-Datenbank.|  
|is_peer|**bit**|Gibt an, ob ein Knoten ein schreibgeschützter Abonnent ist. Der Wert **0** einen schreibgeschützten Abonnenten angegeben.|  
|conflict_detection_enabled|**bit**|Gibt an, ob die Konflikterkennung für die Topologie aktiviert ist.|  
|originator_id|**varbinary(16)**|Identifiziert jeden Knoten in der Topologie zum Zweck der Konflikterkennung. Weitere Informationen finden Sie unter [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|peer_conflict_retention|**int**|Zeitraum in Tagen, für den Metadaten in Konflikttabellen gespeichert werden.|  
|peer_subscriptions|**XML**|Informationen über den Knoten, der auf die Anforderung reagiert hat.|  
|progress_phase|**nvarchar(32)**|Identifiziert die aktuelle Phase der Verarbeitung mit einem der folgenden Werte:<br /><br /> Gestartet<br /><br /> Peerversion erfasst<br /><br /> Status erfasst|  
|modified_date|**datetime**|Datum und Uhrzeit, zu der eine Phase abgeschlossen wurde.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
