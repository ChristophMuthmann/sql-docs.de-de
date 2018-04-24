---
title: Unerwartete Systemfehler | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0a01dbd774aaaecb7b00baff624dc65c003e6cdd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="unexpected-system-failures"></a>Unerwartete Systemfehler
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Diese Regel überprüft das SYSTEM-Ereignis 6008 im Ereignisprotokoll auf dem Computer. Dieses Ereignis gibt ein unerwartetes Herunterfahren des Systems an. Das System ist möglicherweise instabil und bietet nicht die Stabilität und Integrität, die für das Hosten einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erforderlich ist.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Ermitteln Sie sofort die Ursache der unerwarteten Serverneustarts, oder verschieben Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einen anderen Computer.  
  
  
