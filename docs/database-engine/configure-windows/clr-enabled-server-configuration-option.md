---
title: "CLR-f&#228;hig (Serverkonfigurationsoption) | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Assemblys [CLR-Integration], Überprüfen, ob Ausführung möglich ist"
  - "CLR-fähig (Option)"
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
caps.latest.revision: 36
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 36
---
# CLR-f&#228;hig (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mithilfe der Option CLR-fähig können Sie angeben, ob Benutzerassemblys von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt werden dürfen. Die Option „CLR-fähig“ stellt folgende Werte bereit: 
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|0|Das Ausführen von Assemblys für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist unzulässig.|  
|1|Das Ausführen von Assemblys für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist zulässig.|  
  
Nur WOW64. Starten Sie WOW64-Server neu, damit die Änderungen an den Einstellungen wirksam werden. Für andere Servertypen ist ein Neustart nicht erforderlich.  

Wenn Sie RECONFIGURE ausführen und der Ausführungswert der Option „CLR-fähig“ von 1 in 0 geändert wird, werden alle Anwendungsdomänen mit Benutzerassemblys sofort entladen.  
  
>  **Die Ausführung von Common Language Runtime (CLR) wird für das Lightweightpooling nicht unterstützt**. Deaktivieren Sie eine der beiden folgenden Optionen: „CLR-fähig“ oder „Lightweightpooling“. Zu den Funktionen, die auf CLR basieren und nicht ordnungsgemäß im Fibermodus arbeiten, gehören der Datentyp **hierarchy**, die Replikation und die richtlinienbasierte Verwaltung.  
  
## Beispiel  
 Im folgenden Beispiel wird zunächst die aktuelle Einstellung der Option CLR-fähig angezeigt und die Option dann aktiviert, indem der Optionswert auf 1 festgelegt wird. Wenn Sie die Option deaktivieren möchten, legen Sie den Wert auf 0 fest.  
  
```tsql  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;    
```  
  
## Siehe auch  
 [Lightweightpooling (Serverkonfigurationsoption)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Lightweightpooling (Serverkonfigurationsoption)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
  