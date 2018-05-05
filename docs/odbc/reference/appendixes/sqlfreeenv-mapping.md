---
title: SQLFreeEnv Zuordnung | Microsoft Docs
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
- SQLFreeEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeEnv
ms.assetid: c0f76455-d072-4bae-bee7-452277dfa479
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe0941bc094efbb4c0d0f0ef348b7d17df760997
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlfreeenv-mapping"></a>SQLFreeEnv-Zuordnung
Wenn eine Anwendung ruft **SQLFreeEnv** über einen ODBC 3.*.x* Treiber, den Aufruf von  
  
```  
SQLFreeEnv(henv)   
```  
  
 wird zugeordnet  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 mit der *behandeln* Argument festgelegt wird, auf den Wert in *Henv*.
