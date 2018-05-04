---
title: SQL_C_TCHAR | Microsoft Docs
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
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f2367dcae307e3152005c1bb47885a274c6cc0a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlctchar"></a>SQL_C_TCHAR
Der Typbezeichner SQL_C_TCHAR identifiziert einen-Datentyp nicht tatsächlich; Es ist ein Makro, das in die Headerdatei für Unicode-Konvertierung vorhanden ist. Sie wird von SQL_C_CHAR oder SQL_C_WCHAR ersetzt, abhängig von der Einstellung des Unicode- **#define**. Es eignet sich für eine Anwendung, die Übertragung von Zeichendaten, die als eine ANSI- und Unicode-Anwendung kompiliert werden.
