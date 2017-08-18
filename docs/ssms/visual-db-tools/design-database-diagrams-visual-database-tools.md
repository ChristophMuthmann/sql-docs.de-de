---
title: Entwerfen von Datenbankdiagrammen (Visual Database Tools) | Microsoft-Dokumentation
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
- vdtsql.chm:65536
- vdt.DatabaseDesigner
helpviewer_keywords:
- Database Diagram Designer
- Visual Database Tools [SQL Server], database diagrams
- database diagrams [SQL Server], designing
- diagrams [SQL Server], designing
ms.assetid: 6d2c14e1-3d73-4d10-ae5b-7f2b5d6c4ea8
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 39d9220dc13546a5a1e9c95d034b5a5cf0ac43b5
ms.contentlocale: de-de
ms.lasthandoff: 08/18/2017

---
# <a name="design-database-diagrams-visual-database-tools"></a>Entwerfen von Datenbankdiagrammen (Visual Database Tools)
Der Datenbank-Designer ist ein visuelles Tool, mit dem Sie eine Datenbank, mit der eine Verbindung besteht, entwerfen und anzeigen lassen können. Beim Entwerfen einer Datenbank können Sie mithilfe des Datenbank-Designers Tabellen, Spalten, Schlüssel, Indizes, Beziehungen und Einschränkungen erstellen, bearbeiten oder löschen. Zur Darstellung einer Datenbank können Sie ein oder mehrere Diagramme erstellen, die die Tabellen, Spalten, Schlüssel oder Beziehungen innerhalb der Datenbank teilweise oder ganz anzeigen.  
  
![Datenbankdiagramm zur Illustration von Tabellenbeziehungen](../../ssms/visual-db-tools/media/dv3w7c1.gif "Database diagram illustrating table relationships")  
  
Sie können für jede Datenbank beliebig viele Datenbankdiagramme erstellen, und jede Datenbanktabelle kann in einer beliebigen Anzahl von Diagrammen angezeigt werden. Daher können Sie verschiedene Diagramme erstellen, um unterschiedliche Bereiche der Datenbank darzustellen oder unterschiedliche Aspekte des Entwurfs hervorzuheben. Sie können z. B. ein umfangreiches Diagramm erstellen, in dem alle Tabellen und Spalten angezeigt werden, und ein kleineres Diagramm, in dem die Tabellen ohne ihre Spalten dargestellt sind.  
  
Jedes erstellte Diagramm wird in der zugehörigen Datenbank gespeichert.  
  
## <a name="tables-and-columns-in-a-database-diagram"></a>Tabellen und Spalten in einem Datenbankdiagramm  
Innerhalb eines Datenbankdiagramms können Tabellen mit drei unterschiedlichen Merkmalen angezeigt werden: einer Titelleiste, einem Zeilenselektor und einer Reihe von Eigenschaftenspalten.  
  
**Titelleiste** In der Titelleiste wird der Name der Tabelle angezeigt.  
  
Wenn Sie in einer Tabelle Änderungen vorgenommen und diese noch nicht gespeichert haben, wird am Ende des Tabellennamens ein Sternchen (*) angezeigt, um so auf ungespeicherte Änderungen hinzuweisen. Informationen zum Speichern von geänderten Tabellen und Diagrammen finden Sie unter [Verwenden von Datenbankdiagrammen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  
**Zeilenselektor** Klicken Sie auf den Zeilenselektor, um eine Spalte in einer Datenbank auszuwählen. Der Zeilenselektor zeigt ein Symbol in Form eines Schlüssels an, wenn sich die Spalte im Primärschlüssel der Tabelle befindet. Informationen zu Primärschlüsseln finden Sie unter [Verwenden von Schlüsseln (Visual Database Tools)](http://msdn.microsoft.com/en-us/31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd).  
  
**Eigenschaftenspalten** Die Eigenschaftenspalten werden nur in bestimmten Sichten der Tabellen angezeigt. Sie können sich eine Tabelle in fünf verschiedenen Sichten anzeigen lassen, um dann die Größe und das Layout des betreffenden Diagramms verwalten zu können.  
  
Weitere Informationen zu Tabellensichten finden Sie unter [Anpassen des Umfangs der in Diagrammen angezeigten Informationen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/customize-the-amount-of-information-displayed-in-diagrams-visual-database-tools.md).  
  
## <a name="relationships-in-a-database-diagram"></a>Beziehungen in einem Datenbankdiagramm  
Innerhalb eines Datenbankdiagramms können Eigenschaften mit drei unterschiedlichen Merkmalen angezeigt werden: Endpunkte, eine bestimmte Linienart und verknüpfte Tabellen.  
  
**Endpunkte** Die Endpunkte der Linie geben an, ob es sich um eine 1:1-Beziehung oder um eine 1:n-Beziehung handelt. Wenn eine Beziehung einen Schlüssel an einem Endpunkt und ein Unendlichkeitszeichen am anderen Endpunkt aufweist, handelt es sich um eine 1:n-Beziehung. Wenn eine Beziehung an jedem Endpunkt einen Schlüssel aufweist, handelt es sich um eine 1:1-Beziehung.  
  
**Linienart** Die Linie selbst (ohne die Endpunkte) gibt an, ob das Datenbank-Managementsystem (DBMS) die referenzielle Integrität für die Beziehung erzwingt, wenn der Fremdschlüsseltabelle neue Daten hinzugefügt werden. Bei einer durchgezogenen Linie erzwingt das DBMS die referenzielle Integrität für die Beziehung, wenn Zeilen in der Fremdschlüsseltabelle hinzugefügt oder geändert werden. Bei einer gepunkteten Linie erzwingt das DBMS keine referenzielle Integrität für die Beziehung, wenn Zeilen in der Fremdschlüsseltabelle hinzugefügt oder bearbeitet werden.  
  
**Verknüpfte Tabellen** Die Beziehungslinie gibt an, das zwischen zwei Tabellen eine Fremdschlüsselbeziehung definiert ist. Bei einer 1:n-Beziehung ist die Fremdschlüsseltabelle die Tabelle neben dem Unendlichkeitszeichen der Linie. Wenn beide Endpunkte der Linie mit derselben Tabelle verbunden sind, handelt es sich um eine reflexive Beziehung. Weitere Informationen finden Sie unter [Zeichnen reflexiver Beziehungen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/draw-reflexive-relationships-visual-database-tools.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
[Grundlagen des Besitzes von Datenbankdiagrammen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/understand-database-diagram-ownership-visual-database-tools.md)  
  
[Navigieren im Datenbankdiagramm-Designer &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/navigate-in-database-diagram-designer-visual-database-tools.md)  
  
[Einrichten im Datenbankdiagramm-Designer &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)  
  
[Aktualisieren von Datenbankdiagrammen aus älteren Versionen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
  
[Öffnen des Datenbankdiagramm-Designers &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/open-database-diagram-designer-visual-database-tools.md)  
  
## <a name="see-also"></a>Siehe auch  
[Verwenden von Datenbankdiagrammen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[Verwenden von Tabellen in Datenbankdiagrammen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)  
[Verwenden von Diagrammlayout &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-diagram-layout-visual-database-tools.md)  
  

