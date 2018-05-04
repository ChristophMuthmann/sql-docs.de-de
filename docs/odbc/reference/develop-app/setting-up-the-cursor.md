---
title: Einrichten des Cursors | Microsoft Docs
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
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7261481c5d484f3cff774b00e0318432c0e085d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setting-up-the-cursor"></a>Einrichten der Cursor
Die Anwendung kann den Cursortyp angeben, vor dem Ausführen einer Anweisung, die ein Ergebnis erstellt. Dies geschieht mit dem SQL_ATTR_CURSOR_TYPE-Attribut-Anweisung. Wenn die Anwendung nicht explizit einen Typ angeben, wird ein Vorwärtscursor verwendet werden. Um einen gemischten Cursor zu erhalten, eine Anwendung gibt einen keysetgesteuerter Cursor deklariert jedoch eine Keysetgröße kleiner als die Größe des Resultsets.  
  
 Für keysetgesteuerte und gemischten Cursor verwendet kann die Anwendung auch die Keysetgröße angeben. Dies geschieht mit SQL_ATTR_KEYSET_SIZE-Anweisungsattribut. Wenn die Keysetgröße auf 0 (null) festgelegt ist, wird der Standardwert die Keysetgröße festgelegt ist, um die Größe des Resultsets und ein keysetgesteuerter Cursor verwendet wird. Die Keysetgröße kann geändert werden, nachdem der Cursor geöffnet wurde.  
  
 Die Anwendung kann auch die Rowsetgröße festgelegt; Weitere Informationen finden Sie unter [Verwenden von Blockcursorn](../../../odbc/reference/develop-app/using-block-cursors.md)weiter oben in diesem Abschnitt.
