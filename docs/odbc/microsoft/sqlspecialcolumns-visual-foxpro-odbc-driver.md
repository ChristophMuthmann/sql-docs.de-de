---
title: SQLSpecialColumns (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0356209e6da452f1e901b245d8f4667ad99d564
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 ODBC-API-Konformität: Ebene 1  
  
 Ruft ab, die optimale Gruppe von Spalten, die eine Zeile in der Tabelle eindeutig identifiziert.  
  
 Der Visual FoxPro-ODBC-Treiber gibt die Spalten, die den Primärschlüssel für die Tabelle FoxPro bilden. (Siehe [SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md).) Wenn der Aufruf mit *fColType* SQL_ROWVER festgelegt ist, werden keine Spalten zurückgegeben. **SQLSpecialColumns** funktioniert nur bei Datenquellen, [Datenbanken](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Weitere Informationen finden Sie unter [SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md) in der *ODBC Programmer's Reference*.
