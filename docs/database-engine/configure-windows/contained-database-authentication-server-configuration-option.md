---
title: "Serverkonfigurationsoption „Contained Database Authentication“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- contained database, enabling
- contained database authentication option
ms.assetid: b80768d2-ac20-4035-a335-d9adb74b3f6e
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 27ec2c2ca3da987f9eb09c9620823f1bfe084bf1
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="contained-database-authentication-server-configuration-option"></a>Contained Database Authentication (Serverkonfigurationsoption)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Verwenden Sie die **contained database authentication** -Option, um in der Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]eigenständige Datenbanken zu aktivieren.  
  
 Mit dieser Serveroption können Sie **contained database authentication**steuern.  
  
-   Wenn **contained database authentication** für die Instanz deaktiviert (0) ist, können keine eigenständigen Datenbanken erstellt oder an das [!INCLUDE[ssDE](../../includes/ssde-md.md)]angefügt werden.  
  
-   Wenn **contained database authentication** für die Instanz aktiviert (1) ist, können eigenständige Datenbanken erstellt oder an das [!INCLUDE[ssDE](../../includes/ssde-md.md)]angefügt werden.  
  
 Eine eigenständige Datenbank schließt alle erforderlichen Datenbankeinstellungen und Metadaten zum Definieren der Datenbank ein, und ihre Konfiguration ist nicht von der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz abhängig, in der die Datenbank installiert ist. Benutzer können eine Verbindung mit der Datenbank herstellen, ohne dass sie bei der Anmeldung auf der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Ebene eine Authentifizierung durchführen. Das Isolieren der Datenbank vom Datenbankmodul ermöglicht das einfache Verschieben der Datenbank in eine andere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Dadurch, dass alle Datenbankeinstellungen in der Datenbank enthalten sind, können Datenbankbesitzer sämtliche Konfigurationseinstellungen für die Datenbank verwalten. Weitere Informationen zu eigenständigen Datenbanken finden Sie unter [Eigenständige Datenbanken](../../relational-databases/databases/contained-databases.md).  

> [!NOTE]
> Eigenständige Datenbanken sind für [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] und [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] immer aktiviert und können nicht deaktiviert werden.
  
 Wenn eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz über eigenständige Datenbanken verfügt, kann die Einstellung **contained database authentication** mit der **RECONFIGURE WITH OVERRIDE** -Anweisung auf 0 festgelegt werden. Indem **contained database authentication** auf 0 festgelegt wird, wird die Authentifizierung eigenständiger Datenbanken für diese Datenbanken deaktiviert.  
  
> [!IMPORTANT]  
>  Wenn eigenständige Datenbanken aktiviert sind, können Datenbankbenutzer mit der Berechtigung ALTER ANY USER, wie z. B. Mitglieder der Rollen db_owner und db_accessadmin Zugriff auf Datenbanken gewähren und auf diese Weise auch Zugriff auf die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gewähren. Das bedeutet, dass die Kontrolle über den Zugriff zum Server nicht mehr auf Mitglieder der festen Serverrollen „sysadmin“ und „securityadmin“ sowie Zugangsdaten mit den Serverebenenberechtigungen CONTROL SERVER und ALTER ANY LOGIN beschränkt ist. Bevor Sie eigenständige Datenbanken zulassen, sollten Sie die Risiken kennen, die eigenständige Datenbanken mit sich bringen. Weitere Informationen finden Sie unter [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden enthaltene Datenbanken für die [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz aktiviert.  
  
```sql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
