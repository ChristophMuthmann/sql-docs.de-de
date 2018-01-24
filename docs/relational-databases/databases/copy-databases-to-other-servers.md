---
title: Kopieren von Datenbanken auf andere Server | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- servers [SQL Server], copying databases between
- bulk exporting [SQL Server], between servers
- database copying [SQL Server]
- migrating databases [SQL Server]
- moving databases
- copying databases
- bulk importing [SQL Server], between servers
ms.assetid: 978406d6-a3c8-4902-b1f4-4ced75234be5
caps.latest.revision: "42"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ab6019a97e97f916173aeed53586376a7e76f543
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="copy-databases-to-other-servers"></a>Kopieren von Datenbanken auf andere Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Es ist manchmal hilfreich, eine Datenbank von einem Computer zum anderen zu kopieren, z.B. für Tests, das Überprüfen von Konsistenz, das Entwickeln von Software, das Ausführen von Berichten, das Erstellen einer Spiegeldatenbank oder eventuell zum Verfügbarmachen der Datenbank für externe Niederlassungen.  
  
 Es gibt mehrere Möglichkeiten, eine Datenbank zu kopieren:  
  
-   Verwenden des Assistenten zum Kopieren von Datenbanken  
  
     Sie können den Assistenten zum Kopieren von Datenbanken verwenden, um Datenbanken zwischen Servern zu kopieren oder zu verschieben oder um eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank auf eine höhere Version zu aktualisieren. Weitere Informationen finden Sie unter [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
-   Wiederherstellen einer Datenbanksicherung  
  
     Mit den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen BACKUP und RESTORE können Sie eine ganze Datenbank kopieren. Typischerweise wird das Wiederherstellen einer vollständigen Datenbanksicherung aus vielen Gründen zum Kopieren einer Datenbank von einem Computer auf einen anderen verwendet. Weitere Informationen zum Sichern und Wiederherstellen zum Zweck des Kopierens einer Datenbank finden Sie unter [Kopieren von Datenbanken durch Sichern und Wiederherstellen](../../relational-databases/databases/copy-databases-with-backup-and-restore.md).  
  
    > [!NOTE]  
    >  Zum Einrichten einer Spiegeldatenbank für die Datenbankspiegelung müssen Sie die Datenbank mithilfe von RESTORE DATABASE *<Datenbankname>* WITH NORECOVERY auf dem Spiegelserver wiederherstellen. Weitere Informationen finden Sie unter [Vorbereiten einer Spiegeldatenbank auf die Spiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)verwendet.  
  
-   Verwenden des Assistenten zum Generieren von Skripts, um Datenbanken zu veröffentlichen  
  
     Sie können mit dem Assistenten zum Generieren von Skripts eine Datenbank von einem lokalen Computer auf einen Webhostinganbieter übertragen. Weitere Informationen finden Sie unter [Assistent zum Generieren und Veröffentlichen von Skripts](../../relational-databases/scripting/generate-and-publish-scripts-wizard.md).  
  
  
