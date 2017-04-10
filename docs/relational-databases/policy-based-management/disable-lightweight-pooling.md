---
title: "Deaktivieren des Lightweightpoolings | Microsoft Docs"
ms.custom: ""
ms.date: "08/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Best Practices [Datenbankmodul]"
ms.assetid: 481bb43d-6fe5-497c-9096-971fb6bf733b
caps.latest.revision: 13
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 13
---
# Deaktivieren des Lightweightpoolings
  Diese Regel überprüft, ob Lightweightpooling auf dem Server deaktiviert ist. Wenn Lightweightpooling auf 1 festgelegt wird, wechselt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Fibermodusplanung. Der Fibermodus ist für bestimmte Situationen vorgesehen, in denen der Kontextwechsel der UMS-Arbeitsthreads kritische Engpässe bei der Leistung verursacht. Da dies nur selten auftritt, verbessert der Fibermodus auch nur selten die Leistung oder die Skalierbarkeit auf einem typischen System.  
  
## Empfehlungen zu Best Practices  
 Die Lightweightpooling-Option darf nur nach gründlichen Tests aktiviert werden, nachdem alle anderen Möglichkeiten zur Leistungsoptimierung ausgewertet wurden und der Kontextwechsel ein bekanntes Problem in Ihrer Umgebung darstellt.  
  
 Es wird empfohlen, die Fibermodusplanung nicht für Routinevorgänge zu verwenden, da sie die Leistung verringern kann, indem die normalen Vorteile des Kontextwechsels unterdrückt werden, und da einige Komponenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die den lokalen Threadspeicher (TLS) verwenden, oder Thread-eigene Objekte, z. B. Mutexe (eine Art Win32-Kernel-Objekt), im Fibermodus nicht ordnungsgemäß arbeiten können.  
  
 Um Lightweightpooling zu entfernen, führen Sie die folgende Anweisung aus, und starten Sie dann [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] neu.  
  
```tsql  
sp_configure 'show advanced options', 1;  
GO  
sp_configure 'lightweight pooling', 0;  
GO  
RECONFIGURE;  
GO  
```  
  
## Weitere Informationen  
 [Lightweightpooling (Serverkonfigurationsoption)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
## Siehe auch  
 [Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  