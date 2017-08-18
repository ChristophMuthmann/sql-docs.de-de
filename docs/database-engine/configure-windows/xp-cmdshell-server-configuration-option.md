---
title: xp_cmdshell (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b32eef170d0834b44932f753075bbd2df67762a2
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="xpcmdshell-server-configuration-option"></a>xp_cmdshell (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **xp_cmdshell** -Option ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Serverkonfigurationsoption, mit der Systemadministratoren steuern können, ob auf einem System die erweiterte gespeicherte Prozedur **xp_cmdshell** ausgeführt werden kann. Die Option **xp_cmdshell** ist in neuen Installationen standardmäßig deaktiviert. Sie kann mithilfe der richtlinienbasierten Verwaltung oder durch Ausführen der gespeicherten Systemprozedur **sp_configure** aktiviert werden, wie im folgenden Beispiel dargestellt:  
  
```  
-- To allow advanced options to be changed.  
EXEC sp_configure 'show advanced options', 1;  
GO  
-- To update the currently configured value for advanced options.  
RECONFIGURE;  
GO  
-- To enable the feature.  
EXEC sp_configure 'xp_cmdshell', 1;  
GO  
-- To update the currently configured value for this feature.  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  

