---
title: CHECKPOINT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4d48ae22fd01db35b0c5d6b924044dccd3a79b4f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="checkpoint-transact-sql"></a>CHECKPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Generiert einen manuellen Prüfpunkt in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank, mit der Sie aktuell verbunden sind.  
  
> [!NOTE]  
>  Informationen zu verschiedenen Typen von Datenbankprüfpunkten und Prüfpunktvorgängen im Allgemeinen finden Sie unter [Datenbankprüfpunkte &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CHECKPOINT [ checkpoint_duration ]  
```  
  
## <a name="arguments"></a>Argumente  
 *checkpoint_duration*  
 Gibt den Zeitraum in Sekunden an, in dem der manuelle Prüfpunkt abgeschlossen werden muss. Wenn *checkpoint_duration* angegeben ist, versucht [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], den Prüfpunkt innerhalb des angeforderten Zeitraums auszuführen. *checkpoint_duration* muss ein Ausdruck vom Typ **int** sein, der größer ist als 0 (null). Wird dieser Parameter nicht angegeben, wird die Prüfpunktdauer von [!INCLUDE[ssDE](../../includes/ssde-md.md)] angepasst, sodass die Leistung von Datenbankanwendungen nur minimal beeinträchtigt wird. Bei *checkpoint_duration* handelt es sich um eine erweiterte Option.  
  
## <a name="factors-affecting-the-duration-of-checkpoint-operations"></a>Faktoren, die sich auf die Dauer von Prüfpunktvorgängen auswirken  
 Im Allgemeinen erhöht sich die für einen Prüfpunktvorgang benötigte Zeit mit der Anzahl der modifizierten Seiten, die geschrieben werden müssen. Um die Leistungseinbußen in anderen Anwendungen zu minimieren, passt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] standardmäßig die Häufigkeit von Schreibvorgängen durch Prüfpunkte an. Durch das Verringern der Schreibhäufigkeit wird die Zeit erhöht, die zum Abschließen des Prüfpunktvorgangs erforderlich ist. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nutzt diese Strategie für einen manuellen Prüfpunkt, außer im Befehl CHECKPOINT wird ein *checkpoint_duration*-Wert angegeben.  
  
 Die Auswirkungen auf die Leistung durch *checkpoint_duration* hängen von der Anzahl der modifizierten Seiten, der Aktivität im System und der angegebenen tatsächlichen Dauer ab. Wenn der Prüfpunkt z.B. normalerweise innerhalb von 120 Sekunden abgeschlossen wird, wird durch Angabe eines *checkpoint_duration*-Werts von 45 Sekunden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dazu veranlasst, mehr Ressourcen für den Prüfpunkt zur Verfügung zu stellen, als gemäß der Standardeinstellung zugewiesen sind. Durch Angabe eines *checkpoint_duration*-Werts von 180 Sekunden würde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hingegen dazu veranlasst, weniger Ressourcen zuzuweisen als standardmäßig vorgesehen. Im Allgemeinen steigt durch einen niedrigen Wert für *checkpoint_duration* die Ressourcenmenge, die einem Prüfpunkt zugewiesen wird, während die einem Prüfpunkt zugeordneten Ressourcen bei einem hohen Wert für *checkpoint_duration* abnehmen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schließt einen Prüfpunkt nach Möglichkeit immer ab, und die CHECKPOINT-Anweisung wird unmittelbar nach Abschluss eines Prüfpunkts zurückgegeben. Aus diesem Grund kann ein Prüfpunkt sowohl vor Ablauf des angegebenen Zeitraumes abgeschlossen werden als auch länger als angegeben benötigen.  
  
##  <a name="Security"></a> Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Die CHECKPOINT-Berechtigungen sind standardmäßig Mitgliedern der festen Serverrolle **sysadmin** und der festen Datenbankrolle **db_owner** und **db_backupoperator** zugewiesen und nicht übertragbar.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Datenbankprüfpunkte &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [Konfigurieren der Serverkonfigurationsoption Wiederherstellungsintervall](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)   
 [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)  
  
  
