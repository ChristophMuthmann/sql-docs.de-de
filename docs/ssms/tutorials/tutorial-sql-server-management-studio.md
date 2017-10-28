---
title: 'Tutorial: SQL Server Management Studio (SSMS) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 08/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.tutorialstart.ssms.f1
helpviewer_keywords:
- projects [SQL Server Management Studio], tutorials
- templates [SQL Server], SQL Server Management Studio
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- solutions [SQL Server Management Studio], tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.assetid: d2bade70-07cf-4d94-b5d2-88aecb538ed1
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: 5aa858aff03e93db9db36b8caa710cc3a3b874ca
ms.openlocfilehash: dde887f6e0999c5ebc107a300c33981a38ec7034
ms.contentlocale: de-de
ms.lasthandoff: 08/31/2017

---
# <a name="tutorial-sql-server-management-studio"></a>Lernprogramm: SQL Server Management Studio
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Dieses Tutorial zu SQL Server Management Studio (SSMS) bietet eine Einführung in die integrierte Umgebung zum Verwalten Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Infrastruktur. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verfügt über eine grafische Oberfläche zum Konfigurieren, Überwachen und Verwalten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanzen. Darüber hinaus vermittelt Ihnen das Tutorial, wie Sie die von Ihren Anwendungen, z.B. Datenbanken, verwendeten Datenebenenkomponenten bereitstellen, überwachen und aktualisieren. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] stellt auch Editoren für die [!INCLUDE[tsql](../../includes/tsql-md.md)]-, MDX-, DMX- und XML-Sprache bereit, um Skripts zu bearbeiten und zu debuggen.  
  
## <a name="what-you-will-learn"></a>Lernziele  
Dieses Tutorial hilft Ihnen, die Darstellung von Informationen in SSMS besser zu verstehen und die Funktionen effektiv zu nutzen.
  
Am besten machen Sie sich mit SSMS vertraut, indem Sie einige praktische Aufgaben durchführen. In diesem Tutorial erfahren Sie, wie Sie die Komponenten von SSMS verwalten und wie Sie die Funktionen finden, die Sie regelmäßig verwenden.  
  
Dieses Lernprogramm ist in drei Lektionen aufgeteilt:  
  
[Lektion 1: Grundlegendes zur Navigation in SQL Server Management Studio](lesson-1-basic-navigation-in-sql-server-management-studio.md)  
In dieser Lektion erfahren Sie, wie Sie die Komponenten von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]verwenden, wie das Umgebungslayout neu konfiguriert wird und wie Sie das Standardlayout wiederherstellen.  
  
[Lektion 2: Schreiben von Transact-SQL-Code](lesson-2-writing-transact-sql.md)  
In dieser Lektion erfahren Sie, wie Sie den Abfrage-Editor öffnen, Code verwalten und weitere Funktionen des Abfrage-Editors verwenden.  
  
[Lektion 3: Verwenden von Vorlagen, Lösungen und Skriptprojekten](lesson-3-working-with-templates-solutions-and-script-projects.md)  
In dieser Lektion erfahren Sie, wie Sie Vorlagen verwenden und Skripts in Lösungen und Projekten organisieren.  
  
## <a name="requirements"></a>Anforderungen  
Dieses Tutorial richtet sich an erfahrene Datenbankadministratoren und -entwickler, die [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] noch nicht kennen, aber mit Datenbankkonzepten und [!INCLUDE[tsql](../../includes/tsql-md.md)] vertraut sind.  
  
Zum Durchlaufen dieses Tutorials muss Folgendes installiert sein:  

  
-   Installieren Sie die neueste Version von [SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md).  
-   SQL Server 2016 oder höher mit der AdventureWorks-Beispieldatenbank. Informationen zum Installieren der AdventureWorks-Beispieldatenbank finden Sie unter [AdventureWorks2014](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2014). Installieren Sie die Datenbank „AdventureWorks2014 (OLTP)“.  

  
## <a name="see-also"></a>Siehe auch  
[Lernprogramme zum Datenbankmodul](../../relational-databases/database-engine-tutorials.md)  
  
  
  


