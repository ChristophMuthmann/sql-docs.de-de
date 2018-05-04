---
title: SQLStatistics (Excel-Treiber) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Excel Driver
ms.assetid: 02506664-8dcc-4bd0-a8bb-d49fcbdd5722
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1f3a8a7671021e420384d9f2b3baf65beb077bc7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlstatistics-excel-driver"></a>SQLStatistics (Excel-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Excel-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Column|Kommentare|  
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
