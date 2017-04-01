---
title: "Anmeldeinformationen (Datenbankmodul) | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Prinzipale [SQL Server], Anmeldeinformationen"
  - "Schemas [SQL Server], Anmeldeinformationen"
  - "Berechtigungen [SQL Server], Anmeldeinformationen"
  - "Gruppen [SQL Server], Anmeldeinformationen"
  - "ALTER ANY CREDENTIAL-Berechtigung"
  - "Sicherheit [SQL Server], Anmeldeinformationen"
  - "Authentifizierung [SQL Server], Anmeldeinformationen"
  - "Benutzer [SQL Server], Anmeldeinformationen"
  - "Anmeldeinformationen [SQL Server], Informationen zu Anmeldeinformationen"
  - "Anmeldeinformationen [SQL Server]"
ms.assetid: c8df6022-e0b4-46b8-9670-3f86938d3177
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# Anmeldeinformationen (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

  Anmeldeinformationen sind in einem Datensatz gespeichert, in dem die Authentifizierungsinformationen (Anmeldeinformationen) enthalten sind, die zum Herstellen einer Verbindung mit einer Ressource außerhalb von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] erforderlich sind. Diese Informationen werden intern von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verwendet. Die meisten Anmeldeinformationen enthalten einen Windows-Benutzernamen und ein Kennwort.  
  
 Die in Anmeldeinformationen gespeicherten Informationen ermöglichen einem Benutzer, der eine Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] über die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Authentifizierung hergestellt hat, auf Ressourcen außerhalb der Serverinstanz zuzugreifen. Wenn es sich bei der externen Ressource um Windows handelt, wird der Benutzer als der in den Anmeldeinformationen angegebene Windows-Benutzer authentifiziert. Eine einzelne Anmeldung kann mehreren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldungen zugeordnet werden. Eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldung kann allerdings nur einer Anmeldung zugeordnet werden.  
  
 Informationen zu Anmeldeinformationen, die in der Masterdatenbank gespeichert sind und in der gesamten Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verwendet werden können, finden Sie unter [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md). Informationen zu Anmeldeinformationen, die von einer bestimmten Datenbank verwendet werden und mit dieser Datenbank portabel sind, finden Sie unter [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
 Systemanmeldeinformationen werden automatisch erstellt und mit bestimmten Endpunkten verbunden. Namen für Systemanmeldeinformationen beginnen mit zwei Nummernzeichen (##).  
  
 Weitere Informationen zu Anmeldeinformationen finden Sie in den Katalogansichten [sys.credentials](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) und [sys.database_credentials &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-credentials-transact-sql.md).  
  
## Verwandte Inhalte  
 [Erstellen von Anmeldeinformationen](../../../relational-databases/security/authentication-access/create-a-credential.md) [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md) [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
  
 [Sichern von SQL Server](../../../relational-databases/security/securing-sql-server.md)  
  
  