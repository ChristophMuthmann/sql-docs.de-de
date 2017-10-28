---
title: Wide World Importers-Dokumentation | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 17cabd9d-cb2f-436c-ad9c-ce02225808b7
caps.latest.revision: 3
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 00c70ac3c82cc5a2e21a687a21c51739b75909ef
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="wide-world-importers-documentation"></a>Wide World Importers-Dokumentation
Wide World Importers ist der neuen Beispieldatenbank für SQL Server 2016 und Azure SQL-Datenbank. Es veranschaulicht die Kernfunktionen von SQL Server 2016 und Azure SQL-Datenbank für Transactional Processing (OLTP), Datawarehousing und Analyse (OLAP)-Arbeitslasten sowie Hybrid-Transaktion und analysearbeitsauslastungen Verarbeitung (HTAP) dar.

## <a name="about-this-sample"></a>Zu diesem Beispiel

Wide World Importers ist eine umfassende Beispieldatenbank aus, die sowohl Datenbankentwurf veranschaulicht, und veranschaulicht, wie SQL Server-Funktionen in einer Anwendung genutzt werden können.

Beachten Sie, dass das Beispiel soll eine normale Datenbank repräsentativ sein. Es umfasst nicht jede Funktion von SQL Server. Der Entwurf der Datenbank entspricht, einen gemeinsamen Satz von Standards, aber es gibt viele Möglichkeiten, eine Datenbank erstellen kann.

**Neueste Version**: [Wide World Importers-Version](http://go.microsoft.com/fwlink/?LinkID=800630)

**Quellcode für das Beispiel**: [Wide-World-Importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers).

**Feedback**: Senden Sie bitte an [ sqlserversamples@microsoft.com ](mailto:sqlserversamples@microsoft.com).

Die Dokumentation des Beispiels ist wie folgt aufgebaut:

## <a name="overview"></a>Übersicht

Übersicht über das Beispielunternehmen Wide World Importers sind und welche Workflows, die im Beispiel adressiert.

## <a name="main-oltp-database-wideworldimporters"></a>Main-OLTP-Datenbank "wideworldimporters"

Anweisungen für die Installation und Konfiguration des Kerns der Datenbank "wideworldimporters", die für Transaction Processing (OLTP - OnLine Transaction Processing) und betriebsanalysen (HTAP - Hybrid transaktional/Analytical Processing) verwendet wird.

Beschreibung des Schemas und Tabellen in der Datenbank "wideworldimporters" verwendet.  

Beschreibt, wie "wideworldimporters" SQL Server-Kernfunktionen nutzt.

Beispielabfragen für die Datenbank "wideworldimporters".

## <a name="data-warehousing-and-analytics-database-wideworldimportersdw"></a>Datawarehousing und Analytics Datenbank WideWorldImportersDW

Anweisungen für die Installation und Konfiguration der OLAP-Datenbank WideWorldImportersDW.

Beschreibung des Schemas und Tabellen in der Datenbank WideWorldImportersDW, in der Beispieldatenbank für Datawarehousing und Analytics Processing (OLAP) verwendet.

Workflow für den Prozess von ETL (extrahieren, transformieren, laden), der Daten aus der transaktionalen Datenbank "wideworldimporters" in das Datawarehouse WideWorldImportersDW migriert.

Beschreibt, wie die WideWorldImportersDW SQL Server-Funktionen für Analysen nutzt.

Beispiel-Analyseabfragen WideWorldImportersDW-Datenbank nutzen.

## <a name="data-generation"></a>Der datengenerierung

Beschreibt, wie zusätzliche Daten in der Beispieldatenbank, z. B. Einfügen von Sales generiert werden, und erwerben von Daten bis zum aktuellen Datum.

