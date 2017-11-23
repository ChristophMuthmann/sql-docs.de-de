---
title: Sp_pdw_remove_network_credentials (SQL Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: c12696a2-5939-402b-9866-8a837ca4c0a3
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 30f35803c804b6e895bf5287cb864c9cc979f013
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sppdwremovenetworkcredentials-sql-data-warehouse"></a>Sp_pdw_remove_network_credentials (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Dadurch werden in gespeicherten Anmeldeinformationen für das Netzwerk entfernt [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] auf eine Dateifreigabe im Netzwerk zugreifen. Verwenden Sie diese gespeicherte Prozedur z. B. So entfernen Sie die Berechtigung für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Sicherung durchführen und Wiederherstellungsvorgänge auf einem Server, die sich in Ihrem eigenen Netzwerk befindet.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_remove_network_credentials 'target_server_name'  
```  
  
## <a name="arguments"></a>Argumente  
 "*Target_server_name*"  
 Gibt an, die Ziel-Serverhostnamen oder die IP-Adresse. Anmeldeinformationen für den Zugriff auf diesen Server aus entfernt [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Dies nicht ändern oder entfernen Sie alle Berechtigungen auf dem tatsächlichen Zielserver der von Ihr Team verwaltet wird.  
  
 *Target_server_name* als nvarchar(337) definiert ist.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert **ALTER SERVER STATE** Berechtigung.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Ein Fehler tritt auf, wenn Entfernen von Anmeldeinformationen auf den Knoten "Zugriffssteuerung" und alle Serverknoten nicht erfolgreich ist.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Diese gespeicherte Prozedur entfernt die Anmeldeinformationen für das Netzwerk aus dem NetworkService-Konto für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Das NetworkService-Konto ausgeführt wird, jede Instanz des SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf den Knoten "Zugriffssteuerung" und die Computeknoten. Z. B. bei ein Sicherungsvorgang ausgeführt wird, werden der Knoten "Zugriffssteuerung" und jeder Serverknoten verwenden die Anmeldeinformationen für das NetworkService-Konto auf den Zielserver zugreifen.  
  
## <a name="metadata"></a>Metadaten  
 Verwenden Sie zum Auflisten aller Anmeldeinformationen und überprüfen die Anmeldeinformationen wurden entfernt [sys.dm_pdw_network_credentials &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
 Verwenden Sie zum Hinzufügen von Anmeldeinformationen [Sp_pdw_add_network_credentials &#40; SQL Datawarehouse &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-remove-credentials-for-performing-a-database-backup"></a>A. Entfernen Sie die Anmeldeinformationen zum Ausführen einer datenbanksicherung  
 Im folgenden Beispiel wird die Benutzeranmeldeinformationen Namen und das Kennwort für den Zugriff auf dem Zielserver, der IP-Adresse 10.192.147.63 hat.  
  
```  
EXEC sp_pdw_remove_network_credentials '10.192.147.63';  
```  
  
  

