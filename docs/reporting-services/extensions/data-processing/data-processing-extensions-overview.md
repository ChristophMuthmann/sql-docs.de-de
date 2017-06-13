---
title: "Übersicht über die Datenverarbeitung | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], about extensions
ms.assetid: 1d652605-9313-4c75-98b4-ba4dcbbb222d
caps.latest.revision: 39
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c30ea734a30e00fdefeb9b30a1ced9c3f60d5fca
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="data-processing-extensions-overview"></a>Übersicht über Datenverarbeitungserweiterungen
  Mithilfe von Datenverarbeitungserweiterungen in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] können Sie eine Verbindung zu einer Datenquelle herstellen und Daten abrufen. Sie dienen außerdem als Verbindung zwischen einer Datenquelle und einem Dataset. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]datenverarbeitungserweiterungen werden nach einer Untermenge der modelliert die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] .NET-datenanbieterschnittstellen nachgebildet.  
  
 In folgender Tabelle finden Sie eine Liste der Datenverarbeitungserweiterungen, die in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] enthalten sind.  
  
|Datenverarbeitungserweiterung|Description|  
|-------------------------------|-----------------|  
|Datenverarbeitungserweiterung für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Verwendet die .NET Framework-Datenanbieter für SQL Server herstellen und Abrufen von Daten aus der [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)].|  
|Datenverarbeitungserweiterung für OLE DB|Verwendet die .NET Framework-Datenanbieter für OLE DB. Mit dieser Erweiterung kann der Berichtsserver jede Datenquelle abfragen, die über einen OLE DB-Anbieter verfügt.|  
|Datenverarbeitungserweiterung für Oracle|Der .NET Framework-Datenanbieter verwendet für Oracle. Mit dieser Erweiterung kann der Berichtsserver über die Oracle-Clientkonnektivitätssoftware auf Oracle-Datenquellen zugreifen.|  
|Datenverarbeitungserweiterung für ODBC|Verwendet die .NET Framework-Datenanbieter für ODBC. Mit dieser Erweiterung kann der Berichtsserver auf Daten in jeder Datenbank zugreifen, für die ein ODBC-Treiber vorhanden ist.|  
  
 Sie können die [!INCLUDE[ssRS](../../../includes/ssrs-md.md)]-Datenverarbeitungs-API verwenden, um benutzerdefinierte Datenverarbeitungen zu Ihrem Berichtsserver hinzuzufügen.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] verfügt über integrierte Unterstützung von Datenanbietern in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Wenn Sie bereits einen kompletten Datenanbieter implementiert haben, müssen Sie die [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Datenverarbeitungserweiterung nicht implementieren. Sie sollten jedoch überlegen, ob Sie Ihren Datenanbieter erweitern, sodass er spezifische Funktionen für [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 2005 enthält, z. B. sichere Verbindungsanmeldeinformationen und serverseitige Aggregate.  
  
 Jede in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] enthaltene Datenverarbeitungserweiterung verwendet eine Reihe gemeinsamer Schnittstellen. Damit wird sichergestellt, dass jede Erweiterung vergleichbare Funktionen implementiert.  
  
 Sie können Datenverarbeitungserweiterungen für Ihre eigenen Datenquellen entwickeln, oder Sie können die Schnittstellen verwenden, um den allgemeinen Datenbankinfrastrukturen eine weitere Datenverarbeitungsebene hinzuzufügen. Sie können Ihre benutzerdefinierten Datenverarbeitungserweiterungen so bereitstellen, dass sie eine nahtlose Integration der Daten in die bestehenden Berichtsserver in Ihrer Organisation ermöglichen. Sie können Sie auch als Teil einer benutzerdefinierten Berichtssuite verwenden, die Sie Ihren Consumern anbieten.  
  
 ![Architektur von datenverarbeitungserweiterungen](../../../reporting-services/extensions/data-processing/media/bk-dataprocess-extensions.gif "Data processing extension architecture")  
Architektur für Berichtsserver-Datenverarbeitungserweiterungen  
  
 Die Implementierung einer benutzerdefinierten [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Datenverarbeitungserweiterung hat folgende Vorteile:  
  
-   Eine vereinfachte Datenzugriffsarchitektur, häufig mit besserer Verwaltbarkeit und verbesserter Leistung.  
  
-   Die Fähigkeit, erweiterungsspezifische Funktionen direkt für die Consumer verfügbar zu machen.  
  
-   Eine spezifische Schnittstelle für die Consumer, um auf die Datenquelle in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] zuzugreifen.  
  
## <a name="data-extension-process-flow"></a>Verarbeitungsablauf für Datenerweiterungen  
 Bevor Sie Ihre benutzerdefinierte Datenerweiterung bereitstellen, sollten Sie wissen, wie der Berichtsserver Datenerweiterungen zur Verarbeitung von Daten verwendet. Sie sollten auch die Konstruktoren und Verfahren kennen, die vom Berichtsserver aufgerufen werden.  
  
 ![Prozessablauf für datenverarbeitungserweiterung](../../../reporting-services/extensions/data-processing/media/bk-ext-01.gif "Process flow for data processing extension")  
Der schrittweise Verarbeitungsablauf einer Datenerweiterung, die vom Berichtsserver aufgerufen wird  
  
 Die Abbildung stellt die folgende Abfolge von Ereignissen dar:  
  
1.  Der Berichtsserver erstellt ein Verbindungsobjekt und übergibt die Verbindungszeichenfolge und die zum Bericht gehörigen Anmeldeinformationen.  
  
2.  Der Befehlstext des Berichts wird verwendet, um ein Befehlsobjekt zu erstellen. Im Prozess kann die Datenverarbeitungserweiterung Code enthalten, der den Befehlstext analysiert und alle Parameter für den Befehl erstellt.  
  
3.  Sobald das Befehlsobjekt und die Parameter verarbeitet sind, wird ein Datenleser generiert, der ein Resultset zurückgibt und den Berichtsserver in die Lage versetzt, die Berichtsdaten mit dem Berichtslayout zu verknüpfen.  
  
## <a name="developer-requirements"></a>Anforderungen für die Entwickler  
 Für die Entwicklung einer [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Datenverarbeitungserweiterung benötigen Sie Folgendes:  
  
-   Einen Bereitstellungscomputer, auf dem Berichts-Designer oder ein Berichtsserver installiert ist.  
  
-   Einen Entwicklungscomputer mit [!INCLUDE[vsprvsext](../../../includes/vsprvsext-md.md)] oder höher, oder die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Software Development Kit (SDK) installiert.  
  
-   Sehr gute Kenntnisse der [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Funktionen und -Möglichkeiten.  
  
-   Eine sehr gute Kenntnisse der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] Architektur verteilter Transaktionen, [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Datenanbieter, ADO.NET DataSet-Objekte sowie die allgemeinen [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] Schnittstellen.  
  
-   Entwicklungserfahrung in einer [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Sprache, z. B. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#- oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET.  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Erweiterungen](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
