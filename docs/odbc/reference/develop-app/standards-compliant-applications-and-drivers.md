---
title: Mit Standards kompatible Anwendungen und-Treiber | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c62e19d2d7c2c856b358649955a5b1540a802a12
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="standards-compliant-applications-and-drivers"></a>Mit Standards kompatible Anwendungen und-Treiber
Eine mit Standards kompatible Anwendung oder Treiber ist, die Open Group CAE-Spezifikation "Data Management: SQL Call-Level Interface (CLI)" und der ISO/IEC 9075 entspricht-3:1995 (E) Call-Level-Interface (SQL/CLI).  
  
 ODBC 3.*.x* gewährleistet die folgenden Funktionen:  
  
-   Die Open Group und ISO-CLI-Spezifikationen geschriebene Anwendung funktioniert mit einer ODBC 3.*.x* oder eine Standards kompatible Treiber bei der Kompilierung mit der ODBC 3.*.x* Header-Dateien und verknüpft Sie mit ODBC 3.*.x* Bibliotheken, und wenn er erhält Zugriff auf die vom Treiber über die ODBC 3.*.x* -Treiber-Manager.  
  
-   Ein Treiber, die den Spezifikationen Open Group und ISO-CLI geschrieben funktioniert mit einer ODBC 3.*.x* oder eine standardisierte Anwendung bei der Kompilierung mit der ODBC 3.*.x* Header-Dateien und verknüpft mit ODBC 3.*.x* Bibliotheken, und wenn die Anwendung erhält Zugriff auf die vom Treiber über die ODBC 3.*.x* -Treiber-Manager.  
  
 Mit Standards kompatible Anwendungen und-Treiber werden mit dem Flag "ODBC_STD Kompilierung" kompiliert.  
  
 Mit Standards kompatible Anwendungen weisen folgendes Verhalten auf:  
  
-   Wenn eine mit Standards kompatible Anwendung aufruft **SQLAllocEnv** (das kann auftreten, da **SQLAllocEnv** ist eine gültige Funktion in der Open Group und ISO-CLI), der Aufruf zugeordnet ist  **SQLAllocHandleStd** zum Zeitpunkt der Kompilierung. Zur Laufzeit ruft die Anwendung daher **SQLAllocHandleStd**. Im Verlauf der Verarbeitung dieser Aufruf wird der Treiber-Manager das SQL_ATTR_ODBC_VERSION-Umgebung-Attribut auf SQL_OV_ODBC3 fest. Ein Aufruf von **SQLAllocHandleStd** ist gleichbedeutend mit einem Aufruf von **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_ENV und einem Aufruf von **SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION auf SQL_OV_ODBC3 festgelegt.  
  
-   Wenn eine Anwendung mit Standards kompatible aufruft **SQLBindParam** (das kann auftreten, da **SQLBindParam** ist eine gültige Funktion in der Open Group und ISO-CLI), die ODBC 3.*.x* Treiber-Manager ordnet den Aufruf an den entsprechenden Aufruf in **SQLBindParameter**. (Siehe [SQLBindParam Zuordnung](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität.)  
  
-   Die ISO-CLI, die ODBC 3. veröffentlichungshäufigkeit*.x* Headerdateien enthalten Aliase für Typen von Informationen in Aufrufen verwendet **SQLGetInfo**. Eine mit Standards kompatible Anwendung kann diese Aliase verwenden, statt die ODBC 3.*.x* Informationstypen. Weitere Informationen finden Sie im nächste Thema [Headerdateien](../../../odbc/reference/develop-app/header-files.md).  
  
-   Eine mit Standards kompatible Anwendung muss überprüfen, ob alle Funktionen, die es unterstützt der Treiber unterstützt werden mit geeignet sind. Festlegen der Anweisungsattribut SQL_ATTR_CURSOR_SCROLLABLE auf SQL_SCROLLABLE und das Festlegen der Anweisungsattribut SQL_ATTR_CURSOR_SENSITIVITY auf SQL_INSENSITIVE oder SQL_SENSITIVE sind Funktionen, die als optionale Funktionen in den Standards verfügbar sind jedoch nicht enthalten sind, in die ODBC 3.*.x* Core level und daher möglicherweise nicht unterstützt durch alle ODBC 3.*.x* Treiber. Eine mit Standards kompatible Anwendung diese Funktionen verwendet, sollten sie sicher, dass der Treiber, dem er arbeitet unterstützt.
