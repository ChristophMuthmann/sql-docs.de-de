---
title: Anmeldeinformationen (Datenbankmodul) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- principals [SQL Server], credentials
- schemas [SQL Server], credentials
- permissions [SQL Server], credentials
- groups [SQL Server], credentials
- ALTER ANY CREDENTIAL permission
- security [SQL Server], credentials
- authentication [SQL Server], credentials
- users [SQL Server], credentials
- credentials [SQL Server], about credentials
- credentials [SQL Server]
ms.assetid: c8df6022-e0b4-46b8-9670-3f86938d3177
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 62f6c7af449631e7ae308e1f69858257e0bc3420
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="credentials-database-engine"></a>Anmeldeinformationen (Datenbankmodul)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Anmeldeinformationen sind in einem Datensatz gespeichert, in dem die Authentifizierungsinformationen (Anmeldeinformationen) enthalten sind, die zum Herstellen einer Verbindung mit einer Ressource außerhalb von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]erforderlich sind. Diese Informationen werden intern von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]verwendet. Die meisten Anmeldeinformationen enthalten einen Windows-Benutzernamen und ein Kennwort.  
  
 Die in Anmeldeinformationen gespeicherten Informationen ermöglichen einem Benutzer, der eine Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] über die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung hergestellt hat, auf Ressourcen außerhalb der Serverinstanz zuzugreifen. Wenn es sich bei der externen Ressource um Windows handelt, wird der Benutzer als der in den Anmeldeinformationen angegebene Windows-Benutzer authentifiziert. Eine einzelne Anmeldung kann mehreren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldungen zugeordnet werden. Eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldung kann allerdings nur einer Anmeldung zugeordnet werden.  
  
 Informationen zu Anmeldeinformationen, die in der Masterdatenbank gespeichert sind und in der gesamten Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verwendet werden können, finden Sie unter [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md). Informationen zu Anmeldeinformationen, die von einer bestimmten Datenbank verwendet werden und mit dieser Datenbank portabel sind, finden Sie unter [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
 Systemanmeldeinformationen werden automatisch erstellt und mit bestimmten Endpunkten verbunden. Namen für Systemanmeldeinformationen beginnen mit zwei Nummernzeichen (##).  
  
 Weitere Informationen zu Anmeldeinformationen finden Sie in den Katalogansichten [sys.credentials](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) und [sys.database_scoped_credentials](../../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md).  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Erstellen von Anmeldeinformationen](../../../relational-databases/security/authentication-access/create-a-credential.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
 [Sichern von SQL Server](../../../relational-databases/security/securing-sql-server.md)  
  
  
