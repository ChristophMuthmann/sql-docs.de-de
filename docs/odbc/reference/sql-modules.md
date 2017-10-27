---
title: SQL-Module | Microsoft Docs
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
- SQL modules [ODBC]
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], modules
- modules [ODBC]
- SQL statements [ODBC], modules
ms.assetid: 07551472-87ee-4765-951f-1364ed32f0c0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f37ab932ef230d29a5db23aec920230de0443e37
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sql-modules"></a>SQL-Module
Das zweite Verfahren zum Senden von SQL-Anweisungen an das DBMS erfolgt über Module. Ein Modul besteht nur kurz, eine Gruppe von Prozeduren, die vom Host Programmiersprache aufgerufen werden. Jede Prozedur enthält eine einzelne SQL-Anweisung, und Daten werden in und aus der Prozedur über Parameter übergeben.  
  
 Ein Modul kann als eine Objektbibliothek betrachtet werden, die mit den Code der Anwendung verknüpft ist. Allerdings genau wie die Prozeduren und den Rest der Anwendung verknüpft sind, ist implementierungsabhängig. Z. B. die Prozeduren in Objektcode kompiliert und direkt mit dem Anwendungscode verknüpft werden konnte, kompiliert und auf das DBMS und die Plan-IDs im Anwendungscode platziert den Zugriff auf Aufrufe gespeichert werden konnten oder zur Laufzeit interpretiert werden konnte.  
  
 Der Hauptvorteil von Modulen ist, dass sie ordnungsgemäß SQL-Anweisungen in der Programmiersprache fungieren. Theoretisch sollte es möglich, einer ohne Änderung der anderen geändert, und einfach zu verknüpfen.

