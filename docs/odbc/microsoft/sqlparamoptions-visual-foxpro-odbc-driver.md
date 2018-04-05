---
title: SQLParamOptions (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ade98eb2f7d0096c1ef6bf28a7c5ab694f1b4853
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 ODBC-API-Konformität: Ebene 1  
  
 Ermöglicht es einer Anwendung mehrere Werte für den Satz von Parametern, die vom zugewiesen an [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md). Die Möglichkeit, mehrere Werte für einen Satz von Parametern anzugeben, eignet sich für masseneinfügungen und andere arbeiten, die erfordert die Datenquelle die gleiche SQL-Anweisung mehrmals mit verschiedenen Parameterwerten zu verarbeiten. Eine Anwendung kann z. B. drei Sätze von Werten für den Satz von Parametern für angeben einer **einfügen** Anweisung und führen Sie dann die **einfügen** insert-Anweisung einmal die drei ausgeführt DDL-Vorgänge.  
  
 Weitere Informationen finden Sie unter [SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md) in der *ODBC Programmer's Reference*.
