---
title: Ergebnisse von Triggern nicht zulassen (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- triggers [SQL Server], result sets
- result sets [SQL Server], triggers
- disallow results from triggers option
ms.assetid: 47149073-307d-47a5-b7d2-66a737d3231d
caps.latest.revision: "30"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0c9ea4ef45f56d22c6bdaa11cc6466d0c844e6f0
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="disallow-results-from-triggers-server-configuration-option"></a>Ergebnisse von Triggern nicht zulassen (Serverkonfigurationsoption)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Verwenden Sie die Option **Ergebnisse von Triggern nicht zulassen** , um zu steuern, ob Trigger Resultsets zurückgeben. Durch Trigger, die Resultsets zurückgeben, kann es in Anwendungen, die hierfür nicht konzipiert wurden, zu unerwartetem Verhalten kommen.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Diesen Wert sollten Sie auf 1 festlegen.  
  
 1 bedeutet, dass die Option **Ergebnisse von Triggern nicht zulassen** auf ON festgelegt ist. Die Standardeinstellung für diese Option ist 0 (OFF). Wenn diese Option auf 1 (ON) festgelegt ist, können Trigger keine Resultsets zurückgeben, und es wird folgende Fehlermeldung ausgegeben:  
  
 "Meldung '524', Ebene '16', Status '1', Prozedur '\<Prozedurname>', Zeile \<Zeilennummer>"  
  
 "Ein Trigger hat ein Resultset zurückgegeben, und die disallow_results_from_triggers-Serveroption ist TRUE".  
  
 Die Option **Ergebnisse von Triggern nicht zulassen** wird auf der Instanzebene von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angewendet und bestimmt das Verhalten sämtlicher vorhandener Trigger in der Instanz.  
  
 Bei der Option **Ergebnisse von Triggern nicht zulassen** handelt es sich um eine erweiterte Option. Wenn Sie die Einstellung mithilfe der gespeicherten Systemprozedur **sp_configure** ändern, können Sie **Ergebnisse von Triggern nicht zulassen** nur ändern, wenn Erweiterte Optionen anzeigen auf 1 festgelegt ist. Die Einstellung tritt ohne Neustarten des Servers sofort in Kraft.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
