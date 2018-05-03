---
title: Desktop-Treiber-Datenbankkompatibilität | Microsoft Docs
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
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a8390be6d2aa4fa7999f19018a4a2750c7d44fd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="desktop-database-driver-compatibility"></a>Kompatibilität von Desktop-Datenbank
Unicode ist, dass eine Methode der Software zeichencodierung, die alle Zeichen behandelt, als mit einer festen Breite von zwei Bytes. Diese Methode dient als Alternative zur Windows-ANSI-zeichencodierung, d. h., da es Zeichen in ein Byte repräsentiert auf 256 Zeichen beschränkt. Da Unicode über 65.000 Zeichen darstellen kann, verfügt es viele Sprachen, deren Zeichen werden nicht dargestellt, in ANSI-Codierung.  
  
 Der ODBC 3.5 (oder höher)-Treiber-Manager ist die Unicode-aktiviert. Dies wirkt sich auf zwei Hauptbereichen: Funktionsaufrufe und string-Datentypen. Der Treiber-Manager Maps Zeichenfolge Funktionsargumente und die Zeichenfolgendaten nach Bedarf von der Anwendung und Treiber, können beide entweder Unicode oder ANSI-aktiviert sein.  
  
 Der ODBC 3.5 (oder höher)-Treiber-Manager unterstützt die Verwendung eines Unicode-Treibers mit einer Unicode-Anwendung und eine ANSI-Anwendung. Unterstützt auch die Verwendung eines ANSI-Treibers mit einer ANSI-Anwendung. Der Treiber-Manager bietet begrenzte Unicode in ANSI-Zuordnung für eine Unicode-Anwendung mit einem ANSI-Treiber verwenden. Dies ermöglicht den Zugriff auf die 3.5 Jet-Datenbanken und die Unterstützung für alle vorhandenen ISAM-Dateitypen.  
  
 Wenn eine ANSI-Anwendung verwendet die ODBC-Desktop Datenbank Driver 4.0 und greift auf Microsoft Access 4.0 oder höher und der Treiber stellt den Datentyp als SQL_CHAR, SQL_VARCHAR oder SQL_LONGVARCHAR, obwohl Jet 4.0 Breite Version unterstützt. Ältere Versionen von Jet, unterstützen keine SQL_WCHAR, SQL_WVARCHAR oder SQL_WLONGVARCHAR. Diese Einschränkung gilt auch in Fällen, in denen der alte Formate mit dem Jet 4.0-Datenbankmodul verwendet werden.  
  
 Weitere Informationen zu Unicode-Probleme mit dem ODBC finden Sie unter [Unicode](../../odbc/reference/develop-app/unicode.md) Überlegungen programmieren.
