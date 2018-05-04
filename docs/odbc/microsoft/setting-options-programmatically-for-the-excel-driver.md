---
title: Festlegen von Optionen für Excel-Treibers programmgesteuert | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], setting options programmatically
ms.assetid: b5ee3636-4591-427a-a65a-a2d5926fcc1a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30c48b72009b687e85edafc383213ae048b942f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Festlegen von Optionen für Excel-Treibers programmgesteuert
|Option|Description|Methode|  
|------------|-----------------|------------|  
|Datenquellenname|Ein Name, der die Datenquelle, z. B. Gehaltsabrechnungen oder Mitarbeiter identifiziert.|Um diese Option dynamisch festzulegen, verwenden die **DSN** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Datenbank|Eine Microsoft Access-Datenquelle kann ohne auswählen oder erstellen eine Datenbank eingerichtet werden. Wenn beim Setup keine Datenbank angegeben ist, wird der Benutzer aufgefordert werden, um eine Datei auszuwählen, beim Verbinden mit der Datenquelle.|Um diese Option dynamisch festzulegen, verwenden die **DBQ** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Description|Eine optionale Beschreibung der Daten in der Datenquelle; z. B. "Hire Date, Gehaltsverlauf und aktuelle Überprüfung aller Mitarbeiter."|Um diese Option dynamisch festzulegen, verwenden die **Beschreibung** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Verzeichnis|Zeigt den aktuell ausgewählte Verzeichnis.<br /><br /> Für Microsoft Excel 3.0/4.0-Dateien, die Pfad-Anzeige ist mit der Bezeichnung "Directory", während Sie sich für Microsoft Excel 5.0, 7.0 oder 97-Dateien, die Pfad-Anzeige ist mit der Bezeichnung "Arbeitsmappe".|Um diese Option dynamisch festzulegen, verwenden die **Wert** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Schreibgeschützt|Legt die Datenbank als schreibgeschützt fest.|Um diese Option dynamisch festzulegen, verwenden die **READONLY** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Zu scannende Zeilen|Die Anzahl der Zeilen zu scannen, um den Datentyp jeder Spalte zu bestimmen. Der Datentyp wird bestimmt, angesichts der maximalen Anzahl von Arten von Daten gefunden. Wenn Daten, der den Datentyp für die Spalte ermittelten nicht übereinstimmt erkannt werden, wird der Datentyp als NULL-Wert zurückgegeben.<br /><br /> Microsoft Excel-Treiber können Sie eine Zahl von 1 bis 16 für die Zeilen zu scannen eingeben. Der Standardwert ist 8; Wenn es auf 0 festgelegt ist, werden alle Zeilen gescannt. (Eine Zahl außerhalb der Grenzwert wird einen Fehler zurückgegeben.)|Um diese Option dynamisch festzulegen, verwenden die **MAXSCANROWS** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Wählen Sie Verzeichnis|Zeigt ein Dialogfeld, in dem Sie ein Verzeichnis mit den Dateien, die Sie zugreifen möchten auswählen können.<br /><br /> Wenn Sie ein Quellverzeichnis Daten (für alle mit Ausnahme von Microsoft Access-Treiber) zu definieren, geben Sie das Verzeichnis, in dem die am häufigsten verwendeten Dateien gespeichert sind. Der ODBC-Treiber verwendet dieses Verzeichnis als Standardverzeichnis. Kopieren Sie andere Dateien in dieses Verzeichnis, wenn sie häufig verwendet werden. Alternativ können Sie den Dateinamen in einer SELECT-Anweisung mit dem Verzeichnisnamen qualifizieren:<br /><br /> WÄHLEN SIE \* AUS C:\MYDIR\EMP<br /><br /> Sie können ein neues Standardverzeichnis angeben, mit der **SQLSetConnectOption** Funktion mit der Option SQL_CURRENT_QUALIFIER.<br /><br /> Für Microsoft Excel 3.0 oder 4.0-Dateien die Pfad-Anzeige ist mit der Bezeichnung "Directory", und die Schaltfläche "Auswahl Pfad" ist mit der Bezeichnung "Verzeichnis auswählen". Für Microsoft Excel 5.0, 7.0 oder 97-Dateien die Pfad-Anzeige ist mit der Bezeichnung "Arbeitsmappe", und die Schaltfläche "Auswahl Pfad" ist mit der Bezeichnung "Arbeitsmappe auswählen". Wenn Sie ein Quellverzeichnis Daten zu definieren, geben Sie das Verzeichnis, in dem die am häufigsten verwendeten Microsoft Excel-Dateien für Microsoft Excel 3.0/4.0 befinden, oder das Verzeichnis, in dem die Datei für Microsoft Excel 5.0, 7.0 oder 97 befindet. **Verwenden Sie die aktuellen Verzeichnis** für Microsoft Excel 5.0, 7.0 und 97 deaktiviert ist.|Um diese Option dynamisch festzulegen, verwenden die **Wert** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|
