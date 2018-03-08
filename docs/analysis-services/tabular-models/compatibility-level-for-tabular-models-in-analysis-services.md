---
title: "Kompatibilitätsgrad für tabellarische Modelle in Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 10/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.bidtoolset.versioncompat.f1
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 4dcc372bb9eac9887a06923cf517e4375ec1bbcb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Kompatibilitätsgrad für tabellarische Modelle von Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  Die *Kompatibilitätsgrad* bezieht sich auf die Release-spezifischen Verhalten in der Analysis Services-Modul. Beispielsweise verfügen DirectQuery und tabellarische Objektmetadaten verschiedene Implementierungen abhängig von den Kompatibilitätsgrad. Im Allgemeinen sollten Sie die neuesten Kompatibilitätsgrad von Ihren Servern unterstützt auswählen.

  **Der aktuelle Kompatibilitätsgrad ist 1400** 
  
Der Kompatibilitätsgrad 1400 Hauptfunktionen sind:

*  Neue Infrastruktur für die datenverbindungen und Import in tabellarischen Modellen mit Unterstützung für TOM-APIs und TMSL-Skripts. Dies ermöglicht die Unterstützung für zusätzliche Datenquellen wie z. B. Azure Blob-Speicher. Zusätzliche Daten von Quellen werden werden in zukünftigen Updates enthalten.
*  Datentransformation und Funktionen für die Mashups mit Daten abrufen und M-Ausdrücken.
*  Measures unterstützen jetzt eine Eigenschaft Detailzeilen mit einem DAX-Ausdruck, und Aktivieren von BI-Tools wie Microsoft Excel Drilldown zu detaillierten Daten aus einem aggregierten Bericht. Wenn Endbenutzer den Gesamtumsatz für eine Region und Monat anzeigen, können sie die zugehörigen Auftragsdetails anzeigen. 
*  Objektebene Sicherheit für Tabellen- und Spaltennamen, zusätzlich zu den darin enthaltenen Daten.
*  Verbesserte Unterstützung für unregelmäßige Hierarchien.
*  Leistung und Überwachung von Verbesserungen.

  
## <a name="supported-compatibility-levels-by-version"></a>Unterstützte Kompatibilitätsgrade nach version
  
|||  
|-|-|- 
|**Kompatibilitätsgrad**|**Serverversion**| 
|1400|Azure Analysis Services, SqlServer 2017 |  
|1200|Azure Analysis Services, SqlServer 2017 SQLServer 2016| 
|1103|SQLServer 2017 *, SqlServer 2016, SqlServer 2014, SQL Server 2012 SP1|  
|1100|SQLServer 2017 *, SqlServer 2016, SqlServer 2014, SQL Server 2012 SP1, SqlServer 2012| 

\*1100 und 1103 Kompatibilitätsgrade sind in SQL Server-2017 veraltet.
  
## <a name="set-compatibility-level"></a>Set-Kompatibilitätsgrad 
 Wenn Sie ein neues Projekt für tabellarische Modelle in SQL Server Data Tools (SSDT) erstellen, können Sie den Kompatibilitätsgrad angeben, auf die **Designer für tabellarische Modelle** Dialogfeld. 
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.png)  
  
 Bei Auswahl der **diese Meldung nicht mehr anzeigen** Option bei allen nachfolgende Projekten werden den Kompatibilitätsgrad, die Sie als Standard angegebene verwenden. Sie können den Standardkompatibilitätsgrad in SSDT unter **Tools** > **Optionen**ändern.  
  
 Um ein Projekt für tabellarische Modelle in SSDT aktualisieren möchten, legen Sie die **Kompatibilitätsgrad** Eigenschaft im Modell **Eigenschaften** Fenster. Bedenken, Aktualisieren des Kompatibilitätsgrads ist nicht umkehrbar.
  
## <a name="check-compatibility-level-for-a-database-in-ssms"></a>Überprüfen des Kompatibilitätsgrads einer Datenbank in SSMS  
 In SSMS mit der Maustaste des Datenbanknamens > **Eigenschaften** > **Kompatibilitätsgrad**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Überprüfen des unterstützten Kompatibilitätsgrads für einen Server in SSMS  
 Klicken Sie in SSMS mit der rechten Maustaste auf den Servernamen > **Eigenschaften** > **Unterstützter Kompatibilitätsgrad**.  
  
 Diese Eigenschaft gibt den höchsten Kompatibilitätsgrad einer Datenbank, die auf dem Server ausgeführt wird. Der unterstützte Kompatibilitätsgrad ist schreibgeschützt und kann nicht geändert werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Kompatibilitätsgrad einer mehrdimensionalen Datenbank](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Neuigkeiten in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Erstellen eines neuen tabellenmodellprojekts](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  
