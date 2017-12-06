---
title: SQL-Modi (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 17254008fad944edba94e0f24a180dba1d4bb8ed
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="sql-modes-mysqltosql"></a>SQL-Modi (MySQLToSQL)
SSMA für MySQL kann in verschiedenen SQL-Modi betrieben werden, und diese Modi für verschiedene Clients unterschiedlich anwenden zu kann.  
  
Modi definieren die SQL-Syntax, die MySQL unterstützen soll, und die Art der Validierung überprüft, dass es durchführen soll. Dies erleichtert es, verwenden MySQL in verschiedenen Umgebungen und MySQL mit SQL Server verwenden.  
  
## <a name="sql-modes-grid"></a>Raster für SQL-Modi:  
  
-   SQL-Modi Raster auf Stammebene enthält die folgenden Spalten: **SQL Modusname**, **geladen SQL Modi**, und **effektiver SQL-Modi**.  
  
-   SQL-Modi Raster auf Datenbanken Kategorie, Datenbank, Tabelle Kategorie, Anweisungen Kategorie, Kategorie Ansichten, Tabelle, Sicht, Funktionen, Prozeduren, UDF und Ereignisebene-Objekt enthält die folgenden Spalten: **SQL Modusname**, **vererbt SQL Modi**, und **effektiver SQL-Modi**.  
  
-   SQL-Modi Raster gespeicherte Prozedur, die gespeicherte Funktion und Trigger Ebene enthält die folgenden Spalten: **SQL Modusname**, **ursprünglichen SQL-Modi**, und **effektiver SQL-Modi**.  
  
> [!NOTE]  
> Gruppe Modi in angezeigt werden fett, unter der Spalte 'SQL-Modusname'.  
  
## <a name="loaded-sql-modes"></a>Geladene SQL-Modi  
Hierbei handelt es sich um die SQL-Modi, die Ebene der Sitzung oder Stamm festgelegt werden. Die SQL-Modi, die einmal geladen, in der Zieldatenbank kann nicht bearbeitet oder geändert werden.  
  
## <a name="inherited-sql-modes"></a>Geerbte SQL-Modi  
Hierbei handelt es sich um die SQL-Modi, die vom entsprechenden übergeordneten Knoten geerbt werden.  
  
Mit Ausnahme der Kategorie "Funktionen", Kategorie Prozeduren (Ereigniskategorie) und Trigger sind diese SQL-Modi auf allen Ebenen (Datenbank, Tabelle Kategorie, Kategorie-Anweisungen, Ansichten Kategorie, Tabelle, Sicht, Funktionen, Prozeduren, UDF und Ereignis-Objekt) vorhanden.  
  
> [!NOTE]  
> Durch Auswahl der **vom übergeordneten Projekt erben** Kontrollkästchen, SQL-Modi geerbt, die vom übergeordneten Knoten geerbt werden kann. Standardmäßig bleibt das Kontrollkästchen ausgewählt.  
  
## <a name="original-sql-modes"></a>Ursprüngliche SQL-Modi  
Hierbei handelt es sich um die SQL-Modi vorhanden auf nur die Ebenen der Funktion, Prozeduren und Trigger.  
  
> [!NOTE]  
> Durch Auswahl der **Original verwenden** überprüfen Feld, die SQL-Modi, die ursprünglich verwendet wurden, in die entsprechende Funktion oder Prozedur oder des Triggers verwendet werden kann. Standardmäßig bleibt das Kontrollkästchen ausgewählt.  
  
## <a name="effective-sql-modes"></a>Effektive SQL-Modi  
Effektive SQL Modi können auf verschiedenen Ebenen auf folgende Weise definiert werden:  
  
-   **Auf Sitzungsebene:**  
  
    1.  Allen geladen SQL Modi aufgerufen werden kann, "Effektiver SQL-Modi".  
  
    2.  Auf dieser Ebene können die effektive SQL Modi direkt und explizit geändert werden.  
  
    3.  Die gültigen SQL-Modus, der explizit festgelegt wird nicht als SQL-Modus geladen vorgenommen und schließlich auf das Objekt angewendet wird.  
  
-   **Ebene der Funktion oder Prozedur oder des Triggers:**  
  
    1.  Die ursprüngliche SQL-Modi aufgerufen werden kann, "Effektiver SQL-Modi".  
  
    2.  Auf dieser Ebene der gültigen SQL-Modus kann explizit geändert werden nur, wenn die **Original verwenden** Kontrollkästchen deaktiviert ist.  
  
    3.  Die gültigen SQL-Modus, der explizit festgelegt wird ist als die ursprüngliche SQL-Modus nicht wiedergegeben und schließlich auf das Objekt angewendet wird.  
  
-   **Auf anderen Knoten als Funktion oder Prozedur oder des Triggers-Ebene:**  
  
    1.  Allen vererbt SQL Modi aufgerufen werden kann, "Effektiver SQL-Modi".  
  
    2.  Auf dieser Ebene der gültigen SQL-Modus kann explizit geändert werden nur, wenn die **vom übergeordneten Projekt erben** Kontrollkästchen deaktiviert ist.  
  
    3.  Die gültigen SQL-Modus, der explizit festgelegt wird nicht als SQL-Modus vererbt vorgenommen und schließlich auf das Objekt angewendet wird.  
  
