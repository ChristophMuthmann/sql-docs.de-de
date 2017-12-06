---
title: Projekteinstellungen (Konvertierung) (MySQLToSQL) | Microsoft Docs
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
ms.assetid: 7ad5fe44-6445-4ba8-a457-5af792631f11
caps.latest.revision: "19"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5c40fe3bcc95b062b188c041477011358d60fba2
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="project-settings-conversion-mysqltosql"></a>Projekteinstellungen (Konvertierung) (MySQLToSQL)
Die Seite "Konvertierung", der die **Projekteinstellungen** Dialogfeld enthält Einstellungen, anpassen, wie SSMA MySQL-Syntax in SQL Server- bzw. SQL Azure-Syntax konvertiert.  
  
Bereich Konvertierung finden Sie in der **Projekteinstellungen** und **Projekt Standardeinstellungen** Dialogfelder.  
  
-   Verwenden der **Projekt Standardeinstellungen** (Dialogfeld), Konfigurationsoptionen für alle Projekte festzulegen. Zum Zugriff auf den Konvertierungseinstellungen für die in den **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**, Migrationstyp-Projekt für die Einstellungen erforderlich sind, angezeigt oder geändert werden, wählen **Migration Zielversion** Dropdown-Liste, klicken Sie auf **allgemeine** am unteren Rand des linken Bereich, und klicken Sie dann wählen **Konvertierung**.  
  
-   Zum Angeben von Einstellungen für das aktuelle Projekt auf die **Tools** klicken Sie im Menü **Projekteinstellungen**, klicken Sie dann auf **allgemeine** am unteren Rand der linken Bereich, und klicken Sie dann auf **Konvertierung**.  
  
## <a name="options"></a>enthalten  
  
### <a name="collate-clause"></a>COLLATE-Klausel  
  
|||  
|-|-|  
|**Begriff**|**Definition**|  
|**Explizite Konvertierung der COLLATE-Klausel**|Explizite Konvertierungsoption für COLLATE-Klausel gibt an, wie explizite COLLATE-Klauseln in MySQL-Code zu konvertieren. Mögliche Optionen: Ignorieren und mit einer Warnung markieren / ein Fehler generiert<br /><br />**Standardmodus**: ignorieren und Markierung mit einer Warnung<br /><br />**Vollständige**: ignorieren und Markierung mit einer Warnung<br /><br />**Vollständige Modus**: ignorieren und Markierung mit einer Warnung|  
  
### <a name="column-constraints"></a>Spalteneinschränkungen  
  
|||  
|-|-|  
|**Begriff**|**Definition**|  
|**Einschränkung für Spalten des Datentyps ENUM generieren**|Einschränkung für Spalten des ENUM-Datentyps in der SQL Server- oder SQL Azure-Tabelle generiert, wenn es nicht in der MySQL-Tabelle vorhanden ist. Falls Ja, werden allen konvertierte Spalten des ENUM-Datentyps mit CHECK-Einschränkung des Werts steuern begleitet.<br /><br />**Standardmodus**: Nein<br /><br />**Vollständige**: Nein<br /><br />**Vollständige Modus**: Ja|  
|**Einschränkung für Spalten des Datentyps Satz generieren**|Einschränkung für Spalten des Datentyps für die Gruppe in der SQL Server- oder SQL Azure-Tabelle generiert, wenn es nicht in der MySQL-Tabelle vorhanden ist. Falls Ja, werden alle konvertierte Spalten des Datentyps für die Gruppe mit CHECK-Einschränkung des Werts steuern begleitet werden.<br /><br />**Standardmodus**: Nein<br /><br />**Vollständige**: Nein<br /><br />**Vollständige Modus**: Ja|  
|**Generieren Sie Einschränkung für Spalten mit Spalten vom Typ ohne Vorzeichen numerische Daten**|Fügen Sie Kontrollkästchen für nicht negativen Wert Spalten ohne Vorzeichen numerischen Datentypen.<br /><br />**Standardmodus**: Nein<br /><br />**Vollständige**: Nein<br /><br />**Vollständige Modus**: Ja|  
|**Einschränkung für Jahr-datentypspalten generieren**|Einschränkung für Jahr-datentypspalten in der SQL Server- oder SQL Azure-Tabelle generiert, wenn es nicht in der MySQL-Tabelle vorhanden ist. Falls Ja, konvertiert alle Spalten der Daten für das Jahr Typ mit CHECK-Einschränkung des Werts steuern begleitet.<br /><br />**Standardmodus**: Nein<br /><br />**Vollständige**: Nein<br /><br />**Vollständige Modus**: Ja|  
  
### <a name="data-types"></a>Datentypen  
  
|||  
|-|-|  
|**Begriff**|**Definition**|  
|**ENUM-datentypkonvertierung**|Gibt an, wie MySQL ENUM-Datentyp konvertiert werden soll, entweder als in NVARCHAR konvertieren oder Umwandeln in numerischen<br /><br />**Standardmodus**: in NVARCHAR konvertieren<br /><br />**Vollständige**: in NVARCHAR konvertieren<br /><br />**Vollständige Modus**: in NVARCHAR konvertieren|  
|**SET-datentypkonvertierung**|Gibt an, wie der Datentyp MySQL festgelegt werden sollen, NVARCHAR (L) konvertiert, konvertieren / in BINARY(L) konvertieren<br /><br />**Standardmodus**: in NVARCHAR(L) konvertieren<br /><br />**Vollständige**: in NVARCHAR(L) konvertieren<br /><br />**Vollständige Modus**: in NVARCHAR(L) konvertieren|  
  
### <a name="generic"></a>Generisch  
  
|||  
|-|-|  
|**Begriff**|**Definition**|  
|**Spalten ohne Standardwert in INSERT- und ersetzen**|Wenn "Ja", alle Anweisungen, die auf Tabellen mithilfe von gespeicherten Module als MyISAM und InnoDb verweisen mit Warnmeldungen für die Konvertierung markiert werden soll.<br /><br />**Standardmodus**: Spaltenliste hinzufügen<br /><br />**Vollständige**: Spaltenliste hinzufügen<br /><br />**Vollständige Modus**: Spaltenliste hinzufügen|  
|**Division durch Null-Konvertierung erzeugt.**|Gibt an, ob MySQL ohne ERROR_FOR_DIVISION_BY_ZERO Verhalten zu emulieren.<br /><br />**Standardmodus**: Fehler<br /><br />**Vollständige**: Fehler<br /><br />**Vollständige Modus**: NULL|  
|**IN-Operator**|Gibt an, wie IN MySQL-Operator zu konvertieren.<br /><br />**Standardmodus**: immer in IN konvertieren<br /><br />**Vollständige**: immer in IN konvertieren<br /><br />**Vollständige Modus**: Erweitern Sie bei Bedarf|  
|**Konvertierung von MySQL-Funktion**|Gibt an, wie standard-MySQL-Funktionen zu konvertieren.<br /><br />**Standardmodus**: optimistische<br /><br />**Vollständige**: optimistische<br /><br />**Vollständige Modus**: präzise|  
|**Speicher-Modulen unterstützt nicht**|Wenn "Ja", alle Anweisungen, die auf Tabellen mithilfe von gespeicherten Module als MyISAM und InnoDb verweisen mit Warnmeldungen für die Konvertierung markiert werden soll.<br /><br />**Standardmodus**: Nein<br /><br />**Vollständige**: Nein<br /><br />**Vollständige Modus**: Ja|  
|**Unterdrücken der ROWID zusätzlichen Spalte generieren**|Falls Ja, verhindert die Erstellung von ROWD zusätzlichen Spalte Erstellung für Zieltabellen. Kann sich auf die Migration von einigen Strukturen auswirken.<br /><br />**Standardmodus**: Nein<br /><br />**Vollständige**: Nein<br /><br />**Vollständige Modus**: Nein|  
|**Konvertierung der TRUNCATE-Anweisung**|Gibt an, wie kürzungsanweisungen zu konvertieren.<br /><br />**Standardmodus**: ABSCHNEIDEN<br /><br />**Vollständige**: ABSCHNEIDEN<br /><br />**Vollständige Modus**: ABSCHNEIDEN|  
  
### <a name="misc"></a>Sonstiges  
  
|||  
|-|-|  
|**Begriff**|**Definition**|  
|**Standardmäßige Schemazuordnung**|Gibt an, wie MySQL-Datenbanken in SQL Server-Schemas zuordnen.<br /><br />**Standardmodus**: Datenbanken<br /><br />**Vollständige**: Datenbanken<br /><br />**Vollständige Modus**: Datenbanken|  
  
### <a name="procedures-and-functions"></a>Prozeduren und Funktionen  
  
|||  
|-|-|  
|**Begriff**|**Definition**|  
|**Konvertierung von Standard-Funktion**|Gibt an, ob Funktionen sollten in der Standardeinstellung werden konvertiert werden T-SQL-Funktionen oder gespeicherte Prozeduren.<br /><br />**Standardmodus**: Funktion konvertieren<br /><br />**Vollständige**: Funktion konvertieren<br /><br />**Vollständige Modus**: Funktion konvertieren|  
|**SET XACT_ABORT auf generieren**|Gibt an, ob SET XACT_ABORT ON muss am Anfang der konvertierten Prozedur oder des Triggers hinzugefügt werden.<br /><br />**Standardmodus**: Ja<br /><br />**Vollständige**: Ja<br /><br />**Vollständige Modus**: Ja|  
|**Generieren von SET NOCOUNT auf**|Gibt an, ob SET NOCOUNT ON muss am Anfang der konvertierten Prozedur oder des Triggers hinzugefügt werden.<br /><br />**Standardmodus**: Ja<br /><br />**Vollständige**: Ja<br /><br />**Vollständige Modus**: Ja|  
  
### <a name="spatial-data-types"></a>Räumliche Datentypen  
  
|||  
|-|-|  
|**Begriff**|**Definition**|  
|**Standard umgebendes Feld {"xmax" &#124; XMIN &#124; YMAX &#124; "Ymin"} für räumliche Indizes**|Standardwert definiert für {"xmax" &#124; XMIN &#124; YMAX &#124; "Ymin"}-Parameter des umgebenden Felds in räumliche Indizes verwendet.<br /><br />**Standardmodus**<br /><br />"XMAX": 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />"YMIN": 0<br /><br />**Optimistische Modus**<br /><br />"XMAX": 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />"YMIN": 0<br /><br />**Vollbildmodus**<br /><br />"XMAX": 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />"YMIN": 0|  
|**Standardrasterdichte für räumliche Indizes**|Standardwert definiert für LEVEL_1, LEVEL_2 LEVEL_3 und LEVEL_4 von rasterdichte im räumlichen Indizes verwendet.<br /><br />**Standardmodus**<br /><br />LEVEL_1: Standard<br /><br />LEVEL_2: Standard<br /><br />LEVEL_3: Standard<br /><br />LEVEL_4: Standard<br /><br />**Optimistische Modus**<br /><br />LEVEL_1: Standard<br /><br />LEVEL_2: Standard<br /><br />LEVEL_3: Standard<br /><br />LEVEL_4: Standard<br /><br />**Vollbildmodus**<br /><br />LEVEL_1: Standard<br /><br />LEVEL_2: Standard<br /><br />LEVEL_3: Standard<br /><br />LEVEL_4: Standard|  
  
### <a name="transactions"></a>Transaktionen  
  
|||  
|-|-|  
|**Begriff**|**Definition**|  
|**Nicht transaktionaler Tabellen**|Gibt an, und zwar unabhängig davon, ob alle Verweise auf die Tabelle, die keine Transaktionen unterstützen mit Warnmeldungen für die Konvertierung markiert werden soll.<br /><br />**Standardmodus**: Nein<br /><br />**Vollständige**: Nein<br /><br />**Vollständige Modus**: Ja|  
|**Transaktionsisolationsstufe**|Gibt an, welche Isolationsstufe für Transaktionen für neue Transaktionen verwendet werden soll.<br /><br />**Standardmodus**: Standard<br /><br />**Vollständige**: Standard<br /><br />**Vollständige Modus**: Repeatable Read|  
  
### <a name="value-control"></a>Steuerelement für Werte  
  
|||  
|-|-|  
|**Begriff**|**Definition**|  
|**Zeichen, das numerische Konvertierung**|Gibt implizite und explizite Konvertierung von Zeichendatentyp in numerische Datentypen zu behandeln.<br /><br />**Standardmodus**: optimistische<br /><br />**Vollständige**: optimistische<br /><br />**Vollständige Modus**: präzise|  
|**Steuern von numerischen Werten ohne Vorzeichen**|Zuweisen von Werten ohne Vorzeichen numerische Variablen und Parameter-Steuerelement.<br /><br />**Standardmodus**: Nein<br /><br />**Vollständige**: Nein<br /><br />**Vollständige Modus**: Ja|  
|**Steuern von nicht SIGNIERTEN Subtraktion**|Ändern Sie negative Werte in Spalten vom Datentyp ohne Vorzeichen eingefügt.<br /><br />**Standardmodus**: Konvertieren von "als-ist"<br /><br />**Vollständige**: Konvertieren von "als-ist"<br /><br />**Vollständige Modus**: Markieren einer Warnung|  
|**Konvertierung in und aus Binary-Datentyp**|Gibt implizite und explizite Konvertierung von Binary-Datentyp zu behandeln.<br /><br />**Standardmodus**: optimistische<br /><br />**Vollständige**: optimistische<br /><br />**Vollständige Modus**: präzise|  
|**Geben Sie die Konvertierung in Datum/Uhrzeit-Daten**|Gibt so behandeln Sie implizite und explizite Konvertierung in Datum/Uhrzeit-Datentyp.<br /><br />**Standardmodus**: emulieren MySQL-Format<br /><br />**Vollständige**: Verwenden von SQL Server-Format<br /><br />**Vollständige Modus**: emulieren MySQL-Format|  
|**Numerische Literale mit einer Genauigkeit 38 überschreitet**|Gibt an, wie numerische Literale mit einer Genauigkeit 38 überschreitet zu konvertieren.<br /><br />**Standardmodus**: gerundet wird, wenn möglich<br /><br />**Vollständige**: gerundet wird, wenn möglich<br /><br />**Vollständige Modus**: gerundet wird, wenn möglich|  
|**NULL-Datum in NOT NULL-Spalten**|Gibt Zuweisung zu NOT NULL-Spalten von 0 (null) bis Datum, 0 (null) in Datum oder ungültige Datum/Uhrzeit-Werte zu behandeln.<br /><br />**Standardmodus**: GETDATE()<br /><br />**Vollständige**: GETDATE()<br /><br />**Vollständige Modus**: GETDATE()|  
  
## <a name="see-also"></a>Siehe auch  
[Referenz zur Benutzeroberfläche &#40; MySQLToSQL &#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
  
