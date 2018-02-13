---
title: SqlServerAlias-Klasse | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- SqlServerAlias Class
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServerAlias class
ms.assetid: 475662b9-6985-45bf-b1e9-b0f26ef50443
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a34ee85fcc625db5bba5c310107339fb2c97f38a
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="sqlserveralias-class"></a>SqlServerAlias-Klasse
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
Die [SqlServerAlias Class](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) -Klasse stellt einen Serververbindungsalias dar.  
  
 Ein Serververbindungsalias ist erforderlich, wenn beide der folgenden Situationen eintreten:  
  
-   Der Client stellt über einen Netzwerktransport, der nicht der standardmäßige Netzwerktransport ist, ein Verbindung zu einer Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] her.  
  
-   Die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , mit der der Client verbunden ist, überwacht einen anderen Named Pipe.  
  
 **Hinweis:** Die [SqlServerAlias-Klasse](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) erbt die **Put** -Methode von der Provider-Klasse. Es werden jedoch keine Ergebnisse ausgegeben , wie von der **Provider::Put** -Methode angegeben. Weitere Informationen finden Sie in der WMI-Dokumentation.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Clientprotokollen](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
