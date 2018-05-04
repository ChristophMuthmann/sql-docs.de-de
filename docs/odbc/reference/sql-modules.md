---
title: SQL-Module | Microsoft Docs
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
- SQL modules [ODBC]
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], modules
- modules [ODBC]
- SQL statements [ODBC], modules
ms.assetid: 07551472-87ee-4765-951f-1364ed32f0c0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10957c8e4a847f13d2dbf4b427382e65ea404c1f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sql-modules"></a>SQL-Module
Das zweite Verfahren zum Senden von SQL-Anweisungen an das DBMS erfolgt über Module. Ein Modul besteht nur kurz, eine Gruppe von Prozeduren, die vom Host Programmiersprache aufgerufen werden. Jede Prozedur enthält eine einzelne SQL-Anweisung, und Daten werden in und aus der Prozedur über Parameter übergeben.  
  
 Ein Modul kann als eine Objektbibliothek betrachtet werden, die mit den Code der Anwendung verknüpft ist. Allerdings genau wie die Prozeduren und den Rest der Anwendung verknüpft sind, ist implementierungsabhängig. Z. B. die Prozeduren in Objektcode kompiliert und direkt mit dem Anwendungscode verknüpft werden konnte, kompiliert und auf das DBMS und die Plan-IDs im Anwendungscode platziert den Zugriff auf Aufrufe gespeichert werden konnten oder zur Laufzeit interpretiert werden konnte.  
  
 Der Hauptvorteil von Modulen ist, dass sie ordnungsgemäß SQL-Anweisungen in der Programmiersprache fungieren. Theoretisch sollte es möglich, einer ohne Änderung der anderen geändert, und einfach zu verknüpfen.
