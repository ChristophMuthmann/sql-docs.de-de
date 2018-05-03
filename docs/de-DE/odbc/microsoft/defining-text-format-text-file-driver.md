---
title: Definieren von Text-Format (Text-Datei-Treiber) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: 3af46dad-52cc-4d5c-a27e-6315d65a74e6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6f5954e7ffe41a7b2d1f6ea66ea651e1db8024a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="defining-text-format-text-file-driver"></a>Definieren von Text-Format (Text-Datei-Treiber)
Wenn der Text-Treiber verwendet wird, können Sie die **Textformat definieren** (Dialogfeld), um das Format für Spalten in einer ausgewählten Datei zu definieren. Dieses Dialogfeld können Sie das Schema für jede Datentabelle angeben. Diese Informationen werden in eine Schema.ini-Datei in das Datenverzeichnis für die Quelle geschrieben. Separate Datei "Schema.ini" wird für jedes Text Data Source-Verzeichnis erstellt.  
  
> [!NOTE]  
>  Das gleiche Standard-Dateiformat gilt für alle neuen Datentabellen von Text. Alle Dateien, die von der CREATE TABLE-Anweisung erstellt, erben die gleichen Format Standardwerte, die festgelegt werden, durch Auswählen der Datei Formatierung von Werten in der **Textformat definieren** Dialogfeld mit \<Standardwert > in der ausgewählt**Tabellen** Liste. Der Treiber Text ändert sich nicht auf das Format einer vorhandenen Textdatei entsprechend das in diesem Dialogfeld definierte Format jedoch einen Fehler zurück, wenn Sie das Format, z. B. beim Versuch zum Abrufen von Daten aus der Textdatei verwendet.  
  
 Die folgenden Optionen stehen in der **Textformat definieren** (Dialogfeld):  
  
|Option|Informationen|  
|------------|-----------------|  
|**Hinzufügen**|Fügt eine Spalte mit den Werten in **Datentyp**, **Namen**, und **Breite** aus dem Dialogfeld und, falls zutreffend, das Trennzeichen für Datumsangaben aus Schema.ini Wert.|  
|**Zeichen**|**ANSI** oder **OEM**. OEM gibt einen nicht-ANSI-Zeichensatz. Wird standardmäßig OEM, wenn das Format des Elements im ausgewählten der **Tabellen** Liste wurde von diesem Dialogfeld nicht zuvor definiert.|  
|**Name der Spaltenüberschrift**|Gibt an, ob die Spalten der ersten Zeile der ausgewählten Tabelle als Spaltennamen verwendet werden. Entweder **"true"** oder **"false"**. Wird standardmäßig auf "false", wenn das Format des ausgewählten Elements in der **Tabellen** Liste wurde von diesem Dialogfeld nicht zuvor definiert.|  
|**Spalten**|Listet die Spaltennamen für jede Spalte in der ausgewählten Tabelle an. Die Reihenfolge der Spalten entspricht der Reihenfolge der Spalten in der Tabelle. Diese Liste ist aktiviert, wenn eine Datei ausgewählt wurde die **Tabellen** Liste.|  
|**Datentyp**|BIT, BYTE, CHAR, Währung, Datum, "float", Integer-, LONGCHAR, kurze oder einzelne möglich. Date-Datentypen kann in den folgenden Formaten: "Dd-mmm-Yy", "mm-Dd-Yy", "mmm-Dd-Yy", "Yyyy-mm-Dd" oder "Yyyy-mmm-Dd". "mm" kennzeichnet die Zahlen für Monate; "mmm" kennzeichnet Buchstaben Monate.|  
|**Trennzeichen**|Gibt das benutzerdefinierte Trennzeichen zum Trennen der Spalten verwendet werden. Aktiviert, wenn die **als Trennzeichen für benutzerdefinierte** Format ausgewählt ist. Das Trennzeichen kann nur ein Zeichen lang sein und doppelte Anführungszeichen (") kann nicht als Trennzeichen verwendet werden. (Das Trennzeichen kann nicht im Hexadezimal-oder Dezimalformat angegeben werden.)|  
|**Format**|Mit Trennzeichen oder mit fester Länge. Wenn Trennzeichen, gibt den Typ des Trennzeichens verwendet: durch Kommas (CSV), Tabstopp oder Sonderzeichen (Benutzerdefiniert). Wird standardmäßig **als CSV-Trennzeichen** , wenn das Format des Elements im ausgewählten der **Tabellen** Liste wurde von diesem Dialogfeld nicht zuvor definiert.<br /><br /> Wenn **Format** fester Länge ist und **Kopfzeile der Spalte Name** ist "true", die erste Zeile muss durch Kommas getrennt werden.|  
|**Erraten**|Generiert automatisch die Werte der Spalte Daten Typ, Name und die Breite der Spalten in der ausgewählten Tabelle durch das Scannen der Tabelleninhalte gemäß der **Format** Feld Auswahl. Aktiviert, wenn das Tabellenformat getrennt wird. Alle zuvor definierten Spalten in der **Spalten** Liste werden gelöscht und neue Einträge ersetzt. Wenn **Kopfzeile der Spalte Name** ist nicht aktiviert, Spaltennamen werden automatisch generiert, als "F1", "F2" und So weiter. Kein Standardwert wird angezeigt, der **Datentyp** Feld.<br /><br /> Diese Funktion funktioniert nur auf Spalten, die kleiner als 64,513 Bytes sind.|  
|**Ändern**|Ändert die ausgewählte Spalte mit den Werten in **Datentyp**, **Namen**, und **Breite**.|  
|**Name**|Zeigt den Namen der ausgewählten Spalte an. Kann verwendet werden, um einen neuen Spaltennamen ein für eine vorhandene Spalte oder eine neue Spalte anzugeben.<br /><br /> Wenn **Kopfzeile der Spalte Name** ist "true", der Spalte angezeigte Name wird ignoriert.|  
|**Entfernen**|Löscht die ausgewählte Spalte an.|  
|**Zu scannende Zeilen**|Die Anzahl der Zeilen, die von Setup oder der Treiber überprüft werden, wenn Sie die Spalten und Spaltendatentypen basierend auf vorhandenen Daten festlegen.<br /><br /> Sie können eine Zahl zwischen 1 und 32767 für die Anzahl der Zeilen eingeben. Wird standardmäßig auf 25, wenn das Format des ausgewählten Elements in der **Tabellen** Liste wurde von diesem Dialogfeld nicht zuvor definiert. (Eine Zahl außerhalb der Grenzwert wird einen Fehler zurückgegeben.)|  
|**Tabellen**|Enthält eine Liste aller Dateien im Verzeichnis ausgewählt, die der **Text Setup** (Dialogfeld), die die Liste der Erweiterungen, die angegebene entsprechen.<br /><br /> Wenn \<Standardwert > aktiviert ist, und eine der folgenden ist "true" werden die Werte der Attribute für die Tabelle in der **Tabellen** Gruppe Schema.ini (es sind keine weiteren Einträge in "Schema.ini" berührt) geschrieben werden:<br /><br /> – Es gibt keine Schema.ini im angegebenen Verzeichnis.<br />-Die Schema.ini-Datei vorhanden ist, aber es gibt keine im Schema.ini eines Text-Dateien (mit der angegebenen Erweiterung) in das Verzeichnis.<br />-Abschnitt für eine Textdatei, die in "Schema.ini" vorhanden ist, aber der Nachrichtentext leer ist.<br /><br /> Wenn \<Standardwert > aktiviert ist, die **Spalten** Gruppe ist deaktiviert.|  
|**Breite**|Die Breite der Spalte kann für CHAR "oder" LONGCHAR Spalten geändert werden. Die Breite wird standardmäßig auf 1, wenn das Format des ausgewählten Elements in der **Tabellen** Liste wurde von diesem Dialogfeld nicht zuvor definiert.<br /><br /> Für andere Datentypen Steuern der Breite ist deaktiviert und wird kein Wert angezeigt.|
