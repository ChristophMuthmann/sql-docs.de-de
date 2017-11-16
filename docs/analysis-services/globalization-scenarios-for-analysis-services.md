---
title: "Globalisierungsszenarien für Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiple language support [Analysis Services]
- languages [Analysis Services]
- SSAS, international considerations
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- SQL Server Analysis Services, international considerations
- Analysis Services, international considerations
ms.assetid: e8af85ff-ef33-4659-a003-bb34578eb2a2
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 23602752bf7a996b66974ce3d5dcf9c8bf6389cd
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="globalization-scenarios-for-analysis-services"></a>Globalisierungsszenarien für Analysis Services
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] speichert und bearbeitet mehrsprachige Daten und Metadaten für tabellarische und mehrdimensionale Datenmodelle. Die Datenspeicherung erfolgt in Unicode (UTF-16) in Zeichensätzen, die Unicode-Codierung verwenden. Wenn Sie ANSI-Daten in ein Datenmodell laden, werden Zeichen mit entsprechenden Unicode-Codepunkten gespeichert.  
  
 Die Auswirkungen der Unicode-Unterstützung sehen so aus, dass [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Daten in allen von den Windows-Client- und -Serverbetriebssystemen unterstützten Sprachen speichern kann, sodass Daten in jedem auf einem Windows-Computer verwendeten Zeichensatz gelesen, geschrieben, sortiert und verglichen werden können. BI-Clientanwendungen, die [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Daten nutzen, können Daten in der vom Benutzer gewünschten Sprache darstellen, vorausgesetzt, die Daten sind in der jeweiligen Sprache im Modell vorhanden.  
  
 Sprachunterstützung kann für verschiedene Benutzer unterschiedliche Bedeutungen haben. In der folgenden Liste werden einige häufig gestellte Fragen im Zusammenhang mit der Sprachunterstützung in Analysis Services behandelt.  
  
-   Daten werden, wie erwähnt, in einem beliebigen, in einem Windows-Clientbetriebssystem vorhandenen Unicode-codierten Zeichensatz gespeichert.  
  
-   Metadaten, z. B. Objektnamen, können übersetzt werden. Zwar variiert die Unterstützung je nach Modelltyp, jedoch unterstützen sowohl mehrdimensionale als auch tabellarische Modelle das Hinzufügen von übersetzten Zeichenfolgen innerhalb des Modells. Sie können mehrere Übersetzungen definieren und dann einen Gebietsschemabezeichner verwenden, um zu bestimmen, welche Übersetzung an den Client zurückgegeben wird. Weitere Informationen finden Sie unten unter [Features](#bkmk_features) .  
  
-   Fehler-, Warn- und Informationsmeldungen, die vom [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Modul (msmdsrv) zurückgegeben werden, werden in die 43 von Office und Office 365 unterstützten Sprachen lokalisiert. Es ist keine Konfiguration erforderlich, um Meldungen in einer bestimmten Sprache abzurufen. Das Gebietsschema der Clientanwendung bestimmt, welche Zeichenfolgen zurückgegeben werden.  
  
-   Die Konfigurationsdatei (msmdsrv.ini) und AMO PowerShell sind nur in Englisch verfügbar.  
  
-   Protokolldateien enthalten eine Mischung aus englischen und lokalisierten Meldungen, vorausgesetzt, Sie haben auf dem Windows-Server, auf dem Analysis Services ausgeführt wird, ein Language Pack installiert.  
  
-   Dokumentation und Tools, wie etwa [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] und [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], wurden in diese Sprachen übersetzt: Chinesisch vereinfacht, Chinesisch traditionell, Französisch, Deutsch, Italienisch, Japanisch, Koreanisch, Portugiesisch (Brasilien), Russisch und Spanisch. Die Kultur wird bei der Installation angegeben.  
  
 Sie können in Analysis Services für mehrsprachige Modelle Sprache, Sortierung und Übersetzungen unabhängig voneinander in der gesamten Objekthierarchie festlegen.  Für tabellarische Modelle können nur Übersetzungen hinzugefügt werden: Sprache und Sortierung werden vom Hostbetriebssystem geerbt.  
  
 Die Globalisierungsfeatures von Analysis Services ermöglichen z. B. die folgenden Szenarien:  
  
-   Ein Datenmodell bietet mehrere übersetzte Beschriftungen, sodass Feldnamen und Werte in der Sprache des Benutzers angezeigt werden. Für Unternehmen, die in zweisprachigen Ländern wie Kanada, Belgien oder der Schweiz agieren, ist die Unterstützung mehrerer Sprachen über Client- und Serveranwendungen hinweg eine Standardcodierungsanforderung. Dieses Szenario wird durch Übersetzungen und Währungsumrechnungen ermöglicht. Weitere Informationen und Links finden Sie unten unter [Features](#bkmk_features) .  
  
-   Entwicklungs- und Produktionsumgebungen befinden sich geografisch in verschiedenen Ländern. Es geschieht immer häufiger, dass eine Lösung in einem Land entwickelt und in einem anderen bereitgestellt wird. Zu wissen, wie Sprach- und Sortierungseigenschaften festgelegt werden, ist sehr wichtig, wenn Sie die Aufgabe erhalten, eine in einer Sprache entwickelte Lösung für die Bereitstellung auf einem Server vorzubereiten, der ein anderes Sprachpaket verwendet. Durch Festlegen dieser Eigenschaften können Sie die geerbten Standardeinstellungen überschreiben, die Sie vom ursprünglichen Hostsystem erhalten. Weitere Informationen finden Sie unten unter [Sprachen und Sortierungen &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md) .  
  
##  <a name="bkmk_features"></a> Features für die Erstellung einer globalisierten mehrsprachigen Lösung  
 Auf der Clientebene können globalisierte Anwendungen, die mehrdimensionale [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Daten verwenden oder bearbeiten, die mehrsprachigen und multikulturellen Features in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]verwenden.  
  
 Rufen Sie Daten und Metadaten von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Objekten ab, in denen Übersetzungen automatisch definiert wurden, indem Sie einen Gebietsschemabezeichner beim Herstellen der Verbindung mit einer [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Instanz angeben.  
  
 In [Tipps und Best Practices für die Globalisierung &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) finden Sie Informationen zu den Entwurfs- und Codierungsmethoden, mit denen Sie Probleme im Zusammenhang mit mehrsprachigen Daten vermeiden können.  
  
||||  
|-|-|-|  
|**Funktion**|**Tabellarisch**|**Multidimensional**|  
|[Sprachen und Sortierungen &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md)|Vom Betriebssystem geerbt.|Geerbt, jedoch mit der Möglichkeit, Sprache und Sortierung für die wichtigsten Objekte in der Modellhierarchie zu überschreiben.|  
|Umfang der Übersetzungsunterstützung|Beschriftungen und Beschreibungen.|Übersetzungen können für Objektnamen, Beschriftungen, Bezeichner und Beschreibungen erstellt werden und können zudem in jeder Unicode-Sprache und jedem Unicode-Skript vorliegen. Dies gilt auch, wenn die Tools und die Umgebung in einer anderen Sprache sind. Beispiel: In einer Entwicklungsumgebung, die die englische Sprache und eine lateinische Sortierung im gesamten Stapel verwendet, können Sie in Ihr Modell ein Objekt einschließen, das kyrillische Zeichen im Namen verwendet.|  
|Implementieren der Übersetzungsunterstützung|Erstellen Sie die Übersetzungen, indem Sie mit [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] Übersetzungsdateien generieren, die Sie ausfüllen und dann zurück in das Modell importieren.<br /><br /> Einzelheiten finden Sie unter [Übersetzungen in Tabellenmodellen &#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md).|Erstellen Sie die Übersetzungen, indem Sie mit [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] die Übersetzungen für die Beschriftung, Beschreibung und Kontotypen für Cubes und Measures, Dimensionen und Attribute definieren.<br /><br /> Einzelheiten finden Sie unter [Übersetzungen in mehrdimensionalen Modellen &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md). Eine Lektion zur Verwendung dieser Funktion finden Sie in [Lektion 9: Definieren von Perspektiven und Übersetzungen](../analysis-services/lesson-9-defining-perspectives-and-translations.md) im Tutorial [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|  
|Währungsumrechnung|Nicht verfügbar.|Die Währungsumrechnung erfolgt über spezielle MDX-Skripts, die Measures mit Währungsdaten konvertieren. Sie können den Business Intelligence-Assistenten in [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] verwenden, um ein MDX-Skript zu generieren, das eine Kombination aus Daten und Metadaten aus Dimensionen, Attributen und Measuregruppen verwendet, um Measures mit Währungsdaten zu konvertieren. Siehe [Währungsumrechnungen &#40;Analysis Services&#41;](../analysis-services/currency-conversions-analysis-services.md).|  
  
## <a name="see-also"></a>Siehe auch  
 [Unterstützung für Übersetzungen in Analysis Services](../analysis-services/translation-support-in-analysis-services.md)   
 [Internationalisierung für Windows-Anwendungen](http://msdn.microsoft.com/library/windows/desktop/dd318661%28v=vs.85%29.aspx)   
 [Go Global-Entwicklercenter](http://msdn.microsoft.com/goglobal/bb871628.aspx)   
 [Schreiben von Windows Store-apps mit gebietsschemabasiertem adaptiven design](https://blogs.windows.com/buildingapps/2014/03/06/writing-windows-store-apps-with-locale-based-adaptive-design/)   
 [Entwicklung von universellen Windows-Apps mit c# und XAML](http://www.microsoftvirtualacademy.com/training-courses/developing-universal-windows-apps-with-c-and-xaml)  
  
  

