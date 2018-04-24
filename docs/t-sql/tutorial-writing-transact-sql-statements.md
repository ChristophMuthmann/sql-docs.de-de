---
title: 'Tutorial: Schreiben von Transact-SQL-Anweisungen | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 08/03/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: get-started-article
helpviewer_keywords:
- Transact-SQL statements, tutorials
- Transact-SQL tutorials
- tutorials [Transact-SQL]
ms.assetid: 2addc9be-67d0-423d-a457-192fe9d7d058
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 65cb72c3cac7c51c702b97c2bcdbb8a793a818de
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-writing-transact-sql-statements"></a>Lernprogramm: Schreiben von Transact-SQL-Anweisungen
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
Willkommen beim Lernprogramm zum Schreiben von [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen. Dieses Lernprogramm richtet sich an Benutzer, die noch keine Erfahrung mit dem Schreiben von SQL-Anweisungen haben. Neuen Benutzern wird der Einstieg erleichtert, indem einige einfache Anweisungen zum Erstellen von Tabellen und Einfügen von Daten behandelt werden. In diesem Lernprogramm wird [!INCLUDE[tsql](../includes/tsql-md.md)]- die Implementierung des SQL-Standards durch [!INCLUDE[msCoName](../includes/msconame-md.md)] - verwendet. Dieses Lernprogramm ist als kurze Einführung in die [!INCLUDE[tsql](../includes/tsql-md.md)] -Sprache und nicht als Ersatz für eine [!INCLUDE[tsql](../includes/tsql-md.md)] -Schulung gedacht. Die Anweisungen in diesem Lernprogramm wurden absichtlich einfach gestaltet und geben nicht die Komplexität einer typischen Produktionsdatenbank wieder.  
  
>**HINWEIS:** Wenn Sie ein Anfänger auf diesem Gebiet sind, ist es möglicherweise einfacher für Sie [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] zu verwenden, anstatt [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen zu schreiben.  
  
## <a name="finding-more-information"></a>Weitere Informationsquellen  
Weitere Informationen zu bestimmten Anweisungen erhalten Sie, indem Sie in der SQL Server-Onlinedokumentation nach dem Namen der jeweiligen Anweisung suchen oder die 1.800 alphabetisch geordneten Sprachelemente unter [Transact-SQL-Referenz &#40;Datenbankmodul&#41;](../t-sql/transact-sql-reference-database-engine.md) über das Inhaltsverzeichnis durchsuchen. Eine weitere gute Strategie zum Suchen von Informationen besteht darin, Stichwörtern zu verwenden, die mit dem betreffenden Fachgebiet zu tun haben. Wenn Sie z.B. wissen möchten, wie Teile eines Datums zurückgegeben werden (z.B. der Monat), suchen Sie im Index nach **Datumsangaben [SQL Server]**, und wählen Sie die **Datumsbestandteile** aus. Dadurch gelangen Sie zum Thema [DATEPART &#40;Transact-SQL&#41;](../t-sql/functions/datepart-transact-sql.md). Wenn Sie beispielsweise Informationen zur Verwendung von Zeichenfolgen benötigen, suchen Sie nach **Zeichenfolgenfunktionen**. Dadurch gelangen Sie zum Thema [Zeichenfolgenfunktionen &#40;Transact-SQL&#41;](../t-sql/functions/string-functions-transact-sql.md).  
  
## <a name="what-you-will-learn"></a>Lernziele  
In diesem Lernprogramm wird Ihnen gezeigt, wie eine Datenbank erstellt wird, eine Tabelle in der Datenbank erstellt wird, Daten in die Tabelle eingefügt werden, die Daten aktualisiert, gelesen und gelöscht werden und die Tabelle anschließend gelöscht wird. Sie erstellen Sichten und gespeicherte Prozeduren und konfigurieren einen Benutzer für die Datenbank und die Daten.  
  
Dieses Lernprogramm ist in drei Lektionen aufgeteilt:  
  
[Lektion 1: Erstellen von Datenbankobjekten](../t-sql/lesson-1-creating-database-objects.md)  
In dieser Lektion erstellen Sie eine Datenbank und eine Tabelle in der Datenbank, fügen Daten in die Tabelle ein und aktualisieren und lesen die Daten.  
  
[Lektion 2: Konfigurieren von Berechtigungen für Datenbankobjekte](../t-sql/lesson-2-configuring-permissions-on-database-objects.md)  
In dieser Lektion erstellen Sie einen Anmeldenamen und einen Benutzer. Sie erstellen auch eine Sicht und eine gespeicherte Prozedur und erteilen dann dem Benutzer eine Berechtigung für die gespeicherte Prozedur.  
  
[Lektion 3: Löschen von Datenbankobjekten](../t-sql/lesson-3-deleting-database-objects.md)  
In dieser Lektion entfernen Sie den Zugriff auf Daten, löschen Daten aus einer Tabelle und löschen die Tabelle und anschließend die Datenbank.  
  
## <a name="requirements"></a>Anforderungen  
Damit Sie dieses Lernprogramm ausführen können, müssen Sie die SQL-Sprache nicht beherrschen, sollten jedoch grundlegende Konzepte einer Datenbank, wie z. B. Tabellen, kennen. Im Verlauf dieses Lernprogramms erstellen Sie eine Datenbank und einen Windows-Benutzer. Für diese Aufgaben sind Berechtigungen auf höherer Ebene erforderlich. Sie sollten sich deshalb als Administrator am Computer anmelden.  
  
Auf dem System muss Folgendes installiert sein:  
  
-   Eine beliebige Edition von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-  [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)  
  

 
  
  
  

