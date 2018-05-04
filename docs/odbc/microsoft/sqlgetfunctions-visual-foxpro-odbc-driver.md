---
title: SQLGetFunctions (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
- SQLGetFunctions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8102932a-88b3-49d8-bf7a-c766f54878c0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc3350e8b6a7a4ddcf505fed14a056422cbbbe41
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetfunctions-visual-foxpro-odbc-driver"></a>SQLGetFunctions (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 ODBC-API-Konformität: Ebene 1  
  
 Gibt "true" für alle unterstützten Funktionen.  
  
 Der Visual FoxPro-ODBC-Treiber unterstützt alle ODBC-API Core und Level 1-Funktionen. Die folgende Tabelle gibt an, ob der Treiber eine bestimmte Ebene-2-Funktion unterstützt.  
  
|*Funktion*|Supported|  
|----------------|---------------|  
|SQL_API_SQLBROWSECONNECT|nein|  
|SQL_API_SQLCOLUMNPRIVELEGES|nein|  
|SQL_API_SQLDATASOURCES|ja|  
|SQL_API_SQLDESCRIBEPARAM|nein|  
|SQL_API_SQLDRIVERS|ja|  
|SQL_API_SQLEXTENDEDFETCH|ja|  
|SQL_API_SQLFOREIGNKEYS|nein|  
|SQL_API_SQLMORERESULTS|ja|  
|SQL_API_SQLNATIVESQL|nein|  
|SQL_API_SQLNUMPARAMS|ja|  
|SQL_API_SQLPARAMOPTIONS|ja|  
|SQL_API_SQLPRIMARYKEYS|ja|  
|SQL_API_SQLPROCEDURECOLUMNS|nein|  
|SQL_API_SQLPROCEDURES|nein|  
|SQL_API_SQLSETPOS|ja|  
|SQL_API_SQLSETSCROLLOPTIONS|ja|  
|SQL_API_SQLTABLEPRIVILEGES|nein|  
  
 Weitere Informationen finden Sie unter [SQLGetFunctions](../../odbc/reference/syntax/sqlgetfunctions-function.md) in der *ODBC Programmer's Reference*.
