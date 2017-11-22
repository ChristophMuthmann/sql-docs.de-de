---
title: ALTER ENDPOINT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER ENDPOINT
- ALTER_ENDPOINT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- ALTER ENDPOINT statement
- modifying endpoints
- endpoints [SQL Server], modifying
ms.assetid: 70f35566-30cf-47c6-8394-dfe5d71629d3
caps.latest.revision: "56"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a035e71325993e088b9910d6538c8bdd61e03f7e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="alter-endpoint-transact-sql"></a>ALTER ENDPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Ermöglicht das Ändern eines vorhandenen Endpunktes auf die folgenden Arten:  
  
-   Durch Hinzufügen einer neuen Methode zu einem vorhandenen Endpunkt.  
  
-   Durch Ändern oder Löschen einer vorhandenen Methode aus dem Endpunkt.  
  
-   Durch Ändern der Eigenschaften eines Endpunkts.  
  
> [!NOTE]  
>  In diesem Abschnitt werden die Syntax und die Argumente beschrieben, die für ALTER ENDPOINT spezifisch sind. Beschreibungen der Argumente, die CREATE ENDPOINT- und ALTER ENDPOINT gemeinsam sind, finden Sie unter [CREATE ENDPOINT &#40; Transact-SQL &#41; ](../../t-sql/statements/create-endpoint-transact-sql.md).  
  
 Systemeigene XML-Webdienste (SOAP/HTTP-Endpunkte) wurden ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] entfernt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER ENDPOINT endPointName [ AUTHORIZATION login ]  
[ STATE = { STARTED | STOPPED | DISABLED } ]  
[ AS { TCP } ( <protocol_specific_items> ) ]  
[ FOR { TSQL | SERVICE_BROKER | DATABASE_MIRRORING } (  
   <language_specific_items>  
        ) ]  
  
<AS TCP_protocol_specific_arguments> ::=  
AS TCP (  
  LISTENER_PORT = listenerPort  
  [ [ , ] LISTENER_IP = ALL | ( 4-part-ip ) | ( "ip_address_v6" ) ]  
)  
<FOR SERVICE_BROKER_language_specific_arguments> ::=  
FOR SERVICE_BROKER (  
   [ AUTHENTICATION = {   
      WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]  
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
    } ]  
   [ , ENCRYPTION = { DISABLED   
       |   
         {{SUPPORTED | REQUIRED }   
       [ ALGORITHM { RC4 | AES | AES RC4 | RC4 AES } ] }   
   ]  
  
  [ , MESSAGE_FORWARDING = {ENABLED | DISABLED} ]  
  [ , MESSAGE_FORWARD_SIZE = forwardSize  
)  
  
<FOR DATABASE_MIRRORING_language_specific_arguments> ::=  
FOR DATABASE_MIRRORING (  
   [ AUTHENTICATION = {   
      WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]  
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
    } ]  
   [ , ENCRYPTION = { DISABLED   
       |   
         {{SUPPORTED | REQUIRED }   
       [ ALGORITHM { RC4 | AES | AES RC4 | RC4 AES } ] }   
    ]   
   [ , ] ROLE = { WITNESS | PARTNER | ALL }  
)  
  
```  
  
## <a name="arguments"></a>Argumente  
  
> [!NOTE]  
>  Die folgenden Argumente gelten nur für ALTER ENDPOINT. Beschreibungen der restlichen Argumente finden Sie [CREATE ENDPOINT &#40; Transact-SQL &#41; ](../../t-sql/statements/create-endpoint-transact-sql.md).  
  
 **AS** { **TCP** }  
 Sie können das Transportprotokoll mit nicht ändern **ALTER ENDPOINT**.  
  
 **Autorisierung** *Anmeldung*  
 Die **Autorisierung** Option ist nicht verfügbar in **ALTER ENDPOINT**. Besitz kann nur zugewiesen werden, wenn der Endpunkt erstellt wird.  
  
 **FÜR** { **TSQL** | **SERVICE_BROKER** | **DATABASE_MIRRORING** }  
 Sie können den Nutzlasttyp mit nicht ändern **ALTER ENDPOINT**.  
  
## <a name="remarks"></a>Hinweise  
 Geben Sie bei Verwendung von ALTER ENDPOINT nur die zu aktualisierenden Parameter an. Alle Eigenschaften eines vorhandenen Endpunktes bleiben unverändert, es sei denn, Sie ändern diese explizit.  
  
 ENDPOINT DDL-Anweisungen können nicht innerhalb einer Benutzertransaktion ausgeführt werden.  
  
 Informationen zum Auswählen eines Verschlüsselungsalgorithmus zur Verwendung mit einem Endpunkt finden Sie unter [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md).  
  
> [!NOTE]  
>  Der RC4-Algorithmus wird nur aus Gründen der Abwärtskompatibilität unterstützt. Neues Material kann nur mit RC4 oder RC4_128 verschlüsselt werden, wenn die Datenbank den Kompatibilitätsgrad 90 oder 100 besitzt. (Nicht empfohlen.) Verwenden Sie stattdessen einen neueren Algorithmus, z. B. einen der AES-Algorithmen. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und höhere Versionen mit RC4 oder RC4_128 verschlüsseltes Material kann entschlüsselt werden in jedem Kompatibilitätsgrad.  
>   
>  RC4 ist ein relativ schwacher Algorithmus, und AES ist ein relativ starker Algorithmus. AES ist jedoch deutlich langsamer als RC4. Wenn Sicherheit für Sie eine höhere Priorität besitzt als Geschwindigkeit, ist es empfehlenswert, AES zu verwenden.  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer muss ein Mitglied der **Sysadmin** festen Serverrolle, der Besitzer des Endpunktes sein, oder die ALTER ANY ENDPOINT-Berechtigung erteilt worden.  
  
 Sie können den Besitz für einen vorhandenen Endpunkt ändern, indem Sie die ALTER AUTHORIZATION-Anweisung verwenden. Weitere Informationen finden Sie unter [ALTER AUTHORIZATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 Weitere Informationen finden Sie unter [GRANT (Endpunktberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [DROP ENDPOINT (Transact-SQL)](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
