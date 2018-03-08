---
title: "Reservierte Wörter für Jet 4.0 verwendet SQL-92-Liste, wenn ExtendedAnsiSQL_Set | Microsoft Docs"
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
helpviewer_keywords: extendedANSISQL [ODBC], reserved words
ms.assetid: 7645187e-7777-4c07-9686-0a80d5c5834d
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8fb1b9b7aec3b0456dc65dd1294403d2b934a4a3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisqlset"></a>Reservierte Wörter für Jet 4.0 verwendet SQL-92-Liste, wenn ExtendedAnsiSQL_Set
Wenn das ExtendedAnsiSQL-Flag aktiviert ist, verwendet Jet 4.0 die Liste der SQL-92-reservierte Wörter. Bei dem Versuch, eine SQL-92 verwenden reservierten Wort als Objektnamen ohne Anführungszeichen ein Syntaxfehler führt. Wenn das Flag ExtendedAnsiSQL deaktiviert ist, können die neuen reservierten Wörter als Objektnamen wie vor verwendet werden.
