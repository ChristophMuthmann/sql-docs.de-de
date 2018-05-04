---
title: Übersicht über die ODBC | Microsoft Docs
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
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39ab7586ebc1cd63d028caab0d3c2f09b82c7172
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-overview"></a>ODBC-Übersicht
Open Database Connectivity (ODBC) ist eine weit verbreitete Anwendungsprogrammierschnittstelle (API) für den Datenbankzugriff. Es basiert auf den (Call-Level Interface, CLI)-Spezifikationen von Open Group und ISO/IEC für Datenbank-APIs und Structured Query Language (SQL) als seine Datenbank-Access-Sprache verwendet.  
  
 ODBC dient für die maximale *Interoperabilität* – d. h. die Möglichkeit einer Anwendung auf andere Datenbank-Managementsystemen (DBMS) mit dem gleichen Quellcode zuzugreifen. Datenbankanwendungen rufen die Funktionen in der ODBC-Schnittstelle, die in smartcardspezifische Module, die datenbankspezifische implementiert werden *Treiber*. Die Verwendung von Treibern isoliert datenbankspezifischen Aufrufe von Anwendungen auf die gleiche Weise, Druckertreiber Textverarbeitungsprogramme druckerspezifische Befehle isolieren. Da der Treiber zur Laufzeit geladen werden, muss ein Benutzer nur einen neuen Treiber für den Zugriff auf eine neue DBMS hinzuzufügen; Es ist nicht erforderlich, neu kompilieren oder erneut binden, die Anwendung.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Warum wurde ODBC erstellt?](../../odbc/reference/why-was-odbc-created.md)  
  
-   [Was ist ODBC?](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC und die Standard-CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
