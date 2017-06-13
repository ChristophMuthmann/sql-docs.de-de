---
title: "Implementieren einer DataReader-Klasse für eine Datenverarbeitungserweiterung | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
- data processing extensions [Reporting Services], data readers
- data readers [Reporting Services]
- DataReader class
- read-only data
ms.assetid: 23e286e7-6074-4fbe-be29-203420d6c3d0
caps.latest.revision: 35
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: fb0f4c2f3ea3137f2e614e688aa5e3823a043e50
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="implementing-a-datareader-class-for-a-data-processing-extension"></a>Implementieren einer DataReader-Klasse für Datenverarbeitungserweiterungen
  Die **DataReader** Objekt kann ein Client einen schreibgeschützten, nur vorwärts-Datenstrom aus einer Datenquelle abzurufen. Ergebnisse werden zurückgegeben, da die Abfrage ausgeführt wird und im Netzwerkpuffer auf dem Client gespeichert, bis Sie sie anfordern mithilfe der **lesen** Methode der **DataReader** Klasse. Zum Erstellen einer **DataReader** -Klasse, implementieren Sie <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> und optional implementieren <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension>. Mit einem **DataReader** Objekt erhöht die Anwendungsleistung durch das Abrufen von Daten wird so bald wie es ist verfügbar, anstatt die gesamten Ergebnisse der Abfrage, und da (standardmäßig) immer nur eine Zeile zu einem Zeitpunkt im Arbeitsspeicher, wodurch der systemmehraufwand werden gewartet.  
  
 Nach dem Erstellen einer Instanz von Ihr **Befehl** -Klasse, die Sie erstellen eine **DataReader** Objekt durch Aufrufen von **Command.ExecuteReader** zum Abrufen von Zeilen aus der Datenquelle. Die **DataReader** Implementierung muss zwei grundlegende Funktionen bereitstellen: Vorwärtszugriff auf die Resultsets abgerufen durch Ausführen von einem Befehl und den Zugriff auf die Spaltentypen, Namen, und Werte innerhalb jeder Zeile. Clients verwenden die **lesen** Methode der **DataReader** Objekt um eine Zeile aus den Ergebnissen der Abfrage abzurufen.  
  
 Im Berichts-Designer Ihre **DataReader** Objekt wird verwendet, um eine Liste der Felder sowie Schemainformationen über das Resultset abzurufen. Dies erfolgt durch Implementierung der **GetName**, **GetValue**, **GetFieldType** und **GetOrdinal** Methoden die <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> Schnittstelle.  
  
 Mit der <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension>-Schnittstelle können Sie bestimmte Aggregationsinformationen über das Resultset angeben. Ein Beispiel **DataReader** -klassenimplementierung, finden Sie unter [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Erweiterungen](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementing a Data Processing Extension](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
