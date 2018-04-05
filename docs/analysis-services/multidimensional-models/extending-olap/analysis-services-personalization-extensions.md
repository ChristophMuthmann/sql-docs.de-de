---
title: Personalisierungserweiterungen für Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- personalization extensions [Multidimensional Databases]
ms.assetid: 0f144059-24e0-40c0-bde4-d48c75e46598
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bd55cabe877554254b63ba31e80a504117d2cf36
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="analysis-services-personalization-extensions"></a>Personalisierungserweiterungen für Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] personalisierungserweiterungen sind die Grundlage für das Konzept der Implementierung einer Plug-in-Architektur. In einer Plug-In-Architektur können Sie neue Cubeobjekte und -funktionalitäten dynamisch entwickeln und problemlos für andere Entwickler freigeben. Daher [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] personalisierungserweiterungen bieten die Funktionen, die mit der Folgendes erreicht werden können:  
  
-   **Dynamischer Entwurf und Bereitstellung** unmittelbar nach dem Entwerfen und Bereitstellen von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] personalisierungserweiterungen, haben Benutzer am Anfang der nächsten benutzersitzung Zugriff auf die Objekte und Funktionen.  
  
-   **Schnittstellenunabhängigkeit** unabhängig von der Schnittstelle, mit denen Sie erstellen die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] personalisierungserweiterungen, Benutzer können eine beliebige Schnittstelle auf die Objekte und Funktionen zugreifen.  
  
-   **Sitzungskontext** [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -personalisierungserweiterungen sind keine permanenten Objekte in der vorhandenen Infrastruktur und erfordern keine den Cube erneut verarbeitet werden. Sie werden zu dem Zeitpunkt für den Benutzer erstellt und verfügbar gemacht, an dem der Benutzer eine Verbindung mit der Datenbank herstellt, und bleiben für die Dauer dieser Benutzersitzung verfügbar.  
  
-   **Schnelle Verteilung** Freigabe [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -personalisierungserweiterungen für andere Softwareentwickler ohne detaillierte Angaben dazu, wo oder wie auf diese erweiterte Funktionalität.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Personalisierungserweiterungen sind vielseitig verwendbar. Zum Beispiel weist das Unternehmen Verkäufe auf, die verschiedene Währungen einschließen. Sie erstellen ein berechnetes Element, das die zusammengefassten Verkäufe in der lokalen Währung der Person zurückgibt, die auf den Cube zugreift. Sie erstellen dieses Element als Personalisierungserweiterung. Sie geben dann dieses berechnete Element für eine Gruppe von Benutzern frei. Nach der Freigabe haben diese Benutzer sofortigen Zugriff auf das berechnete Element, sobald sie eine Verbindung mit dem Server herstellen. Sie haben auch dann Zugriff, wenn sie nicht die gleiche Schnittstelle verwenden, wie die, mit der das berechnete Element erstellt wurde.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-personalisierungserweiterungen sind eine einfache und elegante Änderung der vorhandenen Architektur der verwalteten Assembly und stehen zur Verfügung, während die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] <xref:Microsoft.AnalysisServices.AdomdServer> Objektmodell, Multidimensional Expressions (MDX)-Syntax und-Schemarowsets.  
  
## <a name="logical-architecture"></a>Logische Architektur  
 Die Architektur für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Personalisierungserweiterungen beruht auf der Architektur der verwalteten Assembly und den folgenden vier Grundelementen:  
  
 Das benutzerdefinierte Attribut [PlugInAttribute].  
 Beim Starten des Diensts [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] lädt die erforderlichen Assemblys und bestimmt, welche Klassen verfügen über die <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> benutzerdefinierten Attributs.  
  
> [!NOTE]  
>  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] definiert benutzerdefinierte Attribute als Möglichkeit, den Code zu beschreiben und das Laufzeitverhalten zu beeinflussen. Weitere Informationen finden Sie im Thema "[Übersicht über Attribute](http://go.microsoft.com/fwlink/?LinkId=82929)," in der [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Developer's Guide auf MSDN.  
  
 Für alle Klassen, mit der <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> benutzerdefiniertes Attribut [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Standardkonstruktoren aufruft. Das Aufrufen aller Konstruktoren beim Start bietet einen gebräuchlichen Ort zum Erstellen neuer Objekte von und von Benutzeraktivitäten unabhängig ist.  
  
 Zusätzlich zum Erstellen eines kleinen Informationscaches über das Erstellen und Verwalten von Personalisierungserweiterungen abonniert der Klassenkonstruktor typischerweise die Ereignisse <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened> und <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing>. Wenn kein Abonnement für diese Ereignisse eingerichtet wird, werden die Klassen möglicherweise ungewollt vom Garbage Collector der Common Language Runtime (CLR) für den Cleanup markiert.  
  
 Sitzungskontext  
 Für Objekte, die auf Personalisierungserweiterungen basieren, erstellt [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] während der Clientsitzung eine Ausführungsumgebung und erstellt die meisten dieser Objekte dynamisch in dieser Umgebung. Wie alle anderen CLR-Assemblys hat diese Ausführungsumgebung auch Zugriff auf andere Funktionen und gespeicherte Prozeduren. Wenn der benutzersitzung [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] dynamisch erstellten Objekte entfernt, und schließt die ausführungsumgebung bereitstellt.  
  
 Ereignisse  
 Objekterstellung wird durch die Ereignisse der Sitzung ausgelöst **Cube-OpenedCubeOpened** und **Cube-ClosingCubeClosing**.  
  
 Die Kommunikation zwischen dem Client und dem Server kommt nur durch bestimmte Ereignisse zustande. Durch diese Ereignisse wird der Client auf die Situationen aufmerksam gemacht, die zur Erstellung der Clientobjekte führen. Die Umgebung des Clients wird dynamisch mit zwei Sätzen von Ereignissen erstellt: Sitzungsereignisse und Cubeereignisse.  
  
 Dem Serverobjekt werden Sitzungsereignisse zugeordnet. Wenn ein Client, der einem Server anmeldet [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] erstellt eine Sitzung und löst die <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened> Ereignis. Wenn ein Client die Sitzung auf dem Server beendet [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Trigger die <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing> Ereignis.  
  
 Dem Verbindungsobjekt werden Cubeereignisse zugeordnet. Das Herstellen einer Verbindung mit einem Cube löst das <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeOpened>-Ereignis aus. Das Beenden der Verbindung mit einem Cube, durch Schließen des Cubes oder durch Wechsel zu einem anderen Cube, löst ein <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeClosing>-Ereignis aus.  
  
 Nachweisbarkeit und Fehlerbehandlung  
 Alle Aktivitäten sind mit [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] nachweisbar. Unbehandelte Fehler werden dem Windows-Ereignisprotokoll berichtet.  
  
 Die gesamte Objekterstellung und -verwaltung ist von dieser Architektur unabhängig, und einzig die Entwickler dieser Objekte tragen die Verantwortung dafür.  
  
## <a name="infrastructure-foundations"></a>Infrastrukturgrundlagen  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Personalisierungserweiterungen basieren auf vorhandenen Komponenten. Nachfolgend finden Sie eine Zusammenfassung der Erweiterungen und Verbesserungen, die von der Funktionalität der Personalisierungserweiterungen bereitgestellt werden.  
  
### <a name="assemblies"></a>Assemblys  
 Das benutzerdefinierte Attribut <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> kann Ihren benutzerdefinierten Assemblys hinzugefügt werden, um die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Personalisierungserweiterungsklassen zu identifizieren.  
  
### <a name="changes-to-the-adomdserver-object-model"></a>Änderungen gegenüber dem AdomdServer-Objektmodell  
 Die folgenden Objekte im <xref:Microsoft.AnalysisServices.AdomdServer>-Objektmodell wurden verbessert oder dem Modell hinzugefügt.  
  
#### <a name="new-adomdconnection-class"></a>Neue AdomdConnection-Klasse  
 Die <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection>-Klasse ist neu und macht mehrere Personalisierungserweiterungen durch sowohl Eigenschaften als auch Ereignisse verfügbar.  
  
 **Eigenschaften**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.SessionID%2A>, ein schreibgeschützter Zeichenfolgenwert, der die Sitzungs-ID der aktuellen Verbindung darstellt.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.ClientCulture%2A>, ein schreibgeschützter Verweis auf die der aktuellen Sitzung zugeordnete Clientkultur.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.User%2A>, ein schreibgeschützter Verweis auf die dem aktuellen Benutzer zugeordnete Identitätsschnittstelle.  
  
 **Ereignisse**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeOpened>  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeClosing>  
  
#### <a name="new-properties-in-the-context-class"></a>Neue Eigenschaften in der Kontextklasse  
 Die <xref:Microsoft.AnalysisServices.AdomdServer.Context>-Klasse verfügt über zwei neue Eigenschaften:  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Context.Server%2A>, ein schreibgeschützter Verweis auf das neue Serverobjekt.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentConnection%2A>, ein schreibgeschützter Verweis auf das neue <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection>-Objekt.  
  
#### <a name="new-server-class"></a>Neue Serverklasse  
 Die <xref:Microsoft.AnalysisServices.AdomdServer.Server>-Klasse ist neu und macht mehrere Personalisierungserweiterungen durch sowohl Klasseneigenschaften als auch Klassenereignisse verfügbar.  
  
 **Eigenschaften**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.Name%2A>, ein schreibgeschützter Zeichenfolgenwert, der den Servernamen darstellt.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.Culture%2A>, ein schreibgeschützter Verweis auf die dem Server zugeordnete globale Kultur.  
  
 **Ereignisse**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened>  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing>  
  
#### <a name="adomdcommand-class"></a>AdomdCommand-Klasse  
 Die <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand>-Klasse unterstützt jetzt folgende MDX-Befehle:  
  
-   [CREATE MEMBER-Anweisung &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-member.md)  
  
-   [UPDATE MEMBER-Anweisung &#40; MDX &#41;](../../../mdx/mdx-data-definition-update-member.md)  
  
-   [DROP MEMBER-Anweisung &#40; MDX &#41;](../../../mdx/mdx-data-definition-drop-member.md)  
  
-   [CREATE SET-Anweisung &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-set.md)  
  
-   [DROP SET-Anweisung &#40; MDX &#41;](../../../mdx/mdx-data-definition-drop-set.md)  
  
-   [Erstellen Sie die KPI-Anweisung &#40; MDX &#41;](../../../mdx/mdx-data-definition-create-kpi.md)  
  
-   [DROP KPI-Anweisung &#40; MDX &#41;](../../../mdx/mdx-data-definition-drop-kpi.md)  
  
### <a name="mdx-extensions-and-enhancements"></a>MDX-Erweiterungen und -Verbesserungen  
 Der Befehl CREATE MEMBER wurde durch verbessert die **Beschriftung** -Eigenschaft, die **Display_folder** -Eigenschaft, und die **Associated_measure_group** Eigenschaft.  
  
 Der Befehl UPDATE MEMBER wurde hinzugefügt, um die Neuerstellung eines Elements zu verhindern, wenn ein Update erforderlich ist, aus dem ein Verlust der Lösungsreihenfolge für die Berechnungen erfolgt. Updates können nicht den Bereich des berechneten Elements ändern, verschieben Sie das berechnete Element zu einem anderen übergeordneten Element, oder definieren ein anderes **Solveorder**.  
  
 Der Befehl CREATE SET wird verbessert, mit der **Beschriftung** -Eigenschaft, die **Display_folder** -Eigenschaft, und die neuen **statische | DYNAMISCHE** Schlüsselwort. *Statische* bedeutet, dass der Satz nur zur Erstellungszeit ausgewertet wird. *Dynamische* bedeutet, dass der Satz jedes Mal ausgewertet wird, das der Satz in einer Abfrage verwendet wird. Der Standardwert ist **statische** , wenn ein Schlüsselwort ausgelassen wird.  
  
 Die Befehle CREATE KPI und DROP KPI werden der MDX-Syntax hinzugefügt. KPIs können dynamisch aus einem beliebigen MDX-Skript erstellt werden.  
  
### <a name="schema-rowsets-extensions"></a>Schemarowset-Erweiterungen  
 MDSCHEMA_MEMBERS *Bereich* Spalte hinzugefügt wird. Die Bereichswerte lauten wie folgt: MDMEMBER_SCOPE_GLOBAL=1, MDMEMBER_SCOPE_SESSION=2.  
  
 Mdschema_sets *Set_evaluation_context* Spalte hinzugefügt wird. Die Satzauswertungs-Kontextwerte lauten wie folgt: MDSET_RESOLUTION_STATIC = 1, MDSET_RESOLUTION_DYNAMIC = 2.  
  
 MDSCHEMA_KPIS wird eine scope-Spalte hinzugefügt. Die Bereichswerte lauten wie folgt: MDKPI_SCOPE_GLOBAL=1, MDKPI_SCOPE_SESSION=2.  
  
  
