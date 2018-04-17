---
title: SQLParamOptions (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb73b760a0d63dcf1aa57ea0448dece6cb58b3f2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 ODBC-API-Konformität: Ebene 1  
  
 Ermöglicht es einer Anwendung mehrere Werte für den Satz von Parametern, die vom zugewiesen an [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md). Die Möglichkeit, mehrere Werte für einen Satz von Parametern anzugeben, eignet sich für masseneinfügungen und andere arbeiten, die erfordert die Datenquelle die gleiche SQL-Anweisung mehrmals mit verschiedenen Parameterwerten zu verarbeiten. Eine Anwendung kann z. B. drei Sätze von Werten für den Satz von Parametern für angeben einer **einfügen** Anweisung und führen Sie dann die **einfügen** insert-Anweisung einmal die drei ausgeführt DDL-Vorgänge.  
  
 Weitere Informationen finden Sie unter [SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md) in der *ODBC Programmer's Reference*.
