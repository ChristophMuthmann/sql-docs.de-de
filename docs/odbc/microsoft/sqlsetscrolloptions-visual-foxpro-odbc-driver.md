---
title: SQLSetScrollOptions (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 63efd04bc43855c08a6de02d5396bea45eabbc68
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: Partial  
  
 ODBC-API-Konformität: Ebene 2  
  
 Legt Optionen für die Steuerung des Verhaltens von Cursor ein Anweisungshandle zugeordnet *Befehls beschäftigt*.  
  
 Der Visual FoxPro-ODBC-Treiber unterstützt nur SQL_CONCUR_READ_ONLY; Er unterstützt keine der *fConcurrency* SQL_CONCUR_ROWVER Wert. Der Treiber konvertiert SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC und SQL_CURSOR_KEYSET_DRIVEN SQL_SCROLL_STATIC mit Warnung ODBC_01S02.  
  
 Weitere Informationen finden Sie unter [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) in der *ODBC Programmer's Reference*.
