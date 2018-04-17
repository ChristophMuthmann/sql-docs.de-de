---
title: Sp_cursorprepare (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_prepare
ms.assetid: 6207e110-f4bf-4139-b3ec-b799c9cb3ad7
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1134a3edbbbf1a838207a122e43bbafb5ac0e18b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spcursorprepare-transact-sql"></a>sp_cursorprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Kompiliert die Cursoranweisung oder den Batch in einen Ausführungsplan, erstellt jedoch keinen Cursor. Die kompilierte Anweisung kann später von sp_cursorexecute verwendet werden. Diese mit Sp_cursorexecute gekoppelte gekoppelte Prozedur verfügt über die gleiche Funktion wie Sp_cursoropen, aber ist in zwei Phasen unterteilt. Sp_cursorprepare wird aufgerufen, indem ID = 3 in einem tabular Data Stream (TDS)-Paket.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_cursorprepare prepared_handle OUTPUT, params , stmt , options  
    [ , scrollopt[ , ccopt]]  
```  
  
## <a name="arguments"></a>Argumente  
 *prepared_handle*  
 Eine SQL Server generierter, vorbereiteter *behandeln* Bezeichner, der einen ganzzahligen Wert zurückgibt.  
  
> [!NOTE]  
>  *Prepared_handle* wird anschließend an eine Sp_cursorexecute-Prozedur übergeben, um einen Cursor zu öffnen. Nach der Erstellung bleibt ein Handle so lange bestehen, bis Sie sich abmelden oder es über die sp_cursorunprepare-Prozedur explizit entfernen.  
  
 *params*  
 Identifiziert parametrisierte Anweisungen. Die *params* -Definition der Variablen wird in der Anweisung an die Stelle der Parametermarkierungen gesetzt. *params* ist ein erforderlicher Parameter, der einen Eingabewert vom Typ **ntext**, **nchar**,oder **nvarchar** erfordert. Geben Sie einen NULL-Wert ein, wenn die Anweisung nicht parametrisiert ist.  
  
> [!NOTE]  
>  Verwenden einer **Ntext** -Zeichenfolge als Eingabewert Wert *Stmt* parametrisiert und der *Scrollopt* PARAMETERIZED_STMT-Wert ist auf.  
  
 *stmt*  
 Definiert das Resultset des Cursors. Der *stmt* -Parameter ist erforderlich und erfordert einen der Eingabewerte **ntext**, **nchar** oder **nvarchar** .  
  
> [!NOTE]  
>  Die Regeln zum Angeben der *Stmt* -Werts entsprechen denen für Sp_cursoropen, mit der Ausnahme, die die *Stmt* String-Datentyp muss **Ntext**.  
  
 *options*  
 Ein optionaler Parameter, der eine Beschreibung der Spalten im Cursorresultset zurückgibt. *Optionen* erfordert die folgenden **Int** Eingabewert.  
  
|Wert|Description|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 Scroll (Option). *Scrollopt* ist ein optionaler Parameter, der einen der folgenden erfordert **Int** Eingabewerte.  
  
|Wert|Description|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 Da der angeforderte Wert möglicherweise nicht für den durch definierten Cursor geeignet *Stmt*, dieser Parameter dient als Eingabe und Ausgabe. In solchen Fällen weist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen passenden Wert zu.  
  
 *ccopt*  
 Option für die Parallelitätssteuerung. *Ccopt* ist ein optionaler Parameter, der einen der folgenden erfordert **Int** Eingabewerte.  
  
|Wert|Description|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (vormals bekannt als LOCKCC)|  
|0x0004|**OPTIMISTISCHE** (vormals bekannt als OPTCC)|  
|0x0008|OPTIMISTIC (vormals bekannt als OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 Wie bei *Scrollpt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können einen anderen Wert als den angeforderten zuweisen.  
  
## <a name="remarks"></a>Hinweise  
 Der RPC-Statusparameter entspricht einem der folgenden Werte:  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|0|Success|  
|0x0001|Failure|  
|1FF6|Es konnten keine Metadaten zurückgegeben werden.<br /><br /> Hinweis: Der Grund dafür ist, dass die Anweisung ein Resultset nicht generiert. Beispielsweise ist es eine INSERT- oder DDL-Anweisung.|  
  
## <a name="examples"></a>Beispiele  
 Wenn *Stmt* parametrisiert und der *Scrollopt* PARAMETERIZED_STMT-Wert ist auf, die das Format der Zeichenfolge lautet wie folgt:  
  
 {  *\<Name der lokalen Variablen > **\<Datentyp >* } [,... *n* ]  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_cursorexecute &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Sp_cursorunprepare &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorunprepare-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
