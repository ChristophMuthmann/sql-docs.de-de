---
title: SQLSetConnectOption (Access-Treiber) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b8f7497cb6b36602908443ab4fd9bdeb592ce8af
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (Access-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Access-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Anmerkung|  
|-------------|-------------|  
|SQL_ACCESS_MODE|Die SQL_ACCESS_MODE fOption kann SQL_MODE_READ_ONLY oder SQL_MODE_READ_WRITE festgelegt werden. Der Treiber verhindert allerdings keine Aktualisierungen SQL_ACCESS_MODE auf SQL_MODE_READ_ONLY festgelegt werden.|  
|SQL_AUTOCOMMIT|Wenn der Microsoft Access-Treiber verwendet wird, kann die Option SQL_AUTOCOMMIT SQL_AUTOCOMMIT_ON oder SQL_AUTOCOMMIT_OFF festlegen, festgelegt werden, da Microsoft Access-Treiber [1]-Transaktionen unterstützt.|  
|SQL_CURRENT_QUALIFIER|Unterstützt.|  
|SQL_LOGIN_TIMEOUT|Wird nicht unterstützt.|  
|SQL_OPT_TRACE|Unterstützt.|  
|SQL_OPT_TRACEFILE|Unterstützt.|  
|SQL_PACKET_SIZE|Wird nicht unterstützt.|  
|SQL_QUIET_MODE|Wird nicht unterstützt.|  
|SQL_TRANSLATE_DLL|Wird nicht unterstützt.|  
|SQL_TRANSLATION_OPTION|Wird nicht unterstützt.|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION ist immer SQL_TXN_READ_COMMITTED.|  
  
 [1] Atomarische Transaktionen werden von der Microsoft Access-Treiber nicht unterstützt. Wenn eine Transaktion, die mit dem Microsoft Access-Treiber ein Commit ausgeführt, vorhanden ist eine endliche Verzögerung zwischen dem Zeitpunkt, der die Transaktion ein Commit ausgeführt wird und die Zeit, die die Werte geschrieben werden auf den Datenträger. Diese Verzögerung wird durch eine Verzögerung in der Microsoft Jet-Datenbankmodul inhärenten bestimmt. Das Timeout für die Seite wird nicht kleiner als ein Mindestwert sein, auch wenn die Option ' pagetimeout ' unter diesen Wert festgelegt ist. Daher besteht keine Garantie, die Daten ein Commit ist stabil, da während der Verzögerung Änderungen vorgenommen werden können.

