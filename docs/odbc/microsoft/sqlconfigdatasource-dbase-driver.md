---
title: SQLConfigDataSource (dBASE-Treiber) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f4db30f9e0c291151409d5af6a63226c0c2292bd
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE-Treiber)
> [!NOTE]  
>  Dieses Thema enthält dBASE treiberspezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Die **SQLConfigDataSource** -Funktion, die verwendet wird, hinzuzufügen, ändern oder Löschen einer Datenquelle verwendet, die dynamisch die folgenden Schlüsselwörter.  
  
|Schlüsselwort|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|Die Reihenfolge, in der die Felder sortiert werden.<br /><br /> Die Sequenz sein kann: ASCII (Standard) oder International.<br /><br /> Dadurch wird die gleiche Option als **sortieren Sequenz** im Dialogfeld "Setup".|  
|WERT|Die Pfadangabe in das Verzeichnis.|  
|DELETED|DBASE-Treiber gibt an, ob Zeilen, die als gelöscht markiert wurden abgerufen oder auf positioniert werden können. Wenn der Satz auf 1 festgelegt ist und gelöschten Zeilen nicht angezeigt werden. Wenn 0, gelöschte Zeilen werden gleich behandelt, als Zeilen nicht gelöscht.<br /><br /> Dadurch wird die gleiche Option als **gelöschte Zeilen anzeigen** im Dialogfeld "Setup".|  
|DESCRIPTION|Eine Beschreibung der Daten in der Datenquelle.<br /><br /> Dadurch wird die gleiche Option als **Beschreibung** im Dialogfeld "Setup".|  
|DRIVER|Die Pfadangabe an den Treiber-DLL.|  
|DRIVERID|Eine ganzzahlige ID für den Treiber.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|Datei geben dBase III, dBase IV oder dBase 5|  
|' PAGETIMEOUT '|Gibt die Zeitspanne in Zehntelsekunden, die eine Seite (sofern nicht verwendet) im Puffer bleibt, bevor Sie entfernt werden. Die Standardeinstellung ist 600 Zehntelsekunden (60 Sekunden). Beachten Sie, dass diese Option für alle Datenquellen gilt, die den ODBC-Treiber verwenden.<br /><br /> Dadurch wird die gleiche Option als **Page Timeout** im Dialogfeld "Setup".|  
|READONLY|True, um die Datei schreibgeschützt machen. "False", um die Datei nicht schreibgeschützt sein.<br /><br /> Dadurch wird die gleiche Option als **Read Only** im Dialogfeld "Setup".|  
|STATISTICS|Für den Treiber dBASE bestimmt, ob Statistiken für Tabellen Größe angeglichen werden. Beachten Sie, dass diese Option für alle Datenquellen gilt, die den ODBC-Treiber verwenden.<br /><br /> Dadurch wird die gleiche Option als **Ungefähre Zeilenanzahl** im Dialogfeld "Setup".|  
|THREADS|Die Anzahl der Hintergrundthreads für das Modul nutzen. Dieser Wert ist 3 und kann nicht geändert werden.<br /><br /> Dadurch wird die gleiche Option als **Threads** im Dialogfeld "Setup".|

