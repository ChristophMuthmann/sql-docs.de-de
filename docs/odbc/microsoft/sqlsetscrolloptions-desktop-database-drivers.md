---
title: SQLSetScrollOptions (Desktop-Datenbanktreiber) | Microsoft Docs
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
- SQLSetScrollOptions function [ODBC], Desktop Database Drivers
ms.assetid: 51d643ed-015b-4639-969a-9491d9875aca
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd83d7ce68d0a7bc1045aee76c28b9b5c39c9faf
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (Desktop-Datenbanktreiber)
Vorwärtscursor und statische Cursor werden für SQL_CONCUR_READ_ONLY unterstützt.  
  
 Nur keysetgesteuerte Cursor werden unterstützt, für eine *fConcurrency* Argument SQL_CONCUR_LOCK fest.  
  
 Ein *fConcurrency* Argument SQL_CONCUR_ROWVER wird nicht unterstützt.  
  
 Dynamische Cursor und gemischten Cursor werden nicht unterstützt.

