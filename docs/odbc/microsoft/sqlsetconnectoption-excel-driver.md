---
title: SQLSetConnectOption (Excel-Treiber) | Microsoft Docs
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
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Excel Driver
- Excel driver [ODBC], SQLSetConnectOption
ms.assetid: 528d21d1-4516-4497-9da4-7b87d77e622a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f7ec051fa3ce5c5f916f37d0ac6c5a57abce9efe
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetconnectoption-excel-driver"></a>SQLSetConnectOption (Excel-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Excel-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Anmerkung|  
|-------------|-------------|  
|SQL_ACCESS_MODE|Die SQL_ACCESS_MODE fOption kann SQL_MODE_READ_ONLY oder SQL_MODE_READ_WRITE festgelegt werden. Der Treiber verhindert allerdings keine Aktualisierungen SQL_ACCESS_MODE auf SQL_MODE_READ_ONLY festgelegt werden.|  
|SQL_AUTOCOMMIT|Der Microsoft Excel-Treiber unterstützt nur SQL_AUTOCOMMIT auf (Standardstatus) festgelegt wird, da sie keine Transaktionen unterstützen.|  
|SQL_CURRENT_QUALIFIER|Unterstützt.|  
|SQL_LOGIN_TIMEOUT|Nicht unterstützt.|  
|SQL_OPT_TRACE|Unterstützt.|  
|SQL_OPT_TRACEFILE|Unterstützt.|  
|SQL_PACKET_SIZE|Nicht unterstützt.|  
|SQL_QUIET_MODE|Nicht unterstützt.|  
|SQL_TRANSLATE_DLL|Nicht unterstützt.|  
|SQL_TRANSLATION_OPTION|Nicht unterstützt.|  
|SQL_TXN_ISOLATION|Nicht unterstützt.|
