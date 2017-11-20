---
title: Katalog und Schema-Nutzung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 217f68d674dc7099b741e77d287ca81fcc2688e5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="catalog-and-schema-usage"></a>Katalog und Schema-Verwendung
Datenquellen unterstützt nicht notwendigerweise Katalog-und Schemanamen als Name der Objektbezeichner in allen SQL-Anweisungen. Datenquellen Katalog-und Schemanamen in einer oder mehreren der folgenden Klassen von SQL-Anweisungen unterstützen möglicherweise: (Data Manipulation Language, DML) Anweisungen, Prozeduraufrufe datendefinitionsanweisungen Tabelle, Index-datendefinitionsanweisungen und Recht Definition -Anweisungen. Um die Klassen des SQL-Anweisungen zu ermitteln, bei dem Katalog und Schema Namen verwendet werden können, eine Anwendung ruft **SQLGetInfo** mit den Optionen SQL_CATALOG_USAGE und SQL_SCHEMA_USAGE.

