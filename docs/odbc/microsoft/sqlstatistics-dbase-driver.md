---
title: SQLStatistics (dBASE-Treiber) | Microsoft Docs
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
- SQLStatistics function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLStatistics
ms.assetid: 631cec1b-66b7-4103-b9a7-ffd81da3c442
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cdf146a28104cf74b0f28881b54dec228c7ae65a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlstatistics-dbase-driver"></a>SQLStatistics (dBASE-Treiber)
> [!NOTE]  
>  Dieses Thema enthält dBASE treiberspezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
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
