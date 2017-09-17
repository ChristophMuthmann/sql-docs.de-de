---
title: Standard-Programmierschnittstelle | Microsoft Docs
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
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 235d61849f28b29af7ec0b9ba67fe86b38bf8239
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="standard-programming-interface"></a>Standard-Programmierschnittstelle
Die Programmierschnittstelle ist vielleicht die offensichtlichste Kandidat für die Standardisierung. In der Tat Wenn ODBC entwickelt wurde, ANSI und ISO bereits bereitgestellt Standards für embedded SQL und SQL Module. Zwar keine Standards für eine Datenbank der SQL-Zugriffsgruppe CLI vorhanden waren – eine Branche Consortium von Datenbankhersteller – wurde in Betracht ziehen, ob Elemente erstellt werden ODBC-Komponenten, die höher ist die Grundlage für ihre Arbeit.  
  
 Eine der Anforderungen für ODBC wurde, dass eine einzelne Anwendung binäre arbeiten mit mehreren DBMS musste. Es ist deshalb, dass ODBC embedded SQL oder ein Modul Sprachen nicht verwendet wird. Obwohl die Sprache in eingebetteten SQL-Modul und den Sprachen standardisiert ist, ist jede an DBMS-spezifische Precompilers gebunden. Daher Anwendungen müssen für jede DBMS neu kompiliert werden, und die resultierenden Binärdateien funktionieren nur mit einer einzelnen DBMS. Während dies für die mit geringem Volumen-Programme finden Sie in den Bereichen Minicomputer und Großrechner zulässig ist, ist es in der Welt PC nicht akzeptabel. Zunächst ist es eine logistische Verlusts auf mehrere Versionen der Software hohem Volumen, eingeschweißt Kunden liefern. Zweitens müssen PC Anwendungen häufig mehrere DBMS gleichzeitig zugreifen.  
  
 Andererseits, kann ein Call-Level-Interface implementiert werden, über die Bibliotheken oder Datenbanktreiber, die sich auf jedem lokalen Computer befinden; ein anderer Treiber ist für jede DBMS erforderlich. Modernen Betriebssysteme diese Bibliotheken (z. B. Dynamic Link Libraries unter dem Betriebssystem Microsoft® Windows®) zur Laufzeit geladen werden können, eine einzelne Anwendung Daten aus anderen DBMS ohne Neukompilierung und kann auch Zugriff auf Daten aus mehrere Datenbanken gleichzeitig aus. Sobald neue Datenbanktreiber verfügbar sind, können Benutzer nur installieren Sie diese auf ihren Computern ohne ändern, neu kompilieren und verknüpfen ihre datenbankanwendungen. Darüber hinaus eine Call-Level-Interface ein guter Kandidat für ODBC wurde, da Windows – der Plattform für die ODBC ursprünglich entwickelt wurde – umfassenden Gebrauch von diese Bibliotheken bereits vorgenommen.
