---
title: '@@SERVERNAME (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@SERVERNAME'
- '@@SERVERNAME_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SERVERNAME function'
- local servers [SQL Server]
ms.assetid: b0ef33fb-954a-4294-b05b-a87c14ce25a3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5f1e7dbd47562368653ce75eee9d2a412164a9c9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40servername-transact-sql"></a>&#x40;&#x40;SERVERNAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt den Namen des lokalen Servers, auf denen ausgeführt wird, ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
@@SERVERNAME  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **nvarchar**  
  
## <a name="remarks"></a>Hinweise  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup legt den Servernamen während der Installation auf den Computernamen fest. Um den Namen des Servers zu ändern, verwenden Sie **Sp_addserver**, und starten Sie neu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Mit mehreren Instanzen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist, @@SERVERNAME gibt die folgenden lokalen Server Namensinformationen zurück, wenn der Name des lokalen Servers seit der Installation nicht geändert wurde.  
  
|Instanz|Serverinformationen|  
|--------------|------------------------|  
|Standardinstanz|"*Servername*"|  
|Benannte Instanz|"*Servername*\\*Instancename*"|  
|Failoverclusterinstanz – Standardinstanz|"*Virtualservername*"|  
|Failoverclusterinstanz – benannte Instanz|"*Virtualservername*\\*Instancename*"|  
  
 Obwohl die @@SERVERNAME -Funktion und die SERVERNAME-Eigenschaft der SERVERPROPERTY-Funktion möglicherweise Zeichenfolgen mit ähnlichen Formaten zurückgeben, die Informationen kann unterschiedlich sein. Die SERVERNAME-Eigenschaft meldet Änderungen des Netzwerknamens des Computers automatisch.  
  
 Im Gegensatz dazu @@SERVERNAME gibt keine Auskunft über solche Änderungen. @@SERVERNAME meldet Änderungen auf dem lokalen Server mithilfe der **Sp_addserver** oder **Sp_dropserver** gespeicherte Prozedur.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Verwendung von `@@SERVERNAME` gezeigt.  
  
```  
SELECT @@SERVERNAME AS 'Server Name'  
```  
  
 Hier ist ein Beispielresultset.  
  
```  
Server Name  
---------------------------------  
ACCTG  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurationsfunktionen (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [Sp_addserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)  
  
  
