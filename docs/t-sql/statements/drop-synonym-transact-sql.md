---
title: DROP SYNONYM (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP SYNONYM
- DROP_SYNONYM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting synonyms
- synonyms [SQL Server], removing
- removing synonyms
- DROP SYNONYM statement
- dropping synonyms
ms.assetid: 23578932-e4de-4c39-a5a0-ce45139c4269
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cdfe95b14e8005cb4086b909aea6a5cfb0bbd0cc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="drop-synonym-transact-sql"></a>DROP SYNONYM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Entfernt ein Synonym aus einem angegebenen Schema.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP SYNONYM [ IF EXISTS ] [ schema. ] synonym_name  
```  
  
## <a name="arguments"></a>Argumente  
 *IF EXISTS*  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).
  
 Löscht das Synonym nur, wenn dieses bereits vorhanden ist.  
  
 *schema*  
 Gibt das Schema an, in dem das Synonym vorhanden ist. Wird kein Schema angegeben, verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das Standardschema des aktuellen Benutzers.  
  
 *synonym_name*  
 Der Name des Synonyms, das gelöscht werden soll.  
  
## <a name="remarks"></a>Remarks  
 Verweise auf Synonyme sind nicht an ein Schema gebunden. Deshalb können Sie ein Synonym jederzeit löschen. Verweise auf gelöschte Synonyme werden erst zur Laufzeit gefunden.  
  
 In dynamischem SQL können Synonyme erstellt und gelöscht werden. Außerdem kann auf sie verwiesen werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Löschen eines Synonyms muss ein Benutzer mindestens eine der folgenden Bedingungen erfüllen. Folgende Voraussetzungen müssen erfüllt sein:  
  
-   Der Benutzer muss der aktuelle Besitzer eines Synonyms sein.  
  
-   Der Benutzer muss ein Berechtigter für CONTROL für ein Synonym sein.  
  
-   Der Benutzer muss ein Berechtigter sein, der über die ALTER SCHEMA-Berechtigung für das enthaltene Schema verfügt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird zuerst das Synonym `MyProduct` erstellt und dann gelöscht.  
  
```  
USE tempdb;  
GO  
-- Create a synonym for the Product table in AdventureWorks2012.  
CREATE SYNONYM MyProduct  
FOR AdventureWorks2012.Production.Product;  
GO  
-- Drop synonym MyProduct.  
USE tempdb;  
GO  
DROP SYNONYM MyProduct;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
