---
title: Reservierte Wörter für Jet 4.0 verwendet SQL-92-Liste, wenn ExtendedAnsiSQL_Set | Microsoft Docs
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
- extendedANSISQL [ODBC], reserved words
ms.assetid: 7645187e-7777-4c07-9686-0a80d5c5834d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0d8c81424b215d570961e3a209347694a37393c5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisqlset"></a>Reservierte Wörter für Jet 4.0 verwendet SQL-92-Liste, wenn ExtendedAnsiSQL_Set
Wenn das ExtendedAnsiSQL-Flag aktiviert ist, verwendet Jet 4.0 die Liste der SQL-92-reservierte Wörter. Bei dem Versuch, eine SQL-92 verwenden reservierten Wort als Objektnamen ohne Anführungszeichen ein Syntaxfehler führt. Wenn das Flag ExtendedAnsiSQL deaktiviert ist, können die neuen reservierten Wörter als Objektnamen wie vor verwendet werden.
