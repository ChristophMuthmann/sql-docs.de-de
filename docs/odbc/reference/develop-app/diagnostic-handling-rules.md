---
title: Behandlung von Regeln diagnostische | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], diagnostic handling rules
- SQLGetDiagRec function [ODBC], diagnostic handling rules
- diagnostic information [ODBC], SqlGetDiagRec
ms.assetid: 74387c3a-d6b3-4c35-b209-b9612602b20a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9bea90a96cdfc7e879af64deeb287545d5637382
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="diagnostic-handling-rules"></a>Diagnose Behandlung Regeln
Die folgenden Regeln bestimmen die Diagnose Behandlung in **SQLGetDiagRec** und **SQLGetDiagField**.  
  
 Für alle ODBC-Komponenten:  
  
-   Muss nicht ersetzen, ändern oder Fehler oder Warnungen, die von der eine andere ODBC-Komponente zu maskieren.  
  
-   Hinzufügen eines Eintrags zusätzliche Statusinformationen möglicherweise, wenn sie eine diagnosemeldung aus einer anderen ODBC-Komponente erhalten. Die hinzugefügte Datensatz muss real Informationswert der ursprünglichen Nachricht hinzufügen.  
  
 Für den ODBC-Datenquelle Komponente, die direkt Schnittstellen:  
  
-   Müssen das Präfix der Hersteller-ID, der Komponenten­ID und die Datenquelle Bezeichner, der die diagnosemeldung aus der Datenquelle empfangenen.  
  
-   Systemeigene Fehlercode für die Datenquelle muss beibehalten werden.  
  
-   Diagnosemeldung für die Datenquelle muss beibehalten werden.  
  
 Für jede ODBC-Komponente, die einen Fehler oder die Warnung unabhängig von der Datenquelle generiert:  
  
-   Müssen die richtigen SQLSTATE für den Fehler oder die Warnung angeben.  
  
-   Muss den Text der diagnosemeldung zu generieren.  
  
-   Muss der Hersteller-ID und seine Komponentenbezeichner, der die diagnosemeldung Präfix.  
  
-   Muss ein ursprünglicher Fehlercode: zurückgeben, wenn eine sinnvolle und verfügbar ist.  
  
 Für die ODBC-Komponente, die mit der Treiber-Manager-Schnittstellen:  
  
-   Die Ausgabeargumente des initialisieren müssen **SQLGetDiagRec** und **SQLGetDiagField**.  
  
-   Formatieren und die Diagnoseinformationen als Ausgabeargumente zurückgeben muss **SQLGetDiagRec** und **SQLGetDiagField** Wenn diese Funktion aufgerufen wird.  
  
 Für eine ODBC-Komponente als der Treiber-Manager:  
  
-   Basierend auf der systemeigene Fehler SQLSTATE muss festgelegt werden. Für den dateibasierten Treibern und DBMS-basierten Treibern, die kein Gateway verwenden, muss der Treiber SQLSTATE festgelegt. Für DBMS-basierten Treibern, die ein Gateway verwenden, kann der Treiber oder ein Gateway, die ODBC unterstützt den SQLSTATE festgelegt.
