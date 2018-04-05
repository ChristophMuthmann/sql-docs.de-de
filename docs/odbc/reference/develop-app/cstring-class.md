---
title: CString-Klasse | Microsoft Docs
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
- CString class [ODBC]
ms.assetid: 18630642-76fa-43c4-a154-3f0969ec9b50
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e3d3f3719fbc16a72f692b809eb646e7bbcf24d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="cstring-class"></a>CString-Klasse
Da Objekte von der **CString** Klasse in Microsoft® Visual C++ werden signiert und Zeichenfolgenargumente in ODBC-Funktionen sind ohne Vorzeichen, Anwendungen, die verstreichen **CString** Objekte von ODBC-Funktionen ohne diese Umwandlung erhalten compilerwarnungen.
