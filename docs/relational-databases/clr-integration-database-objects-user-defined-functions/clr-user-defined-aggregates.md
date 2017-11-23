---
title: CLR User-Defined Aggregate | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- custom aggregates [CLR integration]
- calculations [CLR integration]
- user-defined functions [CLR integration]
ms.assetid: bad9b7e8-5967-4afa-8dc8-6d840faf9372
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ead22c2cabcc2cfdb42bc6bc44da788ca6b4882c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="clr-user-defined-aggregates"></a>Benutzerdefinierte CLR-Aggregate
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Aggregatfunktionen führen Berechnungen für eine Gruppe von Werten und einen einzelnen Wert zurückgeben. Bisher [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt nur integrierte Aggregatfunktionen, wie z. B. **Summe** oder **MAX**, die einen Satz von skalaren Eingabewerten arbeiten und eine einzelne gesamtverstärkung generieren der Wert aus dieser Gruppe. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Integration in die [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework common Language Runtime (CLR) ermöglicht jetzt die Entwickler benutzerdefinierte Aggregatfunktionen in verwaltetem Code zu erstellen und sich diese Funktionen für [!INCLUDE[tsql](../../includes/tsql-md.md)] oder anderen verwalteten Code.  
  
 In der folgenden Tabelle sind die Themen dieses Abschnitts aufgeführt.  
  
 [Anforderungen für die CLR User-Defined Aggregate](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates-requirements.md)  
 Stellt eine Übersicht über die Anforderungen zum Implementieren von benutzerdefinierten CLR-Aggregatfunktionen bereit.  
  
 [Aufrufen von CLR-benutzerdefinierten Aggregatfunktionen](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
 Erläutert, wie benutzerdefinierte Aggregate aufgerufen werden.  
  
  
