---
title: SQLGetStmtOption (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
helpviewer_keywords: SQLGetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984a8b1d-f12c-420c-8be4-f555114c764b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9042a1a951d08c60e8dc795cd58f2a525cf39cda
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 ODBC-API-Konformität: Ebene 1  
  
 Gibt die aktuelle Einstellung der Option-Anweisung eine zurück.  
  
|*FOption*|Rückgabewert|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|ganze 32-Bit-Wert, der das Lesezeichen für die aktuelle Datensatznummer ist|  
|SQL_ROW_NUMBER|Legen Sie die 32-Bit-Ganzzahl, die die Position der aktuellen Zeile in das Ergebnis angeben|  
|SQL_TRANSLATE_DLL|Fehler: "Treiber nicht unterstützt"|  
  
 Der Visual FoxPro-ODBC-Treiber hat keine Übersetzung DLLs.  
  
 Weitere Informationen finden Sie unter [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) in der *ODBC Programmer's Reference*.
