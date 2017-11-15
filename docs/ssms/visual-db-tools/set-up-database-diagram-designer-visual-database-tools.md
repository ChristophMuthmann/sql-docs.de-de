---
title: Einrichten des Datenbankdiagramm-Designers (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vdt.diagnostic.InstallSqlDiagramSupport
helpviewer_keywords:
- Database Diagram Designer
- database diagrams [SQL Server], Database Diagram Designer
- diagrams [SQL Server], Database Diagram Designer
ms.assetid: 927321ee-b459-4f5b-9719-4a7a95639143
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da20649fcdacb6cc9e6190e47e179eca20c375e0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="set-up-database-diagram-designer-visual-database-tools"></a>Einrichten des Datenbankdiagramm-Designers (Visual Database Tools)
Der Datenbankdiagramm-Designer kann erst verwendet werden, nachdem er von einem Mitglied der **db_owner** -Rolle für den Zugriff auf Diagramme eingerichtet wurde.  
  
### <a name="to-set-up-database-diagramming"></a>So richten Sie das Erstellen von Datenbankdiagrammen ein  
  
1.  Erweitern Sie im Objekt-Explorer einen Datenbankknoten.  
  
2.  Erweitern Sie den Knoten Datenbankdiagramme unter der Datenbankverbindung.  
  
3.  Wählen Sie an der entsprechenden Aufforderung **Ja** aus, wenn Sie das Erstellen von Datenbankdiagrammen einrichten möchten.  
  
    > [!NOTE]  
    > Damit werden die Datenbankdiagrammtabelle, gespeicherte Systemprozeduren und eine Systemfunktion in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datenbank erstellt.  
  
4.  Visual Studio erstellt die folgenden Objekte für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
    1.  sysdiagrams-Tabelle  
  
    2.  Gespeicherte Prozedur sp_alterdiagram  
  
    3.  Gespeicherte Prozedur sp_creatediagram  
  
    4.  Gespeicherte Prozedur sp_dropdiagram  
  
    5.  Gespeicherte Prozedur sp_renamediagram  
  
    6.  fn_diagramobjects-Funktion  
  
    7.  Gespeicherte Prozedur sp_helpdiagrams  
  
    8.  Gespeicherte Prozedur sp_helpdiagramsdefinition  
  
    9. Gespeicherte Prozedur sp_upgraddiagrams  
  
## <a name="see-also"></a>Siehe auch  
[Grundlagen des Besitzes von Datenbankdiagrammen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/understand-database-diagram-ownership-visual-database-tools.md)  
[Aktualisieren von Datenbankdiagrammen aus älteren Versionen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
[ALTER AUTHORIZATION (Transact-SQL)](http://msdn.microsoft.com/en-us/8c805ae2-91ed-4133-96f6-9835c908f373)  
  
