---
title: SQLStatistics (Access-Treiber) | Microsoft Docs
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
- Access driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Access Driver
ms.assetid: 6117ac77-1020-4f0c-8eed-e671c34c1f21
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bc52e437436f202a0449818031133a27f530bf29
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics (Access-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Access-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Spalte|Kommentare|  
|------------|--------------|  
|TABLE_QUALIFIER|Der Pfad zu einer Datenbankdatei ist für Microsoft Access zurückgegeben.<br /><br /> Musterabgleich wird nicht unterstützt der *SzTableQualifier* Argument.|  
|TABLE_OWNER|In dieser Spalte wird NULL zurückgegeben, da der Name des Besitzers nicht unterstützt wird.|  
|table_name|Nicht durch Trennzeichen getrennten Tabellenname.<br /><br /> Musterabgleich wird nicht unterstützt der *SzTableName* Argument.|  
|INDEX_QUALIFIER|Immer wird NULL zurückgegeben.|  
|INDEX_NAME|Index abhängige.|  
|TYPE|Nur SQL_TABLE_STAT oder SQL_INDEX_OTHER wird für den Typ zurückgegeben.|  
|SEQ_IN_INDEX|Index abhängige.|  
|COLUMN_NAME|Index abhängige.|  
|COLLATION|Index abhängige.|  
|CARDINALITY|Nur zurückgegeben für Microsoft Access.|  
|PAGES|Immer wird NULL zurückgegeben.|  
  
 Filtern von basiert auf Eindeutigkeit (das *fUnique* Argument). Die *fAccuracy* Parameter wird ignoriert.
