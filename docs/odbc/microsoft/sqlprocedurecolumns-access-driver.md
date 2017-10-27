---
title: SQLProcedureColumns (Access-Treiber) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access driver [ODBC], SQLProcedureColumns
- SQLProcedureColumns function [ODBC], Access Driver
ms.assetid: 34fee995-5848-4ecb-bda0-fc362a77b2d9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9faec06a2337e7b3a2e93769486f40e006d9d7c8
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns (Access-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Access-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Anwendungsentwickler sollten Spalten treiberdefinierten, beginnend am Ende des Resultsets und absteigender gesucht.  
  
|Column|Kommentare|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT oder SQL_RESULT_COL|  
|ORDNUNGSZAHL|Dies ist eine treiberspezifische-Spalte, die am Ende des Resultsets zurückgegeben wird. Der SQL-Typ der Spalte ist eine ganze Zahl.|

