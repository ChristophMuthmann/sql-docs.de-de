---
title: "Treiber-Spezifikation Unterschlüssel | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f45130c81f9fc4f669cf95d4bde72155f519c1aa
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="driver-specification-subkeys"></a>Treiber-Spezifikation Unterschlüssel
Jeder Treiber in den ODBC-Treiber-Unterschlüssel aufgeführt verfügt über einen Unterschlüssel selbst. Dieser Unterschlüssel verfügt über den gleichen Namen wie der entsprechende Wert unter dem Unterschlüssel ODBC-Treiber. Die Werte unter dieser Unterschlüssel auflisten, das die vollständigen Pfade der Treiber und Treiber-Setup-DLLs, die Werte der Treiber Schlüsselwörter zurückgegebenes **SQLDrivers**, und die Verwendungsanzahl der. Die Formate der Werte sind wie in der folgenden Tabelle gezeigt.  
  
|Name|Datentyp|data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124; **N**} {**Y**&#124; **N**} {**Y**&#124; **N**}|  
|CreateDSN|REG_SZ|*Treiber-Beschreibung*|  
|Treiber|REG_SZ|*Treiber-DLL-Pfad*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *Datei-extension1*[**,\*.** *Datei-extension2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|Setup|REG_SZ|*Setup-DLL-Pfad*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD-WERT|*count*|  
  
 Die Verwendung von jedes Schlüsselwort ist in der folgenden Tabelle gezeigt.  
  
|Schlüsselwort|Verwendung|  
|-------------|-----------|  
|**APILevel**|Eine Zahl, die ODBC-Schnittstelle Konformitätsgrad vom Treiber unterstützt:<br /><br /> 0 = Keine<br /><br /> 1 = Ebene-1 unterstützt<br /><br /> 2 = Ebene-2 unterstützt<br /><br /> Diese Angabe muss identisch mit der für die SQL_ODBC_INTERFACE_CONFORMANCE-Option in der zurückgegebene Wert **SQLGetInfo**.|  
|**CreateDSN**|Der Name der ein oder mehrere Datenquellen erstellt werden, wenn der Treiber installiert ist. Die Systeminformationen umfasst eine Quelle Spezifikation Datenabschnitt für jede Datenquelle aufgeführt, mit der **CreateDSN** Schlüsselwort. Diese Abschnitte sollten nicht enthalten. der **Treiber** -Schlüsselwort, da dies im Abschnitt Spezifikation Treiber angegeben ist, aber Sie genügend Informationen für auch müssen die **ConfigDSN** Funktion im Treiber Setup-DLL für die Angabe einer Datenquelle zu erstellen, ohne alle Dialogfelder. Das Format eines Abschnitts Data Source-Spezifikation, finden Sie unter [Data Source-Spezifikation Unterschlüssel](../../../odbc/reference/install/data-source-specification-subkeys.md).|  
|**ConnectFunctions**|Eine Zeichenfolge mit drei Zeichen, der angibt, ob der Treiber unterstützt **SQLConnect**, **SQLDriverConnect**, und **SQLBrowseConnect**. Wenn der Treiber unterstützt **SQLConnect**, das erste Zeichen ist "J"; andernfalls ist "N". Wenn der Treiber unterstützt **SQLDriverConnect**, das zweite Zeichen ist "J"; andernfalls ist "N". Wenn der Treiber unterstützt **SQLBrowseConnect**, das dritte Zeichen ist "J"; andernfalls ist "N". Angenommen, ein-Treiber unterstützt **SQLConnect** und **SQLDriverConnect** , aber nicht **SQLBrowseConnect**, drei Zeichen bestehende Zeichenfolge lautet "YYN".|  
|**DriverODBCVer**|Eine Zeichenfolge mit der Version von ODBC, die der Treiber unterstützt. Die Version des Formulars wird *nn.nn*, wobei die ersten beiden Ziffern die Hauptversion sind und die nächsten beiden Ziffern die Nebenversion sind. Für die in diesem Handbuch beschriebenen ODBC-Version muss der Treiber "03.00" zurück.<br /><br /> Diese Angabe muss identisch mit der für die SQL_DRIVER_ODBC_VER-Option in der zurückgegebene Wert **SQLGetInfo**.|  
|**FileExtns**|Für den dateibasierten Treibern kann eine durch Trennzeichen getrennte Liste von Erweiterungen der Dateien den Treiber verwenden. DBASE-Treiber kann zum Beispiel festlegen \*DBF und einen formatierten Text Datei Treiber geben möglicherweise \*".txt",\*CSV. Ein Beispiel dafür, wie eine Anwendung diese Informationen verwenden kann, finden Sie unter der **FileUsage** Schlüsselwort.|  
|**FileUsage**|Eine Zahl, der angibt, wie ein dateibasierte Treiber direkt Dateien in einer Datenquelle behandelt.<br /><br /> 0 = der Treiber ist eine dateibasierte Treiber. Ein ORACLE-Treiber ist z. B. ein DBMS-basierten Treiber.<br /><br /> 1 = eine dateibasierte behandelt Treiberdateien in einer Datenquelle als Tabellen. Xbase-Treiber werden z. B. jede Xbase-Datei als Tabelle behandelt.<br /><br /> 2 = eine dateibasierte behandelt Treiberdateien in einer Datenquelle als Katalog. Beispielsweise behandelt ein Microsoft® Access-Treiber jede Microsoft Access-Datei als eine gesamte Datenbank.<br /><br /> Eine Anwendung kann diese verwenden, um zu bestimmen, wie Benutzer die Daten ausgewählt werden. Beispielsweise denken Xbase und Paradox Benutzer häufig von Daten in Dateien gespeichert werden, während die ORACLE und Microsoft Access-Benutzer in der Regel Daten vorstellen, wie in Tabellen gespeichert.<br /><br /> Wenn ein Benutzer wählt **-Datendatei öffnen** aus der **Datei** Menü, eine Anwendung kann Anzeigen der **Datei geöffnete Fenster** Standarddialogfeld. Die Liste der Dateitypen, verwenden die Dateierweiterungen, die mit angegeben die **FileExtns** Schlüsselwort für Treiber, die angeben, eine **FileUsage** Wert 1 und "Y", als das zweite Zeichen des Werts der  **ConnectFunctions** Schlüsselwort. Nachdem der Benutzer eine Datei auswählt, würde die Anwendung aufrufen **SQLDriverConnect** mit der **Treiber** Schlüsselwort und führen Sie dann eine **wählen \* FROM *Tabellenname***   Anweisung.<br /><br /> Wenn der Benutzer wählt **Daten importieren** aus der **Datei** Menü konnte eine Anwendung eine Liste der Beschreibungen für Treiber, die angeben, Anzeigen einer **FileUsage** Wert von 0 oder 2 und "Y" als das zweite Zeichen des Werts der **ConnectFunctions** Schlüsselwort. Nachdem der Benutzer einen Treiber ausgewählt hat, würde die Anwendung aufrufen **SQLDriverConnect** mit der **Treiber** -Schlüsselwort und zeigen einen benutzerdefinierten **Tabelle auswählen** (Dialogfeld).|  
|**SQLLevel**|Eine Zahl, der angibt, der SQL-92-Grammatik, die vom Treiber unterstützt:<br /><br /> 0 = SQL-92-Eintrag<br /><br /> 1 = FIPS127 2 Transitional<br /><br /> 2 = SQL-92-Zwischenspeicher<br /><br /> 3 = SQL-92-vollständig<br /><br /> Diese Angabe muss identisch mit der für die SQL_SQL_CONFORMANCE-Option in der zurückgegebene Wert **SQLGetInfo**.|  
  
 Informationen zu Verwendungszähler finden Sie unter [zählen Verbrauch](../../../odbc/reference/install/usage-counting.md) weiter oben in diesem Abschnitt.  
  
 Anwendungen sollten die Verwendungsanzahl nicht festlegen. ODBC wird dieser Zähler zu verwalten.  
  
 Beispielsweise angenommen, ein Treiber für Textdateien formatierte einen Treiber-DLL mit dem Namen Text.dll hat, eine separate Treiber Setup DLL mit dem Namen Txtsetup.dll und drei Mal installiert wurde. Wenn der Treiber den Konformitätsgrad Ebene-1-API unterstützt, Konformitätsgrad die minimale SQL-Grammatik unterstützt Dateien als Tabellen behandelt und mit den Erweiterungen ".txt" und CSV-Dateien verwenden, können die Werte unter dem Unterschlüssel Text wie folgt sein:  
  
```  
APILevel : REG_SZ : 1  
ConnectFunctions : REG_SZ : YYN  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\TEXT.DLL  
DriverODBCVer : REG_SZ : 03.00.00  
FileExtns : REG_SZ : *.txt,*.csv  
FileUsage : REG_SZ : 1  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\TXTSETUP.DLL  
SQLLevel : REG_SZ : 0  
UsageCount : REG_DWORD : 0x3  
```

