---
title: SQLColAttributes (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
helpviewer_keywords: SQLColAttribute function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: d403dfa0-c26d-47d4-91d9-2f29aa387399
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8cef195281e4793af925174eb0e13ed6a5ff8667
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 : ODBC-API Core Konformitätsgrad  
  
 Gibt die Deskriptorinformationen für eine Spalte in einem Resultset zurück. Deskriptorinformationen wird als eine Zeichenfolge, einen 32-Bit-Deskriptor abhängiges-Wert oder einen ganzzahligen Wert zurückgegeben.  
  
> [!NOTE]  
>  **SQLColAttributes** kann nicht verwendet werden, um Informationen über die Lesezeichenspalte (Spalte 0) zurückgegeben.  
  
 Der Visual FoxPro-ODBC-Treiber unterstützt alle *fDescType* Werte. Die folgende Tabelle enthält Kommentare auf den Treiber-Implementierung der ausgewählten Werte.  
  
|*fDescType*|Anmerkung|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|Gibt "false": Visual FoxPro sind keine Leistungsindikator-Felder.|  
|SQL_COLUMN_CASE_SENSITIVE|Wenn der Spaltentyp Zeichen ist, wird immer TRUE zurückgegeben.|  
|SQL_COLUMN_LABEL|Gibt den Namen der Spalte, die auch von SQL_COLUMN_NAME zurückgegeben wird.|  
|SQL_COLUMN_MONEY|Gibt "true" zurück, wenn der Spaltentyp Währung (dargestellt durch "Y" in der Visual FoxPro-Sprache).|  
|SQL_COLUMN_OWNER_NAME|Gibt immer eine leere Zeichenfolge zurück.|  
|SQL_COLUMN_QUALIFIER_NAME|Gibt immer eine leere Zeichenfolge zurück.|  
|SQL_COLUMN_SEARCHABLE|Für Spalten vom Typ Allgemein SQL_UNSEARCHABLE zurückgegeben; Diese Spalten können nicht in einer WHERE-Klausel verwendet werden.<br /><br /> Gibt SQL_SEARCHABLE für Spalten vom Typ "Zeichen" oder "Memo mit NOCPTRANS festgelegt nicht. Diese Spalten können in einer WHERE-Klausel mit jedem Vergleichsoperator verwendet werden.<br /><br /> Für alle anderen Spaltentypen SQL_ALL_EXCEPT_LIKE zurückgegeben; Diese Spalten können in einer WHERE-Klausel mit allen Vergleichsoperatoren mit Ausnahme von LIKE verwendet werden.|  
|SQL_COLUMN_TABLE_NAME|Gibt immer eine leere Zeichenfolge zurück.|  
  
 Weitere Informationen finden Sie unter [SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) in der *ODBC Programmer's Reference*.
