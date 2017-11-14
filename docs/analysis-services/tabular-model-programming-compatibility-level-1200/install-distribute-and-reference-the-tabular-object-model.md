---
title: Installieren, verteilen und verweisen auf die tabellarischen Objektmodell | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e51769f7-aac7-4835-a5ae-91aac04aa476
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9688a692d25d484b05bca88e0779d2812944f3af
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="install-distribute-and-reference-the-tabular-object-model"></a>Installieren, verteilen und verweisen auf die tabellarischen Objektmodell

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

In diesem Artikel erläutert, wie herunterladen, verweisen und Verteilen von Analysis Services Tabular Objekt Model (TOM), eine c#-Klassenbibliothek zum Erstellen und verwalten tabellarische Modelle und Datenbanken in verwaltetem Code.  
  
PETER ist eine Erweiterung der AMO-Clientbibliothek (Microsoft.AnalysisServices.dll), die mit SQL Server 2016 geliefert wird. Es funktioniert mit tabellarischen Modellen, die in der SQL Server 2016-Version der tabellarischen metadatenmoduls abzielt. Um TOM verwenden zu können, müssen das Modell und die Datenbank mit dem Kompatibilitätsgrad 1200 oder höher sein.  

## <a name="amo-tom-assemblies"></a>AMO-TOM Assemblys

SQL Server 2016 umgestaltet und erweitert AMO, um neue Core, tabellarisch und JSON-Assemblys enthalten. Darüber hinaus die ursprüngliche AMO-Assembly Microsoft.AnalysisServices.dll, die Teil von Analysis Services seit der ersten Veröffentlichung wurde. Ein neu strukturierte AMO allgemeine Klassen auf eine Assembly, ab und stellt eine logische Unterteilung zwischen tabellarischen und mehrdimensionalen APIs über zusätzliche Assemblys. 

Die folgende Tabelle beschreibt jede Assembly.
  
Assembly  |Funktionalität  |Wichtige Klassen |
---------|---------|--------------  |
Core <br/>Microsoft.AnalysisServices.Core.dll | Tabellarische und mehrdimensionale Datenbanken, die gemeinsam sind. <br/><br/>Stellt eine Ausnahmebehandlung, generischen Verbindungen mit einer Analysis Services-Instanz und-Datenbank und den Zugriff auf Allgemeine Eigenschaften und Methoden für die Server- und Datenbankobjekten bereit. <br/><br/>Es wurde für alle AMO-Lösung, die für SQL Server 2016 erforderlich. | Core&nbsp;Server<br/>Core&nbsp;Datenbank<br/>AmoException
PETER<br/> Microsoft.AnalysisServices.Tabular.dll, Version 13.0.1601.5 oder höher.| Erstellen Sie und verwalten Sie tabellarische Metadatenobjekte. | TOM&nbsp;Server <br/>TOM&nbsp;Datenbank<br /> Model<br /> Tabelle<br /> Column<br /> Beziehung
  AMO<br /> Microsoft.AnalysisServices.dll| Erstellen und Verwalten von mehrdimensionalen Servermetadaten-Objekten, einschließlich tabellarischer 1050-1103-Datenbanken. | AMO&nbsp;Server <br />AMO&nbsp;Datenbank <br /> Cube <br /> Dimension <br /> Measuregruppe 
JSON<br/>Microsoft.AnalysisServices.Tabular.Json.dll | Ein Hilfsprogramm-DLL, die zum Steuern von Updates, die NewtonSoftJson.dll (JSON.NET) dient als Wrapper für das Risiko, dass der einführen von funktionalen Änderungen in JSON-Serialisierung in Analysis Services-arbeitsauslastungen. <br /> <br />Diese DLL ist als eine Abhängigkeit in TOM vorhanden und sollte nicht direkt im Code verwendet werden. | Keine.  
  
 ### <a name="understanding-assembly-dependencies"></a>Grundlegendes zu Assemblyabhängigkeiten
  
Zum Programmieren von AMO, muss die Projektmappe Verweise auf abhängige DLLs enthalten. Sowohl AMO als auch TOM hängen Core, da diese Basisklassen bietet.

AMO hängt TOM, da einige Klassen in AMO Klassen von TOM verweisen. Das AMO-Datenbankobjekt hat beispielsweise eine Eigenschaft Modell des Typs Modell, in der Dll TOM implementiert. 

![AMO TOM Abhängigkeiten](../../analysis-services/tabular-model-programming-compatibility-level-1200/media/amo-tom-dependencies.png)

Sie können nicht ohne Microsoft.AnalysisServices.Tabular.dll Microsoft.AnalysisServices.dll verteilen, jedoch können Sie ihre jeweiligen Namespaces ohne den anderen verweisen.

### <a name="choosing-which-namespace-to-use-in-code"></a>Auswählen der Namespace zur Verwendung in code

In der [-Objekthierarchie](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md) , jedes Objekt unter der Datenbank ist eine tabellarische Metadatenerstellung über das Modellobjekt oder eine Konstruktion mehrdimensionale Metadaten über ein Cube, Dimension oder MeasureGroup-Objekt. Vorgänge auf höherer Ebene, auf der Server-, Datenbank-, Rolle oder Trace-Ebene muss die Wahl, welche Namespace zum Verweisen auf die arbeitsauslastungen Code richtet sich nach, unterstützen.

* Verwenden Sie Tabular.Server oder Tabular.Database, wenn Ihre Lösung Kompatibilitätsgrad 1200 oder höher ist und das Datenbankobjekt arbeiten Sie mit den Zugriff auf das Modell, Tabelle, Spalten und anderen Objekten wie tabellarischen Metadaten Konstruktionen ausgedrückt ermöglichen muss.
* Verwenden Sie AnalysisServices.Server oder AnalysisServices.Database aus, wenn downstreamer-Code verweisen auf mehrdimensionale Objekte wie Cubes, Datenquellen, DataSourceViews und Dimensionen.

Sie benötigen beide Namespaces für Tools und Anwendungen, die eine Mischung aus Datenbanken und Modelltypen unterstützen. 

Verweisen auf die Core-Namespace in Ihrem Code ist nicht erforderlich. die Klassen im Kern sind Basisklassen, die zum Bereitstellen von allgemeine Eigenschaften wie Name und Beschreibung für die wichtigsten Objekte erstellt.  
  
## <a name="determine-whether-amo-and-tom-installation-is-required"></a>Bestimmen Sie, ob AMO und TOM Installation erforderlich ist.  
   
 AMO und TOM sind in einer einzelnen Client-Bibliothek gebündelt. Wenn Sie eine SQL Server 2016 Analysis Services-Instanz, die Clientbibliotheken oder eine Version von SQL Server Data Tools, die auf eine SQL Server 2016-Instanz bereits installiert, ist die Microsoft.AnalysisServices.dll bereits installiert.  
  
 Um zu bestimmen, ob die Assemblys bereits installiert sind, überprüfen Sie jedem dieser Speicherorte:
* C:\WINDOWS\Microsoft.NET\assembly\GAC_MSIL
* C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies
* C:\Program Files\Microsoft SQL Server\130\DTS\Tasks
* C:\Program Files\Microsoft SQL Server\MSAS13. MSSQLSERVER\OLAP\bin
 
 Stellen Sie sicher, dass die folgenden Assemblys vorhanden sind:
*  Microsoft.AnalysisServices.Core.dll
*  Microsoft.AnalysisServices.dll
*  Microsoft.AnalysisServices.Tabular.dll
*  Microsoft.AnalysisServices.Tabular.Json.dll   
   
## <a name="download-sqlasamo"></a>SQL_AS_AMO herunterladen  
 
 Beachten Sie, dass die Microsoft.AnalysisServices.dll nicht über NuGet-Manager verfügbar ist.
  
1. Wechseln Sie zu [Downloadseite von SQL Server 2016 Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).  
  
2. Klicken Sie auf **Herunterladen**.  
  
3. Wählen Sie entweder **\X64\SQL_AS_AMO.msi** oder **\X86\SQL_AS_AMO.msi**. Sie können wählen Sie entweder eine: AMO und TOM Assemblys sind plattformunabhängiges.
  
4. Klicken Sie auf **Weiter** mit dem Download zu fortfahren. Sie finden die MSI-Dateien in Ihrem **Downloads** Ordner.  
  
## <a name="install-sqlasamo"></a>Installieren von SQL_AS_AMO  
  
1. Doppelklicken Sie auf **SQL_AS_AMO.msi** und die Installation zu durchlaufen.  
  
2. Wechseln Sie zu **C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies** , bestätigen die Platzierung von "Microsoft.AnalysisServices.Core.dll", Microsoft.AnalysisServices.dll, Microsoft.AnalysisServices.Tabular.dll, und Microsoft.AnalysisServices.Tabular.Json.dll.   
  
## <a name="add-references"></a>Fügen Sie Verweise hinzu  
  
1. In **Projektmappen-Explorer** > **Verweis hinzufügen** > **Durchsuchen**.  
2. Wechseln Sie zu **C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies** , und wählen Sie:  
   * "Microsoft.AnalysisServices.Core"  
   * Microsoft.AnalysisServices.Tabular  
   * Microsoft.AnalysisSerivces.Tabular.Json  
  
3. Klicken Sie auf **OK**.  In **Projektmappen-Explorer**, vergewissern Sie sich die Assemblys im Ordner "Verweise" vorhanden.
  
4. Fügen Sie in der Codepage der Namespace "Microsoft.analysisservces.Tabular" hinzu, wenn Datenbanken und Modelle Tabular 1200 oder höheren Kompatibilitätsgrad sind. 
  
   ```   
   using Microsoft.AnalysisServices; 
   using Microsoft.AnalysisServices.Tabular;
   ```  
    Fügen Sie Microsoft.AnalysisServces, um einen größeren Satz von Verbindungen mit Instanzen von Analysis Services unterstützen, die nicht speziell SQL Server 2016 im tabellarischen Servermodus sind. 
 
    Vermeiden Sie bei Namespaces einschließen, die Klassen für Server, Datenbank, Role und Trace Objekte gemeinsam haben, die mehrdeutige Verweise durch die Qualifizierung der Namespace, die Sie verwenden möchten (z. B. Microsoft.AnalysisServices.Tabular.Server instanziiert einen Server Objekt mithilfe des tabellarischen Namespaces).

## <a name="redistribute-amo-and-tom-with-your-application"></a>Verteilen Sie AMO und TOM mit der Anwendung.  
  
Verteilung von AMO und TOM erfolgt über die **sql_as_amo.msi** Installationspaket. Wenn Sie in AMO oder TOM ein Setupprogramm für eine Clientanwendung, die Aufrufe erstellen, fügen Sie **sql_as_amo.msi** an die ausführbare Datei. Dies ist der einzige unterstützte Mechanismus für das Verteilen von Clientbibliotheken AMO und TOM.  
  
Das Paket ist in sich geschlossen und enthält alle Assemblys, die zum Aufrufen von AMO und TOM in Ihrem Code erforderlich. Andere Pakete, z. B. SQL_AS_OLEDB.msi oder SQL_AS_ADOMD.msi, müssen sich nicht speziell für TOM Programmierszenarien.

