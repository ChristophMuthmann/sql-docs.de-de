---
title: "Übersicht über die Treiber-Architektur | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], architecture
- FoxPro ODBC driver [ODBC], architecture
ms.assetid: ef5a91cd-158e-40bf-b5a8-8ba535c4705e
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6755e4b04c0d56995fb83f64891e5fcd7d765a49
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="driver-architecture-overview"></a>Treiber-Architekturübersicht
Microsoft Visual FoxPro-ODBC-Treiber ist ein 32-Bit-Treiber, der Sie öffnen, und Fragen Sie eine Microsoft Visual FoxPro-Datenbank oder FoxPro-Tabellen über die Benutzeroberfläche öffnen Database Connectivity (ODBC) ermöglicht. Sie erreichen FoxPro-Daten mithilfe der folgenden Anwendungstypen:  
  
-   Microsoft Office-Anwendung, z. B. Microsoft Excel oder Microsoft Word, Microsoft Query für die Kommunikation mit ODBC verwendet.  
  
-   Eine Anwendung in Microsoft Visual C++ oder C#, die die ODBC-SDK-API verwendet.  
  
-   Eine Anwendung in Microsoft Visual Basic oder Microsoft Visual Basic for Applications geschrieben.  
  
 In jedem Fall verwendet die Anforderung von Informationen über die ODBC-API. Der ODBC-Treiber-Manager arbeitet mit der Visual FoxPro-ODBC-Treiber zu öffnen und das Abrufen von Daten aus FoxPro-Tabellen und Datenbanken.  
  
 Die Architektur wird in der folgenden Abbildung dargestellt:  
  
 ![Zeigt die Architektur der ODBC-Treiber](../../odbc/microsoft/media/vfparch.gif "Vfparch")  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Visual FoxPro-Terminologie](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [Installieren und Konfigurieren des Visual FoxPro-ODBC-Treibers](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Mithilfe der Visual FoxPro-ODBC-Treibers](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)

