---
title: SQLProcedureColumns (Access-Treiber) | Microsoft Docs
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
- Access driver [ODBC], SQLProcedureColumns
- SQLProcedureColumns function [ODBC], Access Driver
ms.assetid: 34fee995-5848-4ecb-bda0-fc362a77b2d9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f293c0af98eb262abd838c957e0228dc8b69a813
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns (Access-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Access-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Anwendungsentwickler sollten Spalten treiberdefinierten, beginnend am Ende des Resultsets und absteigender gesucht.  
  
|Column|Kommentare|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT oder SQL_RESULT_COL|  
|ORDNUNGSZAHL|Dies ist eine treiberspezifische-Spalte, die am Ende des Resultsets zurückgegeben wird. Der SQL-Typ der Spalte ist eine ganze Zahl.|
