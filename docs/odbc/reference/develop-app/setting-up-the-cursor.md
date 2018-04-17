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
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39bb6f6f61d8477fae1f0a07b2960b77dd987643
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="setting-up-the-cursor"></a>Einrichten der Cursor
Die Anwendung kann den Cursortyp angeben, vor dem Ausführen einer Anweisung, die ein Ergebnis erstellt. Dies geschieht mit dem SQL_ATTR_CURSOR_TYPE-Attribut-Anweisung. Wenn die Anwendung nicht explizit einen Typ angeben, wird ein Vorwärtscursor verwendet werden. Um einen gemischten Cursor zu erhalten, eine Anwendung gibt einen keysetgesteuerter Cursor deklariert jedoch eine Keysetgröße kleiner als die Größe des Resultsets.  
  
 Für keysetgesteuerte und gemischten Cursor verwendet kann die Anwendung auch die Keysetgröße angeben. Dies geschieht mit SQL_ATTR_KEYSET_SIZE-Anweisungsattribut. Wenn die Keysetgröße auf 0 (null) festgelegt ist, wird der Standardwert die Keysetgröße festgelegt ist, um die Größe des Resultsets und ein keysetgesteuerter Cursor verwendet wird. Die Keysetgröße kann geändert werden, nachdem der Cursor geöffnet wurde.  
  
 Die Anwendung kann auch die Rowsetgröße festgelegt; Weitere Informationen finden Sie unter [Verwenden von Blockcursorn](../../../odbc/reference/develop-app/using-block-cursors.md)weiter oben in diesem Abschnitt.
