---
title: Konfigurieren von Parametern für die Datensammlung (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: data-collection
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data collection [SQL Server]
ms.assetid: 850905b6-35d2-4ed1-ab51-de64daa832b2
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f49cfcfef48c7f652ca6a5f05a7c49a97efe38fc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="configure-data-collection-parameters-transact-sql"></a>Konfigurieren von Parametern für die Datensammlung (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Bevor Sie einen benutzerdefinierten Sammlungssatz erstellen, müssen Sie zuerst Datensammlungsparameter konfigurieren. Hierfür können Sie die gespeicherten Prozeduren verwenden, die mit dem Datensammler bereitgestellt werden. Um diese Aufgabe auszuführen, müssen Sie mit dem Abfrage-Editor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] den folgenden Vorgang durchführen.  
  
> [!NOTE]  
>  Parameter für die Datensammlung können nur einmal konfiguriert werden. Nach der Konfiguration werden diese Parameter für alle zusätzlichen Sammlungssätze verwendet, die Sie erstellen.  
  
### <a name="configure-data-collection-parameters"></a>Konfigurieren von Parametern für die Datensammlung  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit der Datenbank her, in der Sie einen benutzerdefinierten Sammlungssatz erstellen möchten.  
  
2.  Führen Sie im Abfrage-Editor die folgenden Anweisungen aus.  
  
    ```sql  
    USE msdb;  
    EXEC sp_syscollector_set_warehouse_instance_name N'INSTANCE_NAME';-- where instance name is the name of the SQL Server instance  
    EXEC sp_syscollector_set_warehouse_database_name N'MDW';  
    EXEC sp_syscollector_set_cache_directory N'D:\tempdata';  
    ```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)   
 [Gespeicherte Prozeduren für den Datensammler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
