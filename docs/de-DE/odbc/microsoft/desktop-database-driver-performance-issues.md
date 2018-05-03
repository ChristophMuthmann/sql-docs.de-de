---
title: Desktop-Datenbank-Treiber-Leistungsprobleme | Microsoft Docs
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
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 760cec404f274d77d5382a3d164898c95545894e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="desktop-database-driver-performance-issues"></a>Treiber-Leistungsprobleme Desktop-Datenbank
Um Kompatibilität mit vorhandenen ANSI-Anwendungen zu gewährleisten, werden die Datentypen SQL_WCHAR, SQL_WVARCHAR oder SQL_WLONGVARCHAR als SQL_CHAR, SQL_VARCHAR oder SQL_LONGVARCHAR für Microsoft Access 4.0 oder höher Datenquellen verfügbar gemacht. Die Datenquellen keine WIDE CHAR-Datentypen zurückgeben, sondern die Daten noch müssen an gesendet werden Jet im Formular Wide Char. Es ist wichtig zu verstehen, dass die Konvertierung ausgeführt wird, wenn eine Spalte SQL_C_CHAR, Parameter oder ein Ergebnis in einen Datentyp SQL_CHAR in eine ANSI-Anwendung gebunden ist.  
  
 Diese Konvertierung kann insbesondere im Hinblick auf Speicher ineffizient sein, wenn ein SQL_C_CHAR-Typ an einen Parameter vom Typ LONGVARCHAR gebunden ist. Da das Jet 4.0-Modul Stream LONGTEXT Parameterdaten kann, muss ein Unicode-Konvertierung Puffer zugeordnet werden, der zweimal der Größe des Puffers SQL_C_CHAR ANSI ist. Die effizienteste Mechanismus ist für die Anwendung die Unicode-Konvertierung ausführen und binden Sie den Parameter als SQL_C_WCHAR-Typ. Wenn ein Parameter als Data-at-Execution-markiert ist, und die Daten in mehreren Aufrufen SQLPutData bereitgestellt werden, wird ein Datenpuffer Longtext-Anweisung vergrößert. Eine Möglichkeit, vergrößert dies die Kosten zu vermeiden "Put" Datenpuffer ist eine optionale Länge über SQL_DATA_AT_EXEC_LEN(x), angeben, in denen *x* wird die erwartete Länge von Bytes. Initialisieren dieses eine interne PutData Puffergröße auf *x* Bytes.  
  
> [!NOTE]  
>  Eine effiziente Möglichkeit zum Einfügen oder Aktualisieren von long-Daten kann mithilfe von durchgeführt werden **SQLBulkOperations()** oder **SQLSetPos()** und die langen Daten auf SQL_DATA_AT_EXEC festlegen. (EXEC_LEN ist in diesem Fall ignoriert). Daten können in Segmenten gestreamt werden, durch den Aufruf **SQLPutData** mehrere Male, die effektiv fügt der das an der Tabelle.  
  
 Wenn eine Anwendung mithilfe einer Jet 3.5-Datenbank über den Microsoft ODBC-Desktop-Datenbank-Treiber, Version 4.0 aktualisiert wird, können einer Verringerung der Leistung und eine höhere Größe des Workingsets auftreten. Grund hierfür ist, wenn eine Version 3. *x* Datenbank geöffnet wird, verwenden die neue Version 4.0-Treiber, lädt er Jet 4.0. Wenn Jet 4.0 wird die Datenbank geöffnet und angezeigt werden, ist die Datenbank eine 3. *x* Version, lädt es installierbare ISAM-Treiber, die auf das Laden des 3.5 Jet-Moduls entspricht. So entfernen Sie die Leistung und Größe-Nachteil der Jet-3. *x* Datenbank in eine Datenbank der Jet 4.0-Format komprimiert werden soll. Dies vermeiden, Laden zwei Jet-Module und Minimieren der Codepfad, auf die Daten.  
  
 Darüber hinaus ist das Jet 4.0-Modul ein Unicode-Modul. Alle Zeichenfolgen gespeichert und bearbeitet, die im Unicode-Format. Wenn eine ANSI-Anwendung eine Jet-3 zugreift. *x* Datenbank durch das Jet 4.0-Modul die Daten wird von ANSI in Unicode und zurück zu ANSI konvertiert. Wenn die Datenbank in das Versionsformat 4.0 aktualisiert wird, werden die Zeichenfolgen in Unicode, entfernen eine Ebene der zeichenfolgenkonvertierung sowie zum Minimieren der Codepfad, auf die Daten durch das Ergebnis nur ein Jet-Datenbankmodul konvertiert.
