---
title: Normale Argumente | Microsoft Docs
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
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a97c5c7125b24239d0eaae1a75efdd65c37d7b04
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ordinary-arguments"></a>Normale Argumente
Wenn ein Argument für Katalog-Funktion ein normales Argument ist, wird er als Literalzeichenfolge behandelt. Gewöhnliche Argument akzeptiert eine Zeichenfolge Suchmuster weder eine Liste mit Werten. Spielt die Groß-/Kleinschreibung des normalen Argument und Anführungszeichen in der Zeichenfolge wörtlich genommen werden. Diese Argumente werden als normale Argumente behandelt, wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_FALSE festgelegt ist; Sie werden stattdessen als Bezeichner Argumente behandelt, wenn dieses Attribut auf SQL_TRUE festgelegt ist.  
  
 Wenn eine gewöhnliche-Argument ein null-Zeiger festgelegt wird, und das Argument ein erforderliches Argument ist, gibt die Funktion SQL_ERROR und SQLSTATE HY009 (Ungültige Verwendung eines null-Zeiger). Wenn eine gewöhnliche-Argument ein null-Zeiger festgelegt wird, und das Argument kein erforderliches Argument ist, ist das Argument Verhalten Treiber abhängig. Die erforderlichen Argumente sind in der folgenden Tabelle aufgeführt.  
  
|Funktion|Erforderliche Argumente|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
