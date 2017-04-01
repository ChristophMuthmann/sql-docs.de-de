---
title: "Option Abbrechen (Verwaltungstool Distributed Replay) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fea376de-307a-4b45-b7e2-37df88f3681a
caps.latest.revision: 15
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 15
---
# Option Abbrechen (Verwaltungstool Distributed Replay)
  Das Verwaltungstool [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay (**DReplay.exe**) ist ein Befehlszeilentool, das Sie für die Kommunikation mit dem Distributed Replay-Controller verwenden können. In diesem Thema werden die **cancel**-Befehlszeilenoption und die entsprechende Syntax beschrieben.  
  
 Die **cancel** -Option bricht den aktuellen Vorgang ab, der auf dem Controller ausgeführt wird.  
  
 ![Themenlink (Symbol)](../../database-engine/configure-windows/media/topic-link.png "Themenlink (Symbol)") Weitere Informationen zu den Syntaxkonventionen für das Verwaltungstool finden Sie unter [Transact-SQL-Syntaxkonventionen &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## Syntax  
  
```  
  
dreplay cancel [-m controller] [-q]   
```  
  
#### Parameter  
 **-m** *controller*  
 Der Computername des Controllers. Sie können mit "`localhost`" oder "`.`" auf den lokalen Computer verweisen.  
  
 Wenn der **-m**-Parameter nicht angegeben ist, wird der lokale Computer verwendet.  
  
 **-q**  
 Stiller Modus. Fordert nicht zur Bestätigung auf.  
  
 Der **-q**-Parameter ist optional.  
  
## Beispiele  
 Im folgenden Beispiel wird eine Abbruchanforderung im stillen Modus gesendet. Der Wert `localhost` gibt an, dass der Controllerdienst auf demselben Computer wie das Verwaltungstool ausgeführt wird.  
  
```  
dreplay cancel –m localhost -q  
```  
  
## Berechtigungen  
 Sie müssen das Verwaltungstool als interaktiver Benutzer mit einem lokalen Benutzerkonto oder Domänenbenutzerkonto ausführen. Um ein lokales Benutzerkonto zu verwenden, müssen das Verwaltungstool und der Controller auf demselben Computer ausgeführt werden.  
  
 Weitere Informationen finden Sie unter [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
## Siehe auch  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  