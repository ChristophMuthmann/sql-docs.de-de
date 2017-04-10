---
title: "Bandbreite f&#252;r Volltextdurchforstung (Serverkonfigurationsoption) | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "Große Speicherpuffer"
  - "Arbeitsspeicher [SQL Server], Puffer"
  - "ft crawl bandwidth (Option)"
ms.assetid: e5864ad9-92f5-43b5-95de-46d68ded8694
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Bandbreite f&#252;r Volltextdurchforstung (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verwenden Sie die Option **ft crawl bandwidth** , um anzugeben, auf welche Größe der Pool von großen Speicherpuffern erhöht werden kann. Große Speicherpuffer sind 4 Megabyte (MB) groß. Der **max**-Parameterwert gibt die maximale Anzahl der Puffer an, die der Volltextspeicher-Manager in einem großen Pufferpool verwalten soll. Wenn der **max** -Wert gleich null ist, gibt es keine obere Grenze für die Anzahl der Puffer in einem großen Pufferpool.  
  
 Der **min** -Parameter gibt die minimale Anzahl der Speicherpuffer an, die im großen Speicherpufferpool verwaltet werden müssen. Auf Anforderung vom [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Speicher-Manager werden alle zusätzlichen Pufferpools freigegeben, die Mindestzahl an Puffern wird jedoch beibehalten. Ist der angegebene **min** -Wert jedoch gleich null, werden alle Speicherpuffer freigegeben.  
  
 Unter diesen Umständen ist die Anzahl der Puffer, die derzeit zugewiesen sind, kleiner als der vom **min** -Parameter angegebene Wert.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## Siehe auch  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Bandbreite für Volltextbenachrichtigung (Serverkonfigurationsoption)](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  