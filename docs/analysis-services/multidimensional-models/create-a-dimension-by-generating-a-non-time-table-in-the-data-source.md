---
title: Erstellen einer Dimension durch Generieren einer Nichtzeittabelle in der Datenquelle | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [Analysis Services], dimensions without data source
- dimensions [Analysis Services], standard
- dimensions [Analysis Services], creating without data source
- standard dimensions [Analysis Services]
ms.assetid: a37f7a46-7451-4582-ba19-2595196d97bc
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dda2fe632e3a4cae0f36d766d4778f5ff910d649
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="create-a-dimension-by-generating-a-non-time-table-in-the-data-source"></a>Erstellen einer Dimension durch Generieren einer Nichtzeittabelle in der Datenquelle
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]können Sie mit dem Dimensions-Assistenten von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] eine Dimension ohne vorhandene Datenquelle erstellen. Hierzu wählen Sie auf der Seite **Erstellungsmethode auswählen** des Assistenten die Option **Nichtzeittabelle in der Datenquelle generieren** aus. Um in der zugrunde liegenden Datenquelle eine neue Dimensionstabelle zu erstellen, müssen Sie über die Berechtigung zum Erstellen von Objekten in der zugrunde liegenden Datenquelle verfügen. Wenn Sie eine Dimension ohne vorab definierte Datenquellensicht definieren, können Sie entweder eine vollständig neue Dimension definieren oder eine Dimensionsvorlage verwenden.  
  
 Im Dimensions-Assistenten werden Dimensionsvorlagen bereitgestellt, die Sie als Grundlage für verschiedene gängige Dimensionstypen verwenden können. Sie haben die Wahl zwischen den folgenden Dimensionstypen:  
  
-   Konto  
  
-   Customer  
  
-   Datum  
  
-   Department  
  
-   Destination Currency  
  
-   Employee  
  
-   Geography  
  
-   Internet Sales Order Details  
  
-   Organization  
  
-   Product  
  
-   Promotion  
  
-   Reseller Sales Order Details  
  
-   Reseller  
  
-   Sales Channel  
  
-   Sales Reason  
  
-   Sales Summary Order Details  
  
-   Sales Territory  
  
-   Szenario  
  
-   Source Currency  
  
 Die einzelnen Standardvorlagen unterstützen Attribute, die Sie der Dimension hinzufügen können. Sie können auch eigene Vorlagendateien für Dimensionen hinzufügen, die häufig mit Ihren Daten verwendet werden. Die Dimensionsvorlagen befinden sich im folgenden Ordner:  
  
 `C:\Program Files\Microsoft SQL Server\100\Tools\Templates\olap\1033\Dimension Templates`  
  
 Nach Abschluss des Dimensions-Assistenten können Sie den Dimensions-Designer zum Hinzufügen, Entfernen und Konfigurieren von Attributen und Hierarchien in der Dimension verwenden.  
  
 Wenn Sie eine Nichtzeitdimension ohne eine Datenquelle erstellen, führt Sie der Dimensions-Assistent durch die Schritte zum Angeben des Dimensionstyps und Identifizieren des Schlüsselattributs und langsam veränderlicher Dimensionen.  
  
## <a name="specify-dimension-type"></a>Angeben des Dimensionstyps  
 Auf der Seite **Dimensionstyp angeben** des Dimensions-Assistenten können Sie den Dimensionstyp angeben. Wenn Sie die Dimension auf Basis einer Vorlage erstellen, wird der Dimensionstyp für Sie definiert. Auf dieser Seite können Sie außerdem Standardattribute für den angegebenen Dimensionstyp auswählen, sofern welche verfügbar sind.  
  
 Wenn Sie eine Vorlage ausgewählt haben, die einem Dimensionstyp entspricht, wird diese Seite mit den Optionen für den jeweiligen Dimensionstyp aufgefüllt. Wenn Sie keine Vorlage ausgewählt haben, oder wenn kein entsprechender Dimensionstyp vorhanden ist, ist der Standarddimensionstyp **Regular**. Falls noch kein Dimensionstyp ausgewählt ist, wählen Sie den am besten geeigneten Typ für die von Ihnen erstellte Dimension aus. Falls kein geeigneter Typ für **Dimensionstyp**aufgelistet ist, verwenden Sie **Regular**.  
  
 Wenn Sie einen Dimensionstyp auswählen, werden im Assistenten unter **Dimensionsattribute**die Attributtypen für diese Dimension aufgelistet. Zum Auswählen eines Attributtyps aktivieren Sie das Kontrollkästchen **Einschließen** neben dem Attributtyp, und geben Sie unter **Dimensionsattribut**den Namen für das Attribut ein. Der Standardname entspricht dem **Attributtyp**.  
  
## <a name="identify-key-attribute-and-changing-dimensions"></a>Identifizieren von Schlüsselattributen und veränderlichen Dimensionen  
 Wählen Sie auf der Seite **Dimensionsschlüssel und -typ angeben** das Attribut aus, das Sie als Schlüsselattribut für die Dimension festlegen möchten. Das Schlüsselattribut entspricht normalerweise der Primärschlüsselspalte in der Hauptdimensionstabelle und indiziert die Blattelemente der Dimension.  
  
 Wenn Sie eine Vorlage ausgewählt haben und in der Vorlage ein Schlüsselattribut definiert ist, handelt es sich bei diesem Attribut um das Standardschlüsselattribut. Wenn Sie eine Vorlage ausgewählt haben, aber in der Vorlage kein Schlüsselattribut definiert ist, wird das erste Attribut als Standardschlüsselattribut verwendet. Die Liste enthält alle Attribute, die Sie auf der Seite **Dimensionstyp angeben** ausgewählt haben. Sie können jedes der Attribute, die Sie auf der Seite **Dimensionstyp angeben** ausgewählt haben, als Schlüsselattribut festlegen. Falls Sie keine Attribute ausgewählt haben, erstellt der Assistent automatisch ein Schlüsselattribut und benennt es, indem er den Dimensionsnamen und "ID" verkettet.  
  
 Geben Sie schließlich an, ob es sich bei dieser Dimension um eine veränderliche Dimension handelt. Elemente in einer veränderlichen Dimension werden im Laufe der Zeit an andere Positionen in der Hierarchie verschoben. Der Assistent generiert zusätzliche Spalten und erstellt Attribute, die diesen Spalten entsprechen. Anhand dieser Spalten können Benutzer die Dimension so abfragen, dass die Änderung berücksichtigt wird. Sämtliche Pakete, die Sie anschließend mit dem Schemagenerierungs-Assistenten erstellen, verwalten Ersatzschlüssel auf der Basis der Eigenschaften langsam veränderlicher Dimensionen für die Dimension.  
  
 Wenn Sie das Kontrollkästchen **Dies ist eine veränderliche Dimension** aktivieren, definiert der Dimensions-Assistent die in der folgenden Tabelle aufgeführten Attribute:  
  
|Attribut|Typ|  
|---------------|----------|  
|SCD-Original-ID|SCDOriginalID|  
|SCD-Enddatum|SCDEndDate|  
|SCD-Startdatum|SCDStartDate|  
|SCD-Status|SCDStatus|  
  
 Das Kontrollkästchen **Dies ist eine veränderliche Dimension** ist standardmäßig aktiviert, wenn Sie eine Vorlage verwenden, für die diese Attribute für langsam veränderliche Dimensionen definiert sind. Wenn Sie das Kontrollkästchen deaktivieren, werden die Attribute für langsam veränderliche Dimensionen aus der Dimension entfernt.  
  
 Sie können die Eigenschaften für eine langsam veränderliche Dimension mithilfe des Dimensions-Designers konfigurieren.  
  
## <a name="completing-the-dimension-wizard"></a>Abschließen des Dimensions-Assistenten  
 Geben Sie auf der Seite **Assistenten abschließen** einen Namen für die neue Dimension ein, und zeigen Sie die Dimensionsstruktur an. Aktivieren Sie das Kontrollkästchen **Schema jetzt generieren** , damit nach dem Klicken auf **Fertig stellen**der Schemagenerierungs-Assistent gestartet wird. In den meisten Fällen sollten Sie dieses Kontrollkästchen nicht aktivieren, wenn Sie weitere Objekte erstellen möchten. Wenn Sie dieses Kontrollkästchen nicht aktivieren, können Sie das Schema später mithilfe des Dimensions-Designers generieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer Zeitdimension durch Generieren einer Zeittabelle](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [Erstellen einer Zeitdimension durch Generieren einer Zeittabelle](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)  
  
  
