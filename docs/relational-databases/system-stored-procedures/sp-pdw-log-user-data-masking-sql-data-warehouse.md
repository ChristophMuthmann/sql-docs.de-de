---
title: Sp_pdw_log_user_data_masking (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-data-warehouse
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 27b303f1e78826e74fb94f254a0c2e3692fbef7e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sppdwloguserdatamasking-sql-data-warehouse"></a>Sp_pdw_log_user_data_masking (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Verwendung **Sp_pdw_log_user_data_masking** zum Aktivieren von Benutzerdaten maskiert [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle. Benutzer datenmaskierung wirkt sich auf die Anweisungen für alle Datenbanken auf dem Gerät.  
  
> [!IMPORTANT]  
>  Die [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle betroffen **Sp_pdw_log_user_data_masking** sind bestimmte [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle. **Sp_pdw_log_user_data_masking** wirkt sich nicht auf die Datenbank-Transaktionsprotokolle oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Fehlerprotokolle.  
  
 **Hintergrund:** In der Standardkonfiguration [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle enthalten vollständige [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen, und es in einigen Fällen enthalten Benutzerdaten in Operationen wie z. B. **einfügen**,  **UPDATE**, und **wählen** Anweisungen. Wenn auf dem Gerät ein Problem vorliegt ermöglicht dies die Analyse der Bedingungen, die das Problem ohne Bedarf an, das Problem zu reproduzieren verursacht hat. Um zu verhindern, dass die Benutzerdaten in geschriebenen [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle, Kunden können die Benutzer die datenmaskierung aktivieren, indem Sie mit dieser gespeicherten Prozedur. Die Anweisungen werden noch geschrieben werden, um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle jedoch alle die Literale in Anweisungen, die Benutzerdaten enthalten möglicherweise werden maskierte; durch einige vordefinierte Konstante Werte ersetzt.  
  
 Wenn transparente datenverschlüsselung auf dem Gerät aktiviert ist, der den Benutzerdaten in maskiert [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle ist automatisch aktiviert.  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```  
  
#### <a name="parameters"></a>Parameter  
 [ **@masking_mode=** ] *masking_mode*  
 Bestimmt, ob transparent Data Encryption Protokoll Maskieren von Benutzerdaten aktiviert ist. *Masking_mode* ist **Int**, und kann einen der folgenden Werte:  
  
-   0 = deaktiviert, Benutzer, die Daten, in angezeigt der [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle.  
  
-   1 = aktiviert, Benutzer, die DDL-Anweisungen Data, in angezeigt der [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle, aber die Benutzerdaten maskiert wird.  
  
-   2 = Anweisungen, die mit Benutzerdaten werden nicht in der [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle.  
  
 Ausführen von **Sp_pdw_ Log_user_data_masking** ohne Parameter gibt den aktuellen Status von TDE Protokoll Benutzer die datenmaskierung auf dem Gerät als skalare Resultset zurück.  
  
## <a name="remarks"></a>Hinweise  
 Benutzerdaten maskiert [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitäten protokolliert aktiviert die Ersetzung von literalen mit vordefinierten Konstanten Werten in **wählen** und DML-Anweisungen, wie sie die Benutzerdaten enthalten können. Festlegen von *Masking_mode* auf 1 wird nicht maskiert Metadaten, z. B. Spaltennamen und Tabellennamen auf Richtigkeit. Festlegen von *Masking_mode* entfernt Sie 2-Anweisungen mit Metadaten, z. B. Spaltennamen und Tabellennamen auf Richtigkeit.  
  
 Benutzerdaten maskiert [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle auf folgende Weise implementiert wird:  
  
-   TDE und Benutzer datenmaskierung [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle sind standardmäßig deaktiviert. Die Anweisungen werden nicht automatisch maskiert werden, wenn die Verschlüsselung der Datenbank auf dem Gerät nicht aktiviert ist.  
  
-   Aktivieren von TDE automatisch auf dem Gerät aktiviert der Benutzer die datenmaskierung in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle.  
  
-   Deaktivieren von TDE wirkt sich nicht auf Benutzerdaten maskiert [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle.  
  
-   Sie können Benutzerdaten maskiert explizit aktivieren [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Aktivitätsprotokolle mithilfe der **Sp_pdw_log_user_data_masking** Prozedur.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Sysadmin** feste Datenbankrolle oder **CONTROL SERVER** Berechtigung.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird TDE Benutzer Protokolldaten auf dem Gerät maskiert.  
  
```  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_pdw_database_encryption aktiviert werden &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  
