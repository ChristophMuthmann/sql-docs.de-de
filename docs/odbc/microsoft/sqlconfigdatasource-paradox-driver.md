---
title: SQLConfigDataSource (Paradox-Treiber) | Microsoft Docs
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
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b9acd359d2d99531e3fe4092b3bd20f00e94622a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (Paradox-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Paradox treiberspezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Die **SQLConfigDataSource** -Funktion, die verwendet wird, hinzuzufügen, ändern oder Löschen einer Datenquelle verwendet, die dynamisch die folgenden Schlüsselwörter.  
  
|Schlüsselwort|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|Die Reihenfolge, in der die Felder sortiert werden.<br /><br /> Wenn der Paradox-Treiber verwendet wird, kann die Sequenz ASCII (Standard), internationale, Schwedisch Finnisch oder Norwegisch Dänisch.<br /><br /> Dadurch wird die gleiche Option als **sortieren Sequenz** im Dialogfeld "Setup".|  
|DBQ|Der Name der Datenbankdatei.<br /><br /> Dadurch wird die gleiche Option als **Datenbank** im Dialogfeld "Setup".|  
|WERT|Die Pfadangabe in das Verzeichnis.|  
|DESCRIPTION|Eine Beschreibung der Daten in der Datenquelle.<br /><br /> Dadurch wird die gleiche Option als **Beschreibung** im Dialogfeld "Setup".|  
|DRIVER|Die Pfadangabe an den Treiber-DLL.|  
|DRIVERID|Eine ganzzahlige ID für den Treiber.<br /><br /> 26 (Paradox 3.x)<br /><br /> 282 (Paradox 4.x)<br /><br /> 538 (Paradox 5.x)|  
|EXKLUSIVE|Bestimmt, ob die Datenbank im exklusiven Modus (Zugriff durch nur einen Benutzer zu einem Zeitpunkt) geöffnet wird oder Modus freigegebenen (Zugriff durch mehrere Benutzer gleichzeitig). "True" (exklusiven Modus) oder "false" (im freigegebenen Modus) möglich.<br /><br /> Dadurch wird die gleiche Option als **exklusive** im Dialogfeld "Setup".|  
|FIL|Dateityp Paradox 3.x, Paradox 4.x oder Paradox 5.x|  
|DATEITYP|Der Dateityp für den Text-Treiber (Text).|  
|' PAGETIMEOUT '|Gibt die Zeitspanne in Zehntelsekunden, die eine Seite (sofern nicht verwendet) im Puffer bleibt, bevor Sie entfernt werden. Die Standardeinstellung ist 600 Zehntelsekunden (60 Sekunden). Beachten Sie, dass diese Option für alle Datenquellen gilt, die den ODBC-Treiber verwenden.<br /><br /> Dadurch wird die gleiche Option als **Page Timeout** im Dialogfeld "Setup".|  
|X|Der vollständige Pfad des Verzeichnisses, eine Datenbank Paradox Sperren enthält, da sie entweder die Datei PDOXUSRS.net enthält (in 4 Paradox. *X*) oder die Datei PARADOX.net (5 Paradox. *X*). Wenn das Verzeichnis nicht eine dieser Dateien enthält, erstellt der Paradox-Treiber eine. Informationen zu diesen Dateien finden Sie unter der Paradox-Dokumentation.<br /><br /> Vor einem Netzwerkverzeichnis ausgewählt werden kann, muss ein Benutzername Paradox eingegeben werden.<br /><br /> Dadurch wird die gleiche Option als **Netzwerkverzeichnis wählen** im Dialogfeld "Setup".|  
|PARADOXNETSTYLE|Für den Treiber Paradox auf das Netzwerk zu verwendende Format beim Paradox-Daten zugreifen: entweder "3.x" für Paradox 3. *x* oder "4.x" für Paradox 4. *X* oder 5. *X*. Kann festgelegt werden, "3.x" oder "4.x" ist die Version 4 Paradox. *x* oder 5. *X*; Wenn die Version 3 Paradox. *X*, das Format muss "3.x" sein.<br /><br /> Dadurch wird die gleiche Option als **Net Stil** im Dialogfeld "Setup".|  
|PARADOXUSERNAME|Für den Treiber Paradox, den Benutzernamen Paradox.<br /><br /> Dadurch wird die gleiche Option als **Benutzername** im Dialogfeld "Setup".|  
|PWD|Das Kennwort.<br /><br /> Dies ist ein optionales Schlüsselwort, und wird vom Treiber nie in die Datei geschrieben werden. Es dient in einem Aufruf von **SQLDriverConnect** für Paradox Dateien Kennwort geschützt. Das verwendete Kennwort ist gültig, wenn eine Tabelle geöffnet wird. Wenn kein Kennwort in der Verbindungszeichenfolge übergeben wird, wird kein Kennwort für diese Tabelle eingerichtet. Wenn Tabellen unterschiedliche Kennwörter haben, mehr als eine kann nicht in derselben Sitzung geöffnet werden, noch können die Tabellen verknüpft werden.|  
|READONLY|True, um die Datei schreibgeschützt machen. "False", um die Datei nicht schreibgeschützt sein.<br /><br /> Dadurch wird die gleiche Option als **Read Only** im Dialogfeld "Setup".|  
|THREADS|Die Anzahl der Hintergrundthreads für das Modul nutzen. Dieser Wert ist 3 und kann nicht geändert werden.<br /><br /> Dadurch wird die gleiche Option als **Threads** im Dialogfeld "Setup".|

