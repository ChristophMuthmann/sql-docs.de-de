---
title: SQLTransact (Access-Treiber) | Microsoft Docs
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
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 657d0324132b279300e2a61151c790f066e4a3f5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqltransact-access-driver"></a>SQLTransact (Access-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Access-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Wenn der Microsoft Access-Treiber verwendet wird, die SQL_COMMIT und SQL_ROLLBACK werden für unterstützt die *fType* Argument in einem Aufruf von **SQLTransact**.  
  
 Wenn während der Commit-Prozess ein Fehler auftreten, die betroffene Datenbank kann repariert werden über die Option Reparieren der Datenbank, in der Microsoft Access-Treiber-Setup oder durch die Verwendung des Schlüsselworts REPAIR_DB in der **SQLConfigDataSource** Funktion.
