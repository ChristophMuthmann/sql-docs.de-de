---
title: Löschen von Zeilen im Rowset mit SQLSetPos | Microsoft Docs
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
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fadeb361a97cead2e43baee99bd59cad9ebbf87b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>Löschen von Zeilen im Rowset mit SQLSetPos
Der Löschvorgang des **SQLSetPos** macht die Datenquelle, die eine oder mehrere ausgewählte Zeilen einer Tabelle zu löschen. So löschen Sie Zeilen mit **SQLSetPos**, ruft die Anwendung **SQLSetPos** mit *Vorgang* auf SQL_DELETE festgelegt und *RowNumber* legen Sie auf der Anzahl der zu löschenden Zeile. Wenn *RowNumber* gleich 0 ist, werden alle Zeilen im Rowset gelöscht.  
  
 Nach dem **SQLSetPos** zurückgibt, die gelöschte Zeile wird die aktuelle Zeile und der Status SQL_ROW_DELETED. Die Zeile kann nicht verwendet werden, in allen weiteren positionierten Operationen, z. B. Aufrufe der **SQLGetData** oder **SQLSetPos**.  
  
 Beim Löschen aller Zeilen im Rowset (*RowNumber* gleich 0 ist), die Anwendung kann verhindern, dass den Treiber bestimmte Zeilen löscht, mit der Zeile Operation-Array, auf die gleiche Weise wie für den Updatevorgang **SQLSetPos** . (Siehe [Aktualisieren von Zeilen im Rowset mit SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).)  
  
 Jede Zeile, die gelöscht wird, sollte eine Zeile sein, die im Resultset vorhanden ist. Wenn die Anwendungspuffer durch Abrufen gefüllt wurden und ein zeilenstatusarray beibehalten wurde, sollten die Werte an jeder dieser Positionen Zeile nicht SQL_ROW_DELETED, SQL_ROW_ERROR oder SQL_ROW_NOROW sein.
