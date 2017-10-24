---
title: LOGINPROPERTY (Transact-SQL) | Microsoft Docs
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
- BadPasswordCount_TSQL
- BadPasswordTime_TSQL
- IsLockedIsMustChange
- PasswordLastSetTime
- LOGINPROPERTY_TSQL
- LockoutTime
- BadPasswordCount
- PasswordHash
- HistoryLengthIsExpired
- LockoutTime_TSQL
- PasswordHash_TSQL
- HistoryLengthIsExpired_TSQL
- PasswordLastSetTime_TSQL
- BadPasswordTime
- IsLockedIsMustChange_TSQL
- LOGINPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- default database
- LOGINPROPERTY function
ms.assetid: b34df777-79b0-49a5-88db-b99998479a5d
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 31cbf502614fb348f35474237009f444ed294384
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="loginproperty-transact-sql"></a>LOGINPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu Richtlinieneinstellungen für die Anmeldung zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
LOGINPROPERTY ( 'login_name' , 'property_name' )  
```  
  
## <a name="arguments"></a>Argumente  
 *login_name*  
 Der Name einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung, für die der Status der Anmeldungseigenschaften zurückgegeben wird.  
  
 *Eigenschaftenname*  
 Ein Ausdruck, der die Eigenschafteninformationen enthält, die für die Anmeldung zurückgegeben werden sollen. *PropertyName* kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**BadPasswordCount**|Gibt die Anzahl aufeinanderfolgender Anmeldeversuche mit einem falschen Kennwort zurück.|  
|**BadPasswordTime**|Gibt die Zeit des letzten Anmeldeversuchs mit einem falschen Kennwort zurück.|  
|**DaysUntilExpiration**|Gibt die Anzahl von Tagen zurück, bis das Kennwort abläuft.|  
|**DefaultDatabase**|Gibt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung Standarddatenbank wie in den Metadaten gespeichert oder **master** Wenn keine Datenbank angegeben ist. Gibt NULL für nicht -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellte Benutzer (z. B. Windows-authentifizierten Benutzer).|  
|**DefaultLanguage**|Gibt die bei der Anmeldung angegebene Standardsprache zurück, wie sie in den Metadaten gespeichert ist. Gibt NULL für nicht -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellte Benutzer, z. B. von Windows authentifizierte Benutzer.|  
|**HistoryLength**|Gibt die Anzahl der Kennwörter zurück, die für die Anmeldung mithilfe der Mechanismen zur Durchsetzung von Kennwortrichtlinien nachverfolgt werden. 0, wenn keine Kennwortrichtlinie erzwungen wird. 1, wenn die Kennwortrichtlinie wieder erzwungen wird.|  
|**IsExpired**|Gibt an, ob die Anmeldung abgelaufen ist.|  
|**IsLocked**|Gibt an, ob die Anmeldung gesperrt ist.|  
|**IsMustChange**|Gibt an, ob das Kennwort der Anmeldung beim nächsten Herstellen einer Verbindung geändert werden muss.|  
|**LockoutTime**|Gibt das Datum zurück, an dem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung gesperrt wurde, da die zulässige Anzahl fehlgeschlagener Anmeldeversuche überschritten wurde.|  
|**PasswordHash**|Gibt den Hash des Kennworts zurück.|  
|**PasswordLastSetTime**|Gibt das Datum zurück, an dem das aktuelle Kennwort festgelegt wurde.|  
|**PasswordHashAlgorithm**|Gibt den Algorithmus zurück, der zum Erstellen eines Hashwerts für das Kennwort verwendet wird.|  
  
## <a name="returns"></a>Rückgabewert  
 Der Datentyp hängt vom angeforderten Wert ab.  
  
 **IsLocked**, **IsExpired**, und **IsMustChange** sind vom Typ **Int**.  
  
-   1, wenn sich die Anmeldung im angegebenen Status befindet.  
  
-   0, wenn sich die Anmeldung nicht im angegebenen Status befindet.  
  
 **BadPasswordCount** und **HistoryLength** sind vom Typ **Int**.  
  
 **BadPasswordTime**, **LockoutTime**, **PasswordLastSetTime** sind vom Typ **"DateTime"**.  
  
 **PasswordHash** ist vom Typ **Varbinary**.  
  
 NULL, wenn es sich bei der Anmeldung nicht um eine gültige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung handelt.  
  
 **DaysUntilExpiration** ist vom Typ **Int**.  
  
-   0, wenn die Anmeldung abgelaufen ist oder an dem Tag abläuft, an dem die Abfrage ausgeführt wird.  
  
-   -1, wenn das Kennwort gemäß der lokalen Sicherheitsrichtlinie in Windows nie abläuft.  
  
-   NULL, wenn CHECK_POLICY oder CHECK_EXPIRATION für eine Anmeldung auf OFF festgelegt ist oder wenn das Betriebssystem die Kennwortrichtlinie nicht unterstützt.  
  
 **PasswordHashAlgorithm** ist vom Typ "int".  
  
-   0, wenn ein SQL7.0-Hash verwendet wird.  
  
-   1, wenn ein SHA-1-hash  
  
-   2, wenn ein SHA-2-Hash verwendet wird.  
  
-   NULL, wenn es sich bei der Anmeldung nicht um eine gültige SQL Server-Anmeldung handelt.  
  
## <a name="remarks"></a>Hinweise  
 Diese integrierte Funktion gibt Informationen zu den Kennwortrichtlinien-Einstellungen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung zurück. Die Namen der Eigenschaften sind nicht Groß-/Kleinschreibung beachtet, sodass wie Eigenschaftsnamen **BadPasswordCount** und **Badpasswordcount** äquivalent sind. Die Werte der **PasswordHash, PasswordHashAlgorithm**, und **PasswordLastSetTime** Eigenschaften stehen in allen unterstützten Konfigurationen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die anderen Eigenschaften jedoch nur verfügbar, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] läuft auf [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] und CHECK_POLICY und CHECK_EXPIRATION aktiviert sind. Weitere Informationen finden Sie unter [Password Policy](../../relational-databases/security/password-policy.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW-Berechtigung für die Anmeldung. Wenn der Kennworthash angefordert wird, ist auch die CONTROL SERVER-Berechtigung erforderlich.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-checking-whether-a-login-must-change-its-password"></a>A. Überprüfen, ob das Kennwort einer Anmeldung geändert werden muss  
 Im folgenden Beispiel wird überprüft, ob [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung `John3` Kennwort muss geändert werden beim nächsten Herstellen einer mit einer Instanz von Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT LOGINPROPERTY('John3', 'IsMustChange');  
GO  
```  
  
### <a name="b-checking-whether-a-login-is-locked-out"></a>B. Überprüfen, ob eine Anmeldung gesperrt ist  
 Im folgenden Beispiel wird überprüft, ob der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename `John3` gesperrt ist.  
  
```  
SELECT LOGINPROPERTY('John3', 'IsLocked');  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
  

