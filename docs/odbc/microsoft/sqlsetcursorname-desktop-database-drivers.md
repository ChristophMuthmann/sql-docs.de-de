---
title: SQLSetCursorName (Desktop-Datenbanktreiber) | Microsoft Docs
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
- SQLSetCursorName function [ODBC], Desktop Database Drivers
ms.assetid: 9bd7c87b-d99d-4e23-b2db-868d3b461c94
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc2bfb70c48e353a0f37f020e795057ae54edfd2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName (Desktop-Datenbanktreiber)
Da der Treiber kein positioniertes Update unterstützt oder, indem Sie die WHERE CURRENT OF löschen *Cursorname* Syntax **SQLSetCursorName** wird unterstützt, aber nicht für positionierte Updates verwendet werden. Er kann nur verwendet werden, wenn die Cursorbibliothek aktiviert ist und die Anwendung verwendet **SQLExtendedFetch**.
