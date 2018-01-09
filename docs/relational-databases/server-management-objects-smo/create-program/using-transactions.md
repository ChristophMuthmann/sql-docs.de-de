---
title: Verwenden von Transaktionen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a8beed22985c5f73ff5a4c1fed722fb331155ada
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="using-transactions"></a>Verwenden von Transaktionen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), die Verarbeitung von Transaktionen erfolgt über die Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mithilfe der <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Objekt. Die <xref:Microsoft.SqlServer.Management.Common.ServerConnection> Objekt verweist auf die <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Eigenschaft von der <xref:Microsoft.SqlServer.Management.Smo.Server> Objekt, wenn die Verbindung hergestellt wird. Methoden wie <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>, <xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> und <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> gehören zur <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>-Objekteigenschaft.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen von SMO-Programmen](../../../relational-databases/server-management-objects-smo/create-program/creating-smo-programs.md)  
  
  
