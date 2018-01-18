---
title: Shared Memory-Eigenschaften | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
caps.latest.revision: "21"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 55c0140b55d4a338ead968e5442316d9a9d130cd
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="shared-memory-properties"></a>Shared Memory-Eigenschaften
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Verwenden der **Protokoll**Seite auf die **Eigenschaften von Shared Memory** Dialogfeld zum Aktivieren oder deaktivieren das shared Memory-Protokoll. Shared Memory ist das am einfachsten zu verwendende Protokoll. Es weist keine konfigurierbaren Einstellungen auf. Da Clients, die das Shared Memory-Protokoll verwenden, nur eine Verbindung mit einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen können, die auf demselben Computer ausgeführt wird, ist dieses Protokoll bei den meisten Datenbankaktivitäten nicht hilfreich. Verwenden Sie das Shared Memory-Protokoll zur Problembehandlung, wenn Sie vermuten, dass die anderen Protokolle nicht ordnungsgemäß konfiguriert sind.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]muss neu gestartet werden, um zu aktivieren oder deaktivieren Sie das Protokoll.  
  
## <a name="options"></a>enthalten  
 **Enabled**  
 Mögliche Werte sind **Ja** und **Nein**. Das Shared Memory-Protokoll ist standardmäßig aktiviert.  
  
## <a name="see-also"></a>Siehe auch  
 [Auswählen eines Netzwerkprotokolls](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [Erstellen einer gültigen Verbindungszeichenfolge mithilfe des Shared Memory-Protokoll](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
