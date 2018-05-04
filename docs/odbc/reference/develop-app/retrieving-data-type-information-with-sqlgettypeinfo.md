---
title: Abrufen von Daten von Typinformationen mit SQLGetTypeInfo | Microsoft Docs
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
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d764d8470343d67bd37c1ef7ce5dcf15962079e9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>Abrufen von Informationen mit SQLGetTypeInfo
Da die Zuordnungen von zugrunde liegenden SQL-Datentypen zu ODBC-Datentypbezeichner ungefähre befinden, bietet-ODBC-Funktion (**SQLGetTypeInfo**) beschrieben, über ein Treiber vollständig kann jeder SQL-Datentyp in der Datenquelle. Diese Funktion gibt ein Resultset, die jede Zeile aus, von denen die Eigenschaften eines einzelnen Datentyps, z. B. Name, Typ-ID, Genauigkeit, Dezimalstellen und NULL-Zulässigkeit beschreibt.  
  
 Diese Informationen werden im Allgemeinen von generischen Anwendungen verwendet, mit denen der Benutzer zum Erstellen und Ändern von Tabellen. Solche Anwendungen rufen **SQLGetTypeInfo** zu die Datentypinformationen abrufen und dann einige oder alle Daten für dem Benutzer. Solche Anwendungen müssen zwei Dinge geachtet werden:  
  
-   Mehr als eine SQL-Datentyp kann einen einzelnen Typbezeichner zuordnen, die erschweren können bestimmen, welcher Datentyp verwenden. Um dieses Problem zu beheben, ist das Resultset zuerst nach Typ-ID und zweitens nach Nähe zur Definition der Typbezeichner geordnet. Darüber hinaus Vorrang Daten Datenquelle definierten Datentypen benutzerdefinierte Datentypen. Nehmen wir beispielsweise an, dass eine Datenquelle definiert, die ganze Zahl und LEISTUNGSINDIKATOR-Datentypen, um identisch sein, außer dass Zähler automatisch erhöht wird. Angenommen Sie auch, dass der benutzerdefinierte Typ WHOLENUM ein Synonym für ganze Zahl ist. Jeder dieser Typen wird SQL_INTEGER zugeordnet. In der **SQLGetTypeInfo** Resultset, ganze Zahl wird gefolgt von WHOLENUM zuerst angezeigt und dann LEISTUNGSINDIKATOR. WHOLENUM, die nach ganze Zahl angezeigt werden, da es eine benutzerdefinierte ist, aber bevor Zähler, da es mehrere am ehesten entspricht die Definition der SQL_INTEGER geben Bezeichner.  
  
-   ODBC definiert keine Datentypnamen für die Verwendung in **CREATE TABLE** und **ALTER TABLE** Anweisungen. Die Anwendung sollte verwenden Sie stattdessen den Namen in der Spalte TYPE_NAME des zurückgegebenes Resultset zurückgegebenen **SQLGetTypeInfo**. Der Grund dafür ist, obwohl die meisten SQL variiert nicht viel über DBMS, Datentypnamen erheblich variieren. Anstatt das Erzwingen eines Treiber zum Analysieren von SQL-Anweisungen und DBMS-spezifische Datentypnamen standard Datentypnamen ersetzt, erfordert ODBC-Anwendungen, die DBMS-spezifische Namen ursprünglich.  
  
 Beachten Sie, dass **SQLGetTypeInfo** nicht notwendigerweise beschreibt alle Datentypen, die eine Anwendung auftreten kann. Insbesondere können Resultsets nicht direkt von der Datenquelle unterstützte Datentypen enthalten. Beispielsweise werden die Datentypen der Spalten in Resultsets von Katalogfunktionen von ODBC definiert und diese Datentypen möglicherweise nicht von der Datenquelle unterstützt. Um die Merkmale der Datentypen in einem Resultset zu ermitteln, eine Anwendung ruft **SQLColAttribute**.
