---
title: "Always Encrypted (Cliententwicklung) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
caps.latest.revision: 33
author: "stevestein"
manager: "jhubbard"
caps.handback.revision: 33
---
# Always Encrypted (Cliententwicklung)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) ist eine clientseitige Verschlüsselungstechnologie, die sicherstellt, dass vertrauliche Daten (und die zugehörigen Verschlüsselungsschlüssel) niemals in der SQL Server- oder Azure SQL-Datenbank offengelegt werden. Mit Always Encrypted verschlüsselt ein Clienttreiber vertrauliche Daten transparent, bevor er die Daten an das Datenbankmodul übergibt, und er entschlüsselt Daten transparent, die aus verschlüsselten Datenbankspalten abgerufen wurden.

Weitere Informationen zum Entwickeln von Anwendungen, die durch Always Encrypted geschützte Datenbanken verwenden, sowie Informationen dazu, welche Clienttreiber und Treiberversionen Always Encrypted unterstützen, finden Sie hier:

- [Verwenden von Always Encrypted mit dem .NET Framework-Datenanbieter für SQL Server](../../../relational-databases/security/encryption/develop using always encrypted with .net framework data provider.md)
- [Verwenden von „Immer verschlüsselt“ mit dem JDBC-Treiber](https://msdn.microsoft.com/library/mt591987.aspx)
- [Verwenden von „Immer verschlüsselt“ mit Windows ODBC Driver](https://msdn.microsoft.com/library/mt637351.aspx)



## Siehe auch

[„Immer verschlüsselt“ (Datenbankmodul)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
