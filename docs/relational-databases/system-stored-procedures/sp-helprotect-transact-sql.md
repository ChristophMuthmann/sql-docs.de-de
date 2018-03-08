---
title: Sp_helprotect (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helprotect
- sp_helprotect_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helprotect
ms.assetid: faaa3e40-1c95-43c2-9fdc-c61a1d3cc0c3
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7c254488d42940c2f88b395082db1cd0079f79f3
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sphelprotect-transact-sql"></a>sp_helprotect (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt einen Bericht mit Informationen zu den Benutzerberechtigungen für ein Objekt oder zu Anweisungsberechtigungen in der aktuellen Datenbank zurück.  
  
> [!IMPORTANT]  
>  **Sp_helprotect** gibt keine Informationen zu sicherungsfähigen Elementen, die in eingeführt wurden zurück [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Verwendung [database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) und [Fn_builtin_permissions](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md) stattdessen.  
  
 Berechtigungen, die immer festen Serverrollen oder Datenbankrollen zugewiesen sind, werden nicht aufgeführt. Anmeldenamen oder Benutzer, die Berechtigungen auf Grundlage ihrer Rollenmitgliedschaft erhalten, sind nicht enthalten.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helprotect [ [ @name = ] 'object_statement' ]   
     [ , [ @username = ] 'security_account' ]   
     [ , [ @grantorname = ] 'grantor' ]   
     [ , [ @permissionarea = ] 'type' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@name =** ] **"***Object_statement***"**  
 Der Name des Objekts in der aktuellen Datenbank oder der Name einer Anweisung mit den auszugebenden Berechtigungen.  *Object_statement* ist **nvarchar(776)**, hat den Standardwert NULL, womit alle Objekt- und Anweisungsberechtigungen Berechtigungen. Handelt es sich um ein Objekt (Tabelle, Sicht, gespeicherte Prozedur oder erweiterte gespeicherte Prozedur), muss dieses ein gültiges Objekt in der aktuellen Datenbank sein. Der Objektname kann einen besitzerqualifizierer im Format *Besitzer***.** *Objekt*.  
  
 Wenn *Object_statement* ist eine Anweisung einer CREATE-Anweisung sind möglich.  
  
 [  **@username =** ] **"***Security_account***"**  
 Der Name des Prinzipals, für den Berechtigungen zurückgegeben werden. *Security_account* ist **Sysname**, hat den Standardwert NULL, womit alle Prinzipale in der aktuellen Datenbank zurückgegeben. *Security_account* muss in der aktuellen Datenbank vorhanden sein.  
  
 [  **@grantorname =** ] **"***Grantor***"**  
 Der Name des Prinzipals, der die Berechtigungen gewährt hat. *GRANTOR* ist **Sysname**, hat den Standardwert NULL, womit alle Informationen für Berechtigungen, die von einem Prinzipal in der Datenbank zurückgegeben.  
  
 [  **@permissionarea =** ] **"***Typ***"**  
 Ist eine Zeichenfolge, die angibt, ob die Berechtigungen für Modellobjekte anzeigen (Zeichenfolge **o**), Anweisungsberechtigungen (Zeichenfolge **s**), oder beide (**os**). *Typ* ist **varchar(10)**, hat den Standardwert **os**. *Typ* kann eine beliebige Kombination von **o** und **s**mit oder ohne Kommas bzw. Leerzeichen zwischen **o** und **s**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Besitzer**|**sysname**|Name des Objektbesitzers.|  
|**Objekt**|**sysname**|Name des Objekts.|  
|**Empfänger**|**sysname**|Name des Prinzipals, dem Berechtigungen erteilt wurden.|  
|**Grantor**|**sysname**|Name des Prinzipals, der dem angegebenen Empfänger (Grantee) Berechtigungen erteilt hat.|  
|**ProtectType**|**nvarchar(10)**|Name des Schutztyps:<br /><br /> GRANT REVOKE|  
|**Aktion**|**nvarchar(60)**|Der Name der Berechtigung. Gültige Berechtigungsanweisungen richten sich nach dem Objekttyp.|  
|**Column**|**sysname**|Berechtigungstyp:<br /><br /> All = Berechtigung gilt für alle aktuellen Spalten des Objekts.<br /><br /> New = Berechtigung gilt für alle neuen Spalten, die später (mithilfe der ALTER-Anweisung) für das Objekt geändert werden.<br /><br /> All+New = Kombination aus All und New.<br /><br /> Gibt einen Punkt zurück, wenn der Berechtigungstyp nicht für Spalten gilt.|  
  
## <a name="remarks"></a>Hinweise  
 Alle Parameter in der folgenden Prozedur sind optional. Wenn Sie `sp_helprotect` ohne Parameter ausführen, werden alle Berechtigungen angezeigt, die in der aktuellen Datenbank erteilt oder verweigert wurden.  
  
 Wenn einige, aber nicht alle Parameter angegeben werden, verwenden Sie benannte Parameter zum Identifizieren des entsprechenden Parameters oder aber `NULL` als Platzhalter. Führen Sie z. B. folgende Zeile aus, um alle Berechtigungen für den Datenbankbesitzer (`dbo`) auszugeben, der der Berechtigende (GRANTOR) ist:  
  
```  
EXEC sp_helprotect NULL, NULL, dbo;  
```  
  
 oder  
  
```  
EXEC sp_helprotect @grantorname = 'dbo';  
```  
  
 Der Ausgabebericht wird nach Berechtigungskategorie, Besitzer, Objekt, Empfänger (Grantee), Berechtigendem (Grantor), Schutztypkategorie, Schutztyp, Aktion und spaltensequenzieller ID sortiert.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
 Die zurückgegebenen Informationen unterliegen den Einschränkungen, die für den Zugriff auf Metadaten gelten. Entitäten, für die der Prinzipal keine Berechtigungen besitzt, werden nicht angezeigt. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-listing-the-permissions-for-a-table"></a>A. Auflisten der Berechtigungen für eine Tabelle  
 Im folgenden Beispiel werden die Berechtigungen für die `titles`-Tabelle aufgelistet.  
  
```  
EXEC sp_helprotect 'titles';  
```  
  
### <a name="b-listing-the-permissions-for-a-user"></a>B. Auflisten der Berechtigungen für einen Benutzer  
 Im folgenden Beispiel werden alle Berechtigungen des Benutzers `Judy` für die aktuelle Datenbank aufgelistet.  
  
```  
EXEC sp_helprotect NULL, 'Judy';  
```  
  
### <a name="c-listing-the-permissions-granted-by-a-specific-user"></a>C. Auflisten der von einem bestimmten Benutzer erteilten Berechtigungen  
 Im folgenden Beispiel werden alle Berechtigungen aufgelistet, die von Benutzer `Judy` in der aktuellen Datenbank erteilt wurden. Dabei wird `NULL` als Platzhalter für die fehlenden Parameter verwendet.  
  
```  
EXEC sp_helprotect NULL, NULL, 'Judy';  
```  
  
### <a name="d-listing-the-statement-permissions-only"></a>D. Ausschließliches Auflisten der Anweisungsberechtigungen  
 Im folgenden Beispiel werden alle Anweisungsberechtigungen in der aktuellen Datenbank aufgelistet. Dabei wird `NULL` als Platzhalter für die fehlenden Parameter verwendet.  
  
```  
EXEC sp_helprotect NULL, NULL, NULL, 's';   
```  
  
### <a name="e-listing-the-permissions-for-a-create-statement"></a>e. Auflisten der Berechtigungen für eine CREATE-Anweisung  
 Im folgenden Beispiel werden alle Benutzer aufgelistet, denen die CREATE TABLE-Berechtigung erteilt wurde.  
  
```  
EXEC sp_helprotect @name = 'CREATE TABLE';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
