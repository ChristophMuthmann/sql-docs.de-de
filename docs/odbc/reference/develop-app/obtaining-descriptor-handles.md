---
title: Abrufen von Deskriptor behandelt | Microsoft Docs
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
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f66fb64b8d54e2b620779e6548e9ff4a965d31ef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="obtaining-descriptor-handles"></a>Behandelt Deskriptor abrufen
Ruft eine Anwendung als ausgabeargument des Aufrufs an das Handle für alle explizit reservierte Deskriptor ab **SQLAllocHandle**. Das Handle für eine implizit zugeordnete Sicherheitsbeschreibung wird abgerufen, indem Aufrufen **SQLGetStmtAttr**.
