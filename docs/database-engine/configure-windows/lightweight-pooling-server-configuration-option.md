---
title: Lightweightpooling (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default lightweight pooling
- decreasing overhead
- lightweight pooling option
- system overhead [SQL Server]
- performance [SQL Server], lightweight pooling
- context switching [SQL Server], lightweight pooling option
- excessive context switching [SQL Server]
- reducing overhead
- overhead [SQL Server]
ms.assetid: 2dc11b61-d065-4126-8e00-acf40390f9fb
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c82f1c64430cd45299b9378f86c6670841de2707
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="lightweight-pooling-server-configuration-option"></a>Lightweightpooling (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mit der Option **lightweight pooling** können Sie den Systemverarbeitungsaufwand im Zusammenhang mit häufigen Kontextumschaltungen senken, die teilweise in symmetrischen Multiprocessing-Umgebungen (SMP) auftreten. Bei häufigen Kontextumschaltungen kann die Option "Lightweightpooling" für einen besseren Durchsatz sorgen, da die Kontextumschaltungen inline ausgeführt werden, was die Anzahl der Benutzer-/Kernelringübergänge verringert.  
  
 Der Fibermodus gilt für bestimmte Situationen, in denen der Kontextwechsel von UMS-Arbeitsthreads kritische Engpässe bei der Leistung verursacht. Da dies nur selten auftritt, verbessert der Fibermodus auch nur selten die Leistung oder die Skalierbarkeit auf einem typischen System. Verbesserter Kontextwechsel in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] hat auch die Notwendigkeit des Fibermodus verringert. Es wird empfohlen, die Fibermodusplanung nicht für Routinevorgänge zu verwenden, da sie die Leistung verringern kann, indem die normalen Vorteile des Kontextwechsels unterdrückt werden, und da einige Komponenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die den lokalen Threadspeicher (TLS) verwenden, oder Thread-eigene Objekte, z. B. Mutexe (eine Art Win32-Kernel-Objekt), im Fibermodus nicht ordnungsgemäß arbeiten können.  
  
 Wenn der Wert der Option **Lightweightpooling** auf 1 festgelegt wird, wechselt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Fibermodusplanung. Der Standardwert für diese Option ist 0.  
  
 Bei **Lightweightpooling** handelt es sich um eine erweiterte Option. Wenn Sie die Einstellung mithilfe der gespeicherten Systemprozedur **sp_configure** ändern, können Sie **Lightweightpooling** nur ändern, wenn **Erweiterte Optionen anzeigen** auf 1 festgelegt ist. Diese Einstellung wird wirksam, nachdem der Server neu gestartet wurde.  
  
> [!NOTE]  
>  Lightweightpooling wird für [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 und [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows XP nicht unterstützt. [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] stellt eine vollständige Unterstützung für Lightweightpooling bereit.  
  
> [!NOTE]  
>  CLR (Common Language Runtime) wird beim Lightweightpooling nicht unterstützt. Deaktivieren Sie eine der beiden Optionen "CLR-fähig" oder "Lightweightpooling". Zu den Funktionen, die auf CLR basieren und nicht ordnungsgemäß im Fibermodus arbeiten, gehören der Hierarchy-Datentyp, die Replikation und die richtlinienbasierte Verwaltung.  
  
## <a name="see-also"></a>Siehe auch  
 [CLR-fähig (Serverkonfigurationsoption)](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CLR-fähig (Serverkonfigurationsoption)](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)  
  
  

