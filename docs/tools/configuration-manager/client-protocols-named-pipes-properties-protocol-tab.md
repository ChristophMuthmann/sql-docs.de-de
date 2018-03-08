---
title: Clientprotokolle - Named Pipes-Eigenschaften (Registerkarte Protokoll) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pipes [SQL Server], connecting to
- Named Pipes [SQL Server], default pipe
- client protocols [SQL Server]
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67a401a8edf4c6818899b755d9444edd09165972
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="client-protocols---named-pipes-properties-protocol-tab"></a>Clientprotokolle - Named Pipes-Eigenschaften (Registerkarte Protokoll)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
Verwenden Sie im [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager im Dialogfeld **Named Pipes-Eigenschaften** die Registerkarte **Protokoll** , um die Beschreibung der Standardpipe anzuzeigen oder zu ändern. Um eine Verbindung mit einer anderen Pipe herzustellen, geben Sie die Pipe im Dialogfeld **Standardpipe** ein. Weitere Informationen zu Verbindungszeichenfolgen finden Sie unter [Creating a Valid Connection String Using Named Pipes](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f).  
  
## <a name="options"></a>enthalten  
 **Standardpipe**  
 Gibt die Standardpipe an, die von der Named Pipes-Netzwerkbibliothek zum Herstellen einer Verbindung mit der Zielinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet wird. Standardmäßig wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf das Folgende gelauscht: `\\.\pipe\sql\query`  
  
 Geben Sie `sql\query`  
  
 **Aktiviert**  
 Mögliche Werte sind **Ja** und **Nein**.  
  
## <a name="see-also"></a>Siehe auch  
 [Auswählen eines Netzwerkprotokolls](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
