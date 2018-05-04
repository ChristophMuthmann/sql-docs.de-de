---
title: Katalog und Schema-Nutzung | Microsoft Docs
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
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f0295ee92c6fed4690f33691037e58fe0ae951a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="catalog-and-schema-usage"></a>Katalog und Schema-Verwendung
Datenquellen unterstützt nicht notwendigerweise Katalog-und Schemanamen als Name der Objektbezeichner in allen SQL-Anweisungen. Datenquellen Katalog-und Schemanamen in einer oder mehreren der folgenden Klassen von SQL-Anweisungen unterstützen möglicherweise: (Data Manipulation Language, DML) Anweisungen, Prozeduraufrufe datendefinitionsanweisungen Tabelle, Index-datendefinitionsanweisungen und Recht Definition -Anweisungen. Um die Klassen des SQL-Anweisungen zu ermitteln, bei dem Katalog und Schema Namen verwendet werden können, eine Anwendung ruft **SQLGetInfo** mit den Optionen SQL_CATALOG_USAGE und SQL_SCHEMA_USAGE.
