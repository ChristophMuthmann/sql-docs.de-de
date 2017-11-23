---
title: "Reservierte Wörter für Jet 4.0 verwendet SQL-92-Liste, wenn ExtendedAnsiSQL_Set | Microsoft Docs"
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
helpviewer_keywords: extendedANSISQL [ODBC], reserved words
ms.assetid: 7645187e-7777-4c07-9686-0a80d5c5834d
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6449bd52ad17c63d50f9747d775e7f1fd8ca5efd
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisqlset"></a>Reservierte Wörter für Jet 4.0 verwendet SQL-92-Liste, wenn ExtendedAnsiSQL_Set
Wenn das ExtendedAnsiSQL-Flag aktiviert ist, verwendet Jet 4.0 die Liste der SQL-92-reservierte Wörter. Bei dem Versuch, eine SQL-92 verwenden reservierten Wort als Objektnamen ohne Anführungszeichen ein Syntaxfehler führt. Wenn das Flag ExtendedAnsiSQL deaktiviert ist, können die neuen reservierten Wörter als Objektnamen wie vor verwendet werden.
