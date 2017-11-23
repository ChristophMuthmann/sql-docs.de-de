---
title: CLR-Integration und Transaktionen | Microsoft Docs
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
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- managed code [SQL Server], transactions
- common language runtime [SQL Server], transactions
- System.Transactions namespace
- transactions [CLR integration]
ms.assetid: 381d206e-06e2-48d0-8206-295fcf06ac98
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 91af8f269dce39e8e707c570aba606f743b1a7e6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="clr-integration-and-transactions"></a>CLR-Integration und Transaktionen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Die **System.Transactions** Namespace bietet ein Transaktionsframework, die vollständig in ADO.NET integriert ist und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration der common Language Runtime (CLR). **System.Transactions** und ADO.NET arbeiten zusammen, um erweitern und die Verwendung von lokalen und verteilten Transaktionen in verwalteten Anwendungen zu vereinfachen.  
  
> [!NOTE]  
>  Eine CLR-benutzerdefinierte Prozedur (UDP) kann keine Verbindung zu dem gleichen Server herstellen, auf dem sie ausgeführt wird (Loopbackverbindung), und sich in die gleiche Transaktion eintragen. Wird ein solcher Versuch unternommen, wird die Verbindung blockiert und die Kontrolle nicht wieder an die benutzerdefinierte Prozedur übergeben. Dies führt für die benutzerdefinierte Prozedur zu einem Timeoutfehler (Msg 1206).  
  
 Weitere Informationen zu Transaktionen und .NET Framework finden Sie in den Abschnitten zum Ausführen von Transaktionen und zur Nutzung von Transaktionen im .NET Framework SDK.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Transaktionshöherstufung](../../relational-databases/clr-integration-data-access-transactions/transaction-promotion.md)  
 Beschreibt die Möglichkeit der Höherstufung von Transaktionen und die Verwendung dieser Funktion.  
  
 [Zugriff auf die aktuelle Transaktion](../../relational-databases/clr-integration-data-access-transactions/accessing-the-current-transaction.md)  
 Beschreibt, wie auf eine Transaktion, die gerade auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prozessintern ausgeführt wird, zugegriffen wird.  
  
 [Verwenden von „System.Transactions“](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)  
 Beschreibt, wie die **System.Transactions** -Anwendungsprogrammierschnittstelle (API) in einer verwalteten Anwendung.  
  
 [Lebensdauer von Transaktionen](../../relational-databases/clr-integration-data-access-transactions/transaction-lifetimes.md)  
 Beschreibt den Unterschied in der Lebensdauer von Transaktionen, die in [!INCLUDE[tsql](../../includes/tsql-md.md)]-gespeicherten Prozeduren gestartet wurden, und Transaktionen, die in CLR-Anwendungen gestartet wurden.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenzugriff von CLR-Datenbankobjekten aus](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
