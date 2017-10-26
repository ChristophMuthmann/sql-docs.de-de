---
title: Translation-DLLs | Microsoft Docs
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
- translation DLLs [ODBC]
ms.assetid: 38975059-b346-410f-bb27-326f3f7bbf39
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 06e496e3999904a019f481374598a9a774729ab3
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="translation-dlls"></a>Translation-DLLs
Die Anwendung und die Datenquellensicht speichern Daten häufig in anderen Zeichensätze. ODBC stellt einen generischen Mechanismus dar, der Daten aus einem Zeichensatz in eine andere übersetzt den Treiber ermöglicht. Es besteht aus einer DLL, die die Übersetzung Funktionen implementiert **SQLDriverToDataSource** und **SQLDataSourceToDriver**, die aufgerufen werden, vom Treiber alle Daten, die zwischen der Datenquelle übersetzt. und -Treiber. Diese DLL-Datei geschrieben werden kann, vom Anwendungsentwickler, die Entwickler Treiber oder einem Drittanbieter stammen.  
  
 Die Übersetzung-DLL für eine bestimmte Datenquelle kann in die Systeminformationen für diese Datenquelle angegeben werden. Weitere Informationen finden Sie unter [Data Source-Spezifikation Unterschlüssel](../../../odbc/reference/install/data-source-specification-subkeys.md). Er kann auch zur Laufzeit mit der SQL_ATTR_TRANSLATE_DLL und SQL_ATTR_TRANSLATE_OPTION Verbindungsattribute festgelegt werden.  
  
 Die Übersetzungsoption ist ein Wert, der nur von einer bestimmten DLL-Übersetzung interpretiert werden kann. Z. B. die Übersetzung zwischen verschiedenen Codepages DLL übersetzt, möglicherweise die Option die Nummern der Codepages verwendet werden, die Anwendung und die Datenquelle erhalten. Es ist nicht notwendig Konvertierungs-DLL auf eine Übersetzungsoption verwenden.  
  
 Nach der eine Übersetzung, die DLL angegeben wurde, wird der Treiber geladen und aufgerufen, um alle Daten, die zwischen der Anwendung und die Datenquelle übersetzt. Dies schließt alle SQL-Anweisungen und Zeichenparameter an die Datenquelle gesendet werden, und alle Zeichen Ergebnisse, Metadaten Zeichen, z. B. Spaltennamen und Fehlermeldungen aus der Datenquelle abgerufen. Verbindungsdaten ist nicht übersetzt, da der Konvertierungs-DLL nicht bis geladen wird, nachdem die Anwendung mit der Datenquelle verbunden ist.

