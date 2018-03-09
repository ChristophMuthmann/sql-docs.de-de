---
title: Unerwartete Systemfehler | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 57104ed0869aa6916d11d7329d18526cdaa72836
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="unexpected-system-failures"></a>Unerwartete Systemfehler
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Diese Regel überprüft das SYSTEM-Ereignis 6008 im Ereignisprotokoll auf dem Computer. Dieses Ereignis gibt ein unerwartetes Herunterfahren des Systems an. Das System ist möglicherweise instabil und bietet nicht die Stabilität und Integrität, die für das Hosten einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erforderlich ist.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Ermitteln Sie sofort die Ursache der unerwarteten Serverneustarts, oder verschieben Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einen anderen Computer.  
  
  
