---
title: "Hilfsprogramm-Explorer „F1-Hilfe“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/19/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.swb.ue.navigation.f1
- sql13.SWB.UE.dac.details.F1
- sql13.SQB.UE.dac.details.F1
- utility details
helpviewer_keywords:
- Utility
- management
- data-tier application
ms.assetid: 8697e4a4-4f59-4cda-af71-7de86005bd4a
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 46b3d92d8c1f6a720eb39a701aca50a8bc2733b9
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="utility-explorer-f1-help"></a>Hilfsprogramm-Explorer (F1-Hilfe)
  In den folgenden Abschnitten werden die Funktionalität und die zugehörigen Vorgänge des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Hilfsprogramms dokumentiert.  
  
  ## <a name="utility-dashboard-sql-server-utility"></a>Dashboard des Hilfsprogramms (SQL Server-Hilfsprogramm)
 Um Daten im Dashboard des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramms anzuzeigen, wählen Sie den obersten Knoten in der Struktur des Hilfsprogramm-Explorers aus: Hilfsprogramm<UCP_Name>\\(ComputerName\UCP). Das Dashboard enthält Zusammenfassungs- und Detaildaten aus allen verwalteten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und allen Datenebenenanwendungen im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramm. Zum Aktualisieren der Dashboarddaten klicken Sie mit der rechten Maustaste auf den obersten Knoten in der Struktur des Hilfsprogramm-Explorers und wählen dann **Aktualisieren**aus.  
  
 Weitere Informationen zum Erstellen eines Steuerungspunkts für das Hilfsprogramm finden Sie unter [Erstellen eines Steuerungspunkts für das SQL Server-Hilfsprogramm &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)aus. Weitere Informationen zum Hinzufügen einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm finden Sie unter [Registrieren einer Instanz von SQL Server &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)aus.  
 
  
### <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 Zustand der verwalteten Instanz  
 Der Zustand verwalteter Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird links im Inhaltsbereich des Hilfsprogramm-Explorers angezeigt.  
  
 Die Zustandsparameter für verwaltete Instanzen lauten wie folgt:  
  
-   CPU-Auslastung für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Auslastung der Datenbankdatei  
  
-   Speicherplatzauslastung auf Speichervolumes  
  
-   CPU-Auslastung für den Computer  
  
-   Der Status jedes Parameters ist in drei Kategorien unterteilt:  
  
-   Normal ausgelastet – Die Anzahl verwalteter Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die nicht gegen Richtlinien zur Ressourcennutzung verstoßen.  
  
-   Unterausgelastet – Die Anzahl verwalteter Ressourcen, die gegen Richtlinien zur Unterauslastung von Ressourcen verstoßen.  
  
-   Überausgelastet – Die Anzahl verwalteter Ressourcen, die gegen Richtlinien zur Überauslastung von Ressourcen verstoßen.  
  
-   Keine Daten verfügbar – Für verwaltete Instanzen von SQL Server sind keine Daten verfügbar, weil die Instanz von SQL Server entweder gerade erst registriert und der erste Datensammlungsvorgang noch nicht abgeschlossen wurde oder weil bei der verwalteten Instanz von SQL Server ein Problem im Hinblick auf die Sammlung und das Upload von Daten auf den UCP aufgetreten ist.  
  
 Der ausführliche Status für Zustandsparameter kann an verschiebbaren Indikatoren abgelesen werden. Der Teil rechts von den verschiebbaren Indikatoren zeigt an, wie viele verwaltete Instanzen sich in jeder Statuskategorie befinden.  
  
 Um eine gefilterte Sicht einer verwalteten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder einer Datenebenenanwendung zu erstellen, klicken Sie auf den Link für eine Auslastungskategorie neben dem entsprechenden verschiebbaren Indikator im Hilfsprogrammdashboard. Wenn Sie z. B. im Bereich **Inhalt des Hilfsprogramm-Explorers** auf **Überausgelastete Instanz-CPU** klicken, erstellt SSMS eine gefilterte Listenansicht von verwalteten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die auf der Grundlage der aktuellen Richtlinieneinstellungen eine überausgelastete CPU haben.  
  
 Beachten Sie, dass der entsprechende Knoten im Hilfsprogramm-Explorer-Navigationsbereich mit **(gefiltert)** angefügt wird, wenn Sie auf einen Link für eine Auslastungskategorie klicken, d.h., **Verwaltete Instanzen** wird als **Verwaltete Instanzen (gefiltert)**bezeichnet. Um Filtereinstellungen anzuzeigen, klicken Sie mit der rechten Maustaste auf den Knoten im Navigationsbereich, wählen Sie **Filter**aus, und klicken Sie dann auf **Filtereinstellungen**. Um Filtereinstellungen zu löschen, klicken Sie mit der rechten Maustaste auf den Knoten im Navigationsbereich, wählen **Filter** aus und klicken dann auf **Filter entfernen**.  
  
 Weitere Informationen zum Anzeigen des Zustands einzelner Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bzw. zum Anzeigen oder Ändern der Einstellungen für die Richtlinienkonfiguration finden Sie unter [Details zu verwalteten Instanzen &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2).  
  
 Hilfsprogrammzusammenfassung  
 Zeigt die Anzahl der verwalteten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und die Anzahl der Datenebenenanwendungen an, die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm verwaltet werden.  
  
 Zustand der Datenebenenanwendung  
 Der Zustand der Datenebenenanwendungen wird rechts im Inhaltsbereich des Hilfsprogramm-Explorers angezeigt.  
  
 Die Zustandsparameter für Datenebenenanwendungen lauten wie folgt:  
  
-   CPU-Auslastung für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Auslastung der Datenbankdatei  
  
-   Speicherplatzauslastung auf Speichervolumes  
  
-   CPU-Auslastung für den Computer  
  
 Der Status jedes Parameters ist in drei Kategorien unterteilt:  
  
-   Normal ausgelastet – Die Anzahl der Datenebenenanwendungen, die nicht gegen Richtlinien zur Ressourcennutzung verstoßen.  
  
-   Überausgelastet – Die Anzahl der Datenebenenanwendungen, die gegen Richtlinien zur Überauslastung von Ressourcen verstoßen.  
  
-   Unterausgelastet – Die Anzahl der Datenebenenanwendungen, die gegen Richtlinien zur Unterauslastung von Ressourcen verstoßen.  
  
-   Keine Daten verfügbar – Für Datenebenenanwendungen sind keine Daten verfügbar, weil die verwaltete Instanz von SQL Server, die die Datenebenenanwendung enthält, keine Daten übermittelt.  
  
 Der ausführliche Status für Zustandsparameter kann an verschiebbaren Indikatoren abgelesen werden. Der Teil rechts neben den verschiebbaren Indikatoren zeigt an, wie viele Datenebenenanwendungen in jeder Statuskategorie enthalten sind. Weitere Informationen zum Anzeigen des Zustands einzelner Datenebenenanwendungen bzw. zum Anzeigen oder Ändern der Richtlinienkonfigurationseinstellungen finden Sie unter [Details zu bereitgestellten Datenebenenanwendungen &amp;#40;SQL Server-Hilfsprogramm&amp;#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
 Verlauf der Auslastung des Hilfsprogrammspeichers  
 Der Verlauf der Auslastung wird in einem Zeitdiagramm unten im Dashboard des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms angezeigt. Die Zeitangaben zeigen das lokale Datum und die lokale Uhrzeit des UCPs unter Verwendung des datetime-Datentyps an. Weitere Informationen finden Sie unter dem Thema [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) . Beachten Sie bei Verwendung des Hilfsprogramm-Objektmodells, dass SSMS den datetimeoffset-Datentyp verwendet. Weitere Informationen finden Sie unter dem Thema [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 Verwenden Sie die Optionsfelder links neben dem Anzeigebereich, um den Berichtszeitraum für das Diagramm zu ändern.  
  
 Die Optionen für das Berichtsintervall lauten:  
  
-   1 Tag, in Intervallen von 15 Minuten  
  
-   1 Woche, in Intervallen von 1 Tag  
  
-   1 Monat, in Intervallen von 1 Woche  
  
-   1 Jahr, in Intervallen von 1 Monat  
  
 Nachdem Sie eine Änderung am Berichtsintervall vorgenommen haben, werden die Daten automatisch aktualisiert.  
  
 Auslastung des Hilfsprogrammspeichers  
 Im Kreisdiagramm zur Speicherplatzauslastung unten rechts im Dashboard wird das Verhältnis von belegtem Speicherplatz zu freiem Speicherplatz auf Volumes angezeigt, die sich auf Computern mit verwalteten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]befinden. Die Daten in dieser Anzeige werden alle 15 Minuten aktualisiert.  
 
 ## <a name="deployed-data-tier-application-details-sql-server-utility"></a>Details zu bereitgestellten Datenebenenanwendungen (SQL Server-Hilfsprogramm)
  Die Informationen in der Listenansicht Bereitgestellte Datenebenenanwendungen des Hilfsprogramm-Explorers enthalten Auslastungsdaten für einzelne Datenebenenanwendungen, Verlaufsdaten zur CPU-Auslastung und Details zur Speicherplatzauslastung auf Dateiebene sowie die Möglichkeit, Richtlinienschwellenwerte anzuzeigen und zu aktualisieren. Richtlinienschwellenwerte können auf der Ebene der Datenebenenanwendung für die CPU-Auslastung sowie Datenbankdateien und Protokolldateien gesteuert werden. Sie können auch Eigenschaftendetails für einzelne Datenebenenanwendungen anzeigen.  
  
### <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 Listenansicht  
 In der Listenansicht im oberen Bereich werden Daten zu einzelnen Datenebenenanwendungen angezeigt. Zustandssymbole zeigen den Zusammenfassungsstatus für die einzelnen Datenebenenanwendungen nach Auslastungskategorie an:  
  
-   Grünes Häkchen – ![](../../relational-databases/manage/media/well-utilized.gif "Well_utilized") : Anzahl der Datenebenenanwendungen, die nicht gegen Richtlinien zur Ressourcennutzung verstoßen. Die Ressourcen sind normal ausgelastet.  
  
-   Grüner Pfeil nach unten – ![](../../relational-databases/manage/media/utility-down-arrow.gif "Utility_down_arrow") : Die Ressourcen sind unterausgelastet.  
  
-   Roter Pfeil nach oben – ![](../../relational-databases/manage/media/utility-up-arrow.gif "Utility_up_arrow") : Die Ressourcen sind überausgelastet.  
  
 Die Abfolge der Spalten in der Listenansicht kann geändert werden, indem Sie sie nach links oder nach rechts ziehen. Sie können Spalten in der Listenansicht hinzufügen oder löschen, indem Sie mit der rechten Maustaste auf die Spaltenüberschriften klicken und die Spalten auswählen bzw. deren Auswahl aufheben. Darüber hinaus enthält das Kontextmenü Sortieroptionen. Die Sortierung kann auch aktiviert werden, indem Sie oben auf den Spaltennamen klicken.  
  
 Um auf Filteroptionen für die Listenansicht des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms zuzugreifen, klicken Sie mit der rechten Maustaste auf den Knoten **Bereitgestellte Datenebenenanwendungen** im Navigationsbereich des Hilfsprogramm-Explorers, und wählen Sie **Filtern**aus. Nachdem die Filtereinstellungen implementiert wurden, hat der Knoten **Bereitgestellte Datenebenenanwendungen** im Hilfsprogramm-Explorer die Beschriftung **Bereitgestellte Datenebenenanwendungen (gefiltert)**. Weitere Informationen finden Sie unter [Filtereinstellungen &#40;Objekt-Explorer und Hilfsprogramm-Explorer&#41;](http://msdn.microsoft.com/library/4aab04bc-e1ab-4d4b-ab74-b287fc805bc2).  
  
 In den folgenden Spalten werden standardmäßig Zustandsinformationen zu den einzelnen Datenebenenanwendungen angezeigt.  
  
-   Name – Der Name der Datenebenenanwendung.  
  
-   Anwendungs-CPU – Zeigt den Zustand der Prozessorauslastung für diese Datenebenenanwendung an. Der Zustand dieses Parameters wird anhand der Richtlinie zur CPU-Auslastung bestimmt, die für die Datenebenenanwendung festgelegt wurde, und anhand der Konfigurationseinstellung der Auswertungsrichtlinie für veränderliche Ressourcen. Weitere Informationen finden Sie unter [ Reduzieren von Informationsrauschen bei Richtlinien zur CPU-Auslastung &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Um den Verlauf der Prozessorauslastung für diese Datenebenenanwendung anzuzeigen bzw. die Richtliniengrenzwerte einzusehen oder zu ändern, klicken Sie auf die Registerkarte **CPU-Auslastung**.  
  
-   Computer-CPU: Zeigt den Zustand der Prozessorauslastung für den Computer an. Der Zustand dieses Parameters wird anhand der Richtlinie zur CPU-Auslastung bestimmt, die für den Computer festgelegt wurde, und anhand der Konfigurationseinstellung der Auswertungsrichtlinie für veränderliche Ressourcen. Weitere Informationen finden Sie unter [ Reduzieren von Informationsrauschen bei Richtlinien zur CPU-Auslastung &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Um den Verlauf der Prozessorauslastung für diese Datenebenenanwendung anzuzeigen bzw. die Richtliniengrenzwerte einzusehen oder zu ändern, klicken Sie auf die Registerkarte **CPU-Auslastung**.  
  
-   Dateispeicherplatz – Zeigt eine Zusammenfassung der Zustände der Dateispeicherplatzauslastung für die einzelnen Datenebenenanwendungen an.  
  
    -   Grünes Häkchen – Die Zustände für alle Dateigruppen und die Protokolldateigruppe sind weder überausgelastet noch unterausgelastet.  
  
    -   Grüner Pfeil nach unten – Der Zustand für mindestens eine Dateigruppe oder Protokolldateigruppe ist unterausgelastet, und keine Dateigruppe oder Protokolldateigruppe ist überausgelastet.  
  
    -   Roter Pfeil nach oben – Der Integritätsstatus für mindestens eine Dateigruppe oder die Protokolldateigruppe ist überausgelastet. Wenn eine Datenbank den Status "Notfall" aufweist, wird für den Integritätsstatus ein überausgelasteter Protokolldateispeicherplatz angezeigt.  
  
     Um die Richtliniengrenzwerte für den Dateispeicherplatz anzuzeigen oder zu ändern, klicken Sie auf die Registerkarte **Speicherauslastung** .  
  
-   Volumespeicherplatz – Zeigt eine Zusammenfassung der Zustände der Volumespeicherplatzauslastung für alle Volumes mit Datenbanken an, die der ausgewählten Datenebenenanwendung angehören. Wenn der Zustand eines beliebigen Volumes überausgelastet ist, dann wird der Zustand des Volumespeicherplatzes in der Listenansicht als überausgelastet angezeigt. Wenn der Zustand eines beliebigen Volumes unterausgelastet und kein Volume überausgelastet ist, wird der Zustand des Volumespeicherplatzes in der Listenansicht als unterausgelastet angezeigt. Andernfalls wird der Zustand des Volumespeicherplatzes in der Listenansicht als normal angezeigt. Um die Richtliniengrenzwerte anzuzeigen oder zu ändern, klicken Sie auf die Registerkarte **Speicherauslastung** .  
  
-   Richtlinientyp – Gibt an, ob Standardrichtlinien (vom Typ "Global") oder benutzerdefinierte Richtlinien (vom Typ "Überschreibung") für die Datenebenenanwendung wirksam sind.  
  
-   Instanzname – Gibt den Namen der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, die die Datenebenenanwendung hostet.  
  
 Weitere Spalten können über das Kontextmenü im Spaltenüberschriftenbereich der Listenansicht angezeigt werden:  
  
-   Datenbankname  
  
-   Bereitstellungsdatum  
  
-   Vertrauenswürdig: (True oder False)  
  
-   Sortierung  
  
-   Kompatibilitätsgrad: (z. B. Version100)  
  
-   Verschlüsselung aktiviert: (True oder False)  
  
-   Wiederherstellungsmodell: (SIMPLE, FULL oder BULK_LOGGED)  
  
-   Letzter Berichtszeitpunkt: Diese Spalte zeigt das lokale Datum und die lokale Uhrzeit des UCPs unter Verwendung des datetime-Datentyps an. Weitere Informationen finden Sie unter dem Thema [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) . Beachten Sie bei Verwendung des Hilfsprogramm-Objektmodells, dass SSMS den datetimeoffset-Datentyp verwendet. Weitere Informationen finden Sie unter dem Thema [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 Registerkarte CPU-Auslastung  
 Die Registerkarte CPU-Auslastung enthält Vergleichsdiagramme mit Verlaufsdaten für die Datenebenenanwendung und die CPU-Auslastung des Computers.  
  
 Das Diagramm enthält Verlaufsdaten zur Prozessorauslastung. Diese beziehen sich auf den Zeitraum, der mithilfe der Optionsfelder auf der rechten Seite des Anzeigebereichs festgelegt wurde. Um das Anzeigeintervall zu ändern und das Dataset zu aktualisieren, aktivieren Sie ein Optionsfeld aus der Liste.  
  
 Folgende Intervalloptionen stehen zur Verfügung:  
  
-   1 Tag, in Intervallen von 15 Minuten  
  
-   1 Woche, in Intervallen von 1 Tag  
  
-   1 Monat, in Intervallen von 1 Woche  
  
-   1 Jahr, in Intervallen von 1 Monat  
  
 Registerkarte Speicherauslastung  
 Die Registerkarte Speicherauslastung verfügt über eine Strukturansicht, in der Details zur Speicherauslastung für Datenbankdateien und Protokolldateien angezeigt werden, die zu der in der Listenansicht ausgewählten Datenebenenanwendung gehören. Die Zeitangaben zeigen das lokale Datum und die lokale Uhrzeit des UCPs unter Verwendung des datetime-Datentyps an. Weitere Informationen finden Sie unter dem Thema [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) . Beachten Sie bei Verwendung des Hilfsprogramm-Objektmodells, dass SSMS den datetimeoffset-Datentyp verwendet. Weitere Informationen finden Sie unter dem Thema [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 Die Anzeige kann nach Dateigruppe oder nach Volume gruppiert werden. Um die Strukturansicht für Dateigruppen zu verwenden, aktivieren Sie im Bereich **Dateien gruppieren nach** das Optionsfeld **Dateigruppe** .  
  
 Welche Daten im Diagramm mit Verlaufsdaten zur Speicherauslastung angezeigt werden, hängt von dem Knoten ab, der in der Strukturansicht ausgewählt ist:  
  
-   Wählen Sie den Dateigruppenknoten aus, um den Dateispeicherplatz, der von allen Datendateien der ausgewählten Dateigruppe belegt wird, in einem Diagramm darzustellen.  
  
-   Wählen Sie den Protokolldateiknoten aus, um den Dateispeicherplatz, der von allen Protokolldateien der ausgewählten Datenbank belegt wird, in einem Diagramm darzustellen.  
  
-   Wählen Sie den Datenbankknoten aus, um ein Diagramm anzuzeigen, in dem der Dateispeicherplatz addiert wird, der von allen Datendateien und Protokolldateien belegt wird, die der ausgewählten Datenbank angehören.  
  
 Um den Status der Speicherauslastung für einzelne Dateien anzuzeigen, klicken Sie neben einem Dateinamen in der Strukturansicht auf das Pluszeichen.  
  
 Zustandssymbole liefern auf einen Blick Statusinformationen zu den einzelnen Dateigruppen in Relation zu Richtlinienschwellenwerten:  
  
-   Grünes Häkchen – Die Auslastung des Dateispeicherplatzes für mindestens eine Datendatei in der Dateigruppe ist weder überausgelastet noch unterausgelastet.  
  
-   Grüner Pfeil nach unten – Die Auslastung des Dateispeicherplatzes für mindestens eine Datendatei in der Dateigruppe ist unterausgelastet, und keine Dateien in der Dateigruppe sind überausgelastet.  
  
-   Roter Pfeil nach oben – Die Auslastung des Dateispeicherplatzes für alle Datendateien in der Dateigruppe ist überausgelastet. Wenn eine Datenbank den Status "Notfall" aufweist, wird für den Integritätsstatus ein überausgelasteter Protokolldateispeicherplatz angezeigt.  
  
 Um die Dateien nach Volume anzuzeigen, aktivieren Sie im Auswahlbereich **Dateien gruppieren nach** das Optionsfeld **Volume** . Im Diagramm mit Verlaufsdaten zur Speicherplatzauslastung wird der Dateispeicherplatz dargestellt, der von allen Datendateien und Protokolldateien auf dem Speichervolume belegt wird. Erweitern Sie die Struktur, um Details zu einzelnen Datenbankdatendateien und Protokolldateien anzuzeigen.  
  
 Statussymbole werden verwendet, um den Status der einzelnen Volumes anzuzeigen:  
  
-   Grünes Häkchen – Die Ressourcen sind normal ausgelastet.  
  
-   Grüner Pfeil nach unten – Die Ressourcen sind unterausgelastet.  
  
-   Roter Pfeil nach oben – Die Ressourcen sind überausgelastet.  
  
 Das Messgerät neben den einzelnen Dateinamen auf der Registerkarte Speicherauslastung zeigt die Speicherplatzkapazität an, die von der Datei relativ zur effektiven Kapazität der Datei belegt wird. Der neben dem Messgerät angezeigte Prozentwert gibt das Verhältnis des von der Datei belegten Speicherplatzes relativ zur effektiven Kapazität der Datei an. QuickInfos liefern Informationen, die zur Berechnung der Prozentwerte für jedes Volume und jede Datei im Vergleich zu deren effektiven Kapazität verwendet werden.  
  
 Wenn die Datei nicht für die automatische Vergrößerung konfiguriert ist, entspricht die effektive Kapazität der Speicherplatzkapazität, die der Datei zugewiesen ist. Wenn die Datei für die automatische Vergrößerung konfiguriert ist, entspricht die effektive Kapazität der Summe aus dem Speicherplatz, der derzeit von der Datei belegt wird, und dem freien Speicherplatz, der derzeit auf dem Volume verfügbar ist.  
  
 Richtlinien zur Speicherauslastung können für Datendateien und Protokolldateien konfiguriert werden. Um die Schwellenwerte der Richtlinien zur Speicherauslastung anzuzeigen oder zu ändern, klicken Sie auf den Link **Dateirichtlinie** unten im Bereich Speicherauslastung. Um die Schwellenwerte der Richtlinien zur Speicherauslastung für ein Speichervolume anzuzeigen oder zu ändern, klicken Sie auf den Link **Volumerichtlinie** unten im Bereich Speicherauslastung.  
  
 Um die Schwellenwerte für Standardrichtlinien zu überschreiben, klicken Sie auf das Optionsfeld **Standardrichtlinie überschreiben**, geben obere und untere Grenzwerte ein und klicken dann auf **OK**.  
  
 Weitere Informationen zum Ändern der Toleranz für Richtlinienverstöße finden Sie unter [Reduzieren von Informationsrauschen bei Richtlinien zur CPU-Auslastung &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
 Registerkarte Eigenschaftendetails  
 Die für Datenebenenanwendungen aufgeführten Eigenschaftendetails umfassen die folgenden Kategorien:  
  
-   Datenbankname  
  
-   Bereitstellungsdatum  
  
-   Vertrauenswürdig: (True oder False)  
  
-   Sortierung  
  
-   Kompatibilitätsgrad: (z. B. Version100)  
  
-   Verschlüsselung aktiviert: (True oder False)  
  
-   Wiederherstellungsmodell: (SIMPLE, FULL oder BULK_LOGGED)  
  
-   Letzter Berichtszeitpunkt: Diese Spalte zeigt das lokale Datum und die lokale Uhrzeit des UCPs unter Verwendung des datetime-Datentyps an. Weitere Informationen finden Sie unter dem Thema [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) . Beachten Sie bei Verwendung des Hilfsprogramm-Objektmodells, dass SSMS den datetimeoffset-Datentyp verwendet. Weitere Informationen finden Sie unter dem Thema [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) .

## <a name="managed-instance-details-sql-server-utility"></a>Details zu verwalteten Instanzen (SQL Server-Hilfsprogramm)
 Die Informationen in der Listenansicht Verwaltete Instanzen des Hilfsprogramm-Explorers enthalten Auslastungsdaten für einzelne Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Verlaufsdaten zur CPU-Auslastung sowie Details zur Speicherplatzauslastung auf Dateiebene. Zudem können Sie hier Richtlinienschwellenwerte anzeigen und aktualisieren. Richtlinienschwellenwerte können auf der Ebene von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen, per Computer, für Datenbank- und Protokolldateien sowie auf der Ebene von Speichervolumes gesteuert werden. Darüber hinaus können Sie Eigenschaftendetails für einzelne verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]anzeigen.  
  
### <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 Listenansicht  
 Die Listenansicht im oberen Bereich enthält Daten zu einzelnen Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die zeilenweise nach ComputerName\InstanceName aufgeführt sind.  
  
 Zustandssymbole zeigen den Zusammenfassungsstatus für die einzelnen Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nach Auslastungskategorie an:  
  
-   Grünes Häkchen – ![](../../relational-databases/manage/media/well-utilized.gif "Well_utilized") : Anzahl der verwalteten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die nicht gegen Richtlinien zur Ressourcennutzung verstoßen. Die Ressourcen sind normal ausgelastet.  
  
-   Grüner Pfeil nach unten – ![](../../relational-databases/manage/media/utility-down-arrow.gif "Utility_down_arrow") : Die Ressourcen sind unterausgelastet.  
  
-   Roter Pfeil nach oben – ![](../../relational-databases/manage/media/utility-up-arrow.gif "Utility_up_arrow") : Die Ressourcen sind überausgelastet.  
  
 Die Abfolge der Spalten in der Listenansicht kann geändert werden, indem Sie sie nach links oder nach rechts ziehen. Sie können Spalten in der Listenansicht hinzufügen oder löschen, indem Sie mit der rechten Maustaste auf die Spaltenüberschriften klicken und die Spalten auswählen bzw. deren Auswahl aufheben. Darüber hinaus enthält das Kontextmenü Sortieroptionen. Die Sortierung kann auch aktiviert werden, indem Sie oben auf den Spaltennamen klicken.  
  
 Um auf Filteroptionen für die Listenansicht des Hilfsprogramms zuzugreifen, klicken Sie mit der rechten Maustaste im Navigationsbereich des Hilfsprogramm-Explorers auf den Knoten **Verwaltete Instanzen** und wählen **Filtern**aus. Nachdem die Filtereinstellungen implementiert wurden, hat der Knoten **Verwaltete Instanzen** im Hilfsprogramm-Explorer die Beschriftung **Verwaltete Instanzen (gefiltert)**. Weitere Informationen finden Sie unter [Filtereinstellungen &#40;Objekt-Explorer und Hilfsprogramm-Explorer&#41;](http://msdn.microsoft.com/library/4aab04bc-e1ab-4d4b-ab74-b287fc805bc2).  
  
 Die folgenden Spalten enthalten standardmäßig Zustandsinformationen zu den einzelnen verwalteten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Instanz-CPU: Zeigt den Zustand der Prozessorauslastung für diese Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]an. Der Zustand dieses Parameters wird anhand der Richtlinie zur CPU-Auslastung bestimmt, die für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] festgelegt wurde, und anhand der Konfigurationseinstellung der Auswertungsrichtlinie für veränderliche Ressourcen. Weitere Informationen finden Sie unter [ Reduzieren von Informationsrauschen bei Richtlinien zur CPU-Auslastung &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Um den Verlauf der Prozessorauslastung für diese Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]anzuzeigen bzw. die Richtliniengrenzwerte einzusehen oder zu ändern, klicken Sie auf die Registerkarte **CPU-Auslastung** .  
  
-   Computer-CPU: Zeigt den Zustand der Prozessorauslastung für den Computer an. Der Zustand dieses Parameters wird anhand der Richtlinie zur CPU-Auslastung bestimmt, die für den Computer festgelegt wurde, und anhand der Konfigurationseinstellung der Auswertungsrichtlinie für veränderliche Ressourcen. Weitere Informationen finden Sie unter [ Reduzieren von Informationsrauschen bei Richtlinien zur CPU-Auslastung &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Um den Verlauf der Prozessorauslastung für diese Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]anzuzeigen bzw. die Richtliniengrenzwerte einzusehen oder zu ändern, klicken Sie auf die Registerkarte **CPU-Auslastung** .  
  
-   Dateispeicherplatz: Zeigt eine Zusammenfassung der Zustände der Dateispeicherplatzauslastung für alle Datenbanken an, die der ausgewählten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angehören. Wenn der Zustand einer beliebigen Datenbank überausgelastet ist, wird der Zustand des Dateispeicherplatzes in der Listenansicht als überausgelastet angezeigt. Wenn der Zustand einer beliebigen Datenbank unterausgelastet und keine Datenbank überausgelastet ist, wird der Zustand des Dateispeicherplatzes in der Listenansicht als unterausgelastet angezeigt. Andernfalls wird der Zustand des Dateispeicherplatzes in der Listenansicht als normal angezeigt. Um die Richtliniengrenzwerte anzuzeigen oder zu ändern, klicken Sie auf die Registerkarte **Speicherauslastung** .  
  
-   Volumespeicherplatz – Zeigt eine Zusammenfassung der Zustände der Volumespeicherplatzauslastung für alle Volumes mit Datenbanken an, die der ausgewählten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angehören. Wenn der Zustand eines beliebigen Volumes überausgelastet ist, dann wird der Zustand des Volumespeicherplatzes in der Listenansicht als überausgelastet angezeigt. Wenn der Zustand eines beliebigen Volumes unterausgelastet und kein Volume überausgelastet ist, wird der Zustand des Volumespeicherplatzes in der Listenansicht als unterausgelastet angezeigt. Andernfalls wird der Zustand des Volumespeicherplatzes in der Listenansicht als normal angezeigt. Um die Richtliniengrenzwerte anzuzeigen oder zu ändern, klicken Sie auf die Registerkarte **Speicherauslastung** .  
  
-   Richtlinientyp – Gibt an, ob Standardrichtlinien (vom Typ "Global") oder benutzerdefinierte Richtlinien (vom Typ "Überschreibung") für die verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wirksam sind.  
  
 Weitere Spalten können über das Kontextmenü im Spaltenüberschriftenbereich der Listenansicht angezeigt werden:  
  
-   Prozessorname:  
  
-   Prozessorgeschwindigkeit (MHz):  
  
-   Prozessoranzahl:  
  
-   Physischer Speicher (MB):  
  
-   Betriebssystemversion:  
  
-   SQL Server-Version:  
  
-   SQL Server-Edition:  
  
-   Gruppiert: (True oder False)  
  
-   Sicherungsverzeichnis:  
  
-   Sortierung:  
  
-   Unterscheidung nach Groß-/Kleinschreibung (True oder False)  
  
-   Sprache:  
  
-   Letzter Berichtszeitpunkt: Diese Spalte zeigt das lokale Datum und die lokale Uhrzeit des UCPs unter Verwendung des datetime-Datentyps an. Weitere Informationen finden Sie unter dem Thema [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) . Beachten Sie bei Verwendung des Hilfsprogramm-Objektmodells, dass SSMS den datetimeoffset-Datentyp verwendet. Weitere Informationen finden Sie unter dem Thema [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 Registerkarte CPU-Auslastung  
 Die Registerkarte CPU-Auslastung enthält Vergleichsdiagramme mit Verlaufsdaten für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz und die CPU-Auslastung des Computers.  
  
 Das Diagramm enthält Verlaufsdaten zur Prozessorauslastung. Diese beziehen sich auf den Zeitraum, der mithilfe der Optionsfelder auf der rechten Seite des Anzeigebereichs festgelegt wurde. Um das Anzeigeintervall zu ändern und das Dataset zu aktualisieren, aktivieren Sie ein Optionsfeld aus der Liste.  
  
 Folgende Intervalloptionen stehen zur Verfügung:  
  
-   1 Tag, in Intervallen von 15 Minuten  
  
-   1 Woche, in Intervallen von 1 Tag  
  
-   1 Monat, in Intervallen von 1 Woche  
  
-   1 Jahr, in Intervallen von 1 Monat  
  
 Registerkarte Speicherauslastung  
 Die Registerkarte Speicherauslastung verfügt über eine Strukturansicht, in der Details zur Speicherauslastung angezeigt werden. Die Zeitangaben zeigen das lokale Datum und die lokale Uhrzeit des UCPs unter Verwendung des datetime-Datentyps an. Weitere Informationen finden Sie unter dem Thema [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) . Beachten Sie bei Verwendung des Hilfsprogramm-Objektmodells, dass SSMS den datetimeoffset-Datentyp verwendet. Weitere Informationen finden Sie unter dem Thema [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 Die Informationen in der Anzeige können nach Datenbank oder nach Volume gruppiert werden. Um die Datenbankstrukturansicht zu verwenden, aktivieren Sie im Auswahlbereich **Dateien gruppieren nach** das Optionsfeld **Datenbank** . Um den Status der Speicherauslastung für einzelne Datenbankdateien anzuzeigen, klicken Sie neben einem Datenbanknamen in der Strukturansicht auf das Pluszeichen. Die aufgeführten Datenbankdateien enthalten alle System- und Benutzerdatenbanken, die der verwalteten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angehören, die Sie in der Listenansicht ausgewählt haben.  
  
 Die Baumstruktur entspricht der Speicherhierarchie. Der Stammknoten in der Strukturansicht entspricht der Datenbank. Die nächste Ebene der Strukturansicht enthält einen Dateigruppenknoten oder Knoten, die zur Datenbank gehören, sowie einen Protokolldateiknoten für die Protokolle, die der Datenbank zugeordnet sind. Die nächste Ebene enthält die Datendateien, die zur Dateigruppe gehören.  
  
 Welche Daten im Diagramm mit Verlaufsdaten zur Speicherauslastung angezeigt werden, hängt von dem Knoten ab, der in der Strukturansicht ausgewählt ist:  
  
-   Wählen Sie den Dateigruppenknoten aus, um den Dateispeicherplatz, der von allen Datendateien der ausgewählten Dateigruppe belegt wird, in einem Diagramm darzustellen.  
  
-   Wählen Sie den Protokolldateiknoten aus, um den Dateispeicherplatz, der von allen Protokolldateien der ausgewählten Datenbank belegt wird, in einem Diagramm darzustellen.  
  
-   Wählen Sie den Datenbankknoten aus, um ein Diagramm anzuzeigen, in dem der Dateispeicherplatz addiert wird, der von allen Datendateien und Protokolldateien belegt wird, die der ausgewählten Datenbank angehören.  
  
 Zustandssymbole liefern auf einen Blick Statusinformationen zu Datenbankdateien, Dateigruppen und Protokolldateien:  
  
 Datenbanken:  
  
-   Grünes Häkchen – Die Zustände aller Dateigruppen und Protokolldateien sind weder überausgelastet noch unterausgelastet.  
  
-   Grüner Pfeil nach unten – Der Zustand mindestens einer Dateigruppe oder Protokolldatei ist unterausgelastet, und keine Zustände sind überausgelastet.  
  
-   Roter Pfeil nach oben – Der Zustand mindestens einer Dateigruppe oder Protokolldatei ist überausgelastet.  
  
 Dateigruppen und Protokolldateien:  
  
-   Grünes Häkchen – Die Auslastung des Dateispeicherplatzes für alle Dateien in der Dateigruppe ist weder überausgelastet noch unterausgelastet.  
  
-   Grüner Pfeil nach unten – Die Auslastung des Dateispeicherplatzes für mindestens eine Datei in der Dateigruppe ist unterausgelastet, und keine Dateien in der Dateigruppe sind überausgelastet.  
  
-   Roter Pfeil nach oben – Die Auslastung des Dateispeicherplatzes für alle Datendateien in der Dateigruppe ist überausgelastet.  
  
 Um die Dateien nach Volume anzuzeigen, aktivieren Sie im Auswahlbereich **Dateien gruppieren nach** das Optionsfeld **Volume** . Im Diagramm mit Verlaufsdaten zur Speicherplatzauslastung wird der Dateispeicherplatz dargestellt, der von allen Datendateien und Protokolldateien auf dem Speichervolume belegt wird. Erweitern Sie die Struktur, um Details zu einzelnen Datenbankdatendateien und Protokolldateien anzuzeigen.  
  
 Statussymbole werden verwendet, um den Status der einzelnen Volumes anzuzeigen:  
  
-   Grünes Häkchen – Die Ressourcen sind normal ausgelastet.  
  
-   Grüner Pfeil nach unten – Die Ressourcen sind unterausgelastet.  
  
-   Roter Pfeil nach oben – Die Ressourcen sind überausgelastet.  
  
 Das Messgerät neben den einzelnen Dateinamen auf der Registerkarte Speicherauslastung zeigt die Speicherplatzkapazität an, die von der Datei relativ zur effektiven Kapazität der Datei belegt wird. Der neben dem Messgerät angezeigte Prozentwert gibt das Verhältnis des von der Datei belegten Speicherplatzes relativ zur effektiven Kapazität der Datei an. QuickInfos liefern Informationen, die zur Berechnung der Prozentwerte für jedes Volume und jede Datei im Vergleich zu deren effektiven Kapazität verwendet werden.  
  
 Wenn die Datei nicht für die automatische Vergrößerung konfiguriert ist, entspricht die effektive Kapazität der Speicherplatzkapazität, die der Datei zugewiesen ist. Wenn die Datei für die automatische Vergrößerung konfiguriert ist, entspricht die effektive Kapazität der Summe aus dem Speicherplatz, der derzeit von der Datei belegt wird, und dem freien Speicherplatz, der derzeit auf dem Volume verfügbar ist.  
  
 Richtlinien zur Speicherauslastung können für Datendateien und Protokolldateien konfiguriert werden. Um die Schwellenwerte der Richtlinien zur Speicherauslastung anzuzeigen oder zu ändern, klicken Sie auf den Link **Dateirichtlinie** unten im Bereich Speicherauslastung. Um die Schwellenwerte der Richtlinien zur Speicherauslastung für ein Speichervolume anzuzeigen oder zu ändern, klicken Sie auf den Link **Volumerichtlinie** unten im Bereich Speicherauslastung.  
  
 Um die Schwellenwerte für Standardrichtlinien zu überschreiben, klicken Sie auf das Optionsfeld **Standardrichtlinie überschreiben**, geben obere und untere Grenzwerte ein und klicken dann auf **OK**.  
  
 Weitere Informationen zum Ändern der Toleranz für Richtlinienverstöße finden Sie unter [Reduzieren von Informationsrauschen bei Richtlinien zur CPU-Auslastung &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
 Registerkarte Eigenschaftendetails  
 Die für Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgeführten Eigenschaftendetails umfassen die folgenden Kategorien:  
  
-   Prozessorname:  
  
-   Prozessorgeschwindigkeit (MHz):  
  
-   Prozessoranzahl:  
  
-   Physischer Speicher (MB):  
  
-   Betriebssystemversion:  
  
-   SQL Server-Version:  
  
-   SQL Server-Edition:  
  
-   Gruppiert: (True oder False)  
  
-   Sicherungsverzeichnis:  
  
-   Sortierung:  
  
-   Unterscheidung nach Groß-/Kleinschreibung (True oder False)  
  
-   Sprache:  

## <a name="utility-administration-sql-server-utility"></a>Hilfsprogrammverwaltung (SQL Server-Hilfsprogramm)
Verwenden Sie die Registerkarten der Hilfsprogrammverwaltung zum Verwalten von Richtlinien-, Sicherheits- und Data Warehouse-Einstellungen für ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm. Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogrammkonzepten finden Sie unter [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
### <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente
 **Registerkarte Richtlinie** Verwenden Sie die Registerkarte Richtlinie, um globale Überwachungsrichtlinien anzuzeigen oder anzugeben.  
  
 Legen Sie globale Überwachungsrichtlinien für Datenebenenanwendungen fest. Um die Werteliste für diese Option zu erweitern, klicken Sie neben dem Richtliniennamen auf den Pfeil, oder klicken Sie auf den Richtlinientitel.  
 Wann wird die Prozessorkapazität für eine Anwendung knapp? Zum Ändern dieser Richtlinie verwenden Sie das Steuerelement rechts neben der Richtlinienbeschreibung, und klicken Sie auf **Anwenden**. Mithilfe der Schaltflächen unten in der Anzeige können Sie auch Standardwerte wiederherstellen oder Änderungen verwerfen.  
  
-   Der maximale Standardwert für die Prozessorauslastung beträgt 70 %.  
  
-   Der minimale Standardwert für die Prozessorauslastung beträgt 0 %.  
  
 Wann wird der Dateispeicherplatz für eine Anwendung knapp? Um die Richtlinie zur Speicherplatzauslastung einer Daten- oder Protokolldatei zu ändern, verwenden Sie das Steuerelement rechts neben der Richtlinienbeschreibung, und klicken Sie auf **Anwenden**. Mithilfe der Schaltflächen unten in der Anzeige können Sie auch Standardwerte wiederherstellen oder Änderungen verwerfen.  
  
-   Der maximale Standardwert für die Auslastung des Dateispeicherplatzes beträgt 70 %.  
  
-   Der minimale Standardwert für die Auslastung des Dateispeicherplatzes beträgt 0 %.  
  
 Legen Sie globale Überwachungsrichtlinien für verwaltete Instanzen von SQL Server fest. Um die Werteliste für diese Option zu erweitern, klicken Sie neben dem Richtliniennamen auf den Pfeil, oder klicken Sie auf den Richtlinientitel.  
 Wann wird die Prozessorkapazität für eine verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] knapp? Zum Ändern dieser Richtlinie verwenden Sie das Steuerelement rechts neben der Richtlinienbeschreibung, und klicken Sie auf **Anwenden**. Mithilfe der Schaltflächen unten in der Anzeige können Sie auch Standardwerte wiederherstellen oder Änderungen verwerfen.  
  
-   Der maximale Standardwert für die Prozessorauslastung von Instanzen beträgt 70 %.  
  
-   Der minimale Standardwert für die Prozessorauslastung von Instanzen beträgt 0 %.  
  
 Wann wird die Prozessorkapazität auf einem Computer mit einer verwalteten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] knapp? Zum Ändern dieser Richtlinie verwenden Sie das Steuerelement rechts neben der Richtlinienbeschreibung, und klicken Sie auf **Anwenden**. Mithilfe der Schaltflächen unten in der Anzeige können Sie auch Standardwerte wiederherstellen oder Änderungen verwerfen.  
  
-   Der maximale Standardwert für die Prozessorauslastung von Computern beträgt 70 %.  
  
-   Der minimale Standardwert für die Prozessorauslastung von Computern beträgt 0 %.  
  
 Wann wird der Dateispeicherplatz für eine verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] knapp? Um die Richtlinie zur Speicherplatzauslastung einer Daten- oder Protokolldatei zu ändern, verwenden Sie das Steuerelement rechts neben der Richtlinienbeschreibung, und klicken Sie auf **Anwenden**. Mithilfe der Schaltflächen unten in der Anzeige können Sie auch Standardwerte wiederherstellen oder Änderungen verwerfen.  
  
-   Der maximale Standardwert für die Auslastung des Dateispeicherplatzes beträgt 70 %.  
  
-   Der minimale Standardwert für die Auslastung des Dateispeicherplatzes beträgt 0 %.  
  
 Wann wird die Speichervolumekapazität auf einem Computer mit einer verwalteten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] knapp? Zum Ändern dieser Richtlinie verwenden Sie das Steuerelement rechts neben der Richtlinienbeschreibung, und klicken Sie auf **Anwenden**. Mithilfe der Schaltflächen unten in der Anzeige können Sie auch Standardwerte wiederherstellen oder Änderungen verwerfen.  
  
-   Der maximale Standardwert für die Auslastung des Volumespeicherplatzes auf einem Computer beträgt 70 %.  
  
-   Der minimale Standardwert für die Auslastung des Volumespeicherplatzes auf einem Computer beträgt 0 %.  
  
 Reduzieren von Informationsrauschen aufgrund von Richtlinienverstößen bei stark veränderlichen Ressourcen. Um weitere Steuerelemente für diese Funktion anzuzeigen, klicken Sie rechts in der Anzeige auf den nach unten weisenden Pfeil.  
 Weitere Informationen finden Sie unter [ Reduzieren von Informationsrauschen bei Richtlinien zur CPU-Auslastung &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
 
**Registerkarte Sicherheit** Zeigt Anmeldenamen mit Berechtigungen zum Verwalten oder Lesen von Informationen aus dem UCP an.  
  
 Wählen Sie die Anmeldenamen aus dem UCP aus, die der Hilfsprogrammleser-Rolle hinzugefügt werden.  
 Die Hilfsprogrammleser-Berechtigung ermöglicht folgende Aktionen unter dem Benutzerkonto:  
  
-   Herstellen einer Verbindung mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm  
  
-   Anzeigen aller Blickpunkte im Hilfsprogramm-Explorer in SSMS  
  
-   Anzeigen der Einstellungen im Knoten Hilfsprogrammverwaltung im Hilfsprogramm-Explorer in SSMS  
  
 Hilfsprogrammadministratoren können SQL Server-Instanzen registrieren und SQL Server-Instanzen aus einem SQL Server-Hilfsprogramm entfernen sowie Richtlinien für verwaltete Instanzen und Verwaltungseinstellungen für den UCP ändern.  
  
 Als Hilfsprogrammadministrator müssen Sie über sysadmin-Berechtigungen für die SQL Server-Instanz verfügen. Um Benutzerkonten für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-UCP hinzuzufügen oder zu ändern, fügen Sie dem Benutzer mithilfe des Objekt-Explorers in SSMS Serveranmeldenamen der UCP-Instanz von SQL Server hinzu. Weitere Informationen finden Sie unter [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md).  
  
 
**Registerkarte Data Warehouse** Zeigt Konfigurationsdetails für das UMDW (Utility Management Data Warehouse) an.  
  
 Datenbeibehaltung  
 Geben Sie die Beibehaltungsdauer von Auslastungsdaten an, die für verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gesammelt wurden. Der Standardzeitraum beträgt ein Jahr. Der Minimalwert beträgt einen Monat. Der längste unterstützte Wert beträgt zwei Jahre.  
  
 Konfigurationsinformationen für das Hilfsprogramm-Data Warehouse  
 Die folgenden Konfigurationseinstellungen sind in dieser Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nicht konfigurierbar:  
  
-   UMDW-Name: Sysutility_mdw_\<GUID>_DATA.  
  
-   Uploadfrequenz für den Sammlungssatz: Alle 15 Minuten  
  
 Das UMDW-Verzeichnis ist konfigurierbar: \<Systemlaufwerk>:\Programme\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\, wobei \<Systemlaufwerk> normalerweise Laufwerk C:\ entspricht. Die Protokolldatei UMDW_\<GUID>_LOG befindet sich im selben Verzeichnis.  
  
> **HINWEIS:** Der Speicherort der UMDW-Datei (sysutility_mdw) kann mithilfe von Detach/Attach oder ALTER DATABASE geändert werden. Es wird empfohlen, ALTER DATABASE zu verwenden. Weitere Informationen zu dieser Einstellung finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 Wiederherstellen vordefinierter Standardwerte  
 Um die Einstellungen auf dieser Registerkarte auf die Standardwerte zurückzusetzen, klicken Sie auf die Schaltfläche **Standardwerte wiederherstellen** und anschließend auf **Anwenden**.  
 
  
## <a name="reference"></a>Verweis  
 [Erstellen eines Steuerungspunkts für das SQL Server-Hilfsprogramm &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)  
  
 [Verbinden mit einem SQL Server-Hilfsprogramm](../../relational-databases/manage/connect-to-a-sql-server-utility.md)  
  
 [Registrieren einer Instanz von SQL Server &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)  
  
 [Konfigurieren von Integritätsrichtlinien &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)  
  
 [Überwachen von SQL Server-Instanzen im SQL Server-Hilfsprogramm](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Problembehandlung beim SQL Server-Hilfsprogramm](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  

