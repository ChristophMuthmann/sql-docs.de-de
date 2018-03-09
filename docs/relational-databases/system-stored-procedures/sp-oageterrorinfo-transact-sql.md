---
title: Sp_OAGetErrorInfo (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_OAGetErrorInfo_TSQL
- sp_OAGetErrorInfo
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetErrorInfo
ms.assetid: ceecea08-456f-4819-85d9-ecc9647d7187
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7b4477349f95fc286fce553f81e449162d8de511
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spoageterrorinfo-transact-sql"></a>sp_OAGetErrorInfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ruft OLE-Automatisierungsfehlerinformationen ab.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_OAGetErrorInfo [ objecttoken ]  
    [ , source OUTPUT ]   
    [ , description OUTPUT ]   
    [ , helpfile OUTPUT ]   
    [ , helpid OUTPUT ]   
```  
  
## <a name="arguments"></a>Argumente  
 *objecttoken*  
 Ist das Objekttoken ein OLE-Objekt, das zuvor erstellten **Sp_OACreate** oder ist NULL. Wenn *Objecttoken* wird angegeben, werden Fehlerinformationen für dieses Objekt zurückgegeben. Wird NULL angegeben, werden die Fehlerinformationen für den gesamten Batch zurückgegeben.  
  
 *Quelle* **Ausgabe**  
 Die Quelle der Fehlerinformation. Wenn angegeben, muss es sich um eine lokale **Char**, **Nchar**, **Varchar**, oder **Nvarchar** Variable. Der Rückgabewert wird bei Bedarf entsprechend der Länge der lokalen Variablen abgeschnitten.  
  
 *Beschreibung* **Ausgabe**  
 Ist die Beschreibung des Fehlers. Wenn angegeben, muss es sich um eine lokale **Char**, **Nchar**, **Varchar**, oder **Nvarchar** Variable. Der Rückgabewert wird bei Bedarf entsprechend der Länge der lokalen Variablen abgeschnitten.  
  
 *HelpFile* **Ausgabe**  
 Die Hilfedatei des OLE-Objekts. Wenn angegeben, muss es sich um eine lokale **Char**, **Nchar**, **Varchar**, oder **Nvarchar** Variable. Der Rückgabewert wird bei Bedarf entsprechend der Länge der lokalen Variablen abgeschnitten.  
  
 *HilfeID* **Ausgabe**  
 Die Kontext-ID für die Hilfedatei. Wenn angegeben, muss es sich um eine lokale **Int** Variable.  
  
> [!NOTE]  
>  Die Parameter für diese gespeicherte Prozedur werden anhand der Position, kein Name angegeben.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder eine Zahl ungleich Null (Fehler), die dem ganzzahligen Wert von HRESULT entspricht, der vom OLE-Automatisierungsobjekt zurückgegeben wird.  
  
 Weitere Informationen zu HRESULT-Rückgabecodes finden Sie unter [OLE-Automatisierung Rückgabecodes und Fehlerinformationen](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="result-sets"></a>Resultsets  
 Ist kein Ausgabeparameter angegeben, werden die Fehlerinformationen dem Client als Resultset zurückgegeben.  
  
|Spaltennamen|Datentyp|Description|  
|------------------|---------------|-----------------|  
|**Fehler**|**Binary(4)**|Binärdarstellung der Fehlernummer|  
|**Quelle**|**nvarchar(NN)**|Fehlerquelle|  
|**Description**|**nvarchar(NN)**|Beschreibung des Fehlers|  
|**HelpFile**|**nvarchar(NN)**|Hilfedatei für die Quelle|  
|**HelpID**|**int**|Hilfekontext-ID in der Hilfequelldatei|  
  
## <a name="remarks"></a>Hinweise  
 Jeder Aufruf von OLE-Automatisierung gespeicherte Prozedur (mit Ausnahme von **Sp_OAGetErrorInfo**) setzt die Fehlerinformationen zurück, daher braucht **Sp_OAGetErrorInfo** Plattforminformationen Fehler nur die neuesten OLE Automatisierung Aufruf der gespeicherten Prozedur. Beachten Sie, dass, weil **Sp_OAGetErrorInfo** die Fehlerinformationen nicht zurücksetzt es kann mehrfach aufgerufen werden, dieselben Fehlerinformationen abzurufen.  
  
 In der folgenden Tabelle werden OLE-Automatisierungsfehler und deren übliche Ursachen aufgelistet.  
  
|Fehler und HRESULT|Übliche Ursache|  
|-----------------------|------------------|  
|**Falscher Variablentyp (0 x 80020008)**|Datentyp des einen [!INCLUDE[tsql](../../includes/tsql-md.md)] Wert übergeben wird, wie ein Parameter der Methode nicht übereinstimmte der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] den Datentyp des Parameters der Methode oder ein NULL-Wert wurde als Methodenparameter übergeben.|  
|**Unbekannter Name (0 x 8002006)**|Der angegebene Eigenschafts- oder Methodenname für das angegebene Objekt wurde nicht gefunden.|  
|**Ungültige Klassenzeichenfolge (0x800401f3)**|Die angegebene ProgID oder CLSID wurde in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht als OLE-Objekt registriert. Benutzerdefinierte OLE-Automatisierungsserver müssen registriert werden, bevor sie mit instanziiert werden können **Sp_OACreate**. Dies kann geschehen, indem Sie mit dem Hilfsprogramm Regsvr32.exe für prozessinterne (.dll)-Server oder die **/RegServer** Befehlszeilenoption für lokale (.exe)-Servern.|  
|**Ausführen des Servers fehlgeschlagen (0 x 80080005)**|Das angegebene OLE-Objekt ist als lokaler OLE-Server (EXE-Datei) registriert, aber die EXE-Datei konnte nicht gefunden oder nicht ausgeführt werden.|  
|**Das angegebene Modul wurde nicht gefunden (0x8007007e)**|Das angegebene OLE-Objekt ist als In-Process-OLE-Server (DLL-Datei) registriert, aber die DLL-Datei konnte nicht gefunden oder nicht geladen werden.|  
|**Typenkonflikt (0 x 80020005)**|Der Datentyp einer lokalen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Variablen, die zum Speichern eines zurückgegebenen Eigenschaftswertes oder eines Rückgabewertes einer Methode verwendet wird, entspricht nicht dem [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-Datentyp des Rückgabewertes der Eigenschaft oder Methode. Oder der Rückgabewert einer Eigenschaft oder einer Methode wurde angefordert, gibt jedoch keinen Wert zurück.|  
|**Der Datentyp oder Wert des 'context'-Parameters von sp_OACreate ist ungültig. (0x8004275B)**|Der Wert des Kontextparameters sollte 1, 4 oder 5 sein.|  
  
 Weitere Informationen zur Verarbeitung von HRESULT-Rückgabecodes finden Sie unter [OLE-Automatisierung Rückgabecodes und Fehlerinformationen](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden OLE-Automatisierungsfehlerinformationen angezeigt.  
  
```  
DECLARE @output varchar(255);  
DECLARE @hr int;  
DECLARE @source varchar(255);  
DECLARE @description varchar(255);  
PRINT 'OLE Automation Error Information';  
EXEC @hr = sp_OAGetErrorInfo @object, @source OUT, @description OUT;  
IF @hr = 0  
BEGIN  
    SELECT @output = '  Source: ' + @source  
    PRINT @output  
    SELECT @output = '  Description: ' + @description  
    PRINT @output  
END  
ELSE  
BEGIN  
    PRINT '  sp_OAGetErrorInfo failed.'  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OLE-Automatisierung gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE-Automatisierungsbeispielskript](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
