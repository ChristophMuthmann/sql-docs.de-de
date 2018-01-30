---
title: "Transformation für Suche | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.lookuptrans.f1
- sql13.dts.designer.lookuptransformation.general.f1
- sql13.dts.designer.lookuptransformation.referencetable.f1
- sql13.dts.designer.lookuptransformation.columns.f1
- sql13.dts.designer.lookuptransformation.advanced.f1
helpviewer_keywords:
- Lookup transformation
- joining columns [Integration Services]
- cache [Integration Services]
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: de1cc8de-e7af-4727-b5a5-a1f0a739aa09
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 316fa73c7acd3e66a21ae285217c8ec917c7afbc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="lookup-transformation"></a>Transformation für Suche
  Die Transformation für die Suche führt Suchvorgänge aus, indem Daten in Eingabespalten mit Spalten in einem Verweisdataset verknüpft werden. Mithilfe der Transformation für Suche können Sie auf zusätzliche Informationen in einer zugehörigen Tabelle zugreifen, die auf Werten in gemeinsamen Spalten basiert.  
  
 Das Verweisdataset kann eine Cachedatei, eine vorhandene Tabelle oder Sicht, eine neue Tabelle oder das Ergebnis einer SQL-Abfrage sein. Die Transformation für Suche stellt entweder mithilfe eines OLE DB-Verbindungs-Managers oder eines Cacheverbindungs-Managers eine Verbindung mit dem Verweisdataset her. Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md) und [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md)  
  
 Es gibt folgende Möglichkeiten, um die Transformation für die Suche zu konfigurieren:  
  
-   Wählen Sie den Verbindungs-Manager aus, den Sie verwenden möchten. Wenn Sie eine Verbindung mit einer Datenbank herstellen möchten, wählen Sie einen OLE DB-Verbindungs-Manager aus. Wenn Sie eine Verbindung mit einer Cachedatei herstellen möchten, wählen Sie einen Cacheverbindungs-Manager aus.  
  
-   Geben Sie die Tabelle oder Sicht an, die das Verweisdataset enthält.  
  
-   Generieren Sie ein Verweisdataset, indem Sie eine SQL-Anweisung angeben.  
  
-   Geben Sie Joins zwischen der Eingabe und dem Verweisdataset an.  
  
-   Fügen Sie der Ausgabe der Transformation für Suche Spalten aus dem Verweisdataset hinzu.  
  
-   Konfigurieren Sie die Optionen für die Zwischenspeicherung.  
  
 Die Transformation für Suche unterstützt die folgenden Datenbankanbieter für den OLE DB-Verbindungs-Manager:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   Oracle  
  
-   DB2  
  
 Die Transformation für Suche versucht, einen Gleichheitsjoin zwischen Werten in der Transformationseingabe und Werten im Verweisdataset auszuführen. (Ein Gleichheitsjoin bedeutet, dass jede Zeile in der Transformationseingabe mindestens einer Zeile aus dem Verweisdataset entsprechen muss.) Wenn ein Gleichheitsjoin nicht ausgeführt werden kann, führt die Transformation für Suche eine der folgenden Aktionen aus:  
  
-   Falls im Verweisdataset kein entsprechender Eintrag vorhanden ist, wird kein Join ausgeführt. Standardmäßig werden bei Verwendung einer Transformation für Suche die Zeilen ohne übereinstimmende Einträge als Fehler behandelt. Sie haben jedoch die Möglichkeit, die Transformation für Suche so zu konfigurieren, dass die Zeilen an eine Ausgabe nicht übereinstimmender Einträge weitergeleitet werden.  
  
-   Sind in der Verweistabelle mehrere übereinstimmende Einträge vorhanden, gibt die Transformation für Suche nur den ersten übereinstimmenden Eintrag zurück, der von der Suchabfrage zurückgegeben wird. Wenn mehrere übereinstimmende Einträge gefunden werden, wird von der Transformation für Suche nur dann ein Fehler bzw. eine Warnung generiert, wenn die Transformation für das Laden des gesamten Verweisdatasets in den Cache konfiguriert ist. In diesem Fall, wird von der Transformation für Suche eine Warnung generiert, wenn die Transformation während des Füllens des Caches mehrere übereinstimmende Einträge erkennt.  
  
 Der Join kann ein zusammengesetzter Join sein. Das bedeutet, dass Sie mehrere Spalten in der Transformationseingabe mit Spalten im Verweisdataset verknüpfen können. Die Transformation unterstützt Joinspalten eines beliebigen Datentyps, außer DT_R4, DT_R8, DT_TEXT, DT_NTEXT oder DT_IMAGE. Weitere Informationen finden Sie unter [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Normalerweise werden Werte aus dem Verweisdataset der Transformationsausgabe hinzugefügt. Beispielsweise kann die Transformation für die Suche einen Produktnamen aus einer Tabelle mithilfe eines Wertes aus einer Eingabespalte extrahieren und den Produktnamen dann der Transformationsausgabe hinzufügen. Die Werte aus der Verweistabelle können Spaltenwerte ersetzen oder können neuen Spalten hinzugefügt werden.  
  
 Bei den von der Transformation für die Suche ausgeführten Suchvorgängen wird nach Groß-/Kleinschreibung unterschieden. Um Fehler bei der Suche aufgrund von unterschiedlicher Groß-/Kleinschreibung bei den Daten zu vermeiden, konvertieren Sie die Daten zunächst mit der Transformation für Zeichenzuordnung in Groß- oder Kleinbuchstaben. Anschließend fügen Sie der SQL-Anweisung, mit der die Verweistabelle generiert wird, die UPPER- oder LOWER-Funktion hinzu. Weitere Informationen finden Sie unter [Transformation zum Zuordnen der Zeichen](../../../integration-services/data-flow/transformations/character-map-transformation.md), [UPPER &#40;Transact-SQL&#41;](../../../t-sql/functions/upper-transact-sql.md) und [LOWER &#40;Transact-SQL&#41;](../../../t-sql/functions/lower-transact-sql.md).  
  
 Die Transformation für Suche weist die folgenden Ein- und Ausgaben auf:  
  
-   Eingabe.  
  
-   Ausgabe übereinstimmender Einträge. Bei der Ausgabe übereinstimmender Einträge werden in der Transformationseingabe die Zeilen behandelt, die mindestens einem Eintrag im Verweisdataset entsprechen.  
  
-   Ausgabe nicht übereinstimmender Einträge. Bei der Ausgabe nicht übereinstimmender Einträge in der Eingabe werden die Zeilen verarbeitet, die nicht mindestens einem Eintrag im Verweisdataset entsprechen. Wenn Sie die Transformation für Suche so konfigurieren, dass die Zeilen ohne übereinstimmende Einträge als Fehler behandelt werden, werden die Zeilen an die Fehlerausgabe weitergeleitet. Andernfalls würde die Transformation diese Zeilen an die Ausgabe nicht übereinstimmender Einträge weiterleiten.  
  
-   Fehlerausgabe.  
  
## <a name="caching-the-reference-dataset"></a>Zwischenspeichern des Verweisdatasets  
 In einem speicherresidenten Cache werden das Verweisdataset und eine Hashtabelle gespeichert, mit der die Daten indiziert werden. Der Cache bleibt speicherresident, bis die Ausführung des Pakets abgeschlossen ist. Sie können den Cache in einer Cachedatei (.caw) persistent speichern.  
  
 Wenn Sie den Cache in einer Datei persistent speichern, lädt das System den Cache schneller. Dies verbessert die Leistung der Transformation für Suche und des Pakets. Bei Verwendung einer Cachedatei arbeiten Sie mit Daten, die weniger aktuell sind als die Daten in der Datenbank.  
  
 Im Folgenden finden Sie weitere Vorteile einer persistenten Speicherung des Caches in einer Datei:  
  
-   ***Die Cachedatei kann für mehrere Pakete freigegeben werden. Weitere Informationen finden Sie unter*** [Implementieren einer Suchtransformation im Vollcachemodus mit der Transformation für Cacheverbindungs-Manager](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md) ***.***  
  
-   Die Cachedatei kann mit einem Paket bereitgestellt werden. ***Die Daten können dann auf mehreren Computern verwendet werden.*** Weitere Informationen finden Sie unter [Erstellen und Bereitstellen eines Cache für die Transformation für Suche](../../../integration-services/data-flow/transformations/create-and-deploy-a-cache-for-the-lookup-transformation.md).  
  
-   Sie können die Rohdatendatei-Quelle zum Lesen der Daten aus der Cachedatei verwenden. Dann können Sie die Daten mithilfe anderer Datenflusskomponenten umwandeln oder verschieben. Weitere Informationen finden Sie unter [Raw File Source](../../../integration-services/data-flow/raw-file-source.md).  
  
    > [!NOTE]  
    >  Der Cacheverbindungs-Manager unterstützt keine mithilfe des Rohdatendatei-Ziels erstellten oder geänderten Cachedateien.  
  
-   Mit dem Task Dateisystem können Sie für die Cachedatei Vorgänge ausführen und Attribute festlegen. Weitere Informationen finden Sie unter [File System Task](../../../integration-services/control-flow/file-system-task.md).  
  
 Folgende die Optionen für die Zwischenspeicherung sind verfügbar:  
  
-   Das Verweisdataset wird durch die Verwendung einer Tabelle, Sicht oder SQL-Abfrage generiert und in den Cache geladen, bevor die Transformation für Suche ausgeführt wird. Für den Zugriff auf das Dataset verwenden Sie den OLE DB-Verbindungs-Manager.  
  
     Diese Option für die Zwischenspeicherung ist kompatibel mit der Option für die vollständige Zwischenspeicherung, die für die Transformation für Suche in [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]verfügbar ist.  
  
-   Das Verweisdataset wird aus einer verbundenen Datenquelle im Datenfluss oder aus einer Cachefile generiert und in den Cache geladen, bevor die Transformation für Suche ausgeführt wird. Für den Zugriff auf das Dataset verwenden Sie den Cacheverbindungs-Manager und optional die Cachetransformation. Weitere Informationen finden Sie unter [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md) und [Cache Transform](../../../integration-services/data-flow/transformations/cache-transform.md).  
  
-   Das Verweisdataset wird durch die Verwendung einer Tabelle, Sicht oder SQL-Abfrage während der Ausführung der Transformation für Suche generiert. Die Zeilen mit übereinstimmenden Einträgen im Verweisdataset und die Zeilen ohne übereinstimmende Einträge im Dataset werden in den Cache geladen.  
  
     Wenn die Speichergröße des Caches überschritten wird, entfernt die Transformation zum Suchen automatisch die am seltensten verwendeten Zeilen aus dem Cache.  
  
     Diese Option für die Zwischenspeicherung ist kompatibel mit der Option für die teilweise Zwischenspeicherung, die für die Transformation für Suche in [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]verfügbar ist.  
  
-   Das Verweisdataset wird durch die Verwendung einer Tabelle, Sicht oder SQL-Abfrage während der Ausführung der Transformation für Suche generiert. Es werden keine Daten zwischengespeichert.  
  
     Diese Option für die Zwischenspeicherung ist kompatibel mit der Option für keine Zwischenspeicherung, die für die Transformation für Suche in [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]verfügbar ist.  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterscheiden sich in der Art des Zeichenfolgenvergleichs. Wenn die Transformation für Suche so konfiguriert ist, dass das Verweisdataset in den Cache geladen wird, bevor die Transformation für Suche ausgeführt wird, führt [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] den Suchvergleich im Cache aus. Andernfalls verwendet der Suchvorgang eine parametrisierte SQL-Anweisung, und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] führt den Suchvergleich aus. Dies bedeutet, dass die Transformation für Suche je nach Cachetyp möglicherweise eine unterschiedliche Anzahl von Übereinstimmungen aus der gleichen Suchtabelle zurückgibt.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen. Weitere Einzelheiten finden Sie in den folgenden Hilfethemen:  
  
-   [Implementieren einer Suche im Modus "Kein Cache" oder "Teilcache"](../../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)  
  
-   [Implementieren einer Suchtransformation im Vollcachemodus mit der Transformation für Cacheverbindungs-Manager](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
-   [Implementieren einer Suchtransformation im Vollcachemodus mit dem OLE DB-Verbindungs-Manager](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   Video [Vorgehensweise: Implementieren einer Suchtransformation im Vollcachemodus](http://go.microsoft.com/fwlink/?LinkId=131031)(Vorgehensweise: Implementieren einer Suchtransformation im Vollcachemodus) unter msdn.microsoft.com  
  
-   Blog-Artikel [Bewährte Vorgehensweisen für die Verwendung des Cachemodus der Transformation für Suche](http://go.microsoft.com/fwlink/?LinkId=146623)(Bewährte Vorgehensweisen für die Verwendung des Cachemodus der Transformation für Suche) unter blogs.msdn.com  
  
-   Blogeintrag [Suchmuster: Keine Beachtung von Groß-/Kleinschreibung](http://go.microsoft.com/fwlink/?LinkId=157782)auf blogs.msdn.com.  
  
-   Beispiel [Transformation für Suche](http://go.microsoft.com/fwlink/?LinkId=267528)auf msftisprodsamples.codeplex.com.  
  
     Informationen zum Installieren von [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Produktbeispielen und Beispieldatenbanken finden Sie unter [SQL Server Integration Services-Produktbeispiele](http://go.microsoft.com/fwlink/?LinkId=267527).  
  
## <a name="lookup-transformation-editor-general-page"></a>Transformations-Editor für Suche (Seite 'Allgemein')
  Auf der Seite **Allgemein** des Dialogfelds Transformations-Editor für Suche können Sie den Cachemodus und den Verbindungstyp auswählen sowie angeben, wie Zeilen ohne übereinstimmende Einträge behandelt werden sollen.  
  
### <a name="options"></a>enthalten  
 **Vollcache**  
 Das Verweisdataset wird generiert und in den Cache geladen, bevor die Transformation für Suche ausgeführt wird.  
  
 **Teilcache**  
 Das Verweisdataset wird während der Ausführung der Transformation für Suche generiert. Die Zeilen mit übereinstimmenden Einträgen im Verweisdataset und die Zeilen ohne übereinstimmende Einträge im Dataset werden in den Cache geladen.  
  
 **Kein Cache**  
 Das Verweisdataset wird während der Ausführung der Transformation für Suche generiert. Es werden keine Daten in den Zwischenspeicher geladen.  
  
 **Cacheverbindungs-Manager**  
 Die Transformation für Suche wird für die Verwendung eines Cacheverbindungs-Managers konfiguriert. Diese Option ist nur verfügbar, wenn die Option Vollcache ausgewählt ist.  
  
 **OLE DB-Verbindungs-Manager**  
 Die Transformation für Suche wird für die Verwendung eines OLE DB-Verbindungs-Managers konfiguriert.  
  
 **Angeben, wie Zeilen ohne übereinstimmende Einträge behandelt werden sollen**  
 Wählen Sie eine Option für die Behandlung von Zeilen aus, die nicht mindestens einem Eintrag im Verweisdataset entsprechen.  
  
 Wenn Sie **Zeilen an Ausgabe nicht übereinstimmender Einträge umleiten**auswählen, werden die Zeilen an eine Ausgabe nicht übereinstimmender Einträge weitergeleitet und nicht als Fehler behandelt. Die Option **Fehler** auf der Seite **Fehlerausgabe** des Dialogfelds **Transformations-Editor für Suche** ist nicht verfügbar.  
  
 Wenn Sie im Listenfeld **Angeben, wie Zeilen ohne übereinstimmende Einträge behandelt werden sollen** eine andere Option auswählen, werden die Zeilen als Fehler behandelt. In diesem Fall ist die Option **Fehler** auf der Seite **Fehlerausgabe** verfügbar.  
  
### <a name="external-resources"></a>Externe Ressourcen  
 Blogeintrag [Lookup cache modes](http://go.microsoft.com/fwlink/?LinkId=219518) (Suchcachemodi) auf blogs.msdn.com  
  
## <a name="lookup-transformation-editor-connection-page"></a>Transformations-Editor für Suche (Seite 'Verbindung')
  Auf der Seite **Verbindung** des Dialogfelds **Transformations-Editor für Suche** können Sie einen Verbindungs-Manager auswählen. Wenn Sie einen OLE DB-Verbindungs-Manager auswählen, wählen Sie auch eine Abfrage, Tabelle oder Sicht zum Generieren des Verweisdatasets aus.  
  
### <a name="options"></a>enthalten  
 Die folgenden Optionen sind verfügbar, wenn Sie im Dialogfeld **Transformations-Editor für Suche** auf der Seite **Allgemein** die Optionen **Vollcache** und Cacheverbindungs-Manager auswählen.  
  
 **Allgemein**  
 Wählen Sie einen vorhandenen Cacheverbindungs-Manager aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Editor für den Cacheverbindungs-Manager** eine neue Verbindung.  
  
 Die folgenden Optionen sind verfügbar, wenn Sie im Dialogfeld **Transformations-Editor für Suche**auf der Seite **Allgemein**die Optionen **Vollcache**, **Teilcache**oder **Kein Cache** und OLE DB-Verbindungs-Manager auswählen.  
  
 **Teilcache**  
 Wählen Sie einen vorhandenen OLE DB-Verbindungs-Manager aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **OLE DB-Verbindungs-Manager konfigurieren** eine neue Verbindung.  
  
 **Tabelle oder Sicht verwenden**  
 Wählen Sie eine vorhandene Tabelle oder Sicht aus der Liste aus, oder erstellen Sie eine neue Tabelle, indem Sie auf **Neu**klicken.  
  
> [!NOTE]  
>  Wenn Sie auf der Seite **Erweitert** im **Transformations-Editor für Suche** eine SQL-Anweisung angeben, wird durch diese SQL-Anweisung der hier ausgewählte Tabellenname überschrieben und ersetzt. Weitere Informationen finden Sie unter [Transformations-Editor für Suche &#40;Seite „Erweitert“&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-advanced-page.md).  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Tabelle erstellen** eine neue Tabelle.  
  
 **Ergebnisse einer SQL-Abfrage verwenden**  
 Wählen Sie diese Option aus, um nach einer vorhandenen Abfrage zu suchen, eine neue Abfrage zu erstellen, die Abfragesyntax zu überprüfen und eine Vorschau der Abfrageergebnisse anzuzeigen.  
  
 **Abfrage erstellen**  
 Erstellen Sie eine auszuführende Transact-SQL-Anweisung mit dem **Abfrage-Generator**, einem grafischen Tool, das verwendet wird, um Abfragen mithilfe des Durchsuchens von Daten zu erstellen.  
  
 **Durchsuchen**  
 Verwenden Sie diese Option, um nach einer vorhandenen Abfrage zu suchen, die als Datei gespeichert ist.  
  
 **Abfrage analysieren**  
 Überprüft die Syntax der Abfrage.  
  
 **Vorschau**  
 Zeigen Sie mithilfe des Dialogfelds **Vorschau der Abfrageergebnisse anzeigen** eine Vorschau der Ergebnisse an. Diese Option zeigt bis zu 200 Zeilen an.  
  
### <a name="external-resources"></a>Externe Ressourcen  
 Blogeintrag [Lookup cache modes](http://go.microsoft.com/fwlink/?LinkId=219518) (Suchcachemodi) auf blogs.msdn.com  
  
## <a name="lookup-transformation-editor-columns-page"></a>Transformations-Editor für Suche (Seite 'Spalten')
  Auf der Seite **Spalten** des Dialogfelds **Transformations-Editor für Suche** können Sie den Join zwischen der Quell- und der Verweistabelle angeben sowie Suchspalten aus der Verweistabelle auswählen.  
  
### <a name="options"></a>enthalten  
 **Verfügbare Eingabespalten**  
 Zeigt die Liste der verfügbaren Eingabespalten an. Die Eingabespalten sind die Spalten im Datenfluss aus einer verbundenen Quelle. Die Datentypen der Eingabe- und Suchspalte müssen übereinstimmen.  
  
 Mithilfe eines Drag-und-Drop-Vorgangs können Sie verfügbare Eingabespalten bestimmten Suchspalten zuordnen.  
  
 Sie können auch mithilfe der Tastatur Eingabespalten bestimmten Suchspalten zuordnen. Dazu heben Sie eine Spalte in der Tabelle **Verfügbare Eingabespalten** hervor, drücken die Anwendungstaste und klicken dann auf **Zuordnungen bearbeiten**.  
  
 **Verfügbare Suchspalten**  
 Zeigt die Liste der Suchspalten an. Die Suchspalten sind Spalten in der Verweistabelle, in denen nach Werten gesucht werden soll, die mit den Eingabespalten übereinstimmen.  
  
 Mithilfe eines Drag-und-Drop-Vorgangs können Sie verfügbare Suchspalten bestimmten Eingabespalten zuordnen.  
  
 Wählen Sie mithilfe der Kontrollkästchen die Suchspalten in der Verweistabelle aus, für die die Suchvorgänge ausgeführt werden sollen.  
  
 Sie können auch mithilfe der Tastatur Suchspalten bestimmten Eingabespalten zuordnen. Dazu heben Sie eine Spalte in der Tabelle **Verfügbare Suchspalten** hervor, drücken die Anwendungstaste und klicken dann auf **Zuordnungen bearbeiten**.  
  
 **Suchspalte**  
 Zeigt die Liste der ausgewählten Suchspalten an. Die Auswahl wird entsprechend in der Auswahl der Kontrollkästchen in der Tabelle **Verfügbare Suchspalten** deutlich.  
  
 **Suchvorgang**  
 Wählen Sie in der Liste einen Suchvorgang aus, der für die Suchspalte ausgeführt werden soll.  
  
 **Ausgabealias**  
 Geben Sie einen Alias für die Ausgabe der einzelnen Suchspalten ein. Standardmäßig wird der Name der Suchspalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist.  
  
## <a name="lookup-transformation-editor-advanced-page"></a>Transformations-Editor für Suche (Seite 'Erweitert')
  Auf der Seite **Erweitert** des Dialogfelds **Transformations-Editor für Suche** können Sie die teilweise Zwischenspeicherung konfigurieren und die SQL-Anweisung für die Suchtransformation ändern.  
  
### <a name="options"></a>enthalten  
 **Cachegröße (32-Bit)**  
 Passen Sie die Cachegröße (in Megabytes) für 32-Bit-Computer an. Der Standardwert ist 5 Megabytes.  
  
 **Cachegröße (64-Bit)**  
 Passen Sie die Cachegröße (in Megabytes) für 64-Bit-Computer an. Der Standardwert ist 5 Megabytes.  
  
 **Cache für Zeilen ohne übereinstimmende Einträge aktivieren**  
 Zeilen ohne übereinstimmende Einträge im Verweisdataset werden zwischengespeichert.  
  
 **Zuordnung von Cache**  
 Geben Sie den Prozentsatz des Caches an, der für Zeilen ohne übereinstimmende Einträge im Verweisdataset zugeordnet werden soll.  
  
 **SQL-Anweisung ändern**  
 Hiermit ändern Sie die zum Generieren des Verweisdatasets verwendete SQL-Anweisung.  
  
> [!NOTE]  
>  Durch die auf dieser Seite angegebene optionale SQL-Anweisung wird der auf der Seite **Verbindung** im **Transformations-Editor für Suche**angegebene Tabellenname überschrieben und ersetzt. Weitere Informationen finden Sie unter [Transformations-Editor für Suche &#40;Seite „Verbindung“&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md).  
  
 **Abfrageparameter festlegen**  
 Ordnen Sie mithilfe des Dialogfelds **Abfrageparameter festlegen** die Eingabespalten den Parametern zu.  
  
### <a name="external-resources"></a>Externe Ressourcen  
 Blogeintrag [Lookup cache modes](http://go.microsoft.com/fwlink/?LinkId=219518) (Suchcachemodi) auf blogs.msdn.com  
  
## <a name="see-also"></a>Siehe auch  
 [Transformation für Fuzzysuche](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)   
 [Transformation für Ausdruckssuche](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)   
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
