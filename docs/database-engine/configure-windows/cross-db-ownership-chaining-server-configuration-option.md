---
title: "Datenbankübergreifende Besitzverkettung (Serverkonfigurationsoption) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cross-database ownership chaining
- cross db ownership chaining option
- chaining ownership
ms.assetid: 7b2d49f2-b91c-4aee-a52b-6cc49bed03af
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: e4a6157cb56c6db911406585f841046a431eef99
ms.openlocfilehash: c42780edef8e57b9d8159d9dfe384554cade4fb2
ms.contentlocale: de-de
ms.lasthandoff: 08/16/2017

---
# <a name="cross-db-ownership-chaining-server-configuration-option"></a>Datenbankübergreifende Besitzverkettung (Serverkonfigurationsoption)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Verwenden Sie die Option **Datenbankübergreifende Besitzverkettung** zum Konfigurieren von datenbankübergreifenden Besitzverkettungen für eine Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Mithilfe dieser Serveroption können Sie die datenbankübergreifende Besitzverkettung für alle Datenbanken auf Datenbankebene steuern oder die datenbankübergreifende Besitzverkettung für alle Datenbanken ermöglichen:  
  
-   Wenn **Datenbankübergreifende Besitzverkettung** für die Instanz deaktiviert ist (0), ist die datenbankübergreifende Besitzverkettung für alle Datenbanken deaktiviert.  
  
-   Wenn **Datenbankübergreifende Besitzverkettung** für die Instanz aktiviert ist (1), ist die datenbankübergreifende Besitzverkettung für alle Datenbanken aktiviert.  
  
-   Sie können die datenbankübergreifende Besitzverkettung für einzelne Datenbanken mithilfe der SET-Klausel der ALTER DATABASE-Anweisung festlegen. Wenn Sie eine neue Datenbank erstellen, können Sie die datenbankübergreifende Besitzverkettungsoption für die neue Datenbank mithilfe der CREATE DATABASE-Anweisung festlegen.  
  
     Es ist nicht empfehlenswert, die Option **Datenbankübergreifende Besitzverkettung** auf 1 festzulegen, es sei denn, alle von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz gehosteten Datenbanken müssen an der datenbankübergreifenden Besitzverkettung teilnehmen. Darüber hinaus sollten Ihnen die Sicherheitsauswirkungen dieser Einstellung bewusst sein.  

Um den aktuellen Status der datenbankübergreifenden Besitzverkettung zu bestimmen, führen Sie die folgende Abfrage aus:  
```sql
SELECT is_db_chaining_on, name FROM sys.databases;
```  
Das Ergebnis „1“ weist darauf hin, dass die datenbankübergreifende Besitzverkettung aktiviert ist.

## <a name="controlling-cross-database-ownership-chaining"></a>Steuern der datenbankübergreifenden Besitzverkettung  
 Vor dem Aktivieren bzw. Deaktivieren der datenbankübergreifenden Besitzverkettung sollten Sie Folgendes berücksichtigen:  
  
-   Sie müssen Mitglied der **sysadmin** -Rolle sein, um die datenbankübergreifende Besitzverkettung aktivieren oder deaktivieren zu können.  
  
-   Vor dem Deaktivieren der datenbankübergreifenden Besitzverkettung auf einem Produktionsserver sollten Sie jede Anwendung testen, einschließlich Anwendungen von Drittanbietern. Auf diese Weise können Sie sicherstellen, dass die Änderungen die Funktionalität der Anwendungen nicht beeinträchtigen.  
  
-   Sie können die Option **Datenbankübergreifende Besitzverkettung** ändern, wenn der Server ausgeführt wird und Sie RECONFIGURE mit **sp_configure**angeben.  
  
-   Verfügen Sie über Datenbanken, die eine datenbankübergreifende Besitzverkettung erfordern, ist es empfehlenswert, die Option **Datenbankübergreifende Besitzverkettung** für die Instanz mithilfe von **sp_configure**zu deaktivieren, und dann die datenbankübergreifende Besitzverkettung für einzelne Datenbanken, die sie erfordern, mithilfe der ALTER DATABASE-Anweisung zu aktivieren.  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  

