---
title: Abrufen von Deskriptor behandelt | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 921d3e9bc76ff49b35b58d3b519a4adcc227d241
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="obtaining-descriptor-handles"></a>Behandelt Deskriptor abrufen
Ruft eine Anwendung als ausgabeargument des Aufrufs an das Handle für alle explizit reservierte Deskriptor ab **SQLAllocHandle**. Das Handle für eine implizit zugeordnete Sicherheitsbeschreibung wird abgerufen, indem Aufrufen **SQLGetStmtAttr**.
