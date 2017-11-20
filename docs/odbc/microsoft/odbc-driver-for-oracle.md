---
title: "ODBC-Treiber für Oracle | Microsoft Docs"
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
- ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], about ODBC driver for Oracle
- Oracle data access [ODBC]
ms.assetid: 937e0662-8b1d-44f7-b077-4015c6605b2c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e66dd7ed6406287c0fb4e6722d8b5915428f705b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-driver-for-oracle"></a>ODBC-Treiber für Oracle
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Microsoft® ODBC-Treiber für Oracle ermöglicht Ihnen, die ODBC-kompatiblen Anwendung mit einer Oracle-Datenbank herzustellen. Der ODBC-Treiber für Oracle entspricht der Open Database Connectivity (ODBC)-Spezifikation beschrieben, die der *ODBC Programmer's Reference*. Es ermöglicht den Zugriff auf PL/SQL-Pakete, XA-DTC-Integration und Oracle-Zugriff von innerhalb von IIS (Internetinformationsdienste).  
  
 Oracle RDBMS ist einer Mehrbenutzer Relationales Datenbankmanagementsystem, das mit verschiedenen Betriebssystemen Arbeitsstation und Minicomputer ausgeführt wird. IBM-kompatiblen Computern unter Microsoft Windows können mit der Oracle-Datenbankserver über ein Netzwerk kommunizieren. Unterstützte Netzwerke umfassen Microsoft LAN-Manager, NetWare, VINES, DECnet und alle Netzwerke, die TCP/IP unterstützt.  
  
 Der ODBC-Treiber für Oracle ermöglicht einer Anwendung Zugriff auf Daten in einer Oracle-Datenbank über die ODBC-Schnittstelle. Der Treiber die lokale Oracle-Datenbanken zugreifen kann, oder können Kommunikation mit dem Netzwerk über SQL * Net. Das folgende Diagramm enthält diese Anwendung und der Treiber-Architektur.  
  
 ![ODBC-Treiber für Oracle-app &#47; Treiberarchitektur](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 Der ODBC-Treiber für Oracle entspricht-API-Konformität Level 1 und SQL-Konformität Level Core. Außerdem werden einige Funktionen in der API-Konformität Level 2 und die meisten der Übereinstimmungsebenen Kern- und erweiterte SQL-Grammatik unterstützt. Der Treiber ODBC 2.5-kompatibel ist und 32-Bit-Systemen unterstützt. Oracle 7.3 x wird vollständig; unterstützt 8 bietet eingeschränkte Unterstützung. Der ODBC-Treiber für Oracle unterstützt die neuen Datentypen von 8 – Unicode-Datentypen, BLOBs, CLOBs, usw. – noch die Unterstützung für neue relationale Objektmodell von Oracle. Weitere Informationen zu unterstützten Datentypen finden Sie unter [Supported Data Types](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) in diesem Handbuch.  
  
 Um die Oracle-Daten zugreifen zu können, sind die folgenden Komponenten erforderlich:  
  
-   Der ODBC-Treiber für Oracle  
  
-   Ein Oracle-RDBMS-Datenbank  
  
-   Oracle-Clientsoftware  
  
 Darüber hinaus für Remoteverbindungen:  
  
-   Ein Netzwerk, die Computer verbindet, die der Treiber und der Datenbank ausgeführt. Das Netzwerk muss unterstützen SQL * Net-Verbindungen.  
  
## <a name="component-documentation"></a>Dokumentation der Komponente  
 Dieses Handbuch enthält ausführliche Informationen zum Einrichten und Konfigurieren von Microsoft ODBC-Treiber für Oracle und programmgesteuerten Funktionen hinzufügen. Darüber hinaus wird die Materialien, die technische Referenz enthält.  
  
 Informationen zu bestimmten Oracle Produktverhalten finden Sie in der Dokumentation, die dem Oracle-Produkt beigefügt.  
  
 Informationen zum Einrichten oder konfigurieren den Microsoft ODBC Driver for Oracle über die ODBC-Datenquellen-Administrator finden Sie unter der [ODBC-Datenquellenadministrator](../../odbc/admin/odbc-data-source-administrator.md) Dokumentation.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [ODBC-Treiber für Oracle-Benutzerhandbuch](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [ODBC-Treiber für Oracle-Programmierreferenz](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)

