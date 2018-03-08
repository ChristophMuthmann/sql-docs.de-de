---
title: Sp_pdw_add_network_credentials (SQL Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0729eeff-ac7e-43f0-80fa-ff5346a75985
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87034c1db40e5762441871cc347eaf37d2c56ea3
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sppdwaddnetworkcredentials-sql-data-warehouse"></a>Sp_pdw_add_network_credentials (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Speichert Anmeldeinformationen für das Netzwerk in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und ordnet sie einem Server. Verwenden Sie diese gespeicherte Prozedur z. B. gewähren [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] entsprechenden Lese-/Schreibberechtigungen zu datenbanksicherung auszuführen und Wiederherstellungsvorgänge auf einem Zielserver oder zum Erstellen einer Sicherung eines Zertifikats für TDE verwendet.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_add_network_credentials 'target_server_name',  'user_name', ꞌpasswordꞌ  
```  
  
## <a name="arguments"></a>Argumente  
 '*target_server_name*'  
 Gibt an, die Ziel-Serverhostnamen oder die IP-Adresse. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]wird für diesen Server erlauben mithilfe der Benutzername und Kennwort-Anmeldeinformationen, die an diese gespeicherte Prozedur übergeben wird.  
  
 Verwenden Sie über das InfiniBand-Netzwerk herstellen möchten die InfiniBand IP-Adresse des Zielservers ein.  
  
 *Target_server_name* als nvarchar(337) definiert ist.  
  
 "*User_name*"  
 Gibt an, der Benutzername, der über Berechtigungen zum Zugriff auf den Zielserver verfügt. Wenn Anmeldeinformationen für den Zielserver bereits vorhanden sind, werden sie auf die neuen Anmeldeinformationen aktualisiert.  
  
 *USER_NAME* als Nvarchar (513) definiert ist.  
  
 "*Kennwort*ꞌ auf  
 Gibt das Kennwort für *User_name*.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert **ALTER SERVER STATE** Berechtigung.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Ein Fehler tritt auf, wenn Hinzufügen von Anmeldeinformationen auf den Knoten "Zugriffssteuerung" und alle Serverknoten nicht erfolgreich ist.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Diese gespeicherte Prozedur fügt Anmeldeinformationen für das Netzwerk auf das NetworkService-Konto für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Das NetworkService-Konto ausgeführt wird, jede Instanz des SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf den Knoten "Zugriffssteuerung" und die Computeknoten. Z. B. wenn ein Sicherungsvorgang ausgeführt wird, verwendet der Knoten "Zugriffssteuerung" und jeder Serverknoten die Anmeldeinformationen für das NetworkService-Konto lesen und Schreibberechtigungen für den Zielserver.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-add-credentials-for-performing-a-database-backup"></a>A. Hinzufügen von Anmeldeinformationen zum Ausführen einer datenbanksicherung  
 Im folgenden Beispiel wird die Benutzeranmeldeinformationen Namen und das Kennwort für die Domäne Benutzer Seattle\david mit einem Zielserver, der IP-Adresse 10.172.63.255 verfügt. Der Benutzer Seattle\david verfügt über Lese-/Schreibberechtigungen auf dem Zielserver. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]Diese Anmeldeinformationen gespeichert wird und zum Lesen und Schreiben in und aus dem Zielserver bei Bedarf für die Sicherung und Wiederherstellungsvorgänge verwenden.  
  
```  
EXEC sp_pdw_add_network_credentials '10.172.63.255', 'seattle\david', '********';  
```  
  
 Der backup-Befehl erfordert, dass der Servername als eine IP-Adresse eingegeben werden.  
  
> [!NOTE]  
>  Zum Durchführen der Sicherung über InfiniBand unbedingt die InfiniBand IP-Adresse des dem backup-Server verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_pdw_remove_network_credentials &#40; SQL Datawarehouse &#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
  

