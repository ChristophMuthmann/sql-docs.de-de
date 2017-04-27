---
title: Sonstige Dateien | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- files [SQL Server Management Studio], miscellaneous
- projects [SQL Server Management Studio], files
- solutions [SQL Server Management Studio], files
- miscellaneous files folder [SQL Server]
ms.assetid: 3c952b0b-8f5f-4d86-9e5d-616c10b9df0d
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6ea72cab23f488c8330d78dc5c6a1275e043728a
ms.lasthandoff: 04/11/2017

---
# <a name="miscellaneous-files"></a>sonstige Dateien
Dateien, die als extern zu allen Projekte betrachtet werden, werden als *sonstige Dateien*bezeichnet. Wenn eine Projektmappe geöffnet ist, können Sie sonstige Dateien, die zum Projekt gehören, öffnen und ändern. Dateien werden als sonstige Dateien eingestuft, wenn die Dateierweiterung nicht dem Code-Editor des Projekts zugeordnet ist. So werden beispielsweise in einem [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Skriptprojekt Dateien mit der Dateinamenerweiterung TXT oder MDX als sonstige Dateien behandelt. In einem MDX-Projekt werden Dateien mit der Dateinamenerweiterung TXT oder SQL als sonstige Dateien behandelt. Informationen zum Zuordnen einer Dateierweiterung zu einem Code-Editor finden Sie unter [Vorgehensweise: Zuordnen von Dateierweiterungen zu einem Code-Editor](http://msdn.microsoft.com/en-us/193630f4-93de-4950-8f36-68702531f925).  
  
Das Hinzufügen von sonstigen Dateien zu Ihren Projekten bietet sich aus mehreren Gründen an. Möglicherweise gibt es eine Datei, die nicht unbedingt ein erkanntes Skript ist, aber wesentlich zur Entwicklung der Projektmappe beiträgt. Typische Beispiele dafür sind Entwicklungshinweise oder -anweisungen, Datendateien und Code Clips.  
  
Durch die sonstigen Dateien erhalten Sie mehr Flexibilität. Angenommen, Sie haben ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Skriptprojekt mit mehreren Skripts zum Erstellen von Tabellen und gespeicherten Prozeduren in Ihrer Datenbank. Außerdem gibt es für die Tabellen mehrere Datendateien mit der Dateinamenerweiterung BCP und eine Infodatei Readme.txt mit Anweisungen zur Ausführung. Sie können die Daten- und die Infodateien als sonstige Dateien zum Projekt hinzufügen, um die Vorteile der Quellcodeverwaltung und der anderen Funktionen des Projektsystems zu nutzen.  
  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] Menüs und Symbolleisten hängen vom Format der Datei ab, die Sie öffnen. Wenn Sie beispielsweise eine Textdatei öffnen, wird die Symbolleiste des Text-Editors angezeigt. Wenn Sie eine XML-Schemadatei öffnen, wird die Symbolleiste des XML-Schemas angezeigt. Beim Bearbeiten des XML-Schemas ist die Symbolleiste des Text-Editors nicht verfügbar. Wenn Sie zwischen einer Projektdatei und einer der sonstigen Dateien wechseln, werden alle projektbezogenen Befehle und Symbolleisten durch solche ersetzt, die für die sonstigen Dateien gelten.  
  
## <a name="see-also"></a>Siehe auch  
[Dateien zum Verwalten von Projektmappen und Projekten](../../ssms/solution/files-that-manage-solutions-and-projects.md)  
[Projektmappen &amp;#40;SQL Server Management Studio&amp;#41;](../../ssms/solution/solutions-sql-server-management-studio.md)  
[Projekte &amp;#40;SQL Server Management Studio&amp;#41;](../../ssms/solution/projects-sql-server-management-studio.md)  
  

