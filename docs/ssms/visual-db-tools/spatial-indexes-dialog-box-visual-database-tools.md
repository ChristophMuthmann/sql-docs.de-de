---
title: "Dialogfeld 'Räumliche Indizes' (Visual Database Tools) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vdt.dlgbox.spatialindexes
ms.assetid: 4d84239a-68c7-4aa2-8602-2b51dd07260f
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efb3e7457ce2406fa52801221b4c9a9d937fc7dd
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="spatial-indexes-dialog-box-visual-database-tools"></a>Dialogfeld 'Räumliche Indizes' (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Verwenden Sie das Dialogfeld **Räumliche Indizes**, um Indizes für Spalten des Datentyps **geometry** oder **geography** (*räumliche Spalten*) zu erstellen, denn diese können nicht mithilfe des Dialogfelds **Index/Schlüssel** indiziert werden. Jede räumliche Spalte kann mehr als einen räumlichen Index aufweisen, jedoch müssen sie einzeln erstellt werden.  
  
Weitere Informationen über die Einschränkungen bei der Erstellung von räumlichen Indizes finden Sie unter [Übersicht über räumliche Indizes](http://msdn.microsoft.com/en-us/b1ae7b78-182a-459e-ab28-f743e43f8293).  
  
## <a name="options"></a>enthalten  
**Ausgewählter räumlicher Index**  
Listet vorhandene räumliche Indizes auf. Wählen Sie einen Index aus, um dessen Eigenschaften anzuzeigen. Wenn die Liste leer ist, wurden bisher keine räumlichen Indizes für die Tabelle definiert.  
  
**Hinzufügen**  
Erstellt einen neuen räumlichen Index.  
  
**Delete**  
Löscht den in der Liste **Ausgewählter räumlicher Index** ausgewählten räumlichen Index.  
  
**Zellen pro Objekt**  
Gibt die Anzahl von Zellen pro Objekt für das Mosaik an, die für ein einzelnes räumliches Objekt im Index verwendet werden können. Bei dieser Zahl kann es sich um jede ganze Zahl von 1 bis 8192 handeln. Der Standardwert ist 16.  
  
Wenn ein Objekt mehr Zellen abdeckt, als durch *n*angegeben sind, werden bei der Indizierung so viele Zellen verwendet, wie zum Bereitstellen eines vollständigen Mosaiks der höchsten Ebene erforderlich sind. In solchen Fällen ist es möglich, dass ein Objekt mehr als die angegebene Anzahl von Zellen erhält. Die maximale Anzahl ist dann die Anzahl von Zellen, die von dem Raster der höchsten Ebene generiert wird, welche von der Dichte der **Ebene 1** abhängt.  
  
**Spalten**  
Gibt den Spaltennamen und die Sortierreihenfolge an.  
  
**IsSpatialIndex**  
Gibt an, dass ein räumlicher Index ausgewählt ist.  
  
**Ebene 1**  
Gibt die Dichte des Rasters der obersten (höchsten) Ebene an.  
  
**Ebene 2**  
Gibt die Dichte des Rasters der zweiten Ebene an.  
  
**Ebene 3**  
Gibt die Dichte des Rasters der dritten Ebene an.  
  
**Ebene 4**  
Gibt die Dichte des Rasters der vierten Ebene an.  
  
**Mosaikschema**  
Gibt das Mosaikschema an:  
  
**Geometriespaltenoptionen** :  
  
-   **Geometrieraster** für eine Geometriespalte  
  
-   **Geografieraster** für eine Geografiespalte  
  
**Typ**  
Gibt an, dass ein räumlicher Index ausgewählt ist.  
  
**Maximaler X-Wert**  
Gibt die X-Koordinate der oberen rechten Ecke des Begrenzungsrahmens an. Diese Eigenschaft wird abgeblendet, wenn das **Mosaikschema** auf **Geografieraster**festgelegt ist.  
  
**Minimaler X-Wert**  
Gibt die X-Koordinate der unteren linken Ecke des umgebenden Felds an. Diese Eigenschaft wird abgeblendet, wenn das **Mosaikschema** auf **Geografieraster**festgelegt ist.  
  
**Maximaler Y-Wert**  
Gibt die Y-Koordinate der oberen rechten Ecke des umgebenden Felds an. Diese Eigenschaft wird abgeblendet, wenn das **Mosaikschema** auf **Geografieraster**festgelegt ist.  
  
**Minimaler Y-Wert**  
Gibt die Y-Koordinate der unteren linken Ecke des umgebenden Felds an. Diese Eigenschaft wird abgeblendet, wenn das **Mosaikschema** auf **Geografieraster**festgelegt ist.  
  
**Identität**  
Wenn die Kategorie erweitert ist, werden die Eigenschaftenfelder für **Name** und **Beschreibung** angezeigt.  
  
**(Name)**  
Zeigt den Namen des räumlichen Indexes an. Wenn ein neuer Index erstellt wird, erhält dieser einen Standardnamen, der auf der Tabelle im aktiven Fenster des Tabellen-Designers basiert. Sie können den Namen jederzeit ändern.  
  
**Beschreibung**  
Beschreibt den Index. Klicken Sie zum Erstellen einer detailliertere Beschreibung auf **Beschreibung** , und klicken Sie dann auf die Schaltfläche mit den Auslassungspunkten (**…**) rechts neben dem Eigenschaftenfeld. Dadurch wird ein größerer Bereich verfügbar, in den Sie Text eingeben können.  
  
**Kategorie Tabellen-Designer**  
Wenn die Kategorie erweitert ist, werden Informationen zu den Eigenschaften dieses räumlichen Indexes angezeigt.  
  
**Füllspezifikation**  
Wenn dieses Element erweitert ist, werden Informationen für **Füllfaktor** und **Index mit Leerstellen auffüllen**angezeigt.  
  
**Füllfaktor**  
Geben Sie an, zu welchem Prozentsatz die Indexseite vom System gefüllt werden kann. Wenn eine Seite gefüllt ist, muss beim Hinzufügen neuer Daten die Seite geteilt werden. Dies beeinträchtigt die Leistung.  
  
-   Ein Wert von 100 bedeutet, dass die Seiten gefüllt werden. Diese Einstellung erfordert den geringsten Aufwand an Speicherplatz, ist aber auch am wenigsten effektiv. Diese Einstellung sollte nur verwendet werden, wenn keine Änderungen an den Daten vorgenommen werden, zum Beispiel in einer schreibgeschützten Tabelle.  
  
-   Durch einen niedrigeren Wert bleibt auf den Datenseiten ein größerer Bereich leer. Dadurch müssen die Datenseiten seltener geteilt werden, wenn Indizes größer werden. Dies erfordert allerdings mehr Speicherplatz. Diese Einstellung empfiehlt sich eher, wenn Änderungen an den Daten in der Tabelle vorgenommen werden.  
  
**Index mit Leerstellen auffüllen**  
Stellt Seiten in diesem Index mit dem in **Füllfaktor**angegebenen Prozentsatz leeren Platzes (Auffüllung) zur Verfügung.  
  
**Seitensperren sind zulässig**  
Gibt an, ob Sperren auf Seitenebene für diesen Index zugelassen sind. Das Zulassen oder Untersagen von Sperren auf Seitenebene wirkt sich auf die Datenbankleistung aus.  
  
**Statistiken** **neu berechnen**  
Gibt an, ob beim Erstellen des Index neue Statistiken berechnet werden sollen. Durch erneutes Berechnen von Statistiken wird die Erstellung der Indizes verlangsamt, die Abfrageleistung wird jedoch meist verbessert.  
  
**Zeilensperren sind zulässig**  
Gibt an, ob das Sperren auf Zeilenebene für diesen Index zugelassen ist. Das Zulassen oder Untersagen von Sperren auf Zeilenebene wirkt sich auf die Datenbankleistung aus.  
  
## <a name="see-also"></a>Siehe auch  
[Übersicht über räumliche Indizes](http://msdn.microsoft.com/en-us/b1ae7b78-182a-459e-ab28-f743e43f8293)  
  
