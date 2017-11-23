---
title: "Festlegen von Optionen für die Datei-Texttreiber programmgesteuert | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5b8127a7249f9f878dcd3d15b9afa874def8c64a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>Festlegen von Optionen für die Datei-Texttreiber programmgesteuert
|Option|Description|Methode|  
|------------|-----------------|------------|  
|Datenquellenname|Ein Name, der die Datenquelle, z. B. Gehaltsabrechnungen oder Mitarbeiter identifiziert.|Um diese Option dynamisch festzulegen, verwenden die **DSN** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Definieren von Format|Zeigt die **Textformat definieren** (Dialogfeld), sodass Sie das Schema für einzelne Tabellen in das Datenverzeichnis für die Quelle angeben.|Diese Option kann nicht dynamisch festgelegt werden, durch den Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Description|Eine optionale Beschreibung der Daten in der Datenquelle; z. B. "Hire Date, Gehaltsverlauf und aktuelle Überprüfung aller Mitarbeiter."|Um diese Option dynamisch festzulegen, verwenden die **Beschreibung** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Verzeichnis|Wählt das gezielte Verzeichnis an.|Um diese Option dynamisch festzulegen, verwenden die **Wert** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Liste der Erweiterungen|Listet die Dateinamenerweiterungen der Textdateien in der Datenquelle an. Wenn der Text-Treiber verwendet wird, wird eine Datei ohne Erweiterung erstellt, wenn die CREATE TABLE-Anweisung mit einem Namen ausgeführt wird, die keine Erweiterung besitzt. Andere Treiber erstellen Sie eine Datei mit der Erweiterung Standardeinstellung, wenn keine Erweiterung angegeben wird. Um eine Datei mit der Erweiterung ".txt" zu erstellen, muss die Erweiterung im Namen enthalten sein. Zum Anzeigen von Dateien ohne Erweiterung in der **Textformat definieren** (Dialogfeld), "*." die Liste der Erweiterungen hinzugefügt werden muss.|Um diese Option dynamisch festzulegen, verwenden die **ERWEITERUNGEN** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Schreibgeschützt|Legt die Datenbank als schreibgeschützt fest.|Um diese Option dynamisch festzulegen, verwenden die **READONLY** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Zu scannende Zeilen|Die Anzahl der Zeilen zu scannen, um den Datentyp jeder Spalte zu bestimmen. Der Datentyp wird bestimmt, angesichts der maximalen Anzahl von Arten von Daten gefunden. Wenn Daten, der den Datentyp für die Spalte ermittelten nicht übereinstimmt erkannt werden, wird der Datentyp als NULL-Wert zurückgegeben.<br /><br /> Für den Text-Treiber können Sie eine Zahl zwischen 1 und 32767 für die Anzahl der Zeilen eingeben; Allerdings wird standardmäßig der Wert immer auf 25. (Eine Zahl außerhalb der Grenzwert wird einen Fehler zurückgegeben.)|Um diese Option dynamisch festzulegen, verwenden die **MAXSCANROWS** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Wählen Sie Verzeichnis|Zeigt ein Dialogfeld, in dem Sie ein Verzeichnis mit den Dateien, die Sie zugreifen möchten auswählen können.<br /><br /> Beim Definieren eines Quellverzeichnisses Daten geben Sie das Verzeichnis, in dem die am häufigsten Dateien verwendeten, befinden. Der ODBC-Treiber verwendet dieses Verzeichnis als Standardverzeichnis. Kopieren Sie andere Dateien in dieses Verzeichnis, wenn sie häufig verwendet werden. Alternativ können Sie den Dateinamen in einer SELECT-Anweisung mit dem Verzeichnisnamen qualifizieren:`SELECT * FROM C:\MYDIR\EMP`<br /><br /> Sie können ein neues Standardverzeichnis angeben, mit der **SQLSetConnectOption** Funktion mit der Option SQL_CURRENT_QUALIFIER.|Um diese Option dynamisch festzulegen, verwenden die **Wert** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|
