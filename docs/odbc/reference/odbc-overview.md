---
title: "Übersicht über die ODBC | Microsoft Docs"
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
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 607e516c8654631ab032dfc6159a8990d464a023
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-overview"></a>ODBC-Übersicht
Open Database Connectivity (ODBC) ist eine weit verbreitete Anwendungsprogrammierschnittstelle (API) für den Datenbankzugriff. Es basiert auf den (Call-Level Interface, CLI)-Spezifikationen von Open Group und ISO/IEC für Datenbank-APIs und Structured Query Language (SQL) als seine Datenbank-Access-Sprache verwendet.  
  
 ODBC dient für die maximale *Interoperabilität* – d. h. die Möglichkeit einer Anwendung auf andere Datenbank-Managementsystemen (DBMS) mit dem gleichen Quellcode zuzugreifen. Datenbankanwendungen rufen die Funktionen in der ODBC-Schnittstelle, die in smartcardspezifische Module, die datenbankspezifische implementiert werden *Treiber*. Die Verwendung von Treibern isoliert datenbankspezifischen Aufrufe von Anwendungen auf die gleiche Weise, Druckertreiber Textverarbeitungsprogramme druckerspezifische Befehle isolieren. Da der Treiber zur Laufzeit geladen werden, muss ein Benutzer nur einen neuen Treiber für den Zugriff auf eine neue DBMS hinzuzufügen; Es ist nicht erforderlich, neu kompilieren oder erneut binden, die Anwendung.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Warum wurde ODBC erstellt?](../../odbc/reference/why-was-odbc-created.md)  
  
-   [Was ist ODBC?](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC und die Standard-CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
