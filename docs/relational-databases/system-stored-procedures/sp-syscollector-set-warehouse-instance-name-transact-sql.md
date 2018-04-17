---
title: Sp_syscollector_set_warehouse_instance_name (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
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
- sp_syscollector_set_warehouse_instance_name_TSQL
- sp_syscollector_set_warehouse_instance_name
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_set_warehouse_instance_name
ms.assetid: 5320fcd4-bed1-468f-b784-a5e10fcfaeb6
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f6a86d97bd56cc85758b955327900d6c830d232
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spsyscollectorsetwarehouseinstancename-transact-sql"></a>sp_syscollector_set_warehouse_instance_name (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Instanznamen für die Verbindungszeichenfolge an, mit der die Verbindung zum Verwaltungs-Data Warehouse hergestellt wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_syscollector_set_warehouse_instance_name [ @instance_name = ] 'instance_name'  
```  
  
## <a name="arguments"></a>Argumente  
 [ @instance_name =] '*Instance_name*"  
 Der Instanzenname. *Instanzname* ist **Sysname** und Standardwerte für die lokale Instanz, wenn der Wert NULL.  
  
> **Hinweis:***Instance_name* muss der vollqualifizierte Instanzname sein, besteht aus den Computernamen und den Instanznamen im Format *ComputerName* \\ *InstanceName*.    
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Sie müssen den Datensammler deaktivieren, bevor Sie die Konfiguration für diesen gesamten Datensammler ändern. Dieser Vorgang schlägt fehl, wenn der Datensammler aktiviert ist.  
  
 Um den aktuellen Instanznamen anzuzeigen, Fragen den [Syscollector_config_store](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md) -Systemsicht.  
  
## <a name="permissions"></a>Berechtigungen  
 Damit diese Prozedur ausgeführt werden kann, ist die Mitgliedschaft in der festen Datenbankrolle dc_admin (mit EXECUTE-Berechtigung) erforderlich.  
  
## <a name="examples"></a>Beispiele  
 In dem folgenden Beispiel wird veranschaulicht, wie sich der Datensammler zur Verwendung einer Verwaltungs-Data Warehouse-Instanz auf einem Remoteserver konfigurieren lässt. In diesem Beispiel erhält der Remoteserver den Namen `RemoteSERVER`, und die Datenbank ist auf der Standardinstanz installiert.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_set_warehouse_instance_name N'RemoteSERVER'; -- the default instance is assumed on the remote server  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für den Datensammler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [syscollector_config_store &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)  
  
  
