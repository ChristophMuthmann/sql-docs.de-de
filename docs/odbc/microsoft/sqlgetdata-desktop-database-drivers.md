---
title: SQLGetData (Desktop-Datenbanktreiber) | Microsoft Docs
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
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae546182d51663c15a14ac25b5349a06da02e952
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (Desktop-Datenbanktreiber)
Diese Funktion kann Daten aus einer beliebigen Spalte abgerufen werden, und zwar unabhängig davon, ob gebundene Spalten vorhanden sind, nachdem sie und unabhängig von der Reihenfolge, in der die Spalten abgerufen werden.  
  
> [!NOTE]  
>  \*PcbValue in **SQLGetData** möglicherweise doppelt so viele Zeichen zurückgeben als die tatsächlich verfügbare beim Binden an die ANSI-Daten, die länger als 510 Zeichen in einer Jet 4.0-Datenbank. Zeichenwerte von 510 oder weniger werden die tatsächliche CbValue zurückgegeben.
