---
title: SQLGetData und Blockcursor | Microsoft Docs
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
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8642e5c228bb0e7976099d2151fe36f4db683f27
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData und Blockcursor
**SQLGetData** arbeitet mit einer einzelnen Spalte aus einer einzelnen Zeile und ein Array mit Daten aus mehreren Zeilen kann nicht abgerufen werden. Dies ist, da der Hauptverwendungszweck des **SQLGetData** wird zum Abrufen von long-Daten in Teilen, und es ist nur wenig oder gar keinen Grund dafür für mehr als eine Zeile zu einem Zeitpunkt.  
  
 Mit **SQLGetData** mit einem Blockcursor, ruft eine Anwendung zunächst **SQLSetPos** zur Positionierung des Cursors für eine einzelne Zeile. Er ruft dann **SQLGetData** für eine Spalte in dieser Zeile. Dieses Verhalten ist jedoch optional. Um festzustellen, ob ein Treiber die Verwendung von unterstützt **SQLGetData** mit Blockcursor, eine Anwendung ruft **SQLGetInfo** mit der Option SQL_GETDATA_EXTENSIONS.
