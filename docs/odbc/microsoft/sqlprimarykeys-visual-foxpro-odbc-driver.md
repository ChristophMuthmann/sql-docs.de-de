---
title: SQLPrimaryKeys (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
helpviewer_keywords: SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e0d7c874fe97f70f5e8d8096a4b03a2f064f2cb1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 ODBC-API-Konformität: Ebene 2  
  
 Gibt die Spaltennamen, die den Primärschlüssel für eine Tabelle bilden. Der Visual FoxPro-ODBC-Treiber-Implementierung von **SQLPrimaryKeys** verhält sich wie folgt:  
  
-   Ignoriert die *SzTableOwner* und *CbTableOwner* Argumente.  
  
-   Funktioniert nur für Datenquellen, [Datenbanken](../../odbc/microsoft/visual-foxpro-terminology.md). Der Treiber gibt dem Fehler "Treiber unterstützt diese Funktion nicht" ist die Datenquelle in einem Verzeichnis [frei Tabellen](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Weitere Informationen finden Sie unter [SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) in der *ODBC Programmer's Reference*.
