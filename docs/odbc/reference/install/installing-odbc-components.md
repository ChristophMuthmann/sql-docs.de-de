---
title: Installieren von ODBC-Komponenten | Microsoft Docs
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
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2cf4bec202249de89178e5618cdaa5f2770778fc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="installing-odbc-components"></a>Installieren von ODBC-Komponenten
> [!NOTE]  
>  Ab Windows XP und Windows Server 2003, ist ODBC in der Windows-Betriebssystem enthalten. Sie sollten nur explizit ODBC in früheren Versionen von Windows installieren.  
  
 In diesem Abschnitt wird beschrieben, wie die ODBC-Komponenten installiert oder entfernt werden. Da Treiberentwickler immer eine ODBC-Komponente (ihre Treiber) installieren, müssen sie diesen Abschnitt lesen. Anwendungsentwickler müssen diesen Abschnitt nur, wenn sie ODBC-Komponenten mit ihren Anwendungen ausliefern zu lesen. ODBC-Komponenten zählen der Treiber-Manager, Treiber, Konvertierer, das Installationsprogramm DLL, die Cursorbibliothek und alle zugehörigen Dateien. Der Rahmen in diesem Abschnitt werden die ODBC-Anwendungen ODBC-Komponenten werden nicht berücksichtigt.  
  
> [!NOTE]  
>  Dieser Abschnitt bezieht sich auf Microsoft Windows-Plattformen. Wie die ODBC-Komponenten auf anderen Plattformen installiert werden, ist plattformspezifisch.  
  
 ODBC-Komponenten sind installiert und entfernt auf Basis von Komponente, nicht-Datei-Basis. Z. B. wenn ein Konvertierungsprogramm des konvertierers selbst und eine Anzahl von Datendateien besteht, diese Dateien sind installiert und als Gruppe entfernt; Sie müssen nicht installiert und entfernt auf Basis von Datei. Der Grund dafür ist, um sicherzustellen, dass nur vollständige Komponenten auf dem System vorhanden.  
  
 Für die Zwecke der installieren und Entfernen von Komponenten werden ODBC-Komponenten die folgenden so definiert:  
  
-   **Kernkomponenten.** Im Zusammenhang mit der Treiber-Manager, Cursorbibliothek, DLL-Installationsprogramm und alle anderen Dateien bilden zusammen die Kernkomponenten und müssen installiert und als Gruppe entfernt.  
  
-   **Treiber.** Jeder Treiber ist eine separate Komponente.  
  
-   **Konvertierer.** Jede Konvertierer ist eine separate Komponente.  
  
 Dank der Unterstützung von Unicode in ODBC 3.5 und höher muss bedacht werden bei der Verwendung von OLE DB-Komponenten mit ODBC. Bestimmte Unicode-Spezifikationen in ODBC 3.0 wurde der Version 1.1 von der OLE DB-Anbieter für ODBC geschrieben. Da diese Spezifikationen in ODBC 3.5 geändert wurde, ist es notwendig, dass die Version 1.5 oder höher des Anbieters ist bei Verwendung von ODBC 3.5 und höher. Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Installationskomponenten](../../../odbc/reference/install/installation-components.md)  
  
-   [Zählen der Verwendung](../../../odbc/reference/install/usage-counting.md)
