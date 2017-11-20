---
title: SQLGetData (Desktop-Datenbanktreiber) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e091bf31e034eaabb9c87931bc6b128f5bdeba84
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (Desktop-Datenbanktreiber)
Diese Funktion kann Daten aus einer beliebigen Spalte abgerufen werden, und zwar unabhängig davon, ob gebundene Spalten vorhanden sind, nachdem sie und unabhängig von der Reihenfolge, in der die Spalten abgerufen werden.  
  
> [!NOTE]  
>  \*PcbValue in **SQLGetData** möglicherweise doppelt so viele Zeichen zurückgeben als die tatsächlich verfügbare beim Binden an die ANSI-Daten, die länger als 510 Zeichen in einer Jet 4.0-Datenbank. Zeichenwerte von 510 oder weniger werden die tatsächliche CbValue zurückgegeben.

