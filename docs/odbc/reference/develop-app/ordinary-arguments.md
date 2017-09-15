---
title: Normale Argumente | Microsoft Docs
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
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9aaaa374817d84eaa01dc96fa3783623e7b4b905
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="ordinary-arguments"></a>Normale Argumente
Wenn ein Argument für Katalog-Funktion ein normales Argument ist, wird er als Literalzeichenfolge behandelt. Gewöhnliche Argument akzeptiert eine Zeichenfolge Suchmuster weder eine Liste mit Werten. Spielt die Groß-/Kleinschreibung des normalen Argument und Anführungszeichen in der Zeichenfolge wörtlich genommen werden. Diese Argumente werden als normale Argumente behandelt, wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_FALSE festgelegt ist; Sie werden stattdessen als Bezeichner Argumente behandelt, wenn dieses Attribut auf SQL_TRUE festgelegt ist.  
  
 Wenn eine gewöhnliche-Argument ein null-Zeiger festgelegt wird, und das Argument ein erforderliches Argument ist, gibt die Funktion SQL_ERROR und SQLSTATE HY009 (Ungültige Verwendung eines null-Zeiger). Wenn eine gewöhnliche-Argument ein null-Zeiger festgelegt wird, und das Argument kein erforderliches Argument ist, ist das Argument Verhalten Treiber abhängig. Die erforderlichen Argumente sind in der folgenden Tabelle aufgeführt.  
  
|Funktion|Erforderliche Argumente|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*Tabellenname*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*Tabellenname*|  
|**SQLSpecialColumns**|*Tabellenname*|  
|**SQLStatistics**|*Tabellenname*|
