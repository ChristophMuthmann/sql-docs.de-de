---
title: "Konfigurieren der Sammlung von Verwendungsdaten für (PowerPivot für SharePoint | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 955ca6d6-9d5b-47a4-a87c-59bd23f1bf74
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 98ec79c14a0ac082c75967a9c81fa7b2027f5511
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="configure-usage-data-collection-for-power-pivot-for-sharepoint"></a>Konfigurieren der Sammlung von Verwendungsdaten für Power Pivot für SharePoint
  Die Sammlung von Verwendungsdaten ist eine SharePoint-Funktion auf Farmebene. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint verwendet und erweitert dieses System, um Berichte im [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard bereitzustellen, die zeigen, wie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten und -Dienste verwendet werden. Abhängig davon, wie SharePoint installiert wird, kann die Sammlung von Verwendungsdaten für die Farm deaktiviert sein. Ein Farmadministrator muss die Verwendungsprotokollierung aktivieren, damit die Verwendungsdaten für die Darstellung im [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard erstellt werden.  
  
 Informationen zu den Verwendungsdaten im [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard finden Sie unter [PowerPivot-Management-Dashboard und Verwendungsdaten](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
 **In diesem Thema:**  
  
 [Aktivieren der Sammlung von Verwendungsdaten und Auswählen der Ereignisse, durch die die Datensammlung ausgelöst wird](#events)  
  
 [Festlegen des Protokolldateispeicherorts](#configdb)  
  
 [Konfigurieren der Zeitgeberaufträge, die bei der Sammlung von Verwendungsdaten verwendet werden](#jobs)  
  
 [Begrenzen der Speicherdauer des Verwendungsdatenverlaufs](#confighist)  
  
 [Definieren schneller, mittlerer und langsamer Abfrageantwortkategorien für die Berichterstellung](#qrh)  
  
 [Festlegen der Häufigkeit, mit der Abfragestatistiken an das System für die Sammlung von Verwendungsdaten gemeldet werden](#ttr)  
  
 [Öffnen der Seite „Power Pivot-Dienstanwendung“, um auf Konfigurationseinstellungen zuzugreifen](#openconfig)  
  
 [Die Standardkonfiguration für die Sammlung von Power Pivot-Verwendungsdaten](#defaultconfig)  
  
> [!IMPORTANT]  
>  Verwendungsdaten geben Einblick in die Daten- und Ressourcenzugriffe durch Benutzer, liefern aber keine zuverlässigen, dauerhaften Daten zu Servervorgängen und Benutzerzugriffen. Bei einem Serverneustart gehen Verwendungsdaten zu Ereignissen beispielsweise verloren und können nicht wiederhergestellt werden. Auch wenn die temporären Protokolldateien ihre maximale Größe erreichen, werden erst wieder neue Daten hinzugefügt, nachdem die Dateien gelöscht wurden. Falls Sie Überwachungsfunktion benötigen, sollten Sie die Verwendung von Funktionen für Workflow- und Inhaltstypen in Erwägung ziehen, die SharePoint zum Aufbau eines Überwachungssubsystems für die Farm bereitstellt. Weitere Informationen finden Sie in Produkt- und Communitydokumentationen im Web.  
  
##  <a name="events"></a> Aktivieren der Sammlung von Verwendungsdaten und Auswählen der Ereignisse, durch die die Datensammlung ausgelöst wird  
 Konfigurieren Sie die Sammlung von Verwendungsdaten in der SharePoint-Zentraladministration.  
  
1.  Klicken Sie in der Zentraladministration auf **Überwachung**.  
  
2.  Klicken Sie im Abschnitt **Berichterstellung**auf **Verwendungs- und Integritätsdatenerfassung konfigurieren**.  
  
3.  Aktivieren Sie **Verwendungsdatenerfassung aktivieren**.  
  
4.  Aktivieren oder deaktivieren Sie im Abschnitt **Zu protokollierende Ereignisse** die entsprechenden Kontrollkästchen, um die folgenden Analysis Services-Ereignisse zu aktivieren oder zu deaktivieren:  
  
    |Ereignis|Description|  
    |-----------|-----------------|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Verbindungen**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Das Verbindungen-Ereignis wird zum Überwachen von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Serververbindungen verwendet, die im Auftrag eines Benutzers hergestellt werden.|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Verwendung von Datenladevorgängen**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Die Verwendung von Datenladevorgängen wird zum Überwachen von Anforderungen verwendet, durch die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten in den Serverarbeitsspeicher geladen werden. Ein Ladeereignis wird für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datendateien generiert, die aus einer Inhaltsdatenbank oder dem Cache geladen werden.|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Verwendung von Datenentladevorgängen**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Die Verwendung von Datenentladevorgängen wird zur Überwachung von Anfragen zum Entladen einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenquelle nach einem bestimmten Zeitraum der Inaktivität verwendet. Das Zwischenspeichern einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenquelle auf einem Datenträger wird als Entladeereignis gemeldet.|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Verwendung von Abfragen**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Die Verwendung von Abfragen wird zur Überwachung von Abfrageverarbeitungszeiten für Daten verwendet, die in eine [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] -Instanz geladen werden.|  
  
    > [!NOTE]  
    >  Obwohl Serverzustands- und Datenaktualisierungsvorgänge auch Verwendungsdaten generieren, ist diesen Prozessen kein Ereignis zugeordnet.  
  
5.  Sie können auch den Speicherort der Protokolldatei aktualisieren. Weitere Informationen finden Sie im nächsten Abschnitt.  
  
6.  Klicken Sie auf **OK** , um die Änderungen zu speichern.  
  
7.  Optional können Sie angeben, ob alle Meldungen oder nur Fehler protokolliert werden. Weitere Informationen zum Einschränken von Ereignismeldungen finden Sie unter [Konfigurieren und Anzeigen der SharePoint-Protokolldateien und -Diagnoseprotokollierung &#40;Power Pivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md).  
  
##  <a name="configdb"></a> Festlegen des Protokolldateispeicherorts  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Verwendungsdaten werden anfänglich in Verwendungsprotokolldateien auf dem lokalen Server gespeichert und anschließend in regelmäßigen Abständen in die Datenbanken der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung verschoben. Der Speicherort der Protokolldatei wird in der Zentraladministration festgelegt. Der Standardspeicherort ist:  
  
 `C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\logs`  
  
 Um diese Eigenschaften anzuzeigen oder zu ändern, verwenden Sie die Seite **Sammlung von Integritäts- und Verwendungsdaten** .  
  
1.  Klicken Sie auf der Homepage in der Zentraladministration auf **Überwachung**.  
  
2.  Klicken Sie im Abschnitt Überwachung auf **Verwendungs- und Integritätsdatenerfassung konfigurieren**.  
  
3.  Zeigen Sie unter Verwendungsdatensammlungseinstellungen den Speicherort, den Namen oder die maximale Größe der Datei an oder ändern Sie sie. Wenn Sie eine zu geringe Dateigröße angeben, erreicht die Datei schnell die maximale Größe und kann erst wieder neue Einträge aufnehmen, nachdem ihr Inhalt in die zentrale Datenbank für Verwendungsdaten verschoben wurde.  
  
##  <a name="jobs"></a> Konfigurieren der Zeitgeberaufträge, die bei der Sammlung von Verwendungsdaten verwendet werden  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Die Serverstatus- und Verwendungsdaten werden durch zwei Zeitgeberaufträge an unterschiedliche Stellen im System zur Sammlung von Verwendungsdaten verschoben:  
  
-   Der Zeitgeberauftrag für den „Import der Microsoft SharePoint Foundation-Verwendungsdaten“ überträgt die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Verwendungsdaten in die Datenbank der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung.  
  
-   Der „Zeitgeberauftrag für die Verarbeitung des[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboards“ überträgt die Daten in eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe, die die Datenquelle für integrierte administrative Berichte darstellt.  
  
 Wenn Sie die Administratorberichte aktualisieren müssen, die häufiger im [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard angezeigt werden, führen Sie die folgenden Schritte aus.  
  
1.  Klicken Sie in der Zentraladministration auf **Überwachung**.  
  
2.  Klicken Sie auf **Zeitgeberaufträge** Klicken Sie im Abschnitt **Auftragsdefinitionen überprüfen** .  
  
3.  Klicken Sie auf **Import der Microsoft SharePoint Foundation-Verwendungsdaten**.  
  
4.  Klicken Sie auf **Jetzt ausführen**. Wenn die Schaltfläche **Jetzt ausführen** deaktiviert ist, klicken Sie auf **Aktivieren** und dann auf **Jetzt ausführen**.  
  
5.  Klicken Sie in der Liste „Auftragsdefinitionen“ auf den **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten**.  
  
6.  Klicken Sie auf **Jetzt ausführen**.  
  
7.  Überprüfen Sie die Berichte, um die aktualisierten Daten anzuzeigen. Weitere Informationen finden Sie unter [PowerPivot-Management-Dashboard und Verwendungsdaten](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
##  <a name="confighist"></a> Begrenzen der Speicherdauer des Verwendungsdatenverlaufs  
 Der Verwendungsdatenverlauf wird für Ereignisse (Verbindungen, Lade-, Entladevorgänge und bedarfsgesteuerte Abfrageverarbeitung) sowie Datenaktualisierungen (geplante Datenverarbeitung) gespeichert. Obwohl Verwendungsdaten durch das SharePoint-System für die Sammlung von Verwendungsdaten gesammelt werden, werden die Berichtsdaten zur längerfristigen Speicherung in eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Anwendungsdatenbank und eine Berichtsdatenbank verschoben. Die Einstellung für den Verwendungsdatenverlauf steuert, wie lange Verwendungsdaten in den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Anwendungsdatenbanken beibehalten werden. Für alle Typen gespeicherter Verwendungsdaten in einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungs-Datenbank gilt der gleiche Grenzwert.  
  
1.  [Öffnen Sie die Seite „Power Pivot-Dienstanwendung“](#openconfig).  
  
2.  Geben Sie im Abschnitt **Sammlung von Verwendungsdaten** unter **Verwendungsdatenverlauf**ein, wie viele Tage ein Datensatz der Datenaktualisierungsaktivitäten für die einzelnen Arbeitsmappen beibehalten werden soll.  
  
    -   Die Standardeinstellung beträgt 365 Tage.  
  
    -   0 gibt eine unbegrenzte Speicherdauer an, bei der Verwendungsdaten unbegrenzt beibehalten werden.  
  
    -   Alternativ können Sie auch einen Bereich zwischen 1 und 5000 angeben.  
  
     Indem Sie die Beibehaltungsdauer auf eine geringere Anzahl von Tagen festlegen, werden Daten gelöscht, die die neue Begrenzung überschreiten. Wenn Sie den Wert beispielsweise von 365 in 30 ändern, werden Verwendungsdaten für alle Verlaufsinformationen gelöscht, die mehr als 30 Tage zurückliegen. Es werden nur Daten der letzten 30 Tage beibehalten.  
  
     Die Daten werden tatsächlich gelöscht, wenn das nächste Ereignis eintritt. Die Begrenzung des Verwendungsdatenverlaufs wird nur überprüft, wenn das System ein Ereignis verarbeitet.  
  
3.  Klicken Sie auf **OK**.  
  
 Weitere Informationen dazu, wie Verwendungsdaten gesammelt und gespeichert werden, finden Sie unter [Sammlung von Power Pivot-Verwendungsdaten](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md).  
  
##  <a name="qrh"></a> Definieren schneller, mittlerer und langsamer Abfrageantwortkategorien für die Berichterstellung  
 Die Leistung der Abfrageverarbeitung wird anhand vordefinierter Kategorien gemessen, in denen ein Anforderung/Antwort-Zyklus durch dessen Ausführungsdauer definiert wird. Die vordefinierten Kategorien lauten: Trivial, Schnell, Erwartet, Lange Ausführung und Überschritten. Jede an einen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Server übermittelte Anforderung wird abhängig von ihrer Ausführungsdauer in eine der Kategorien eingeteilt.  
  
 Die Abfrageantwortinformationen werden in Aktivitätsberichten verwendet. Alle Kategorien werden innerhalb der Berichte unterschiedlich verwendet, um die Leistungstrends des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systems besser zu verdeutlichen. Beispielsweise werden triviale Anforderungen völlig ausgeschlossen, um unwesentliche Daten herauszufiltern und mithilfe der verbleibenden Kategorien aussagekräftigere Trends aufzuzeigen. Im Gegensatz dazu sind Statistiken zu Anforderungen mit langer oder überschrittener Ausführungszeit im Bericht gut erkennbar, damit Administratoren oder Arbeitsmappenbesitzer unverzüglich Korrekturmaßnahme ergreifen können.  
  
 Sie können keine Kategorien hinzufügen oder löschen, haben jedoch die Möglichkeit Ober- und Untergrenzen zu definieren, die bestimmen, wo eine Kategorie aufhört und die nächste beginnt. Wenn Ihre Organisation Vereinbarungen zum Servicelevel (SLAs, Service Level Agreements) zur Festlegung akzeptabler Serververfügbarkeits- und Leistungsebenen verwendet, können Sie diese Kategorien in Anpassung an die erstellte SLA optimieren.  
  
1.  [Öffnen Sie die Seite „Power Pivot-Dienstanwendung“](#openconfig).  
  
2.  Geben Sie im Abschnitt **Sammlung von Verwendungsdaten** unter **Obergrenze für triviale Antworten** einen Wert (in Millisekunden) ein, der angibt, in welcher Zeit eine triviale Antwort maximal abgeschlossen sein muss. Zu Anforderungen aus dieser Kategorie gehören normalerweise Ping-Signale an den Server, Sitzungseinleitungen und Metadatenabfragen. Der Standardwert beträgt 500 Millisekunden (oder eine halbe Sekunde).  
  
3.  Geben Sie unter Obergrenze für schnelle Anforderungen einen Wert (in Millisekunden) ein, der die Obergrenze zum Abschließen einer schnellen Anforderung festlegt. Zu Anforderungen aus dieser Kategorie gehören Abfragen sehr kleiner Datasets oder Metadatenserver großer Datasets. Der Standardwert beträgt 1000 Millisekunden (oder eine Sekunde).  
  
4.  Geben Sie unter **Obergrenze für erwartete Antwortdauer**einen Wert (in Millisekunden) ein, der die Obergrenze zum Abschließen einer Antwort in einem erwarteten oder durchschnittlichen Zeitrahmen festlegt. Zu Anforderungen aus dieser Kategorie gehört das Laden von Daten in einen Viewer. Der Standardwert beträgt 3000 Millisekunden (oder drei Sekunden).  
  
5.  Geben Sie unter **Obergrenze für lange Antworten**einen Wert (in Millisekunden) ein, der die Obergrenze zum Abschließen einer Antwort mit langer Ausführungsdauer festlegt. Anforderungen aus dieser Kategorie werden länger als erwartet, aber immer noch innerhalb eines akzeptablen Bereichs ausgeführt. Der Standardwert beträgt 10000 Millisekunden (oder zehn Sekunden).  
  
     Alle Anforderungen, die diese Grenze überschreiten, werden als *Überschritten*kategorisiert. Für *Überschritten*kann kein Schwellenwert konfiguriert werden. Er wird von der Obergrenze abgeleitet, die Sie unter Obergrenze für lange Anforderungen angeben. Anforderungen aus der Kategorie Überschritten werden länger ausgeführt als in einer von Ihnen definierten SLA zulässig.  
  
6.  Klicken Sie auf **OK**.  
  
##  <a name="ttr"></a> Festlegen der Häufigkeit, mit der Abfragestatistiken an das System für die Sammlung von Verwendungsdaten gemeldet werden  
 Das Intervall für die Berichterstellung gibt an, wie häufig Abfragestatistiken im System für die Sammlung von Verwendungsdaten erfasst werden. Abfragestatistiken werden in einem Prozess gesammelt und in regelmäßigen Intervallen als einzelnes Ereignis gemeldet. Sie können das Intervall anpassen, um häufiger oder seltener eine Protokolldatei zu erstellen.  
  
1.  [Öffnen Sie die Seite „Power Pivot-Dienstanwendung“](#openconfig).  
  
2.  Geben Sie im Abschnitt **Sammlung von Verwendungsdaten** unter **Berichtsintervall für Abfragen**ein, nach wie vielen Sekunden der Server die Abfragestatistiken für alle Kategorien (trivial, schnell, erwartet, mit langer Ausführungsdauer und überschritten) als einzelnes Ereignis an das System für die Sammlung von Verwendungsdaten meldet.  
  
    -   Der Bereich liegt zwischen 1 und einer beliebigen positiven ganzen Zahl.  
  
    -   Der Standardwert beträgt 300 Sekunden (oder fünf Minuten). Dieser Wert wird für dynamische Farmumgebungen empfohlen, in denen eine Vielzahl von Anwendungen und Diensten ausgeführt wird.  
  
     Wenn Sie diesen Wert wesentlich heraufsetzen, können statistische Daten verloren gehen, bevor sie gemeldet werden. Ein Dienstneustart bewirkt z. B., dass Abfragestatistikdaten verloren gehen. Umgekehrt können die integrierten Aktivitätsberichte jedoch auch zu wenig Daten enthalten. In diesem Fall können Sie das Intervall verringern, damit Ereignisse für die Berichterstellung häufiger gemeldet werden.  
  
3.  Klicken Sie auf **OK**.  
  
##  <a name="openconfig"></a> Öffnen der Seite „Power Pivot-Dienstanwendung“, um auf Konfigurationseinstellungen zuzugreifen  
 Nur Farm- oder Dienstadministratoren können Einstellungen für Dienstanwendungen ändern. Wenn Sie mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen in der Farm definiert haben, muss jede Anwendung einzeln geändert werden.  
  
1.  Klicken Sie in der SharePoint-Zentraladministration unter **Anwendungsverwaltung**auf **Dienstanwendungen verwalten**.  
  
2.  Suchen Sie die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung. Sie erkennen eine Dienstanwendung an ihrem Typ. Ein [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungstyp ist **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung**.  
  
3.  Klicken Sie auf den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungsnamen. Das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard wird geöffnet.  
  
4.  Klicken Sie unter **Aktionen**auf **Einstellungen für Dienstanwendung konfigurieren**. Die Seite „Einstellungen für die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung“ wird geöffnet.  
  
##  <a name="defaultconfig"></a> Die Standardkonfiguration für die Sammlung von Power Pivot-Verwendungsdaten  
 Die Sammlung von Verwendungsdaten für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstvorgänge kann mit Standardeinstellungen aktiviert werden, um sie in Anwendungen, die die Analysis Services-Integrationsfunktion unterstützen, direkt verfügbar zu machen. Die Standardeinstellungen umfassen Ereignisse, durch die die Sammlung von Verwendungsdaten ausgelöst wird, Grenzwerte für die Speicherdauer von Verwendungsdaten und Schwellenwerte zum Kategorisieren von Abfrageantwortzeiten.  
  
 Die folgende Tabelle enthält die Standardwerte für die Konfiguration der Sammlung von Verwendungsdaten.  
  
|Einstellung|Standardwert|Typ|Gültiger Bereich|  
|-------------|-------------------|----------|-----------------|  
|**Analysis Services-Verwendungsereignisse** (Verbinden, Laden, Entladen, Anforderungen)|\<aktiviert >|Boolean|Diese Werte werden entweder aktiviert oder deaktiviert.|  
|**Query Reporting interval**|300 (in Sekunden)|Integer|Zwischen 1 und einer beliebigen positiven ganzen Zahl. Der Standardwert ist 5 Minuten.|  
|**Usage data history**|365 (in Tagen)|Integer|0 gibt eine unbegrenzte Dauer an, Sie können jedoch auch eine Obergrenze festlegen, damit Verlaufsdaten ablaufen und automatisch gelöscht werden. Gültige Werte für eine begrenzte Beibehaltungsdauer betragen 1 bis 5000 (Tage).|  
|Obergrenze für triviale Antworten|500 (in Millisekunden)|Integer|Legt eine Obergrenze fest, die den Austausch einer trivialen Anforderung/Antwort definiert. Jede Anforderung, die innerhalb von 0 bis 500 Millisekunden abgeschlossen wird, ist eine triviale Anforderung und wird bei der Berichterstellung ignoriert.|  
|Obergrenze für schnelle Antworten|1000 (in Millisekunden)|Integer|Legt eine Obergrenze fest, die den Austausch einer schnellen Anforderung/Antwort definiert.|  
|Obergrenze für erwartete Antwortdauer|3000 (in Millisekunden)|Integer|Legt eine Obergrenze fest, die die erwartete Dauer für den Austausch einer Anforderung/Antwort definiert.|  
|Obergrenze für lange Antworten|10000 (in Millisekunden)|Integer|Legt eine Obergrenze fest, die den Austausch einer Anforderung/Antwort mit langer Laufzeit definiert. Alle Anforderungen, die diese Obergrenze überschreiten, gehören zur Kategorie Überschritten, die keinen oberen Schwellenwert aufweist.|  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurationseinstellungsverweis &#40;Power Pivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Sammlung von Power Pivot-Verwendungsdaten](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)  
  
  

