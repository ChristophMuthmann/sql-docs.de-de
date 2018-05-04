---
title: Der Cursormerkmale und Cursortyp | Microsoft Docs
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
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: 6f67edd2-ae71-4ca0-9b2d-abf4c20dc17b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b73c8d966f0974b09b672e497238f122bf1b13da
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="cursor-characteristics-and-cursor-type"></a>Der Cursormerkmale und Cursortyp
Eine Anwendung kann die Merkmale eines Cursors anstelle des Cursor-Datentyps (Vorwärtscursor, statische, keysetgesteuerte oder dynamischen) angeben. Zu diesem Zweck wählt die Anwendung den Cursor scrolloptionen (durch Festlegen der SQL_ATTR_CURSOR_SCROLLABLE-Anweisungsattribut) und die Sensitivität (durch Festlegen der SQL_ATTR_CURSOR_SENSITIVITY-Anweisungsattribut) vor dem Öffnen des Cursors für die Anweisung behandeln. Klicken Sie dann wählt der Treiber dem Cursortyp, der möglichst effizient die Merkmale enthält die Anwendung angefordert.  
  
 Wenn eine Anwendung eine die Anweisungsattribute SQL_ATTR_CURSOR_SCROLLABLE, SQL_ATTR_CURSOR_SENSITIVITY oder SQL_ATTR_CURSOR_TYPE SQL_ATTR_CONCURRENCY festlegt, nimmt der Treiber alle erforderlichen Änderungen, die andere Anweisungsattribute, die in diesem Satz von vier Attribute, sodass ihre Werte konsistent bleiben. Daher, wenn die Anwendung ein Merkmal Cursor angegeben ist, kann der Treiber das Attribut ändern, die Cursortyp basierend auf dieser Auswahl implizite; Wenn die Anwendung einen Typ gibt an, kann der Treiber die anderen Attribute mit den Eigenschaften des ausgewählten Typs konsistent ändern. Weitere Informationen zu diesen Anweisungsattribute, finden Sie unter der [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) funktionsbeschreibung.  
  
 Eine Anwendung, die Anweisungsattribute eines Cursortyps und Cursormerkmale an legt ist mit dem Risiko zum Erstellen eines Cursors, das nicht die effizienteste Methode, die auf diesen Treiber Erfüllung von den Anforderungen der Anwendung verfügbar ist.  
  
 Die implizite Einstellung Anweisungsattribute ist treiberdefinierten mit dem Unterschied, dass die folgenden Regeln beachtet werden müssen:  
  
-   Vorwärtscursor werden niemals bildlauffähigen; Anzeigen der Definition der SQL_ATTR_CURSOR_SCROLLABLE in [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
-   INSENSITIVE-Cursor können nie aktualisiert (und somit die Parallelität ist, nur-Lese); Dieser Wert basiert auf ihre Definition im standard ISO SQL insensitive-Cursor.  
  
 Daher tritt auf, die implizite Einstellung Anweisungsattribute, in den Fällen, in der folgenden Tabelle beschrieben.  
  
|Anwendung wird das Attribut auf|Andere Attribute festgelegt implizit.|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY auf SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY auf SQL_INSENSITIVE.|  
|SQL_ATTR_CONCURRENCY zu SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER, SQL_CONCUR_VALUES|SQL_ATTR_CURSOR_SENSITIVITY auf SQL_UNSPECIFIED oder SQL_SENSITIVE, wie vom Treiber definiert. Es kann nie auf SQL_INSENSITIVE, festgelegt werden, da insensitive-Cursor immer schreibgeschützt sind.|  
|SQL_ATTR_CURSOR_SCROLLABLE auf SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE auf SQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN oder SQL_CURSOR_DYNAMIC, wie vom Treiber angegeben. Es wird nie auf SQL_CURSOR_FORWARD_ONLY festgelegt.|  
|SQL_ATTR_CURSOR_SENSITIVITY auf SQL_INSENSITIVE|SQL_ATTR_CONCURRENCY auf SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_STATIC.|  
|SQL_ATTR_CURSOR_SENSITIVITY auf SQL_SENSITIVE|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER oder SQL_CONCUR_VALUES, wie vom Treiber angegeben. Es wird nie auf SQL_CONCUR_READ_ONLY festgelegt.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN oder SQL_CURSOR_DYNAMIC, wie vom Treiber angegeben.|  
|SQL_ATTR_CURSOR_SENSITIVITY auf SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY auf SQL_CONCUR_READ_ONLY, SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER oder SQL_CONCUR_VALUES, wie vom Treiber angegeben.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN oder SQL_CURSOR_DYNAMIC, wie vom Treiber angegeben.|  
|SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLE auf SQL_SCROLLABLE.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY auf SQL_SENSITIVE. (Aber nur, wenn SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY nicht entspricht. Aktualisierbare dynamische Cursor sind immer empfindlich gegenüber Änderungen, die in ihre eigenen Transaktionen vorgenommen wurden.)|  
|SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE auf SQL_NONSCROLLABLE.|  
|SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLE auf SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED oder SQL_SENSITIVE (gemäß den treiberdefinierten Kriterien, wenn SQL_ATTR_CONCURRENCY nicht SQL_CONCUR_READ_ONLY ist).|  
|SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLE auf SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY auf SQL_INSENSITIVE (wenn SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY ist).<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED oder SQL_SENSITIVE (wenn SQL_ATTR_CONCURRENCY nicht SQL_CONCUR_READ_ONLY ist).|
