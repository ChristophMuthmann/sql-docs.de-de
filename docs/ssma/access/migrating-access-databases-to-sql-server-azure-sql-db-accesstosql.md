---
title: Migrieren von Access-Datenbanken zu SQLServer - Azure SQL-Datenbank | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
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
caps.latest.revision: 23
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6d3c44ed3c73edae1b2b8d9cd244a2530c5748cf
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>Migrieren von Access-Datenbanken zu SQLServer – Azure SQL-Datenbank (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) ist eine umfassende Umgebung, mit dem Sie migrieren von Access-Datenbanken zu schnell [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Mithilfe von SSMA können Sie überprüfen, den Zugriff und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbankobjekte, die Access-Datenbank für die Migration zu bewerten, konvertieren den Zugriff auf Datenbankobjekte, laden Sie sie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, und klicken Sie dann die Daten migrieren.  
  
## <a name="recommended-migration-process"></a>Migrationsprozess empfohlen  
Für eine erfolgreiche Migration von Objekten und Daten aus den Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, das folgende Verfahren verwenden:  
  
1.  [Erstellen Sie ein neues SSMA-Projekt](http://msdn.microsoft.com/en-us/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7). Nachdem Sie das Projekt erstellt haben, können Sie [Projektoptionen festlegen](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167). Dazu gehören Konvertierungsoptionen Migrationsoptionen und datentypzuordnungen.  
  
2.  [Fügen Sie Access-Datenbankdateien](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced) zum Projekt.  
  
    Sie können einzelne Dateien hinzufügen, oder Sie können Dateien, die dort hinzufügen, auf dem Computer oder Netzwerk.  
  
3.  [Herstellen einer Verbindung mit der Zielinstanz von SQL Server](http://msdn.microsoft.com/en-us/f84cf007-ddf1-4396-a07c-3e0729abc769) oder [Herstellen einer Verbindung mit der Zielinstanz von SQL Azure](http://msdn.microsoft.com/en-us/1ba0d113-dc05-4431-8689-e14a8821bafd).  
  
    Sie können entweder auf SQL Server- oder SQL Azure verbinden.  
  
4.  Anpassen die Zuordnung zwischen einer oder mehreren Access-Datenbanken und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Schemas [ordnen Sie die Quell- und Zieldatenbanken](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4).  
  
5.  Optional können Sie [Erstellen eines Berichts Assessment](http://msdn.microsoft.com/en-us/8b9e23d6-da62-437a-8c05-8ad2628b9441)zu bestimmen, ob die Zugriff auf Datenbankobjekte erfolgreich konvertiert werden können, können Sie auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
6.  [Konvertieren Sie den Zugriff auf Datenbankobjekte](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c) auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objektdefinitionen.  
  
7.  [Laden Sie die konvertierte Datenbankobjekte in SQL Server](http://msdn.microsoft.com/en-us/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba).  
  
    Sie können entweder die Datenbankobjekte in Load [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure mithilfe von SSMA, oder Sie können speichern [!INCLUDE[tsql](../../includes/tsql_md.md)] Skripts.  
  
8.  [Migrieren Sie den Zugriff auf Daten in SQL Server](http://msdn.microsoft.com/en-us/f3b18af7-1af0-499d-a00d-a0af94895625).  
  
    > [!NOTE]  
    > Sie können zu konvertieren, laden und Migrieren von Schemas und Daten in einem Schritt. Um nur einem Klick Migration durchzuführen, klicken Sie auf die **konvertieren, laden und migrieren** Schaltfläche.  
  
9. Wenn Sie möchten, dass Ihre Anwendungen Zugriff auf die Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure zu verwenden [Access-Tabellen mit der SQL Server-Tabellen verknüpfen](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4).  
  
Der Migrations-Assistent können auch führt Sie durch diesen Prozess. Weitere Informationen finden Sie unter [Paketmigrations-Assistent](http://msdn.microsoft.com/en-us/5bab5914-b2ae-4795-8cf5-83e42d64bef2).  
  
## <a name="see-also"></a>Siehe auch  
[Erste Schritte mit SQL Server Migration Assistant für Access](http://msdn.microsoft.com/en-us/462a731f-08f1-44e1-9eeb-4deac6d2f6c5)  
[Access-Datenbanken vorbereitet für die Migration.](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  

