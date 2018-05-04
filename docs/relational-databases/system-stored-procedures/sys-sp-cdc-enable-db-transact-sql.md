---
title: sp_cdc_enable_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
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
- sp_cdc_enable_db_TSQL
- sp_cdc_enable_db
- sys.sp_cdc_enable_db
- sys.sp_cdc_enable_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_enable_db
- change data capture [SQL Server], enabling databases
- sp_cdc_enable_db
ms.assetid: 176d83b3-493d-43cd-800e-aa123c3bdf17
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: fa011ee5f2b5306ace7365e8ce8f0746d4b4e3d7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysspcdcenabledb-transact-sql"></a>sys.sp_cdc_enable_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aktiviert Change Data Capture für die aktuelle Datenbank. Diese Prozedur muss für eine Datenbank ausgeführt werden, bevor Tabellen in dieser Datenbank für Change Data Capture aktiviert werden können. Change Data Capture zeichnet an aktivierten Tabellen vorgenommene Einfüge-, Update- und Löschvorgänge auf und stellt Informationen zu den einzelnen Änderungen in einem leicht verarbeitbaren relationalen Format dar. Für die geänderten Zeilen werden Spaltendaten, die die Spaltenstruktur der nachverfolgten Quelltabelle widerspiegeln, sowie die Metadaten aufgezeichnet, die zur Anwendung der Änderungen in einer Zielumgebung erforderlich sind.  
  
> [!IMPORTANT]  
>  Change Data Capture ist nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.sp_cdc_enable_db  
```  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Change Data Capture kann nicht aktiviert werden, auf [Systemdatenbanken](../../relational-databases/databases/system-databases.md) oder Verteilungsdatenbanken.  
  
 sys.sp_cdc_enable_db erstellt die Change Data Capture-Objekte, deren Bereich datenbankweit ist, einschließlich von Metatabellen und DDL-Triggern. Außerdem erstellt der cdc-Schema und die cdc-Datenbankbenutzer und setzt die Is_cdc_enabled-Spalte für den Datenbankeintrag in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht auf 1.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle sysadmin.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird Change Data Capture aktiviert.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_db;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. sp_cdc_disable_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)  
  
  
