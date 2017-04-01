---
title: "Sicherungsf&#228;hige Elemente | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "10/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.roleproperties.selectobject.f1"
helpviewer_keywords: 
  - "Sicherungsfähige Elemente [SQL Server]"
  - "Schemas [SQL Server], sicherungsfähige Elemente"
  - "Sicherungsfähige Elemente der Datenbank [SQL Server]"
  - "Hierarchien [SQL Server], sicherungsfähige Elemente"
  - "Sicherungsfähige Elemente des Servers [SQL Server]"
ms.assetid: bfa748f0-70b0-453c-870a-04b7b205b9ff
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Sicherungsf&#228;hige Elemente
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Als sicherungsfähige Elemente werden Ressourcen bezeichnet, auf die der Zugriff durch das Autorisierungssystem von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] reguliert wird. Eine Tabelle ist z. B. ein sicherungsfähiges Element. Bestimmte sicherungsfähige Elemente können sich innerhalb anderer Elemente befinden. Dadurch entstehen geschachtelte Hierarchien, so genannte "Bereiche", die selbst sicherungsfähig sind. Sicherungsfähige Bereiche sind **Server**, **Datenbank**und **Schema**.  
  
## Sicherungsfähiger Bereich: Server  
 Der sicherungsfähige Bereich **Server** enthält die folgenden sicherungsfähigen Elemente:  
  
-   Verfügbarkeitsgruppe  
  
-   Endpunkt  
  
-   Anmeldename  
  
-   Serverrolle  
  
-   Datenbank  
  
## Sicherungsfähiger Bereich: Datenbank  
 Der sicherungsfähige Bereich **Datenbank** enthält die folgenden sicherungsfähigen Elemente:  
  
-   Anwendungsrolle  
  
-   Assembly  
  
-   Asymmetrischer Schlüssel  
  
-   Zertifikat  
  
-   Vertrag  
  
-   Volltextkatalog  
  
-   Volltextstoppliste  
  
-   Nachrichtentyp  
  
-   Remotedienstbindung  
  
-   (Datenbank-)Rolle  
  
-   Route  
  
-   Schema  
  
-   Sucheigenschaftenliste  
  
-   Dienst  
  
-   Symmetrischer Schlüssel  
  
-   Benutzer  
  
## Sicherungsfähiger Bereich: Schema  
 Der sicherungsfähige Bereich **Schema** enthält die folgenden sicherungsfähigen Elemente:  
  
-   Typ  
  
-   XML-Schemaauflistung  
  
-   Objekt – Die Objektklasse enthält die folgenden Elemente:  
  
    -   Aggregat  
  
    -   Funktion  
  
    -   Verfahren  
  
    -   Warteschlange  
  
    -   Synonym  
  
    -   Tabelle  
  
    -   Sicht 
    
    -   Externe Tabelle 
  
## Steuern von Zugriff auf ein sicherungsfähiges Element  
 Die Entität, die die Berechtigung für ein sicherungsfähiges Element empfängt, wird als Prinzipal bezeichnet. Die am häufigsten auftretenden Prinzipale sind Anmeldedaten und Datenbankbenutzer. Der Zugriff auf sicherungsfähige Elemente wird durch das Erteilen oder Verweigern von Berechtigungen gesteuert, oder durch das Hinzufügen von Anmeldedaten und Benutzern zu Rollen, die über Zugriff verfügen. Informationen zum Steuern von Berechtigungen finden Sie unter [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md), [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md), [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md), [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) und [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md).  
  
> [!CAUTION]  
>  Die Standardberechtigungen, die Systemobjekten zum Zeitpunkt der Installation erteilt wurden, werden sorgfältig bezüglich möglicher Bedrohungen ausgewertet und müssen nicht im Rahmen der Härtung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installation geändert werden. Alle Änderungen an den Berechtigungen für Systemobjekte können die Funktionalität einschränken oder unterbrechen und potenziell dazu führen, dass Ihre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installation einen nicht unterstützten Zustand aufweist.  
  
## Verwandte Inhalte  
 [Erste Schritte mit Berechtigungen für das Datenbankmodul](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
 [Sichern von SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
 [sys.server_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
 [sys.sql_logins &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)  
  
  