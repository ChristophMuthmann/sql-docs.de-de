---
title: SQLStatistics (Paradox-Treiber) | Microsoft Docs
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
- Paradox driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Paradox Driver
ms.assetid: 886cab83-d599-4fbc-9c88-e8cb833aac4b
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c2f158fd9d3fc1a7695e49bfa634f8cd064aac13
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlstatistics-paradox-driver"></a>SQLStatistics (Paradox-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Paradox treiberspezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Spalte|Kommentare|  
|------------|--------------|  
|TABLE_QUALIFIER|Der Pfad zu einem Verzeichnis.<br /><br /> Musterabgleich wird nicht unterstützt der *SzTableQualifier* Argument.|  
|TABLE_OWNER|In dieser Spalte wird NULL zurückgegeben, da der Name des Besitzers nicht unterstützt wird.|  
|table_name|Nicht durch Trennzeichen getrennten Tabellenname.<br /><br /> Musterabgleich wird nicht unterstützt der *SzTableName* Argument.|  
|INDEX_QUALIFIER|Immer wird NULL zurückgegeben.|  
|INDEX_NAME|Index abhängige.|  
|TYPE|Nur SQL_TABLE_STAT oder SQL_INDEX_OTHER wird für den Typ zurückgegeben.|  
|SEQ_IN_INDEX|Index abhängige.|  
|COLUMN_NAME|Index abhängige.|  
|COLLATION|Index abhängige.|  
|PAGES|Immer wird NULL zurückgegeben.|  
  
 Filtern von basiert auf Eindeutigkeit (das *fUnique* Argument). Die *fAccuracy* Parameter wird ignoriert.
