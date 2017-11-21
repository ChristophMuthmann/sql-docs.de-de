---
title: PUBLISHINGSERVERNAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PUBLISHINGSERVERNAME_TSQL
- PUBLISHINGSERVERNAME
dev_langs:
- TSQL
helpviewer_keywords:
- PUBLISHINGSERVERNAME function
- Publishers [SQL Server replication], names
ms.assetid: e7c278e5-ab23-419e-ab3e-3bb20b0636df
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a5aeeb414f9c980429d20f123e1f9c986b147eee
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="replication-functions---publishingservername"></a>Replikationsfunktionen - PUBLISHINGSERVERNAME
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Namen des ursprünglichen Verlegers für eine veröffentlichte Datenbank zurück, die an einer Datenbank-Spiegelungssitzung teilnimmt. Diese Funktion wird auf einer Verlegerinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Veröffentlichungsdatenbank ausgeführt. Hiermit bestimmen Sie den ursprünglichen Verleger der veröffentlichten Datenbank.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
PUBLISHINGSERVERNAME()  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **nvarchar**  
  
## <a name="remarks"></a>Hinweise  
 PUBLISHINGSERVERNAME wird für alle Replikationstypen verwendet.  
  
 PUBLISHINGSERVERNAME wird verwendet, wenn eine Datenbank-Spiegelungssitzung für die Veröffentlichungsdatenbank zwischen dem Verleger und einer Spiegelungspartnerinstanz vorhanden ist.  
  
 Diese Funktion muss im Kontext einer Veröffentlichungsdatenbank ausgeführt werden. Wenn PUBLISHINGSERVERNAME für eine Veröffentlichungsdatenbank auf der Spiegelserverinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, wird der Name der Verlegerinstanz, von der die veröffentlichte Datenbank stammt, zurückgegeben. Wenn diese Funktion für eine Datenbank auf der Spiegelserverinstanz ausgeführt wird, die nicht veröffentlicht ist oder die von der Spiegelserverinstanz nach einem Failover veröffentlicht wird, wird der Name der Spiegelserverinstanz zurückgegeben. Wenn diese Funktion auf der ursprünglichen Verlegerinstanz ausgeführt wird, wird der Name des Verlegers zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankspiegelung und Replikation (SQL Server)](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)   
 [Replikationsfunktionen &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/53702dee-de58-47d5-a552-7f32000f77d4)  
  
  

