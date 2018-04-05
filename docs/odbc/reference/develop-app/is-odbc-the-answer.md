---
title: Ist ODBC-die Antwort? | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 390188eb430e51bf0ce27bf2f32f9f82c195d4da
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="is-odbc-the-answer"></a>Ist ODBC-die Antwort?
Vor dem befassen sich in der Frage, Interoperabilität, berücksichtigen Sie folgende Frage: die Anwendung die zu verwendende ODBC überhaupt? Dies mag eine ungewöhnliche Frage in eine Anleitung für ODBC, aber es ist tatsächlich eine rechtmäßige. ODBC wurde nicht entwickelt, um systemeigenen Datenbank-APIs vollständig zu ersetzen, und es bietet Datenbankzugriff in allen Fällen. Es wurde entworfen, um eine allgemeine Schnittstelle für Datenbanken bereitzustellen und wurde frei Anwendungsprogrammierer zu lernen, und Links zu mehreren Datenbanken verwalten soll.  
  
 Benutzerdefinierte Anwendungen sind gut für systemeigenen Datenbank-APIs. Der Hauptgrund ist, dass benutzerdefinierte Anwendungen häufig mit einem einzelnen DBMS und nicht interoperabel müssen. Datenbank im einheitlichen APIs empfiehlt sich besser als ODBC verfügbar machen, das die Funktionen des ein bestimmtes DBMS und möglicherweise nicht von ODBC verfügbar gemachten Funktionen verfügbar. Da die Entwickler benutzerdefinierter Anwendungen in der Regel mit der systemeigenen Datenbank-API für ihre DBMS vertraut sind, besteht außerdem ratsam, um zu erfahren, ODBC. Allerdings ist es interessant, beachten, dass für einige DBMS ODBC die systemeigenen Datenbank-API ist.  
  
 Welche Anwendungen sind Kandidaten für ODBC? Die besten Kandidaten sind Anwendungen, die mit mehr als ein DBMS zu arbeiten. Dies schließt nahezu alle generische und vertikale Anwendungen. Darüber hinaus eine Anzahl von benutzerdefinierten Anwendungen. Beispielsweise sind benutzerdefinierte Anwendungen, die mehrere unterschiedliche DBMS verwenden wesentlich einfacher und übersichtlicher mit ODBC als durch mehrere systemeigene APIs geschrieben. Und benutzerdefinierte Anwendungen, die mit ODBC geschrieben sind wesentlich einfacher, wie ein Unternehmen von einem DBMS in eine andere verschoben oder stellt die gleiche Anwendung für unterschiedliche DBMS bereit zu migrieren.
