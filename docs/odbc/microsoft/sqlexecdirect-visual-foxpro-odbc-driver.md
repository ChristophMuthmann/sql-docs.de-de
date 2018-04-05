---
title: SQLExecDirect (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed4f8501146221737a5af6c33d2196cb92704157
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 : ODBC-API Core Konformitätsgrad  
  
 Führt ein neues [preparable SQL-Anweisung](../../odbc/microsoft/visual-foxpro-terminology.md). Der Visual FoxPro-ODBC-Treiber verwendet die aktuellen Werte der Variablen Marker Parameter an, wenn alle Parameter in der Anweisung vorhanden sind.  
  
 Um einen Batchbefehl zum Übermitteln von mehr als eine SQL-Anweisung zu einem Zeitpunkt zu erstellen, verwenden Sie ein Semikolon (;) trennen Sie jede SQL-Anweisung im Batch.  
  
 Wenn die Tabelle, Sicht oder Feldnamen Leerzeichen enthalten, schließen Sie die Namen wieder in Anführungszeichen eingeschlossen. Beispielsweise, wenn die Datenbank eine Tabelle mit dem Namen Meine Tabelle und das Feld mein Feld enthält, schließen Sie jedes Element des Bezeichners wie folgt:  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 Weitere Informationen finden Sie unter [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) in der *ODBC Programmer's Reference*.
