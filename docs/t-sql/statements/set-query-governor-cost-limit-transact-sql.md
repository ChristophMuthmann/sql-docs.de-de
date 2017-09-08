---
title: SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET QUERY_GOVERNOR_COST_LIMIT
- SET_QUERY_GOVERNOR_COST_LIMIT_TSQL
- QUERY_GOVERNOR_COST_LIMIT
- QUERY_GOVERNOR_COST_LIMIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET QUERY_GOVERNOR_COST_LIMIT statement
- connections [SQL Server], overriding
- QUERY_GOVERNOR_COST_LIMIT option
- overriding connection values
ms.assetid: 3424bb44-6915-462d-a8d7-fe834af81387
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6090e52a9b3b2a701129e6cebeaa8460ab02fc43
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-querygovernorcostlimit-transact-sql"></a>SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Überschreibt den zurzeit konfigurierten **kostenbeschränkung der Abfragekontrolle** Wert für die aktuelle Verbindung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET QUERY_GOVERNOR_COST_LIMIT value  
```  
  
## <a name="arguments"></a>Argumente  
 *value*  
 Ein numerischer oder ganzzahliger Wert, der angibt, wie lange die Ausführung der Abfrage maximal dauern kann. Werte werden zur nächsten Ganzzahl abgerundet. Negative Werte werden zu 0 gerundet. Die Abfragekontrolle lässt die Ausführung von Abfragen, deren geschätzte Kosten über diesem Wert liegen, nicht zu. Wenn Sie 0 (den Standardwert) für diese Option angeben, wird die Abfragekontrolle deaktiviert. In diesem Fall können alle Abfragen ohne zeitliche Begrenzung ausgeführt werden.  
  
 Die Abfragekosten beziehen sich auf die geschätzte Zeit in Sekunden, die für das Ausführen einer Abfrage bei einer bestimmten Hardwarekonfiguration benötigt wird.  
  
## <a name="remarks"></a>Hinweise  
 SET QUERY_GOVERNOR_COST_LIMIT bezieht sich nur auf die aktuelle Verbindung und gilt für die Dauer der aktuellen Verbindung. Verwenden der [konfigurieren Sie die kostenbeschränkung der Abfragekontrolle Serverkonfigurationsoption](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md)Option **Sp_configure** Kosten Grenzwert der serverweite Abfragekontrolle zu ändern. Weitere Informationen zum Konfigurieren dieser Option finden Sie unter [Sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) und [Serverkonfigurationsoptionen &#40; SQLServer &#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
 Die Einstellung von SET QUERY_GOVERNOR_COST_LIMIT wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="see-also"></a>Siehe auch  
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

