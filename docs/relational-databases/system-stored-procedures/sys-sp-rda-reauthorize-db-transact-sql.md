---
title: Sys. sp_rda_reauthorize_db (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_rda_reauthorize_db
- sp_rda_reauthorize_db_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.sp_rda_reauthorize_db stored procedure
ms.assetid: f6f3e4b2-8c72-4d23-a5de-fe671ca5c5cd
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b6e9f73c96cc07bfe442ac3104c4b1f4824596ed
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="syssprdareauthorizedb-transact-sql"></a>Sys. sp_rda_reauthorize_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Stellt die authentifizierte Verbindung zwischen einer lokalen Datenbank für Stretch und der Remotedatenbank aktiviert.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_rda_reauthorize_db @credential = @credential, @with_copy = @with_copy [ , @azure_servername = @azure_servername, @azure_databasename = @azure_databasename ]  
```  
  
## <a name="arguments"></a>Argumente  
 @credential = *@credential*  
 Ist die datenbankbezogenen Anmeldeinformationen der lokalen aktivierter Funktion Stretch-Datenbank zugeordnet.  
  
 @with_copy = *@with_copy*  
 Gibt an, ob eine Kopie der Remotedaten und Herstellen einer Verbindung mit der Kopie (empfohlen). *@with_copy*ist vom Datentyp bit.  
  
 @azure_servername = *@azure_servername*  
 Gibt den Namen des Azure-Servers, der die Remotedaten enthält. *@azure_servername*ist vom Datentyp Sysname.  
  
 @azure_databasename = *@azure_databasename*  
 Gibt den Namen der Azure-Datenbank, die die Remotedaten enthält. *@azure_databasename*ist vom Datentyp Sysname.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder >0 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert Db_owner-Berechtigungen.  
  
## <a name="remarks"></a>Hinweise  
 Bei der Ausführung [sp_rda_reauthorize_db (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) um mit der Azure-Remotedatenbank erneut herstellen, dieser Vorgang automatisch den Abfragemodus auf zurückgesetzt LOCAL_AND_REMOTE, dies ist das Standardverhalten für Stretch-Datenbank. D. h. zurückgeben Abfragen Ergebnisse lokale und Remotedaten.  
  
## <a name="example"></a>Beispiel  
 Im folgende Beispiel wird die authentifizierte Verbindung zwischen einer lokalen Datenbank für Stretch und der Remotedatenbank aktiviert wiederhergestellt. Es wird eine Kopie der Remotedaten (empfohlen) und stellt eine Verbindung her, auf die neue Kopie.  
  
```tsql  
DECLARE @credentialName nvarchar(128);   
SET @credentialName = N'<existing_database_scoped_credential_name>';   
EXEC sp_rda_reauthorize_db @credential = @credentialName, @with_copy = 1;  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. sp_rda_deauthorize_db &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
