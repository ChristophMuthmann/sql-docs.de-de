---
title: SQLTransact (Access-Treiber) | Microsoft Docs
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
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 96085748caf432aeba1d7876edf99ae3a2de4035
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqltransact-access-driver"></a>SQLTransact (Access-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Access-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Wenn der Microsoft Access-Treiber verwendet wird, die SQL_COMMIT und SQL_ROLLBACK werden für unterstützt die *fType* Argument in einem Aufruf von **SQLTransact**.  
  
 Wenn während der Commit-Prozess ein Fehler auftreten, die betroffene Datenbank kann repariert werden über die Option Reparieren der Datenbank, in der Microsoft Access-Treiber-Setup oder durch die Verwendung des Schlüsselworts REPAIR_DB in der **SQLConfigDataSource** Funktion.
