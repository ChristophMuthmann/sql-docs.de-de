---
title: Sys. dm_os_child_instances (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_child_instances
- sys.dm_os_child_instances_TSQL
- dm_os_child_instances
- dm_os_child_instances_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server state information [SQL Server]
- sys.dm_os_child_instances dynamic management view
- monitoring server health
ms.assetid: 1bef3074-0ccc-48fa-8f3d-14f3d99df86b
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d33bda7b901600598446cdea45d434df84b6e7f0
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmoschildinstances-transact-sql"></a>sys.dm_os_child_instances (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Benutzerinstanz zurück, die aus der übergeordneten Serverinstanz erstellt wurde.  
  
> **WICHTIG!** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Vom zurückgegebenen Informationen **dm_os_child_instances** kann verwendet werden, zum Ermitteln des Status jeder Benutzerinstanz (Heart_beat) und des Pipenamens (Instance_pipe_name) abrufen, die verwendet werden kann, um eine Verbindung mit der Benutzer zu erstellen. -Zielinstanz [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder SQLCmd. Die Verbindung zur Benutzerinstanz kann erst hergestellt werden, wenn die Benutzerinstanz von einem externen Vorgang, wie z. B. einer Clientanwendung, gestartet worden ist. Mit den SQL-Verwaltungstools selbst können keine Benutzerinstanzen gestartet werden.  
  
> **Hinweis:** Benutzerinstanzen sind eine Funktion des [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)] nur.  
  
> **Hinweis** von Aufrufen [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_child_instances**.  
  
|Column|Datentyp|Description|  
|------------|---------------|-----------------|  
|**owning_principal_name**|**nvarchar(256)**|Der Name des Benutzers, für den diese Benutzerinstanz erstellt wurde.|  
|owning_principal_sid|nvarchar(256)|Die SID (Sicherheits-ID) des Prinzipals, der Besitzer der Benutzerinstanz ist. Diese SID stimmt mit der Windows-SID überein.|  
|owning_principal_sid_binary|varbinary(85)|Die binäre SID-Version für den Benutzer, der die Benutzerinstanz besitzt.|  
|**instance_name**|**nvarchar(128)**|Der Name der Benutzerinstanz.|  
|**instance_pipe_name**|**nvarchar(260)**|Beim Erstellen einer Benutzerinstanz wird eine benannte Pipe für Verbindungen von Anwendungen erstellt. Dieser Name kann in einer Verbindungszeichenfolge für die Verbindung mit der Benutzerinstanz verwendet werden.|  
|**os_process_id**|**Int**|Die Prozessnummer des Windows-Prozesses für diese Benutzerinstanz.|  
|**os_process_creation_date**|**Datetime**|Datum und Uhrzeit des letzten Starts des Benutzerinstanzprozesses.|  
|**heart_beat**|**nvarchar(5)**|Aktueller Status der Benutzerinstanz – ALIVE oder DEAD.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="remarks"></a>Hinweise  
 Weitere Informationen zur dynamischen verwaltungssicht finden Sie unter [dynamische Verwaltungssichten und-Funktionen &#40; Transact-SQL &#41; ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Online.  
  
## <a name="see-also"></a>Siehe auch  
 [Benutzerinstanzen für Nichtadministratoren](http://msdn.microsoft.com/en-us/85385aae-10fb-4f8b-9eeb-cce2ee7da019)  
  
  



