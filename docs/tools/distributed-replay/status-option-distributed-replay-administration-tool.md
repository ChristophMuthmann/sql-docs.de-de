---
title: "Option Status (Verwaltungstool Distributed Replay) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ea89386e-1598-4412-8b37-680d14b2a5b6
caps.latest.revision: 17
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 17
---
# Option Status (Verwaltungstool Distributed Replay)
  Das Verwaltungstool [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay (**DReplay.exe**) ist ein Befehlszeilentool, das Sie für die Kommunikation mit dem Distributed Replay-Controller verwenden können. In diesem Thema werden die Befehlszeilenoption **status** und die entsprechende Syntax beschrieben.  
  
 Mit der **status** -Option wird der Controller abgefragt und der aktuelle Status angezeigt.  
  
 ![Themenlink (Symbol)](../../database-engine/configure-windows/media/topic-link.png "Themenlink (Symbol)") Weitere Informationen zu den Syntaxkonventionen für das Verwaltungstool finden Sie unter [Transact-SQL-Syntaxkonventionen &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## Syntax  
  
```  
  
dreplay status [-m controller] [-f status_interval]  
```  
  
#### Parameter  
 **-m** *Controller*  
 Gibt den Computernamen des Controllers an. Sie können mit "`localhost`" oder "`.`" auf den lokalen Computer verweisen.  
  
 Wenn der **-m**-Parameter nicht angegeben ist, wird der lokale Computer verwendet.  
  
 **-f** *Statusintervall*  
 Gibt die Häufigkeit (in Sekunden) für die Anzeige des Status an.  
  
 Wenn der **-f**-Parameter nicht angegeben wird, ist das Standardintervall 30 Sekunden.  
  
## Beispiele  
 Im folgenden Beispiel wird der aktuelle Status alle 60 Sekunden angezeigt. Der Wert `localhost` gibt an, dass der Controllerdienst auf demselben Computer wie das Verwaltungstool ausgeführt wird.  
  
```  
dreplay status –m localhost -f 60  
```  
  
## Berechtigungen  
 Sie müssen das Verwaltungstool als interaktiver Benutzer mit einem lokalen Benutzerkonto oder Domänenbenutzerkonto ausführen. Um ein lokales Benutzerkonto zu verwenden, müssen das Verwaltungstool und der Controller auf demselben Computer ausgeführt werden.  
  
 Weitere Informationen finden Sie unter [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
## Siehe auch  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Transact-SQL-Debugger](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  