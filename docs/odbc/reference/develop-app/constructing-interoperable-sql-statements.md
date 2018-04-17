---
title: Erstellen von interoperablen SQL­Anweisungen | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], constructing statements
ms.assetid: dee6f7e2-bcc4-4c74-8c7c-12aeda8a90eb
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b9419a3e242510a0c65ac87f2c1601c59fdafbd8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="constructing-interoperable-sql-statements"></a>Erstellen von interoperablen SQL­Anweisungen
Wie in den vorherigen Abschnitten erwähnt, sollten interoperable Anwendungen ausführen können, die ODBC-SQL-Grammatik verwenden. Hinter dieser Grammatik verwendet wird, muss jedoch eine Reihe von weiteren Problemen von interoperablen Anwendungen Datenwachstums. Beispielsweise vorgehen eine Anwendung, um eine Funktion, z. B. äußeren Joins zu verwenden, die nicht von allen Datenquellen unterstützt wird?  
  
 An diesem Punkt Stellen der Anwendungs-Writer einige Entscheidungen über die Funktionen der Programmiersprache erforderlich sind und welche optional sind. In den meisten Fällen Wenn Sie ein bestimmter Treiber eine Funktion, die von der Anwendung benötigte nicht unterstützt lehnt ab die Anwendung einfach mit diesen Treiber ausgeführt. Jedoch, wenn die Funktion optional ist, kann die Anwendung das Feature umgehen. Es kann z. B. die Teile der Schnittstelle deaktivieren, mit die den Benutzer die Funktion verwenden zu können.  
  
 Um zu bestimmen, welche Funktionen unterstützt werden, Anwendungen, die durch den Aufruf gestartet **SQLGetInfo** mit der Option SQL_SQL_CONFORMANCE. Der Konformitätsgrad SQL ermöglicht es der Anwendung eine umfassende Ansicht der SQL unterstützt wird. Diese Ansicht, ruft die Anwendung optimieren **SQLGetInfo** mit einer Anzahl anderer Optionen. Eine vollständige Liste dieser Optionen finden Sie unter der [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) funktionsbeschreibung. Schließlich **SQLGetTypeInfo** gibt Informationen zu den Datentypen, die von der Datenquelle unterstützt. Den folgenden Abschnitten wird einer Anzahl von möglichen Faktoren, denen Anwendungen in ziehen beim Erstellen von interoperabler SQL-Anweisungen Betracht sollten.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Katalog- und Schemaverwendung](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [Katalogposition](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [Bezeichner in Anführungszeichen](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [Groß-/Kleinschreibung von Bezeichnern](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [Escapesequenzen](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [Literalpräfixe und -suffixe](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [Parametermarkierungen in Prozeduraufrufen](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL-Anweisungen](../../../odbc/reference/develop-app/ddl-statements.md)
