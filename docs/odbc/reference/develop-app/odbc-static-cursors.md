---
title: Statische ODBC-Cursor | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 049eb6998407ad02ca91565d9b26d0a0bf9b37eb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-static-cursors"></a>Statische ODBC-Cursor
Ein statischer Cursor ist in der das Resultset angezeigt wird, um statisch sein. Es kann nicht in der Regel Änderungen erkennen, die an der Mitgliedschaft, Reihenfolge oder Werte des Resultsets nach dem Öffnen des Cursors vorgenommen wurden. Nehmen wir beispielsweise an ein statischer Cursor abruft, eine Zeile und einer anderen Anwendung wird diese Zeile aktualisiert. Wenn der statische Cursor die Zeile refetches, sind die Werte, die er angezeigt wird trotz der von der anderen Anwendung vorgenommenen unverändert.  
  
 Statische Cursor können ihre eigenen Updates, löschungen und einfügungen, erkennen, obwohl sie nicht dazu erforderlich sind. Gibt an, ob diese Änderungen auf ein bestimmter statischer Cursor erkannt wird, wird durch die SQL_STATIC_SENSITIVITY-Option in gemeldet **SQLGetInfo**. Statische Cursor erkennen nie andere aktualisiert, gelöscht und fügt ein.  
  
 Die zeilenstatusarray SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut gemäß kann SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO oder SQL_ROW_ERROR für jede Zeile enthalten. Es gibt SQL_ROW_UPDATED, SQL_ROW_DELETED oder SQL_ROW_ADDED für Zeilen aktualisiert, gelöscht oder eingefügt, indem der Cursor, vorausgesetzt, dass solche Änderungen zu der Cursor erkennen kann.  
  
 Statische Cursor werden in der Regel implementiert durch Sperren von Zeilen im Resultset oder durch Erstellen einer Kopie oder snapshot, der das Ergebnis festgelegt. Sperren von Zeilen relativ einfach ist, hat aber den Nachteil deutlich sinkt Parallelität. Erstellen einer Kopie für erhöhte Parallelität ermöglicht und ermöglicht den Cursor zur nachverfolgung eine eigene Updates, löschungen und fügt durch Ändern der Kopie. Allerdings ist eine Kopie teurer machen und können aus den zugrunde liegenden Daten grundlegend, wie diese Daten von anderen Benutzern geändert werden.
