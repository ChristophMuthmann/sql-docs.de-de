---
title: Structured Query Language (SQL) | Microsoft Docs
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
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e2145a720c1fd9cfedeafe123ac24e7e5ac77173
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="structured-query-language-sql"></a>Structured Query Language (SQL) (Structured Query Language, SQL)
Eine typische DBMS kann Benutzer speichern, zugreifen und Ändern von Daten in eine strukturierte und effiziente Weise. Die Benutzer des DBMS wurden ursprünglich Programmierer. Zugriff auf die gespeicherten Daten erforderlich, ein Programm in einer Programmiersprache wie z. B. COBOL schreiben. Diese Programme häufig geschrieben wurden, um eine entwicklerfreundliche Oberfläche für einem nicht-technische Benutzer anzuzeigen, jedoch Zugriff auf die Daten selbst die Dienste der erfahrene Programmierer. Einer zufälligen Zugriff auf die Daten war nicht praktikabel.  
  
 Benutzer konnten nicht vollständig mit dieser Situation zufrieden. Während sie auf Daten zugreifen können, erforderlich es häufig überzeugende DBMS Programmierer Spezialsoftware schreiben. Z. B. wenn eine Verkaufsabteilung den Gesamtumsatz nach jedem der Vertriebsmitarbeiter, die im vorhergehenden Monat zu sehen wollte und möchten diese Informationen, die mit dem höchsten in der Reihenfolge des Vertriebsmitarbeiters Länge des Diensts im Unternehmen, hatten sie zwei Optionen: entweder ein Programm bereits vorhanden war, die die Informationen auf genau diese Weise zugegriffen werden darf, oder die Abteilung musste ein solches Programm schreiben Programmierer Fragen. In vielen Fällen war dies mehr Arbeit, als es sich hat und war es immer eine teure Lösung für einmalige oder ad hoc Abfragen. Da mehr Benutzer einfach zugreifen wollten, vergrößert wurde dieses Problem, mehr und mehr.  
  
 Zulassen, dass Benutzer Zugriff auf Daten auf einer ad-hoc-Basis erforderlich, weisen Sie ihnen eine Sprache, die ihren Anforderungen auszudrücken. Eine einzelne Anforderung in einer Datenbank wird als eine Abfrage definiert. einer solchen Sprache ist eine Abfragesprache aufgerufen. Viele Abfragesprachen für diesen Zweck entwickelt wurden, aber eine der folgenden ist die beliebteste: Structured Query Language, in der 1970s bei IBM erfunden. Er wird häufig durch seine Akronym, SQL "oder" bezeichnet und ist ausgesprochen als "Ess Cue Ell" und als "Sequel"; In diesem Handbuch wird die frühere Aussprache verfügen. SQL wurde eine ANSI-standard 1986 und ein ISO-standard 1987; Es wird derzeit in eine hervorragende viele Datenbankmanagementsysteme verwendet.  
  
 Obwohl SQL die ad-hoc-Anforderungen von Benutzern gelöst, die Notwendigkeit für den Datenzugriff von Computerprogrammen nicht behoben. In der Tat die meisten Datenbankzugriff weiterhin (und) programmgesteuerte in Form von regelmäßigen Berichten und statistische Analysen Dateneingabe Programme, z. B. die Bearbeitung-Programme, z. B. zum Abstimmen für Auftragseingabe und Daten verwendet und Arbeitsaufträge zu generieren.  
  
 Diese Programme verwenden auch SQL-Anweisung mit einer der folgenden drei Methoden:  
  
-   **Embedded SQL**, in dem SQL-Anweisungen in eine Hostsprache, wie z. B. C# oder COBOL eingebettet sind.  
  
-   **SQL-Module**in die SQL-Anweisungen für das DBMS kompiliert und von einer Hostsprache aufgerufen werden.  
  
-   **Call-Level-Interface**, oder die CLI, besteht aus SQL-Anweisungen an das DBMS übergeben und zum Abrufen von Ergebnissen aus dem DBMS aufgerufenen Funktionen.  
  
> [!NOTE]  
>  Es ist eine historische versehen, die den Begriff Call-Level-Interface wird verwendet, anstatt die anwendungsprogrammierung (API), Schnittstelle eine andere Bezeichnung für dasselbe. In der Datenbankwelt-API wird verwendet, um SQL selbst beschreiben: SQL ist die API für ein DBMS.  
  
 Diese Optionen ist embedded SQL die am häufigsten verwendeten, obwohl die meisten Major DBMS proprietären CLIs unterstützen.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Verarbeiten eine SQL-Anweisung](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [Embedded SQL](../../odbc/reference/embedded-sql.md)  
  
-   [SQL-Module](../../odbc/reference/sql-modules.md)  
  
-   [Call-Level-Interface](../../odbc/reference/call-level-interfaces.md)
