---
title: Konvertierungseinstellungen (MySQLToSQL) | Microsoft Docs
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
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b83e86ce201343d624974244a9d551fb1016d3e7
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="conversion-settings-mysqltosql"></a>Konvertierungseinstellungen (MySQLToSQL)
Die **"Einstellungen"** Registerkarte kann der Benutzer knoteneinstellungen festgelegt. Die Registerkarte "an den folgenden Knoten der Metabasis zur Verfügung:  
  
-   Datenbankknoten  
  
-   Kategorie von Funktionen  
  
-   Funktionsknoten  
  
-   Kategorie Tabellen  
  
-   Table-Knoten  
  
## <a name="specifications"></a>Spezifikationen:  
Die **Einstellungen** Registerkarte verfügt über zwei benutzereinstellungen und begrenzt.:  
  
1.  Funktion-Konvertierung  
  
2.  Tabellenkonvertierung  
  
Diese Einstellungen werden basierend auf den Typ des Metabase-Knotens. Beispielsweise wird Funktion Konvertierung im Zusammenhang festlegen auf den Tabellenknoten nicht verfügbar  
  
> [!NOTE]  
> -   Die vom Benutzer vorgenommene Änderungen werden im Arbeitsbereich "Projekt" als eine separate Einstellung-Datei gespeichert werden.  
> -   Die Erweiterung dieser Datei werden **Ccprefs**.  
  
1.  **Einstellung für die Konvertierung von Funktion:**  
  
    1.  Diese Registerkarte enthält **"Force Funktion Konvertierung"** Option. Die Option kann einen der folgenden vier Werte aufweisen:  
  
        -   Konvertieren Sie gemäß den Einstellungen für Projektdateien [vererbt]  
  
        -   In einer Funktion immer konvertieren  
  
        -   Konvertieren Sie immer in einer Prozedur  
  
        -   Konvertieren Sie gemäß den Einstellungen für Projektdateien  
  
    2.  Basierend auf den Einstellungen, wird die Funktion an eine Funktion oder einer gespeicherten Prozedur konvertiert werden.  
  
    3.  Vom Benutzer festgelegten Einstellungen werden gespeichert, in der Voreinstellungendatei kaskadierenden durch Klicken auf **übernehmen** Schaltfläche.  
  
2.  **Einstellung für die Konvertierung von Tabelle:**  
  
    1.  Diese Registerkarte enthält **"ROWID unterdrücken zusätzlichen Spalte Generation"** Option. Die Option kann einen der folgenden vier Werte aufweisen:  
  
        -   Konvertieren Sie gemäß den Einstellungen für Projektdateien [vererbt]  
  
        -   ja  
  
        -   Nein  
  
        -   Konvertieren Sie gemäß den Einstellungen für Projektdateien  
  
    2.  Wenn **'Ja'**, diese Einstellung verhindert die Erstellung der ROWID zusätzlichen Spalte Erstellung für Zieltabellen.  
  
    3.  Die vom Benutzer vorgenommene Einstellungen werden in kaskadierenden Voreinstellungsdatei durch Klicken auf gespeichert **übernehmen** Schaltfläche.  
  
## <a name="see-also"></a>Siehe auch  
[Projekteinstellungen (Konvertierung) (MySQL zu SQL)](http://msdn.microsoft.com/en-us/7ad5fe44-6445-4ba8-a457-5af792631f11)  
  

