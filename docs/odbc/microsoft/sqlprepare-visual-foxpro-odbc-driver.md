---
title: SQLPrepare (Visual FoxPro-ODBC-Treiber) | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42eabe40eb5324cf82c543525ce286dadc2a510a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: vollständige  
  
 : ODBC-API Core Konformitätsgrad  
  
 Bereitet eine SQL-Anweisung durch das Planen der Verwendung zu optimieren, und führen Sie die Anweisung vor. Die SQL-Anweisung kompiliert wird, für die Ausführung von [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 Wenn die Tabelle, Sicht oder Feldnamen Leerzeichen enthalten, schließen Sie die Namen wieder in Anführungszeichen (') eingeschlossen. Beispielsweise, wenn die Datenbank eine Tabelle mit dem Namen Meine Tabelle und das Feld mein Feld enthält, schließen Sie jedes Element des Bezeichners wie folgt:  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 Weitere Informationen finden Sie unter [SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md) in der *ODBC Programmer's Reference*.
