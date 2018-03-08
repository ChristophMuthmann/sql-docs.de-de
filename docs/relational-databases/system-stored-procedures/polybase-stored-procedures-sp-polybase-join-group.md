---
title: sp_polybase_join_group | Microsoft Docs
ms.custom: 
ms.date: 05/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sp_polybase_join_group
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7f6e4a77e5ce1341269bf9220c5d2a5305b4c314
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="polybase-stored-procedures---sppolybasejoingroup"></a>PolyBase stored procedures - sp_polybase_join_group
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Eine PolyBase-Gruppe für horizontale hochskalierungsberechnung hinzugefügt SQL Server-Instanz als Computeknoten.  
  
 SQL Server-Instanz benötigen den [PolyBase](../../relational-databases/polybase/polybase-guide.md) Feature installiert.  PolyBase ermöglicht die Integration von nicht - SQL Server-Datenquellen, z. B. Hadoop und Azure Blob-Speicher. Siehe auch ["sp_polybase_leave_group" aus &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>Argumente  
 *@head_node_address* = N'*head_node_address*'  
 Der Name des Computers, den SQL Server-Hauptknoten des PolyBase-Erweiterungsgruppe hostet. *@head_node_address*ist vom Datentyp nvarchar(255).  
  
 *@dms_control_channel_port* = dms_control_channel_port  
 Der Port, auf dem der Steuerungskanal für den Hauptknoten PolyBase-Datenverschiebungsdienst ausgeführt wird. *@dms_control_channel_port*ist eine nicht signierte __int16 an. Die Standardeinstellung ist **16450**.  
  
 *@head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 Der Name des Hauptknotens SQL Server-Instanz in der PolyBase-Erweiterungsgruppe. *@head_node_sql_server_instance_name*ist nvarchar(16).  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="remarks"></a>Hinweise  
 Nach dem Ausführen der gespeicherten Prozedur, fahren Sie das PolyBase-Modul herunter, und starten Sie den PolyBase-Datenverschiebungsdienst auf den Computer neu. So überprüfen die folgende DMV auf dem Hauptknoten ausführen: **sys.dm_exec_compute_nodes**.  
  
## <a name="example"></a>Beispiel  
 Im Beispiel werden den aktuellen Computer als Computeknoten einer PolyBase-Gruppe verknüpft.  Der Name des Hauptknotens ist **HST01** und der Name der SQL Server-Instanz auf dem Hauptknoten **MSSQLSERVER**.  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erste Schritte mit PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
