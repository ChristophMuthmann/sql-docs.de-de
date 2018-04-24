---
title: Kontrollieren des Verhaltens von Triggern und Einschränkungen während der Synchronisierung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- identities [SQL Server replication]
- constraints [SQL Server], replication
- triggers [SQL Server], replication
- triggers [SQL Server replication]
- constraints [SQL Server replication]
- NOT FOR REPLICATION option
- NFR option
ms.assetid: 7c4e0f0e-cadc-4c99-98f4-69799b9b356b
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 30c6a0506381234acfbf0eb981881c29ea9e9c68
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="control-behavior-of-triggers-and-constraints-in-synchronization"></a>Kontrollieren des Verhaltens von Triggern und Einschränkungen während der Synchronisierung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Während der Synchronisierung führen Replikation-Agents [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)-Anweisungen und [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md) sowie [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)-Anweisungen für replizierte Tabellen aus, was zur Ausführung von DML (Data Manipulation Language)-Triggern in diesen Tabellen führen kann. Es gibt Fälle, in denen Sie verhindern müssen, dass Trigger während der Synchronisierung ausgelöst werden oder Einschränkungen während der Synchronisierung erzwungen werden. Dieses Verhalten hängt davon ab, wie der Trigger oder die Einschränkung erstellt wird.  
  
### <a name="to-prevent-triggers-from-executing-during-synchronization"></a>So verhindern Sie, dass Trigger während der Synchronisierung ausgeführt werden  
  
1.  Geben Sie bei der Erstellung eines neuen Triggers die Option NOT FOR REPLICATION für [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md) an.  
  
2.  Für einen vorhandenen Trigger geben Sie die Option NOT FOR REPLICATION für [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md) an.  
  
### <a name="to-prevent-constraints-from-being-enforced-during-synchronization"></a>So verhindern Sie, dass Einschränkungen während der Synchronisierung erzwungen werden  
  
1.  Beim Erstellen einer neuen CHECK- oder FOREIGN KEY-Einschränkung geben Sie in der Einschränkungsdefinition von [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) die Option CHECK NOT FOR REPLICATION an.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen von Tabellen &#40;Datenbankmodul&#41;](../../relational-databases/tables/create-tables-database-engine.md)  
  
  
