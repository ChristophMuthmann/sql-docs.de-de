---
title: SQLSetStmtOption (Desktop-Datenbanktreiber) | Microsoft Docs
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
- SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b797d3eddb7eae9232aee3c73ceae7c12ca163d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
