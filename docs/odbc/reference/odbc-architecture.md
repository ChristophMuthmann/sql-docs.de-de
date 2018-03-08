---
title: ODBC-Architektur | Microsoft Docs
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
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7e1d59692492b2b14a51a8541e01d5e06a1a6d88
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-architecture"></a>ODBC-Architektur
Die ODBC-Architektur besteht aus vier Komponenten:  
  
-   **Anwendung** Verarbeitung und ruft ODBC-Funktionen zum Senden von SQL-Anweisungen und Abrufen von Ergebnissen führt.  
  
-   **Treiber-Managers** geladen und Entladen von Treibern im Auftrag von einer Anwendung. Prozesse ODBC-Funktion aufruft oder übergibt sie an einen Treiber.  
  
-   **Treiber** Prozesse ODBC-Funktion aufruft, sendet SQL-Anforderungen an eine bestimmte Datenquelle und gibt Ergebnisse an die Anwendung zurück. Bei Bedarf, ändert der Treiber die Anforderung einer Anwendung, damit die Anforderung von der zugehörigen DBMS unterstützte Syntax entspricht.  
  
-   **Datenquelle** besteht aus den Daten der Benutzer den Zugriff und seine zugehörigen Betriebssystems DBMS, möchte und Netzwerkplattform (sofern vorhanden) verwendet wird, um das DBMS zugreifen.  
  
 Beachten Sie die folgenden Punkte bezüglich der ODBC-Architektur. Erste, mehrere Treibern und Datenquellen können vorhanden sein, dadurch wird die Anwendung auf Daten aus mehr als eine Datenquelle gleichzeitig zugreifen. Zweitens wird der ODBC-API verwendet, an zwei Orten: zwischen der Anwendung und der Treiber-Manager sowie zwischen der Treiber-Manager und jeden Treiber. Die Schnittstelle zwischen der Treiber-Manager und die Treiber wird manchmal als bezeichnet den *Service Provider Interface* oder *SPI*. Für ODBC Application programming Interface (API) und die Service Provider Interface (SPI) sind identisch. der Treiber-Manager und jeden Treiber haben, also die gleiche Schnittstelle für die gleichen Funktionen auf.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Anwendungen](../../odbc/reference/applications.md)  
  
-   [Der Treiber-Manager](../../odbc/reference/the-driver-manager.md)  
  
-   [Treiber](../../odbc/reference/drivers.md)  
  
-   [Datenquellen](../../odbc/reference/data-sources.md)
