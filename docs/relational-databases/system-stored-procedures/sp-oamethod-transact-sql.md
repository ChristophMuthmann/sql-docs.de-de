---
title: Sp_OAMethod (Transact-SQL) | Microsoft Docs
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
- sp_OAMethod
- sp_OAMethod_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAMethod
ms.assetid: 1dfaebe2-c7cf-4041-a586-5d04faf2e25e
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1a2ed3efb39a681e2f3cb4e935e7b7e6d8d41a75
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spoamethod-transact-sql"></a>sp_OAMethod (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ruft eine Methode eines OLE-Objekts auf.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_OAMethod objecttoken , methodname  
    [ , returnvalue OUTPUT ]   
    [ , [ @parametername = ] parameter [ OUTPUT ] [ ...n ] ]   
```  
  
## <a name="arguments"></a>Argumente  
 *objecttoken*  
 Das Objekttoken eines zuvor mit **sp_OACreate**erstellten OLE-Objekts.  
  
 *Methodenname*  
 Der Name der Methode des OLE-Objekts, das aufgerufen wird.  
  
 *ReturnValue***Ausgabe**   
 Der Rückgabewert der Methode des OLE-Objekts. Wenn angegeben, muss es sich um eine lokale Variable vom entsprechenden Datentyp handeln.  
  
 Wenn die Methode einen einzelnen Wert zurückgibt, geben Sie entweder eine lokale Variable für *Returnvalue*, dem die Methode zurückgegeben Wert in der lokalen Variablen zurück, oder geben Sie keine *Returnvalue*, welche gibt die Methode Wert an den Client als einspaltiges, einzeiliges Resultset zurückgeben.  
  
 Wenn der Methodenrückgabewert ein OLE-Objekt *Returnvalue* muss eine lokale Variable vom Datentyp **Int**. Ein Objekttoken wird in der lokalen Variable gespeichert, und dieses Objekttoken kann in anderen gespeicherten Prozeduren der OLE-Automatisierung verwendet werden.  
  
 Wenn der Methodenrückgabewert ein Array, wenn *Returnvalue* angegeben ist, wird er auf NULL festgelegt.  
  
 Unter folgenden Bedingungen wird ein Fehler ausgegeben:  
  
-   *ReturnValue* angegeben ist, aber die Methode gibt keinen Wert zurück.  
  
-   Die Methode gibt ein Array mit mehr als zwei Dimensionen zurück.  
  
-   Die Methode gibt ein Array als Ausgabeparameter zurück.  
  
 [  *@parametername*** =**] *Parameter*[ **Ausgabe** ]  
 Ein Parameter der Methode. Wenn angegeben, *Parameter* muss ein Wert des entsprechenden Datentyps sein.  
  
 Zum Abrufen des Rückgabewert eines Ausgabeparameters *Parameter* muss eine lokale Variable des entsprechenden Datentyps und **Ausgabe** muss angegeben werden. Wenn ein konstanter Parameter angegeben wird, oder wenn **Ausgabe** nicht angegeben ist, wird eine zurückgeben Wert aus einer Output-Parameter wird ignoriert.  
  
 Wenn angegeben, *Parametername* muss der Name des der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] benannter Parameter. Beachten Sie, dass  **@** *Parametername*ist eine [!INCLUDE[tsql](../../includes/tsql-md.md)] lokale Variable. Das at-Zeichen (**@**) wird entfernt, und *Parametername*an OLE-Objekts als Parametername übergeben wird. Alle benannten Parameter müssen nach den Positionsparametern angegeben werden.  
  
 *n*  
 Ein Platzhalter, der anzeigt, dass mehrere Parameter angegeben werden können.  
  
> [!NOTE]  
>  *@parametername* ein benannter Parameter kann sein, da sie Teil der angegebenen Methode und wird an das Objekt übergeben. Die anderen Parameter für diese gespeicherte Prozedur werden nicht nach dem Namen, sondern nach der Position angegeben.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder eine Zahl ungleich Null (Fehler), die dem ganzzahligen Wert von HRESULT entspricht, der vom OLE-Automatisierungsobjekt zurückgegeben wird.  
  
 Weitere Informationen zu HRESULT-Rückgabecodes [OLE-Automatisierung Rückgabecodes und Fehlerinformationen](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="result-sets"></a>Resultsets  
 Wenn die Methode ein Array mit ein oder zwei Dimensionen zurückgibt, wird das Array dem Client folgendermaßen als Resultset zurückgegeben:  
  
-   Ein eindimensionales Array wird dem Client als einzeiliges Resultset zurückgegeben, das so viele Spalten wie Elemente im Array enthält. Das Array wird also als (Spalten) zurückgegeben.  
  
-   Ein zweidimensionales Array wird dem Client als Resultset zurückgegeben, dessen Anzahl an Spalten der Anzahl der Elemente in der ersten Dimension des Arrays entspricht und dessen Anzahl an Zeilen der Anzahl der Elemente in der zweiten Dimension des Arrays entspricht. Das Array wird also als (Spalten, Zeilen) zurückgegeben.  
  
 Beim Rückgabewert für einer Eigenschaft oder Methode werden ein Array **Sp_OAGetProperty** oder **Sp_OAMethod** gibt ein Resultset an den Client zurück. (Ausgabeparameter für Methoden können nicht einem Array entsprechen.) Diese Prozeduren durchsuchen alle Datenwerte des Arrays, um die geeigneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen und -Datenlängen für jede Spalte des Resultsets zu ermitteln. Für eine bestimmte Spalte verwenden diese Prozeduren den Datentyp und die -länge, die erforderlich sind, um alle Datenwerte in dieser Spalte darzustellen.  
  
 Wenn alle Datenwerte einer Spalte denselben Datentyp aufweisen, wird dieser Datentyp für die gesamte Spalte verwendet. Wenn Datenwerte in einer Spalte unterschiedliche Datentypen verwenden, wird der Datentyp für die gesamte Spalte entsprechend der folgenden Tabelle ausgewählt.  
  
||int|float|money|datetime|varchar|nvarchar|  
|------|---------|-----------|-----------|--------------|-------------|--------------|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="remarks"></a>Hinweise  
 Sie können auch **Sp_OAMethod** , einen Eigenschaftswert abzurufen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-calling-a-method"></a>A. Aufrufen einer Methode  
 Im folgenden Beispiel wird die `Connect` Methode des zuvor erstellten **SQLServer** Objekt.  
  
```  
EXEC @hr = sp_OAMethod @object, 'Connect', NULL, 'my_server',  
    'my_login', 'my_password';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
### <a name="b-getting-a-property"></a>B. Abrufen einer Eigenschaft  
 Im folgenden Beispiel wird die `HostName` -Eigenschaft (des zuvor erstellten **SQLServer** Objekt) und speichert ihn in einer lokalen Variablen.  
  
```  
DECLARE @property varchar(255);  
EXEC @hr = sp_OAMethod @object, 'HostName', @property OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
PRINT @property;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OLE Automation gespeicherte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE-Automatisierungsbeispielskript](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
