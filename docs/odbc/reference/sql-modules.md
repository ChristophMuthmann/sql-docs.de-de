---
title: SQL-Module | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL modules [ODBC]
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], modules
- modules [ODBC]
- SQL statements [ODBC], modules
ms.assetid: 07551472-87ee-4765-951f-1364ed32f0c0
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ee18719a325135af480645de3446042339a44f8b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sql-modules"></a>SQL-Module
Das zweite Verfahren zum Senden von SQL-Anweisungen an das DBMS erfolgt über Module. Ein Modul besteht nur kurz, eine Gruppe von Prozeduren, die vom Host Programmiersprache aufgerufen werden. Jede Prozedur enthält eine einzelne SQL-Anweisung, und Daten werden in und aus der Prozedur über Parameter übergeben.  
  
 Ein Modul kann als eine Objektbibliothek betrachtet werden, die mit den Code der Anwendung verknüpft ist. Allerdings genau wie die Prozeduren und den Rest der Anwendung verknüpft sind, ist implementierungsabhängig. Z. B. die Prozeduren in Objektcode kompiliert und direkt mit dem Anwendungscode verknüpft werden konnte, kompiliert und auf das DBMS und die Plan-IDs im Anwendungscode platziert den Zugriff auf Aufrufe gespeichert werden konnten oder zur Laufzeit interpretiert werden konnte.  
  
 Der Hauptvorteil von Modulen ist, dass sie ordnungsgemäß SQL-Anweisungen in der Programmiersprache fungieren. Theoretisch sollte es möglich, einer ohne Änderung der anderen geändert, und einfach zu verknüpfen.
