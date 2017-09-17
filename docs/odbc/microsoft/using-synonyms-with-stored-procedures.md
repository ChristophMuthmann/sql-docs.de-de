---
title: Verwenden von Synonymen mit gespeicherten Prozeduren | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8620b039-a086-4534-8710-cc8b1787dc80
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 46ad4937f804e5557d153ff94dd9c6ab559c9f81
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-synonyms-with-stored-procedures"></a>Verwenden von Synonymen mit gespeicherten Prozeduren
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Der Microsoft ODBC-Treiber für Oracle-Versionen 2.0 und 2.5 unterstützen keine Synonyme, wenn Oracle Aufrufen von gespeicherten Prozeduren. Synonyme funktionieren wie erwartet, wenn Sie mit anderen Oracle-Datenbankobjekte wie Tabellen verwendet.
