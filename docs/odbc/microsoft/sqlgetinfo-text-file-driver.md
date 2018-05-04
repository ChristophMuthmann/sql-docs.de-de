---
title: SQLGetInfo (Text-Datei-Treiber) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetInfo
ms.assetid: 6b7a630e-47f8-4ee1-b2a7-476bc1d0b0d4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61d3f9b63697de19f5f623a567194d2dcf95d66b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetinfo-text-file-driver"></a>SQLGetInfo (Text-Datei-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Textdatei treiberspezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLGetInfo** den Informationstyp SQL_FILE_USAGE unterstützt. Der zurückgegebene Wert ist eine 16-Bit-Ganzzahl, die angibt, wie der Treiber direkt Dateien in einer Datenquelle behandelt:  
  
-   SQL_FILE_NOT_SUPPORTED – Der Treiber ist keinen ein-Ebenen-Treiber.  
  
-   SQL_FILE_TABLE – Ein ein-Ebenen-Treiber behandelt Dateien in einer Datenquelle als Tabellen.  
  
-   SQL_FILE_QUALIFIER – Ein ein-Ebenen-Treiber behandelt Dateien in einer Datenquelle als Qualifizierer an.  
  
 Der ODBC-Treiber gibt SQL_FILE_TABLE für die Textdriver zurück, da jede Datei eine Tabelle handelt.  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|Version|Format der Versionsnummer erneut|  
|----------|-------------|-------------------------------|  
|Text|1,0|01.00.0000|  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &AMP;#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &AMP;#124; SQL_FN_TD_CURTIME &AMP;#124; SQL_FN_TD_DAYOFMONTH &AMP;#124; SQL_FN_TD_DAYOFWEEK &AMP;#124; SQL_FN_TD_DAYOFYEAR &AMP;#124; SQL_FN_TD_HOUR &AMP;#124; SQL_FN_TD_MINUTE &AMP;#124; SQL_FN_TD_MONTH &AMP;#124; SQL_FN_TD_NOW &AMP;#124; SQL_FN_TD_SECOND &AMP;#124; SQL_FN_TD_WEEK &AMP;#124; SQL_FN_TD_YEAR
