---
title: Vorbereiten der Implementierung von Datenverarbeitungserweiterungen | Microsoft Docs
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
- interfaces [Reporting Services]
- data processing extensions [Reporting Services], implementing
ms.assetid: 698817e4-33da-4eb5-9407-4103e1c35247
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 6d516201d8018b1d58b77be8e3cf543745da037a
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="preparing-to-implement-a-data-processing-extension"></a>Vorbereiten der Implementierung von Datenverarbeitungserweiterungen
  Vor der Implementierung Ihrer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] -datenverarbeitungserweiterung, sollten Sie definieren die Schnittstellen implementieren. Möglicherweise möchten Sie erweiterungsspezifische Implementierungen der gesamte Satz von Schnittstellen bereitstellen, oder Sie möchten möglicherweise einfach die Implementierung einer Untergruppe konzentrieren, wie z. B. die <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> und <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand> Schnittstellen, die in der Clients in erster Linie mit einem Resultset als interagieren würden eine **DataReader** Objekt, und verwenden Ihrer [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] datenverarbeitungserweiterung als Brücke zwischen Resultset und Datenquelle.  
  
 Sie können Datenverarbeitungserweiterungen auf zwei Arten implementieren:  
  
-   Implementieren Sie die Klassen der datenverarbeitungserweiterung können die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] -datenanbieterschnittstellen und optional die erweiterten Schnittstellen der datenverarbeitungserweiterung gebotenen [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
-   Mit den Klassen der Datenverarbeitungserweiterung können die Schnittstellen der Datenverarbeitungserweiterung implementiert werden, die von [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] vorgegeben werden, und optional die erweiterten Schnittstellen der Datenverarbeitungserweiterung.  
  
 Wenn die [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Datenverarbeitungserweiterung keine bestimmte Eigenschaft oder Methode unterstützt, implementieren Sie die Eigenschaft oder Methode als Nicht-Vorgang. Wenn ein Client ein besonderes Verhalten erwartet, lösen eine **NotSupportedException** Ausnahme.  
  
> [!NOTE]  
>  Die Nicht-Vorgangs-Implementierung einer Eigenschaft oder Methode betrifft nur die Eigenschaften oder Methoden der Schnittstellen, die Sie für die Implementierung auswählen. Optionale Schnittstellen, die sie nicht für die Implementierung auswählen, sollten nicht in der Assembly für Datenverarbeitungserweiterungen enthalten sein. Weitere Informationen zu der Frage, wann eine Schnittstelle erforderlich und wann optional ist, finden Sie in der Tabelle weiter unten in diesem Kapitel.  
  
## <a name="required-extension-functionality"></a>Erforderliche Erweiterungsfunktionen  
 Jede [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Datenverarbeitungserweiterung muss die folgenden Funktionen enthalten:  
  
-   Öffnen einer Verbindung zu einer Datenquelle.  
  
-   Analysieren einer Abfrage und Rückgabe einer Liste der Feldnamen für das Resultset.  
  
-   Ausführen einer Abfrage für die Datenquelle und Rückgabe eines Rowsets.  
  
-   Übergeben einwertiger Parameter an die Abfrage.  
  
-   Iteration durch die Zeilen im Rowset und Abrufen der Daten.  
  
 Jede Datenverarbeitungserweiterung kann auf folgende Funktionen erweitert werden:  
  
-   Analysieren einer Abfrage und Zurückgeben einer Liste der in der Abfrage verwendeten Parameternamen.  
  
-   Analysieren einer Abfrage und Zurückgeben einer Liste von Feldern, nach der die Abfrage gruppiert wird.  
  
-   Analysieren einer Abfrage und Zurückgeben einer Liste von Feldern, nach der die Abfrage sortiert wird.  
  
-   Angabe eines Benutzernamens und Kennworts für die Verbindung mit der Datenquelle, die unabhängig von der Verbindungszeichenfolge ist.  
  
-   Iteration durch die Zeilen im Rowset und Abrufen der erweiterten Metadaten zu diesen Datenwerten.  
  
-   Aggregieren der Daten im Server.  
  
## <a name="available-extension-interfaces"></a>Verfügbare Erweiterungsschnittstellen  
 In der folgenden Tabelle werden die verfügbaren Schnittstellen beschrieben. Außerdem wird angegeben, ob die Implementierung erforderlich oder optional ist.  
  
|Schnittstelle|Description|Implementierung|  
|---------------|-----------------|--------------------|  
|IDbConnection|Stellt eine eindeutige Sitzung mit einer Datenquelle dar. Bei Client-/Server-Datenbanksystemen kann die Sitzung einer Netzwerkverbindung zum Server entsprechen.|Erforderlich|  
|IDbConnectionExtension|Stellt zusätzliche Verbindungseigenschaften dar, die von den [!INCLUDE[ssRS](../../../includes/ssrs-md.md)]-Datenverarbeitungserweiterungen für die Sicherheit und Authentifizierung implementiert werden können.|Optional|  
|IDbTransaction|Stellt eine lokale Transaktion dar.|Erforderlich|  
|IDbTransactionExtension|Stellt zusätzliche Transaktionseigenschaften dar, die von den [!INCLUDE[ssRS](../../../includes/ssrs-md.md)]-Datenverarbeitungserweiterungen für die Sicherheit und Authentifizierung implementiert werden können.|Optional|  
|IDbCommand|Stellt eine Abfrage oder einen Befehl dar, der beim Herstellen einer Verbindung zu einer Datenquelle verwendet wird.|Erforderlich|  
|IDbCommandAnalysis|Stellt weitere Befehlinformationen für die Analyse einer Abfrage und die Rückgabe einer Liste von Parameternamen dar, die in der Abfrage verwendet werden.|Optional|  
|IDataParameter|Stellt einen Parameter oder ein Name/Wert-Paar dar, das an einen Befehl oder eine Abfrage übergeben wird.|Erforderlich|  
|IDataParameterCollection|Stellt eine Auflistung aller Parameter dar, die für einen Befehl oder eine Abfrage relevant sind.|Erforderlich|  
|IDataReader|Stellt eine Methode zum Lesen eines schreibgeschützten Vorwärtsdatenstroms von der Datenquelle dar.|Erforderlich|  
|IDataReaderExtension|Stellt eine Methode zum Lesen eines oder mehrerer Vorwärtsströme von Resultsets dar, die durch Ausführen eines Befehls an einer Datenquelle abgerufen wurden. Diese Schnittstelle stellt zusätzliche Unterstützung für Feldaggregate bereit.|Optional|  
|IExtension|Stellt die Basisklasse für eine [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Datenverarbeitungserweiterung dar. Ermöglicht es dem Implementierenden außerdem, einen lokalisierten Namen für die Erweiterung anzugeben und die Konfigurationseinstellungen von der Konfigurationsdatei zur Erweiterung zu übergeben.|Erforderlich|  
  
 Die Schnittstellen der Datenverarbeitungserweiterung sind identisch mit einer Teilmenge der [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-Datenanbieterschnittstellen, -methoden und -eigenschaften, wenn zutreffend. Weitere Informationen zur Implementierung eines vollständigen [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-Datenanbieters finden Sie unter "Implementieren eines .NET Framework-Datenanbieters" in der [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-SDK-Dokumentation (Software Development Kit).  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Erweiterungen](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementing a Data Processing Extension](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
