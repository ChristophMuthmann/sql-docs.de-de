---
title: ODBC Jet SQLConfigDataSource (Excel-Treiber) | Microsoft Docs
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
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00b2295ead09d0196a14248b03ee5f6a96936df6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (Excel-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Excel-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Die **SQLConfigDataSource** -Funktion, die verwendet wird, hinzuzufügen, ändern oder Löschen einer Datenquelle verwendet, die dynamisch die folgenden Schlüsselwörter.  
  
|Schlüsselwort|Description|  
|-------------|-----------------|  
|DBQ|Für Microsoft Excel-Treibers beim Zugriff auf Microsoft Excel 5.0 oder höher Dateien, den Namen der Arbeitsmappendatei an.<br /><br /> Dadurch wird die gleiche Option als **Datenbank** im Dialogfeld "Setup".|  
|WERT|Die Pfadangabe in das Verzeichnis.<br /><br /> Dadurch wird die gleiche Option als **Verzeichnis auswählen** oder **Arbeitsmappe auswählen** im Dialogfeld "Setup".|  
|DESCRIPTION|Eine Beschreibung der Daten in der Datenquelle.<br /><br /> Dadurch wird die gleiche Option als **Beschreibung** im Dialogfeld "Setup".|  
|DRIVER|Die Pfadangabe an den Treiber-DLL.|  
|DRIVERID|Eine ganzzahlige ID für den Treiber.<br /><br /> 534 (Microsoft Excel 3.0)<br /><br /> 278 (Microsoft Excel 4.0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|FIL|Dateityp, z. B. Excel-3.0, Excel 4.0, 5.0 Excel, Excel 7.0, Excel 97, Excel 2000 oder Excel 2003.|  
|FIRSTROWHASNAMES|Gibt an, ob die Zellen der ersten Zeile des Bereichs der Spaltennamen für die Tabelle (1) oder nicht enthalten (0).|  
|MAXSCANROWS|Die Anzahl der Zeilen, die beim Festlegen des Datentyps einer Spalte, die basierend auf vorhandenen Daten geprüft werden.<br /><br /> Eine Zahl zwischen 1 und 16 kann für die Zeilen eingegeben werden. Der Standardwert ist 8; Wenn es auf 0 festgelegt ist, werden alle Zeilen gescannt. (Eine Zahl außerhalb der Grenzwert wird einen Fehler zurückgegeben.)<br /><br /> Dadurch wird die gleiche Option als **zu scannende Zeilen** im Dialogfeld "Setup".|  
|READONLY|True, um die Datei schreibgeschützt machen. "False", um die Datei nicht schreibgeschützt sein.<br /><br /> Dadurch wird die gleiche Option als **Read Only** im Dialogfeld "Setup".|  
|THREADS|Die Anzahl der Hintergrundthreads für das Modul nutzen. Microsoft Access-Treiber wird dieser Wert wird standardmäßig auf 3 jedoch geändert werden kann. Für die dBASE MicrosoftExceldriver dieser Wert ist 3 und kann nicht geändert werden.<br /><br /> Dadurch wird die gleiche Option als **Threads** im Dialogfeld "Setup".|
