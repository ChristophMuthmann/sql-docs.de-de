---
title: Schemaansichten | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- schema views [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], schema views
ms.assetid: f1dfb3e8-a7bd-46c3-92b6-c19531e8409d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 82d3624154e272e2f046110473ebe5d8360e6f6d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="schema-views"></a>Schema-Ansichten
Eine Anwendung kann Metadateninformationen aus dem DBMS durch Aufrufen von ODBC-Katalogfunktionen oder INFORMATION_SCHEMA-Sichten abzurufen. Die Ansichten werden gemäß dem ANSI SQL-92-Standard definiert.  
  
 Falls vom DBMS und der Treiber unterstützt, können der INFORMATION_SCHEMA-Sichten leistungsfähigere und umfassende Abrufen von Metadaten als die ODBC-Katalogfunktionen bieten. Eine Anwendung kann einen eigenen benutzerdefinierten ausführen **wählen** -Anweisung für eine dieser Ansichten können Ansichten zu verbinden oder eine Union für Sichten durchführen. Beim Angebots größer Hilfsprogramm und eine größere Anzahl an Metadaten werden INFORMATION_SCHEMA-Sichten nicht häufig vom DBMS unterstützt. Dies kann ändern, wie die Kompatibilität mit SQL-92 Weitere DBMS und-Treiber erreichen.  
  
 Um zu bestimmen, welche Ansichten unterstützt werden, eine Anwendung ruft **SQLGetInfo** mit der Option SQL_INFO_SCHEMA_VIEWS. Zum Abrufen von Metadaten aus einer unterstützten Sicht führt die Anwendung eine **wählen** Anweisung, der angibt, die Schemainformationen, die erforderlich sind.
