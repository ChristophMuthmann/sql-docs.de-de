---
title: Grundlagen des Besitzes von Datenbankdiagrammen (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.diagnostic.CannotOpenWithInvalidOwner
helpviewer_keywords:
- diagrams [SQL Server], ownership
- database diagrams [SQL Server], ownership
- owners [SQL Server], database diagrams
ms.assetid: 4a27a48e-c4ef-4017-82b8-0cac4d0bbcac
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fd71d87c5a2967d23f72b7402c7ca95a8822b688
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="understand-database-diagram-ownership-visual-database-tools"></a>Grundlagen des Besitzes von Datenbankdiagrammen (Visual Database Tools)
Der Datenbankdiagramm-Designer kann erst verwendet werden, nachdem er von einem Mitglied der db_owner-Rolle (eine Rolle von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Datenbanken) für den Zugriff auf Diagramme eingerichtet wurde. Jedes Diagramm hat nur einen einzigen Besitzer, und zwar den Benutzer, der das Diagramm erstellt hat. Weitere Informationen zum Einrichten der Diagrammerstellung finden Sie unter [Einrichten des Datenbankdiagramm-Designers (Visual Database Tools)](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md).  
  
Es folgen einige Punkte, die Sie beim Besitz von Diagrammen beachten sollten:  
  
-   Obwohl jeder beliebige Benutzer mit Zugriff auf eine Datenbank ein Diagramm erstellen kann, können nur der Ersteller des Diagramms und alle Mitglieder der Rolle db_owner das Diagramm anzeigen.  
  
-   Der Besitz von Diagrammen kann nur an Mitglieder der Rolle db_owner übertragen werden. Und dies ist auch nur dann möglich, wenn der vorherige Besitzer des Diagramms aus der Datenbank entfernt wurde.  
  
-   Wenn der Besitzer eines Diagramms aus der Datenbank entfernt wurde, bleibt das Diagramm in der Datenbank, bis ein Mitglied der Rolle db_owner versucht, das Diagramm zu öffnen. Zu diesem Zeitpunkt kann das Mitglied von db_owner entscheiden, den Besitz des Diagramms zu übernehmen.  
  
## <a name="see-also"></a>Siehe auch  
[Arbeiten mit Datenbankdiagrammen (Visual Database Tools)](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[Einrichten des Datenbankdiagramm-Designers (Visual Database Tools)](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)  
  

