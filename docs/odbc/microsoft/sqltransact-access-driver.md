---
title: SQLTransact (Access-Treiber) | Microsoft Docs
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
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 041bd1a56db21dda374a8bd279c890e187f04beb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqltransact-access-driver"></a>SQLTransact (Access-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Access-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Wenn der Microsoft Access-Treiber verwendet wird, die SQL_COMMIT und SQL_ROLLBACK werden für unterstützt die *fType* Argument in einem Aufruf von **SQLTransact**.  
  
 Wenn während der Commit-Prozess ein Fehler auftreten, die betroffene Datenbank kann repariert werden über die Option Reparieren der Datenbank, in der Microsoft Access-Treiber-Setup oder durch die Verwendung des Schlüsselworts REPAIR_DB in der **SQLConfigDataSource** Funktion.
