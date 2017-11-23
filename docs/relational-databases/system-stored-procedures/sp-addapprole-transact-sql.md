---
title: Sp_addapprole (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_addapprole_TSQL
- sp_addapprole
dev_langs: TSQL
helpviewer_keywords: sp_addapprole
ms.assetid: 24200295-9a54-4cab-9922-fb2e88632721
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ed5b4ce0cc3a72ceca252ecfab9e83c6967b4eb1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spaddapprole-transact-sql"></a>sp_addapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt der aktuellen Datenbank eine Anwendungsrolle hinzu.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md) stattdessen.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addapprole [ @rolename = ] 'role' , [ @password = ] 'password'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@rolename =** ] **"***Rolle***"**  
 Der Name der neuen Anwendungsrolle. *Rolle* ist **Sysname**, hat keinen Standardwert. *Rolle* muss ein gültiger Bezeichner sein und darf nicht bereits in der aktuellen Datenbank vorhanden sein.  
  
 Namen von Anwendungsrollen können zwischen 1 und 128 Zeichen (Buchstaben, Sonderzeichen und Ziffern) enthalten. Rollennamen können einen umgekehrten Schrägstrich enthalten (\\) noch NULL oder eine leere Zeichenfolge (").  
  
 [  **@password =** ] **"***Kennwort***"**  
 Das für die Aktivierung der Anwendungsrolle erforderliche Kennwort. *Kennwort* ist **Sysname**, hat keinen Standardwert. *Kennwort* darf nicht NULL sein.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterscheiden sich Benutzer (und Rollen) nicht vollständig von Schemas. Seit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] unterscheiden sich Schemas und Rollen vollständig. Diese neue Architektur spiegelt sich im Verhalten von CREATE APPLICATION ROLE wider. Diese Anweisung hat Vorrang vor **Sp_addapprole**.  
  
 Um die Abwärtskompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **Sp_addapprole** wird Folgendes:  
  
-   Wenn nicht bereits ein Schema mit dem gleichen Namen wie die Anwendungsrolle vorhanden ist, wird ein solches Schema erstellt. Das neue Schema ist im Besitz der Anwendungsrolle und wird als Standardschema der Anwendungsrolle verwendet.  
  
-   Wenn bereits ein Schema mit dem gleichen Namen wie die Anwendungsrolle vorhanden ist, erzeugt die Prozedur einen Fehler.  
  
-   Kennwortkomplexität wird nicht durch überprüft **Sp_addapprole**. Von CREATE APPLICATION ROLE hingegen wird die Kennwortkomplexität überprüft.  
  
 Der Parameter *Kennwort* wird als unidirektionaler Hash gespeichert.  
  
 Die **Sp_addapprole** gespeicherte Prozedur kann nicht innerhalb einer benutzerdefinierten Transaktion ausgeführt werden.  
  
> [!IMPORTANT]  
>  Microsoft ODBC **verschlüsseln** Option wird nicht unterstützt, indem **SqlClient**. Sofern möglich, sollten Benutzer zur Eingabe der Anmeldeinformationen für Anwendungsrollen zur Laufzeit aufgefordert werden. Die Anmeldeinformationen sollten nicht in einer Datei gespeichert werden. Wenn Anmeldeinformationen persistent gespeichert werden müssen, sollten Sie sie mithilfe der CryptoAPI-Funktionen verschlüsseln.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY APPLICATION ROLE-Berechtigung in der Datenbank. Ist nicht bereits ein Schema mit dem gleichen Namen und Besitzer wie die neue Rolle vorhanden, ist auch die CREATE SCHEMA-Berechtigung für die Datenbank erforderlich.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die neue Anwendungsrolle `SalesApp` mit dem Kennwort `x97898jLJfcooFUYLKm387gf3` auf die aktuelle Datenbank.  
  
```  
EXEC sp_addapprole 'SalesApp', 'x97898jLJfcooFUYLKm387gf3' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie APPLICATION ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)  
  
  
