---
title: SQLSetStmtOption (Desktop-Datenbanktreiber) | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 765f61337b28e1791d9853bbc26b057375084749
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (Desktop-Datenbanktreiber)
|*fOption*|Kommentare|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|Die asynchrone Verarbeitung wird nicht unterstützt. Die SQL_ASYNC_ENABLE fOption SQLSTATE S1C00 zurück (Treiber nicht unterstützt).|  
|SQL_KEYSET_SIZE|Die einzigen gültigen Keysetgröße ist 0 (null), da gemischte und dynamische Cursor werden nicht unterstützt. Wenn dieser Wert auf jede andere Zahl festgelegt ist, wird es in 0 geändert und der Aufruf SQL_SUCCESS_WITH_INFO und SQLSTATE 01 s 02 zurück (Optionswert wurde geändert).|  
|SQL_MAX_ROWS|Die einzigen gültigen Rowsetgröße ist 0, da der Remotedesktop-Datenbanktreiber Beschränken der Anzahl von Zeilen, die zurückgegeben werden nicht unterstützt wird. Wenn dieser Wert auf jede andere Zahl festgelegt ist, wird es in 0 geändert und der Aufruf SQL_SUCCESS_WITH_INFO und SQLSTATE 01 s 02 zurück (Optionswert wurde geändert).|  
|SQL_QUERY_TIMEOUT|Nicht unterstützt.|  
|SQL_ROW_NUMBER|Nicht unterstützt.|  
|SQL_SIMULATE_CURSOR|Nicht unterstützt.|
