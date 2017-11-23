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
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2bd9088fa327783019d0b025ab4daaacd951852b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (Desktop-Datenbanktreiber)
Diese Funktion kann Daten aus einer beliebigen Spalte abgerufen werden, und zwar unabhängig davon, ob gebundene Spalten vorhanden sind, nachdem sie und unabhängig von der Reihenfolge, in der die Spalten abgerufen werden.  
  
> [!NOTE]  
>  \*PcbValue in **SQLGetData** möglicherweise doppelt so viele Zeichen zurückgeben als die tatsächlich verfügbare beim Binden an die ANSI-Daten, die länger als 510 Zeichen in einer Jet 4.0-Datenbank. Zeichenwerte von 510 oder weniger werden die tatsächliche CbValue zurückgegeben.
