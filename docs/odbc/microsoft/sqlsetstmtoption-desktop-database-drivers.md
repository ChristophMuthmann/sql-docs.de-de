---
title: SQLSetStmtOption (Desktop-Datenbanktreiber) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8d1f51805413056a06c6cee769920e1ad878abe5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (Desktop-Datenbanktreiber)
|*fOption*|Kommentare|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|Die asynchrone Verarbeitung wird nicht unterstützt. Die SQL_ASYNC_ENABLE fOption SQLSTATE S1C00 zurück (Treiber nicht unterstützt).|  
|SQL_KEYSET_SIZE|Die einzigen gültigen Keysetgröße ist 0 (null), da gemischte und dynamische Cursor werden nicht unterstützt. Wenn dieser Wert auf jede andere Zahl festgelegt ist, wird es in 0 geändert und der Aufruf SQL_SUCCESS_WITH_INFO und SQLSTATE 01 s 02 zurück (Optionswert wurde geändert).|  
|SQL_MAX_ROWS|Die einzigen gültigen Rowsetgröße ist 0, da der Remotedesktop-Datenbanktreiber Beschränken der Anzahl von Zeilen, die zurückgegeben werden nicht unterstützt wird. Wenn dieser Wert auf jede andere Zahl festgelegt ist, wird es in 0 geändert und der Aufruf SQL_SUCCESS_WITH_INFO und SQLSTATE 01 s 02 zurück (Optionswert wurde geändert).|  
|SQL_QUERY_TIMEOUT|Wird nicht unterstützt.|  
|SQL_ROW_NUMBER|Wird nicht unterstützt.|  
|SQL_SIMULATE_CURSOR|Wird nicht unterstützt.|

