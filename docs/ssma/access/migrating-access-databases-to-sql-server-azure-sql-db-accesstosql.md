---
title: Migrieren von Access-Datenbanken zu SQLServer - Azure SQL-Datenbank | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 08/15/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- instructions, migration
- migrating databases, overview
- overview, migration process
- procedure, migration
- recommended migration process
ms.assetid: 76a3abcf-2998-4712-9490-fe8d872c89ca
caps.latest.revision: "23"
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: On Demand
ms.openlocfilehash: 92ab1b9e1bd128c57347f2f68b251fce4648bfe4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>Migrieren von Access-Datenbanken zu SQL Server - Azure SQL-Datenbank (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) ist ein Tool, das eine umfassende Umgebung bereitstellt, mit denen Sie schnell die Access-Datenbanken zu migrieren können [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Mithilfe von SSMA können Sie überprüfen, den Zugriff und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbankobjekte, die Access-Datenbank für die Migration zu bewerten, konvertieren den Zugriff auf Datenbankobjekte, laden Sie sie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, und klicken Sie dann die Daten migrieren.  
  
## <a name="recommended-migration-process"></a>Empfohlene Migrationsprozess  
Für eine erfolgreiche Migration von Objekten und Daten aus den Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, das folgende Verfahren verwenden:  
  
1.  [Erstellen Sie ein neues SSMA-Projekt](http://msdn.microsoft.com/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7). Nachdem Sie das Projekt erstellt haben, können Sie [festgelegt Projektoptionen](http://msdn.microsoft.com/0a7304df-2f35-4453-96ef-7ac83dea1167), einschließlich Konvertierungsoptionen, Migrationsoptionen und datentypzuordnungen.  
  
2.  [Fügen Sie Access-Datenbankdateien](http://msdn.microsoft.com/e944c740-4c8a-4bc1-b0ed-be57bc06dced) zum Projekt.  
  
    Sie können einzelne Dateien, einschließlich Dateien, die sich auf dem Computer oder Netzwerk hinzufügen.  
  
3.  [Herstellen einer Verbindung mit der Zielinstanz von SQL Server](http://msdn.microsoft.com/f84cf007-ddf1-4396-a07c-3e0729abc769) oder [Herstellen einer Verbindung mit der Zielinstanz von SQL Azure](http://msdn.microsoft.com/1ba0d113-dc05-4431-8689-e14a8821bafd).  
  
    Sie können entweder auf SQL Server- oder SQL Azure verbinden.  
  
4.  Anpassen die Zuordnung zwischen einer oder mehreren Access-Datenbanken und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Schemas [ordnen Sie die Quell- und Zieldatenbanken](http://msdn.microsoft.com/69bee937-7b2c-49ee-8866-7518c683fad4).  
  
5.  Optional können Sie [Erstellen eines Berichts Assessment](http://msdn.microsoft.com/8b9e23d6-da62-437a-8c05-8ad2628b9441) zu bestimmen, ob die Zugriff auf Datenbankobjekte erfolgreich konvertiert werden können, können Sie auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
6.  [Konvertieren Sie den Zugriff auf Datenbankobjekte](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c) auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objektdefinitionen.  
  
7.  [Laden Sie die konvertierte Datenbankobjekte in SQL Server](http://msdn.microsoft.com/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba).  
  
    Sie können entweder die Datenbankobjekte in laden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure mithilfe von SSMA, oder Sie können speichern [!INCLUDE[tsql](../../includes/tsql_md.md)] Skripts.  
  
8.  [Migrieren Sie den Zugriff auf Daten in SQL Server](http://msdn.microsoft.com/f3b18af7-1af0-499d-a00d-a0af94895625).  
  
    > [!NOTE]  
    > Sie können zu konvertieren, laden und Migrieren von Schemas und Daten in einem Schritt. Um nur einem Klick Migration durchzuführen, klicken Sie auf die **konvertieren, laden und migrieren** Schaltfläche.  
  
9. Wenn Sie möchten, dass Ihre Anwendungen Zugriff auf die Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure zu verwenden [Access-Tabellen mit der SQL Server-Tabellen verknüpfen](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4).  
  
Der Migrations-Assistent können auch führt Sie durch diesen Prozess. Weitere Informationen finden Sie unter [Paketmigrations-Assistent](http://msdn.microsoft.com/5bab5914-b2ae-4795-8cf5-83e42d64bef2).  
  
## <a name="see-also"></a>Siehe auch  
[Erste Schritte mit SQL Server Migration Assistant für Access](http://msdn.microsoft.com/462a731f-08f1-44e1-9eeb-4deac6d2f6c5)  
[Access-Datenbanken vorbereitet für die Migration.](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)
