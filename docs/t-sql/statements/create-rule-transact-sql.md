---
title: Erstellen Sie die Regel (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RULE_TSQL
- CREATE RULE
- CREATE_RULE_TSQL
- RULE
dev_langs:
- TSQL
helpviewer_keywords:
- list rules [SQL Server]
- unbinding rules
- pattern rules [SQL Server]
- range rules [SQL Server]
- alias data types [SQL Server], rules
- CREATE RULE statement
- reports [SQL Server], rules
- status information [SQL Server], rules
- rules [SQL Server], precedence
- binding rules [SQL Server]
- rules [SQL Server], creating
ms.assetid: b016a289-3a74-46b1-befc-a13183be51e4
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f1893007dd699ffb002884a153ac72fa90fcd103
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-rule-transact-sql"></a>CREATE RULE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt ein Objekt, das als Regel bezeichnet wird. Wenn eine Regel an eine Spalte oder an einen Aliasdatentyp gebunden ist, gibt sie die zulässigen Werte an, die in die betreffende Spalte eingefügt werden können.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Stattdessen wird die Verwendung von CHECK-Einschränkungen empfohlen. CHECK-Einschränkungen werden mit dem CHECK-Schlüsselwort der CREATE TABLE- oder ALTER TABLE-Anweisung erstellt. Weitere Informationen finden Sie unter [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md).  
  
 An eine Spalte oder an einen Aliasdatentyp kann jeweils nur eine Regel gebunden sein. Allerdings können einer Spalte sowohl eine Regel als auch eine oder mehrere CHECK-Einschränkungen zugeordnet werden. Ist dies der Fall, werden alle Einschränkungen berücksichtigt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE RULE [ schema_name . ] rule_name   
AS condition_expression  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *schema_name*  
 Der Name des Schemas, zu dem die Regel gehört.  
  
 *rule_name*  
 Der Name der neuen Regel. Regelnamen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md). Das Angeben des Regelbesitzernamens ist optional.  
  
 *condition_expression*  
 Die Bedingung oder die Bedingungen, die die Regel definieren. Eine Regel kann jeder Ausdruck sein, der in einer WHERE-Klausel zulässig ist, und kann Elemente, wie z. B. arithmetische Operatoren, relationale Operatoren und Prädikate (z. B. IN, LIKE, BETWEEN) einschließen. Eine Regel kann nicht auf Spalten oder andere Datenbankobjekte verweisen. Integrierte Funktionen, die nicht auf Datenbankobjekte verweisen, dürfen in einer Regel eingeschlossen sein. Benutzerdefinierte Funktionen können nicht verwendet werden.  
  
 *Condition_expression* enthält einen Variablenverweis. Das at-Zeichen (**@**) vorangestellt ist jede lokale Variable. Der Ausdruck bezieht sich auf den Wert, der mit der UPDATE- oder INSERT-Anweisung eingegeben wird. Kann einen beliebigen Namen bzw. ein Symbol zur Darstellung des Werts, beim Erstellen der Regel verwendet werden, aber das erste Zeichen muss das at-Zeichen (**@**).  
  
> [!NOTE]  
>  Vermeiden Sie die Erstellung von Regeln für Ausdrücke, die Aliasdatentypen verwenden. Obwohl die Erstellung von Regeln für Ausdrücke, die Aliasdatentypen verwenden, möglich ist, können die Ausdrücke nach dem Binden der Regeln an Spalten oder Aliasdatentypen nicht kompiliert werden, wenn auf diese verwiesen wird.  
  
## <a name="remarks"></a>Hinweise  
 CREATE RULE-Anweisungen können nicht mit anderen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen in einem einzelnen Batch kombiniert werden. Wenn Sie Regeln erstellen, gelten diese nicht für die Daten, die zu diesem Zeitpunkt bereits in der Datenbank vorhanden sind; darüber hinaus können Regeln nicht an Systemdatentypen gebunden werden.  
  
 Eine Regel kann nur in der aktuellen Datenbank erstellt werden. Nachdem Sie eine Regel erstellt haben, führen Sie **Sp_bindrule** auf die Regel an eine Spalte oder an den Aliasdatentyp zu binden. Eine Regel muss mit dem Datentyp der Spalte kompatibel sein. Z. B. "@value wie a%" kann nicht als eine Regel für eine numerische Spalte verwendet werden. Eine Regel kann nicht gebunden werden, um eine **Text**, **Ntext**, **Image**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **Xml**, CLR-benutzerdefinierten Typ oder **Zeitstempel**Spalte. An eine berechnete Spalte kann keine Regel gebunden werden.  
  
 Stellen Sie sicher, dass Sie Zeichen- und Datumskonstanten in einfache Anführungszeichen (') setzen und vor binären Konstanten 0x einfügen. Falls die Regel nicht mit der Spalte kompatibel ist, an die sie gebunden ist, gibt [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] eine Fehlermeldung zurück, wenn ein Wert eingefügt wird, nicht jedoch, wenn die Regel gebunden wird.  
  
 Eine Regel, die an einen Aliasdatentyp gebunden ist, wird nur dann aktiviert, wenn Sie versuchen, einen Wert in eine Datenbankspalte dieses Aliasdatentyps einzufügen bzw. den Spaltenwert zu aktualisieren. Mit Regeln werden keine Variablen getestet. Weisen Sie deshalb einer Variable eines Aliasdatentyps keinen Wert zu, der gegen eine Regel verstoßen würde, die an eine Spalte dieses Datentyps gebunden ist.  
  
 Verwenden Sie zum Abrufen eines Berichts auf eine Regel **Sp_help**. Um den Text einer Regel anzuzeigen, führen Sie **Sp_helptext** mit dem Regelnamen als Parameter. Um eine Regel umzubenennen, verwenden Sie **"Sp_rename"**.  
  
 Eine Regel muss gelöscht werden, mithilfe der DROP RULE, bevor Sie ein neuer Eintrag mit dem gleichen Namen erstellt wird, und die Regel muss ungebundenen mit **Sp_unbindrule** bevor er gelöscht wird. Verwenden Sie zum Aufheben der Bindung einer Regel an eine Spalte, **Sp_unbindrule**.  
  
 Sie können eine neue Regel an eine Spalte oder einen Datentyp binden, ohne die Bindung der alten aufzuheben; die neue Regel überschreibt die alte. Regeln, die an Spalten gebunden sind, haben immer Vorrang vor Regeln, die an Aliasdatentypen gebunden sind. Wenn Sie eine Regel an eine Spalte binden, wird dabei die Regel ersetzt, die bereits an den Aliasdatentyp jener Spalte gebunden ist. Binden Sie dagegen eine Regel an einen Datentyp, so ersetzt diese nicht die Regel, die an eine Spalte mit diesem Aliasdatentyp gebunden wurde. Die folgende Tabelle zeigt die Rangfolge, die gilt, wenn Regeln an Spalten und Aliasdatentypen, für die bereits Regeln vorhanden sind, gebunden werden:  
  
|Neue Regel wird gebunden an|Alte Regel ist gebunden an<br /><br /> Aliasdatentyp|Alte Regel ist gebunden an<br /><br /> Column|  
|-----------------------|-------------------------------------------|----------------------------------|  
|Alias-Datentyp|Ersetzt alte Regel|Keine Änderung|  
|Column|Ersetzt alte Regel|Ersetzt alte Regel|  
  
 Wenn einer Spalte ein Standardwert und eine Regel zugeordnet sind, muss der Standardwert innerhalb der durch die Regel definierten Domäne liegen. Ein Standardwert, der gegen eine Regel verstößt, wird nie eingefügt. Bei jedem Versuch, einen solchen Standardwert einzufügen, generiert das SQL Server-Datenbankmodul eine Fehlermeldung.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ausführen der CREATE RULE-Anweisung muss ein Benutzer mindestens über die CREATE RULE-Berechtigung in der aktuellen Datenbank und über die ALTER-Berechtigung auf dem Schema, in dem die Regel erstellt wird, verfügen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-rule-with-a-range"></a>A. Erstellen einer Regel mit einem Wertebereich  
 Das folgende Beispiel erstellt eine Regel, die den Wertebereich von ganzen Zahlen beschränkt, die in die Spalte(n) eingegeben werden, an die diese Regel gebunden ist.  
  
```  
CREATE RULE range_rule  
AS   
@range>= $1000 AND @range <$20000;  
```  
  
### <a name="b-creating-a-rule-with-a-list"></a>B. Erstellen einer Regel mit einer Liste  
 Das folgende Beispiel erstellt eine Regel, die die Ist-Werte, die in die Spalte oder Spalten eingegeben werden (an die diese Regel gebunden ist), auf Werte beschränkt, die in der Regel aufgelistet sind.  
  
```  
CREATE RULE list_rule  
AS   
@list IN ('1389', '0736', '0877');  
```  
  
### <a name="c-creating-a-rule-with-a-pattern"></a>C. Erstellen einer Regel mit einem Muster  
 Das folgende Beispiel erstellt eine Regel, die ein Muster vorgibt, das aus zwei beliebigen Zeichen, gefolgt von einem Bindestrich (`-`), einer beliebigen Anzahl von Zeichen oder gar keinem Zeichen und abschließend einer ganzen Zahl zwischen `0` und `9` besteht.  
  
```  
CREATE RULE pattern_rule   
AS  
@value LIKE '__-%[0-9]'  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Löschen Sie die STANDARDMÄßIGE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [DROP RULE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Sp_bindrule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [Sp_unbindrule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [WOBEI &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

