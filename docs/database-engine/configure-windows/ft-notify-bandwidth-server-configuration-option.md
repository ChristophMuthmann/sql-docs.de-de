---
title: Bandbreite für Volltextbenachrichtigung (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- ft notify bandwidth opion
- small memory buffers
- memory [SQL Server], buffers
ms.assetid: 9ca284c5-f3e0-4a67-a132-fff376ff0ffe
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1da0739321c11ab0ac712bbcfcbca6fb9292647c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="ft-notify-bandwidth-server-configuration-option"></a>Bandbreite für Volltextbenachrichtigung (Serverkonfigurationsoption)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Mit der **ft notify bandwidth** -Option können Sie angeben, bis zu welcher Größe der Pool mit geringem Arbeitsspeicher anwachsen kann. Kleine Arbeitsspeicherpuffer sind 64 KB groß. Der Parameterwert *max* gibt die maximale Anzahl von Puffern an, die der Volltextspeicher-Manager in einem kleinen Pufferpool verwalten soll. Wenn der **max** -Wert null beträgt, besteht keine obere Grenze für die Anzahl der Puffer in einem Pool mit geringem Arbeitsspeicher.  
  
 Durch den Parameter **min** wird die minimale Anzahl von Speicherpuffern angegeben, die in einem Pool mit geringem Arbeitsspeicher verwaltet werden müssen. Auf Anforderung vom [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Speicher-Manager werden alle zusätzlichen Pufferpools freigegeben, die Mindestzahl an Puffern wird jedoch beibehalten. Ist der angegebene **min** -Wert jedoch gleich null, werden alle Speicherpuffer freigegeben.  
  
 Unter bestimmten Umständen ist die Pufferanzahl, die aktuell zugeordnet ist, geringer als der durch den Parameter **min** angegebene Wert.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Bandbreite für Volltextdurchforstung (Serverkonfigurationsoption)](../../database-engine/configure-windows/ft-crawl-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
