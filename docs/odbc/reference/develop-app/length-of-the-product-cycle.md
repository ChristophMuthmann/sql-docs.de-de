---
title: "Länge des Produktzyklus | Microsoft Docs"
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
helpviewer_keywords:
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ddd48de7b988cf16fb8c3ce5d3bc33088f487308
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="length-of-the-product-cycle"></a>Länge des Produktzyklus
Die letzte Fragen zur Interoperabilität ist Zeit. Entwickeln in der Regel eine interoperable Anwendung dauert länger als eine noninteroperable entwickeln. Der Grund ist, dass die Anwendung muss überprüfen Sie die Funktionen des DBMS, unterschiedlich Ausführen derselben Tasks für die verschiedenen DBMS umgehen von einigen DBMS, aber nicht an einem anderen unterstützten Funktionen und usw. an.  
  
 Zusätzlich zur Entwicklungszeit muss die Produkt-Lebensdauer berücksichtigt werden. Wenn die Anwendung einmal, z. B. eine Anwendung verwendet werden, die Daten zu übertragen, bei der Migration von einem DBMS in eine andere ist gibt es keinen Sinn machen es interoperabel. Die Anwendung werden einmal verwendet und verworfen.  
  
 Wenn die Anwendung für eine lange Zeit vorhanden ist, kann es einfacher zu verwalten als interoperable Anwendung sein. Dies gilt auch für benutzerdefinierte Anwendungen, die eine einzelne DBMS als Ziel haben. Der Grund ist, dass interoperable Code eine begrenzte Teilmenge der Funktionen verwendet. Der Treiber ist erforderlich, um diese Funktionen auch bei Änderungen an das zugrunde liegende DBMS verfügbar zu halten. Daher kann interoperable Code die Last der Umgang mit Änderungen des DBMS seitens des Anwendungsentwicklers dem Treiber Entwickler zu verschieben.
