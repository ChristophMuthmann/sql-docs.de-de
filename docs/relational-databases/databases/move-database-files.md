---
title: Verschieben von Datenbankdateien | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- files [SQL Server], moving
- data files [SQL Server], moving
- file moving [SQL Server]
- moving full-text catalogs
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- scheduled disk maintenance [SQL Server]
- moving files
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0c2b2c9da2059b9810acf51723d3e6fa21e80929
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="move-database-files"></a>Verschieben von Datenbankdateien
  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]können Sie System- und Benutzerdatenbanken durch Angeben des neuen Dateispeicherorts in der FILENAME-Klausel der [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) -Anweisung verschieben. Auf diese Weise können Daten-, Protokoll- und Volltextkatalogdateien verschoben werden. Dies kann in folgenden Situationen nützlich sein:  
  
-   Bei der Wiederherstellung nach Fehlern. Wenn z. B. die Datenbank aufgrund eines Hardwarefehlers als fehlerverdächtig eingestuft oder heruntergefahren wurde.  
  
-   Bei geplanter Verschiebung.  
  
-   Verschiebung aufgrund planmäßiger Datenträgerwartung.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Beschreibung|  
|-----------|-----------------|  
|[Verschieben von Benutzerdatenbanken](../../relational-databases/databases/move-user-databases.md)|Beschreibt die Prozeduren, um Benutzerdatenbankdateien und Volltextkatalogdateien an einen neuen Speicherort zu verschieben.|  
|[Verschieben von Systemdatenbanken](../../relational-databases/databases/move-system-databases.md)|Beschreibt die Prozeduren, um Systemdatenbankdateien an einen neuen Speicherort zu verschieben.|  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Anfügen und Trennen von Datenbanken &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
