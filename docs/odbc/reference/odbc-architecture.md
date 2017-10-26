---
title: ODBC-Architektur | Microsoft Docs
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
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 04e952a79e026697592f8412c48eb2e065da18df
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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

