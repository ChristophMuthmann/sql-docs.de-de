---
title: "PRÜFPUNKT (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKPOINT_TSQL
- CHECKPOINT
dev_langs:
- TSQL
helpviewer_keywords:
- events [SQL Server], checkpoints
- automatic checkpoints
- writing dirty pages to disk
- pages [SQL Server], dirty
- checkpoints [SQL Server]
- CHECKPOINT statement
- log truncate mode [SQL Server]
- dirty pages
- logs [SQL Server], checkpoints
- manual checkpoints [SQL Server]
- pages [SQL Server], checkpoints
ms.assetid: ccdfc689-ad4e-44c0-83f7-0f2cfcfb6406
caps.latest.revision: 59
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d3c0dd607231880ebd7a43b3740eb2cb22b9c195
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="checkpoint-transact-sql"></a>CHECKPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Generiert einen manuellen Prüfpunkt in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank, mit der Sie aktuell verbunden sind.  
  
> [!NOTE]  
>  Informationen zu verschiedenen Typen von datenbankprüfpunkten und Prüfpunktvorgängen im Allgemeinen finden Sie unter [Datenbankprüfpunkte &#40; SQLServer &#41; ](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CHECKPOINT [ checkpoint_duration ]  
```  
  
## <a name="arguments"></a>Argumente  
 *checkpoint_duration*  
 Gibt den Zeitraum in Sekunden an, in dem der manuelle Prüfpunkt abgeschlossen werden muss. Wenn *Checkpoint_duration* angegeben wird, die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] versucht, den Prüfpunkt innerhalb des angeforderten Zeitraums auszuführen. Die *Checkpoint_duration* muss ein Ausdruck vom Typ **Int** und muss größer als 0 (null) sein. Wird dieser Parameter nicht angegeben, wird die Prüfpunktdauer von [!INCLUDE[ssDE](../../includes/ssde-md.md)] angepasst, sodass die Leistung von Datenbankanwendungen nur minimal beeinträchtigt wird. *Checkpoint_duration* ist eine erweiterte Option.  
  
## <a name="factors-affecting-the-duration-of-checkpoint-operations"></a>Faktoren, die sich auf die Dauer von Prüfpunktvorgängen auswirken  
 Im Allgemeinen erhöht sich die für einen Prüfpunktvorgang benötigte Zeit mit der Anzahl der modifizierten Seiten, die geschrieben werden müssen. Um die Leistungseinbußen in anderen Anwendungen zu minimieren, passt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] standardmäßig die Häufigkeit von Schreibvorgängen durch Prüfpunkte an. Durch das Verringern der Schreibhäufigkeit wird die Zeit erhöht, die zum Abschließen des Prüfpunktvorgangs erforderlich ist. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Diese Strategie für einen manuellen Prüfpunkt verwendet, es sei denn, eine *Checkpoint_duration* Wert wird im Befehl CCHECKPOINT angegeben.  
  
 Die Leistungseinbußen bei der Verwendung von *Checkpoint_duration* hängt von der Anzahl der modifizierten Seiten, die Aktivität auf das System und der angegebenen tatsächlichen Dauer. Wenn der Prüfpunkt normalerweise innerhalb von 120 Sekunden abgeschlossen wird, z. B. die Angabe einer *Checkpoint_duration* von 45 Sekunden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mehr Ressourcen anstreben, um den Prüfpunkt als standardmäßig zugewiesen werden. Im Gegensatz dazu angeben einer *Checkpoint_duration* von 180 Sekunden würde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] weniger Ressourcen zuzuweisen als standardmäßig zugewiesen werden. Im Allgemeinen gilt: ein kurzer *Checkpoint_duration* erhöht die Ressourcenverwendung auf den Prüfpunkt, während ein langer *Checkpoint_duration* verringert die Ressourcenverwendung auf den Prüfpunkt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schließt einen Prüfpunkt nach Möglichkeit immer ab, und die CHECKPOINT-Anweisung wird unmittelbar nach Abschluss eines Prüfpunkts zurückgegeben. Aus diesem Grund kann ein Prüfpunkt sowohl vor Ablauf des angegebenen Zeitraumes abgeschlossen werden als auch länger als angegeben benötigen.  
  
##  <a name="Security"></a> Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 CHECKPOINT-Berechtigungen standardmäßig den Mitgliedern der der **Sysadmin** -Serverrolle sysadmin und die **Db_owner** und **Db_backupoperator** festen Datenbankrollen und sind nicht übertragbar.  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Datenbankprüfpunkte &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [Konfigurieren Sie die Wiederherstellungsintervall-Serverkonfigurationsoption](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)   
 [Herunterfahren &#40; Transact-SQL &#41;](../../t-sql/language-elements/shutdown-transact-sql.md)  
  
  

