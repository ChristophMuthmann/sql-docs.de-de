---
title: Always Encrypted (Cliententwicklung) | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 07/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
caps.latest.revision: 33
author: stevestein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 091625c7e502ac131bd045546ca4c587b754e366
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="always-encrypted-client-development"></a>Always Encrypted (Cliententwicklung)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) ist eine clientseitige Verschlüsselungstechnologie, die sicherstellt, dass vertrauliche Daten (und die zugehörigen Verschlüsselungsschlüssel) niemals in der SQL Server- oder Azure SQL-Datenbank offengelegt werden. Mit Always Encrypted verschlüsselt ein Clienttreiber vertrauliche Daten transparent, bevor er die Daten an das Datenbankmodul übergibt, und er entschlüsselt Daten transparent, die aus verschlüsselten Datenbankspalten abgerufen wurden.

Weitere Informationen zum Entwickeln von Anwendungen, die durch Always Encrypted geschützte Datenbanken verwenden, sowie Informationen dazu, welche Clienttreiber und Treiberversionen Always Encrypted unterstützen, finden Sie hier:

- [Verwenden von Always Encrypted mit dem .NET Framework-Datenanbieter für SQL Server](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Verwenden von „Immer verschlüsselt“ mit dem JDBC-Treiber](https://msdn.microsoft.com/library/mt591987.aspx)
- [Verwenden von „Immer verschlüsselt“ mit Windows ODBC Driver](https://msdn.microsoft.com/library/mt637351.aspx)



## <a name="see-also"></a>Siehe auch

[„Immer verschlüsselt“ (Datenbankmodul)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)


