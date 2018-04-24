---
title: Entwicklerhandbuch (Datenbankmodul) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: relational-databases-misc
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- developer's guide [SQL Server Database Engine]
- Database Engine [SQL Server], development
ms.assetid: 7638f46c-9e66-48e6-9a9b-425e0b788311
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 61270789e5adbfe189e1f9e3c9f6ff7448d2185d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="database-engine-developer-documentation"></a>Entwicklerhandbuch (Datenbankmodul)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] stellt einen umfangreichen Satz von Tools zum Entwickeln, Verwalten und Steuern von Datenbankanwendungen bereit.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Common Language Runtime &#40;CLR&#41; Programmierkonzepte für die Integration](../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
 Beschreibt die Integration der CLR-Komponente (Common Language Runtime) von .NET Framework für [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Das bedeutet, dass Sie gespeicherte Prozeduren, Trigger, benutzerdefinierte Typen, benutzerdefinierte Funktionen, benutzerdefinierte Aggregate und Streaming-Tabellenwertfunktionen in einer beliebigen .NET Framework-Sprache schreiben können, einschließlich [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic .NET und [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C#.  
  
 [Programmierung für SQL Server Native Client](../relational-databases/native-client/sql-server-native-client-programming.md)  
 Beschreibt, wie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client zur Erstellung neuer Anwendungen bzw. Erweiterung vorhandener Anwendungen verwendet werden kann, um neue [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Funktionen wie Multiple Active Result Sets (MARS), benutzerdefinierte Datentypen (UDT), Abfragebenachrichtigungen, Momentaufnahmeisolation und Unterstützung für XML-Datentypen zu nutzen.  
  
 [SQLXML 4.0-Programmierkonzepte](../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
 Beschreibt die jüngste Version von SQLXML, die dieselbe Funktionalität wie SQLXML 3.0 bereitstellt. Darüber hinaus bietet sie zusätzliche Updates mit neuen Funktionen, die in [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] eingeführt wurden, wie beispielsweise den XML-Datentyp.  
  
 [Konzepte des WMI-Anbieters für die Konfigurationsverwaltung](../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
 Beschreibt eine veröffentlichte Ebene, die mit dem Snap-In des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Konfigurations-Managers für Microsoft Management Console (MMC) und dem [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Konfigurations-Manager verwendet wird. Sie bietet eine vereinheitlichte Schnittstellenfunktion zu API-Aufrufen, mit denen die vom [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Konfigurations-Manager angeforderten Registrierungsvorgänge verwaltet werden, und ermöglicht eine verbesserte Steuerung und Bearbeitung der ausgewählten [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Dienste.  
  
 [Konzepte des WMI-Anbieters für Serverereignisse](../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)  
 Beschreibt, wie die Windows-Verwaltungsinstrumentation (WMI) verwendet wird, um Ereignisse in einer Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zu überwachen.  
  
 [SQL Server Management Objects &#40;SMO&#41; Programmierhandbuch](../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
 Enthält Informationen über [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Objects (SMO), eine Auflistung von Objekten, die zum Programmieren aller Aspekte der Verwaltung von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vorgesehen sind.  
  
 [Datenbankmodul – Programmierung der erweiterten gespeicherten Prozedur](../relational-databases/database-engine-extended-stored-procedure-programming.md)  
 Beschreibt, wie erweiterte gespeicherte Prozeduren zur Erstellung eigener externer Routinen in einer Programmiersprache wie z. B. C verwendet werden.  
  
 [Programmieren mit dem Datensammler](http://msdn.microsoft.com/library/53b4752b-055d-4716-b2bc-75b4cce84101)  
 Beschreibt das Datensammler-Objektmodell.  
  
 [Programmierung eines Ausnahmemeldungsfelds](http://msdn.microsoft.com/library/0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c)  
 Beschreibt, wie Sie das Ausnahmemeldungsfeld (eine programmgesteuerte Schnittstelle) in Ihren Anwendungen verwenden können, um die Steuerungsmöglichkeiten für Meldungen zu erweitern, Benutzern die Möglichkeit zum Speichern von Fehlermeldungen zur späteren Bezugnahme zu geben und Hilfe zu Meldungen abzurufen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Data Mining-Programmierung](../analysis-services/data-mining-programming.md)   
 [Entwicklerhandbuch (Analysis Services)](../analysis-services/analysis-services-developer-documentation.md)   
 [Entwicklerhandbuch (Integration Services)](../integration-services/integration-services-developer-documentation.md)   
 [Entwicklerhandbuch (Replikation)](../relational-databases/replication/concepts/replication-developer-documentation.md)   
 [Entwicklerhandbuch (Reporting Services)](../reporting-services/reporting-services-developer-documentation.md)  
  
  
