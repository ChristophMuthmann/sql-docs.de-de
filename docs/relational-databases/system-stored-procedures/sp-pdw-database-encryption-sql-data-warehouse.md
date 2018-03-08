---
title: sp_pdw_database_encryption aktiviert werden (SQL Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e63022bd135d7c5fc78dd717b6a0bdd27dc5311
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sppdwdatabaseencryption-sql-data-warehouse"></a>sp_pdw_database_encryption aktiviert werden (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Verwendung **sp_pdw_database_encryption aktiviert werden** So aktivieren Sie für die transparente datenverschlüsselung auf eine [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Appliance. Wenn **sp_pdw_database_encryption aktiviert werden** auf 1 festgelegt, verwendet der **ALTER DATABASE** Anweisung, um eine Datenbank mit TDE zu verschlüsseln.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  
  
#### <a name="parameters"></a>Parameter  
 [ **@enabled=** ] *enabled*  
 Bestimmt, ob die transparente datenverschlüsselung aktiviert ist. *aktiviert* ist **Int**, und kann einen der folgenden Werte:  
  
-   0 = Deaktiviert  
  
-   1 = Aktiviert  
  
 Ausführen von **sp_pdw_database_encryption aktiviert werden** ohne Parameter gibt den aktuellen Status von TDE in der Anwendung als skalare Resultset zurück: 0 für deaktiviert oder 1 für aktiviert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Wenn der TDE aktiviert ist, mit **sp_pdw_database_encryption aktiviert werden**, die Tempdb-Datenbank gelöscht, neu erstellt und verschlüsselt. Aus diesem Grund kann nicht auf eine Einheit der TDE aktiviert werden, während andere aktive Sitzungen, die mithilfe von ' tempdb ' vorhanden sind. Aktivieren bzw. deaktivieren TDE für eine Einheit ist eine Aktion, die den Zustand der Anwendung in den meisten Fällen ändert muss einmal in der Lebensdauer der Anwendung ausgeführt werden und sollte ausgeführt werden, wenn kein Datenverkehr auf dem Gerät vorhanden ist.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Sysadmin** feste Datenbankrolle oder **CONTROL SERVER** Berechtigung.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden TDE auf dem Gerät aktiviert.  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
