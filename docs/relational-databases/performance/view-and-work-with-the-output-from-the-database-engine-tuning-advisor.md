---
title: Anzeigen und Verwenden der Ausgabe des Datenbankoptimierungsratgebers | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dta.sessionmonitor.f1
- sql13.dta.reports.f1
- sql13.dta.recommendations.f1
- sql13.dta.applyrecommendations.f1
helpviewer_keywords:
- viewing logs
- recommendations [Database Engine Tuning Advisor]
- summary tuning information [SQL Server]
- Database Engine Tuning Advisor [SQL Server], recommendations
- Database Engine Tuning Advisor [SQL Server], logs
- Database Engine Tuning Advisor [SQL Server], viewing output
- Database Engine Tuning Advisor [SQL Server], reports
- logs [SQL Server], tuning
- reports [SQL Server], tuning
- viewing tuning output
ms.assetid: 47f9d9a7-80b0-416d-9d9a-9e265bc190dc
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ce827e3df11e103bced1b62afb2329db9c81e0f4
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="view-and-work-with-the-output-from-the-database-engine-tuning-advisor"></a>Anzeigen und Verwenden der Ausgabe des Datenbankoptimierungsratgebers
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wenn der Datenbankoptimierungsratgeber Datenbanken optimiert, erstellt er Zusammenfassungen, Empfehlungen, Berichte und Optimierungsprotokolle. Sie können die Optimierungsprotokollausgabe dazu verwenden, Probleme bei Optimierungssitzungen des Datenbankoptimierungsratgebers zu beheben. Mithilfe der Zusammenfassungen, Empfehlungen und Berichte können Sie bestimmen, ob Sie Optimierungsempfehlungen implementieren möchten oder die Optimierung fortsetzen möchten, bis Sie die Abfrageleistungsverbesserungen erreicht haben, die Sie für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installation benötigen. Informationen über die Verwendung des Datenbankoptimierungsratgebers zum Erstellen von Arbeitslasten und zum Optimieren einer Datenbank finden Sie unter [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
##  <a name="View"></a> Anzeigen der Optimierungsausgabe  
 Die folgenden Verfahren beschreiben das Anzeigen von Optimierungsempfehlungen, -zusammenfassungen, -berichten und -protokollen mithilfe der grafischen Benutzeroberfläche (GUI, Graphical User Interface) des Datenbankoptimierungsratgebers. Weitere Informationen zu den Benutzeroberflächenoptionen finden Sie später in diesem Thema unter [Benutzeroberflächenbeschreibungen](#UI) .  
  
 Sie können die GUI auch dazu verwenden, die Optimierungsausgabe anzuzeigen, die vom Befehlszeilen-Hilfsprogramm **dta** generiert wird.  
  
> [!NOTE]  
>  Falls Sie das Befehlszeilen-Hilfsprogramm **dta** verwenden und mithilfe des Arguments **-ox** angeben, dass die Ausgabe in eine XML-Datei geschrieben wird, können Sie die XML-Ausgabedatei öffnen und anzeigen, indem Sie im Menü **Datei** von **auf** Datei öffnen [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]klicken. Weitere Informationen finden Sie unter [Use SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be). Informationen zum Befehlszeilen-Hilfsprogramm **dta** finden Sie unter [dta (Hilfsprogramm)](../../tools/dta/dta-utility.md).  
  
#### <a name="to-view-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>So zeigen Sie Optimierungsempfehlungen mithilfe der GUI des Datenbankoptimierungsratgebers an  
  
1.  Optimieren Sie eine Datenbank mithilfe der GUI des Datenbankoptimierungsratgebers oder des Befehlszeilen-Hilfsprogramms **dta** . Weitere Informationen finden Sie unter [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Wenn Sie eine vorhandene Optimierungssitzung verwenden möchten, lassen Sie diesen Schritt aus, und fahren Sie mit Schritt 2 fort.  
  
2.  Starten Sie die grafische Benutzeroberfläche des Datenbankoptimierungsratgebers. Weitere Informationen finden Sie unter [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Wenn Sie Optimierungsempfehlungen für eine vorhandene Optimierungssitzung anzeigen möchten, öffnen Sie die Sitzung, indem Sie im Fenster **Sitzungsmonitor**auf den Sitzungsnamen doppelklicken.  
  
     Wenn die neue Optimierungssitzung fertig gestellt ist oder das Programm die vorhandene Sitzung geladen hat, wird die Seite **Empfehlungen** angezeigt.  
  
3.  Klicken Sie auf der Seite **Empfehlungen** auf **Partitionsempfehlungen** und **Indexempfehlungen** , um Bereiche mit den Ergebnissen der Optimierungssitzung anzuzeigen. Wenn Sie beim Festlegen der Optimierungsoptionen für die Sitzung keine Partitionierung angegeben haben, ist der Bereich **Partitionsempfehlungen** leer.  
  
4.  Verwenden Sie im Bereich **Partitionsempfehlungen** bzw. **Indexempfehlungen** die Bildlaufleisten, um alle Informationen im Raster anzuzeigen.  
  
5.  Deaktivieren Sie **Vorhandene Objekte anzeigen** unten auf der Seite **Empfehlungen** im Registerkartenformat. Dadurch werden im Raster nur die Datenbankobjekte angezeigt, auf die in der Empfehlung verwiesen wird. Verwenden Sie die untere Bildlaufleiste, um die Spalte ganz rechts im Empfehlungsraster anzuzeigen, und klicken Sie auf ein Element in der Spalte **Definition** , um das [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript anzuzeigen oder zu kopieren, das dieses Objekt in der Datenbank erstellt.  
  
6.  Wenn Sie alle [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts, die alle Datenbankobjekte in dieser Empfehlung erstellen oder löschen, in einer Skriptdatei speichern möchten, klicken Sie auf **Empfehlungen speichern** im Menü **Aktion** .  
  
#### <a name="to-view-the-tuning-summary-and-reports-with-the-database-engine-tuning-advisor-gui"></a>So zeigen Sie die Optimierungszusammenfassungen und -berichte mithilfe der GUI des Datenbankoptimierungsratgebers an  
  
1.  Optimieren Sie eine Datenbank mithilfe der GUI des Datenbankoptimierungsratgebers oder des Befehlszeilen-Hilfsprogramms **dta** . Weitere Informationen finden Sie unter [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Wenn Sie eine vorhandene Optimierungssitzung verwenden möchten, lassen Sie diesen Schritt aus, und fahren Sie mit Schritt 2 fort.  
  
2.  Starten Sie die grafische Benutzeroberfläche des Datenbankoptimierungsratgebers. Weitere Informationen finden Sie unter [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Wenn Sie Optimierungszusammenfassungen und -berichte für eine vorhandene Optimierungssitzung anzeigen möchten, öffnen Sie die Sitzung, indem Sie in **Sitzungsmonitor**auf den Sitzungsnamen doppelklicken.  
  
3.  Wenn die neue Optimierungssitzung fertig gestellt ist oder das Programm die vorhandene Sitzung geladen hat, klicken Sie auf die Registerkarte **Berichte** .  
  
4.  Der Bereich **Optimierungszusammenfassung** enthält Informationen über die Optimierungssitzung. Die Informationen, die in den Elementen **Prozentsatz für die erwartete Verbesserung** und **Von der Empfehlung verwendeter Speicherplatz (MB)** bereitgestellt werden, können besonders nützlich sein, wenn Sie entscheiden, ob Sie die Empfehlungen implementieren möchten.  
  
5.  Klicken Sie im Bereich **Optimierungsberichte** auf **Berichte auswählen** , um das Anzeigen eines Optimierungsberichts auszuwählen.  
  
#### <a name="to-view-tuning-logs-with-the-database-engine-tuning-advisor-gui"></a>So zeigen Sie Optimierungsprotokolle mithilfe der GUI des Datenbankoptimierungsratgebers an  
  
1.  Optimieren Sie eine Datenbank mithilfe der GUI des Datenbankoptimierungsratgebers oder des Befehlszeilen-Hilfsprogramms **dta** . Sie müssen **Optimierungsprotokoll speichern** auf der Registerkarte **Allgemein** aktivieren, wenn Sie die Arbeitsauslastung optimieren möchten. Wenn Sie eine vorhandene Optimierungssitzung verwenden möchten, lassen Sie diesen Schritt aus, und fahren Sie mit Schritt 2 fort.  
  
2.  Starten Sie die grafische Benutzeroberfläche des Datenbankoptimierungsratgebers. Weitere Informationen finden Sie unter [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Wenn Sie Optimierungszusammenfassungen und -berichte für eine vorhandene Optimierungssitzung anzeigen möchten, öffnen Sie die Sitzung, indem Sie im Fenster **Sitzungsmonitor** auf den Sitzungsnamen doppelklicken.  
  
3.  Wenn die neue Optimierungssitzung fertig gestellt ist oder das Programm die vorhandene Sitzung geladen hat, klicken Sie auf die Registerkarte **Status** . Im Bereich **Optimierungsprotokoll** wird der Inhalt des Protokolls angezeigt. Das Protokoll enthält Informationen über Arbeitsauslastungsereignisse, die der Datenbankoptimierungsratgeber nicht analysieren konnte.  
  
     Wenn alle Ereignisse in der Optimierungssitzung vom Datenbankoptimierungsratgeber analysiert wurden, wird eine Meldung angezeigt, die angibt, dass das Optimierungsprotokoll für die Sitzung leer ist. Wenn **Optimierungsprotokoll speichern** auf der Registerkarte **Allgemein** nicht aktiviert wurde, als die Optimierungssitzung ursprünglich ausgeführt wurde, wird dies in einer Meldung angezeigt.  
  
##  <a name="Implement"></a> Implementieren von Optimierungsempfehlungen  
 Die Empfehlungen des Datenbankoptimierungsratgebers können manuell oder im Rahmen der Optimierungssitzung automatisch implementiert werden. Wenn Sie die Optimierungsergebnisse vor der Implementierung noch überprüfen möchten, verwenden Sie die GUI des Datenbankoptimierungsratgebers. Anschließend können Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwenden, um die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts, die der Datenbankoptimierungsratgeber als Ergebnis der Analyse einer Arbeitsauslastung ausgibt, manuell auszuführen und die Empfehlungen zu implementieren. Falls Sie die Ergebnisse nicht überprüfen müssen, bevor Sie sie implementieren, können Sie die Option **-a** mit dem Eingabeaufforderungs-Hilfsprogramm **dta** verwenden. Dadurch werden die Optimierungsempfehlungen automatisch vom Hilfsprogramm implementiert, nachdem Ihre Arbeitslast analysiert wurde. Im Rahmen der folgenden Verfahren wird erklärt, wie die beiden Oberflächen des Datenbankoptimierungsratgebers bei der Implementierung der Optimierungsempfehlungen verwendet werden.  
  
#### <a name="to-manually-implement-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>So implementieren Sie die Optimierungsempfehlungen manuell über die grafische Benutzeroberfläche des Datenbankoptimierungsratgebers  
  
1.  Optimieren Sie eine Datenbank über die grafische Benutzeroberfläche des Datenbankoptimierungsratgebers oder das Eingabeaufforderungs-Hilfsprogramm **dta** . Weitere Informationen finden Sie unter [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Wenn Sie eine vorhandene Optimierungssitzung verwenden möchten, lassen Sie diesen Schritt aus, und fahren Sie mit Schritt 2 fort.  
  
2.  Starten Sie die grafische Benutzeroberfläche des Datenbankoptimierungsratgebers. Weitere Informationen finden Sie unter [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Wenn Sie Optimierungsempfehlungen für eine vorhandene Optimierungssitzung implementieren möchten, öffnen Sie diese, indem Sie in **Sitzungsmonitor**auf den Namen der Sitzung doppelklicken.  
  
3.  Klicken Sie nach dem Beenden der neuen Optimierungssitzung oder dem Laden der vorhandenen Sitzung durch das Tool im Menü **Aktionen** auf **Empfehlungen anwenden** .  
  
4.  Wählen Sie im Dialogfeld **Empfehlungen anwenden** entweder **Jetzt anwenden** oder **Spätere Ausführung planen**aus. Wenn Sie **Spätere Ausführung planen**auswählen, müssen Sie auch das entsprechende Datum und die Uhrzeit angeben.  
  
5.  Klicken Sie auf **OK** , um die Empfehlungen anzuwenden.  
  
#### <a name="to-automatically-implement-tuning-recommendations-using-the-dta-command-prompt-utility"></a>So implementieren Sie die Optimierungsempfehlungen automatisch über das Eingabeaufforderungs-Hilfsprogramm "dta"  
  
1.  Legen Sie die Datenbankfunktionen (Indizes, indizierte Sichten, Partitionierung) fest, die während der Analyse vom Datenbankoptimierungsratgeber hinzugefügt, entfernt oder beibehalten werden sollen.  
  
     Bedenken Sie Folgendes, bevor Sie mit der Optimierung beginnen:  
  
    -   Wenn als Arbeitsauslastung eine Ablaufverfolgungstabelle verwendet wird, muss diese Tabelle auf dem Server vorhanden sein, auf dem die Optimierung durch den Datenbankoptimierungsratgeber vorgenommen wird. Wenn die Ablaufverfolgungstabelle auf einem anderen Server erstellt wird, muss sie auf den Server verschoben werden, auf dem die Optimierung durch den Datenbankoptimierungsratgeber vorgenommen wird.  
  
    -   Wenn eine Optimierungssitzung bei der Ausführung den erwarteten zeitlichen Rahmen überschreitet, können Sie die Optimierungssitzung mit STRG+C beenden. Durch Drücken von STRG+C wird die Erstellung der auf der Grundlage der verbrauchten Arbeitsauslastung bestmöglichen Empfehlung durch **dta** erzwungen. Dadurch wird die Zeit, die das Tool bereits zur Optimierung der Arbeitsauslastung verbraucht hat, nicht verschwendet.  
  
2.  Geben Sie an einer Eingabeaufforderung folgenden Befehl ein:  
  
    ```  
    dta -E -D DatabaseName -if WorkloadFile -s SessionName -a  
    ```  
  
     **-E** gibt hier an, dass für Ihre Optimierungssitzung eine vertrauenswürdige Verbindung (anstelle einer Anmelde-ID und eines Kennworts) verwendet wird, **-D** gibt den Namen der zu optimierenden Datenbank oder eine durch Trennzeichen getrennte Liste mehrerer Datenbanken, welche die Arbeitsauslastung verwendet, an, **-if** gibt den Namen und den Pfad einer Arbeitsauslastungsdatei an, **-s** gibt den Namen Ihrer Optimierungssitzung an, und **-a** gibt an, dass die Optimierungsempfehlungen nach der Analyse der Arbeitsauslastung ohne vorherige Eingabeaufforderung automatisch durch das Eingabeaufforderungs-Hilfsprogramm **dta** angewendet werden sollen. Weitere Informationen zum Verwenden des Eingabeaufforderungs-Hilfsprogramms **dta** bei der Optimierung von Datenbanken finden Sie unter [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
3.  Drücken Sie die EINGABETASTE.  
  
##  <a name="Analysis"></a> Ausführen von explorativen Analysen  
 Die vom Benutzer angegebene Konfigurationsfunktion des Datenbankoptimierungsratgebers ermöglicht es Datenbankadministratoren, explorative Analysen auszuführen. Mithilfe dieser Funktion geben Datenbankadministroren einen gewünschten physischen Datenbankentwurf für den Datenbankoptimierungsratgeber an. Danach können sie die Leistungsauswirkungen dieses Entwurfs bewerten, ohne diesen zu implementieren. Vom Benutzer angegebene Konfigurationen werden sowohl von der grafischen Benutzeroberfläche (GUI) des Datenbankoptimierungsratgebers als auch vom Befehlszeilen-Hilfsprogramm unterstützt. Jedoch stellt das Befehlszeilen-Hilfsprogramm die größte Flexibilität bereit.  
  
 Wenn Sie die GUI des Datenbankoptimierungsratgebers verwenden, können Sie die Auswirkungen der Implementierung einer Untergruppe einer Optimierungsempfehlung des Datenbankoptimierungsratgebers auswerten. Sie können jedoch zum Auswerten mit dem Datenbankoptimierungsratgeber keine hypothetischen physischen Entwurfsstrukturen hinzufügen.  
  
 In den folgenden schrittweisen Anleitungen erfahren Sie, wie Sie die vom Benutzer angegebene Konfigurationsfunktion mit beiden Tooloberflächen verwenden.  
  
### <a name="using-database-engine-tuning-advisor-gui-to-evaluate-tuning-recommendations"></a>Verwenden der GUI des Datenbankoptimierungsratgebers zum Auswerten von Optimierungsempfehlungen  
 In den folgenden schrittweisen Anleitungen wird beschrieben, wie Sie eine mit dem Datenbankoptimierungsratgeber generierte Empfehlung auswerten. Die GUI ermöglicht Ihnen jedoch nicht, neue physische Entwurfsstrukturen für die Auswertung anzugeben.  
  
##### <a name="to-evaluate-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>So werten Sie Optimierungsempfehlungen mit der GUI des Datenbankoptimierungsratgebers aus  
  
1.  Verwenden Sie zum Optimieren einer Datenbank die GUI des Datenbankoptimierungsratgebers. Weitere Informationen finden Sie unter [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Wenn Sie eine vorhandene Optimierungssitzung auswerten möchten, doppelklicken Sie auf diese in **Sitzungsmonitor**.  
  
2.  Heben Sie auf der Registerkarte **Empfehlungen** die Auswahl für die physischen Entwurfsstrukturen auf, die Sie nicht verwenden möchten.  
  
3.  Klicken Sie im Menü **Aktionen** auf **Empfehlungen bewerten**. Eine neue Optimierungssitzung wird für Sie erstellt.  
  
4.  Geben Sie in **Sitzungsname**den neuen Sitzungsnamen ein. Um die physische Datenbankentwurfsstruktur-Konfiguration, die Sie gerade auswerten, anzuzeigen, wählen Sie im Bereich **Beschreibung** im unteren Bereich des Anwendungsfensters des Datenbankoptimierungsratgebers **Klicken Sie hier, um den Konfigurationsabschnitt anzuzeigen** aus.  
  
5.  Klicken Sie auf der Symbolleiste auf die Schaltfläche **Analyse starten** . Wenn der Datenbankoptimierungsratgeber die Analyse abgeschlossen hat, können Sie die Ergebnisse auf der Registerkarte **Empfehlungen** anzeigen.  
  
### <a name="using-database-engine-tuning-advisor-gui-to-export-tuning-session-results-for-what-if-tuning-analysis"></a>Verwenden der GUI des Datenbankoptimierungsratgebers zum Exportieren von Optimierungssitzungsergebnissen für die Was-wäre-wenn-Optimierungsanalyse  
 In den folgenden schrittweisen Anleitungen wird beschrieben, wie Sie die Optimierungssitzungsergebnisse des Datenbankoptimierungsratgebers in eine XML-Datei exportieren, die Sie bearbeiten und dann mit dem Befehlszeilen-Hilfsprogramm **dta** optimieren können. Dadurch können Sie Optimierungsanalysen für hypothetische, neue physische Entwurfsstrukturen ausführen. So müssen Sie Implementierungsaufwand in Ihrer Datenbank erst dann leisten, wenn Sie sicher sind, dass sie zu den von Ihnen benötigten Leistungsverbesserungen führen. Die Verwendung der GUI des Datenbankoptimierungsratgebers, um die Datenbank zunächst zu optimieren und dann die Optimierungsergebnisse in eine **XML** -Datei zu exportieren, ist optimal für Benutzer mit geringen XML-Kenntnissen, die die Flexibilität des XML-Schemas des Datenbankoptimierungsratgebers zum Ausführen der Was-wäre-wenn-Analyse verwenden.  
  
##### <a name="to-export-tuning-session-results-from-the-database-engine-tuning-advisor-gui-for-what-if-analysis-with-the-dta-command-line-utility"></a>So exportieren Sie die Optimierungssitzungsergebnisse aus der GUI des Datenbankoptimierungsratgebers für die Was-wäre-wenn-Analyse mithilfe des Befehlszeilen-Hilfsprogramms dta  
  
1.  Verwenden Sie zum Optimieren einer Datenbank die GUI des Datenbankoptimierungsratgebers. Weitere Informationen finden Sie unter [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md). Wenn Sie eine vorhandene Optimierungssitzung auswerten möchten, doppelklicken Sie auf diese in **Sitzungsmonitor**.  
  
2.  Klicken Sie im Menü **Datei** auf **Sitzungsergebnisse exportieren** , und speichern Sie sie als XML-Datei.  
  
3.  Öffnen Sie die in Schritt 2 erstellte XML-Datei in dem von Ihnen bevorzugten XML-Editor, Text-Editor oder in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Scrollen Sie zum **Configuration** -Element. Kopieren Sie den **Configuration** -Elementabschnitt und fügen Sie ihn in eine XML-Eingabedateivorlage hinter dem **TuningOptions** -Element ein. Speichern Sie diese XML-Eingabedatei.  
  
4.  Geben Sie in der neuen XML-Eingabedatei, die Sie in Schritt 3 erstellt haben, Optimierungsoptionen für das **TuningOptions**-Element an. Bearbeiten Sie den **Configuration**-Elementabschnitt (fügen Sie die physischen Entwurfsstrukturen hinzu oder löschen Sie sie, je nachdem, wie Sie Ihre Analyse ausführen möchten). Speichern Sie die Datei, und überprüfen Sie sie mithilfe des XML-Schemas des Datenbankoptimierungsratgebers. Informationen zum Bearbeiten dieser XML-Datei finden Sie unter [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md).  
  
5.  Verwenden Sie die in Schritt 4 erstellte XML-Datei als Eingabewert für das Befehlszeilen-Hilfsprogramm **dta** . Informationen zur Verwendung von XML-Eingabedateien mit diesem Tool finden Sie im Abschnitt "Optimieren einer Datenbank mithilfe des dta-Hilfsprogramms" in [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
### <a name="using-the-user-specified-configuration-feature-with-the-dta-command-line-utility"></a>Verwenden des vom Benutzer angegebene Konfigurationsfunktion mit dem Befehlszeilen-Hilfsprogramm dta  
 Wenn Sie ein erfahrener XML-Entwickler sind, können Sie eine XML-Eingabedatei des Datenbankoptimierungsratgebers erstellen, in der Sie eine Arbeitsauslastung und eine hypothetische Konfiguration der physischen Datenbankentwurfsstrukturen, wie z. B. Indizes, indizierte Sichten oder Partitionierungen, angeben können. Dann können Sie mithilfe des Befehlszeilen-Dienstprogramms **dta** die Auswirkungen dieser hypothetischen Konfiguration auf die Abfrageleistung Ihrer Datenbank analysieren. In den folgenden schrittweisen Anleitungen wird dieser Prozess Schritt für Schritt beschrieben:  
  
##### <a name="to-use-the-user-specified-configuration-feature-with-the-dta-command-line-utility"></a>So verwenden Sie die vom Benutzer angegebene Konfigurationsfunktion mithilfe des Befehlszeilen-Hilfsprogramms dta  
  
1.  Erstellen Sie eine zu optimierende Arbeitsauslastung. Weitere Informationen zum Ausführen dieser Aufgabe finden Sie unter [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
2.  Kopieren Sie das [Beispiel für eine XML-Eingabedatei mit benutzerdefinierter Konfiguration &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md), und fügen Sie es in Ihren XML-Editor oder einen Text-Editor ein. Verwenden Sie dieses Beispiel zum Erstellen einer XML-Eingabedatei für Ihre Optimierungssitzung. Informationen zum Ausführen dieses Tasks finden Sie im Abschnitt "Erstellen von XML-Eingabedateien" in [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
3.  Bearbeiten Sie die in der Beispiel-XML-Eingabedatei enthaltenen **TuningOptions** - und **Configuration** -Elemente. Geben Sie im **TuningOptions** -Element an, welche physischen Entwurfsstrukturen der Datenbankoptimierungsratgeber während der Optimierungssitzung berücksichtigen soll. Geben Sie im **Configuration** -Element die physischen Entwurfsstrukturen an, die der hypothetischen Konfiguration der physischen Datenbankentwurfsstrukturen entsprechen, die der Datenbankoptimierungsratgeber analysieren soll. Weitere Informationen darüber, welche Attribute und untergeordneten Elemente Sie mit den übergeordneten Elementen **TuningOptions** und **Configuration** verwenden können, finden Sie unter [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md).  
  
4.  Speichern Sie die Eingabedatei mit der Dateinamenerweiterung XML **** .  
  
5.  Überprüfen Sie die in Schritt 4 gespeicherte XML-Eingabedatei mit dem XML-Schema des Datenbankoptimierungsratgebers. Bei der Installation von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird dieses Schema unter dem folgenden Pfad installiert:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\100\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd  
    ```  
  
     Das XML-Schema des Datenbankoptimierungsratgebers ist auch online unter [http://schemas.microsoft.com/sqlserver/2004/07/dta](http://schemas.microsoft.com/sqlserver/2004/07/dta)verfügbar.  
  
6.  Nach dem Erstellen einer Arbeitsauslastung und einer XML-Eingabedatei können Sie die Eingabedatei an das Befehlszeilen-Hilfsprogramm **dta** zur Analyse übergeben. Stellen Sie sicher, dass Sie einen XML-Ausgabedateinamen für das **-ox** -Argument des Hilfsprogramms angeben. Auf diese Weise wird eine XML-Ausgabedatei mit einer empfohlenen Konfiguration erstellt, die im **Configuration** -Element angegeben ist. Wenn Sie den Datenbankoptimierungsratgeber zum Überprüfen einer weiteren, auf der Ausgabe basierenden hypothetischen Konfiguration ausführen möchten, kopieren Sie den **Configuration** -Elementinhalt aus der Ausgabedatei und fügen Sie ihn in eine neue oder in Ihre ursprüngliche XML-Eingabedatei ein. Informationen zum Verwenden einer XML-Eingabedatei mit dem Hilfsprogramm **dta** finden Sie im Abschnitt "Optimieren einer Datenbank mithilfe des dta-Hilfsprogramms" in [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
     Nach Abschluss der Optimierung können Sie die Optimierungsberichte mithilfe der GUI des Datenbankoptimierungsratgebers anzeigen. Sie können auch die XML-Ausgabedatei öffnen, um über die **TuningSummary** - und **Configuration** -Elemente die Empfehlungen des Datenbankoptimierungsratgebers anzuzeigen. Informationen zum Anzeigen der Ergebnisse der Optimierungssitzung finden Sie weiter oben unter [Anzeigen der Optimierungsausgabe](#View) in diesem Thema. Beachten Sie auch, dass die XML-Ausgabedatei Analyseberichte des Datenbankoptimierungsratgebers enthalten kann.  
  
7.  Wiederholen Sie die Schritte 6 und 7, bis Sie die hypothetische Konfiguration erstellen, mit der die erforderlichen Abfrageleistungsverbesserungen erzielt werden. Dann können Sie die neue Konfiguration implementieren. Weitere Informationen finden Sie unter [Implementieren von Optimierungsempfehlungen](#Implement) weiter oben in diesem Thema.  
  
##  <a name="ReviewEvaluateClone"></a> Überprüfen, Auswerten und Klonen von Optimierungssitzungen  
 Der Datenbankoptimierungsratgeber erstellt jeweils eine neue Optimierungssitzung, wenn Sie die Auswirkungen einer Arbeitsauslastung auf die Datenbank(en) analysieren. Sie können den **Sitzungsmonitor** der grafischen Benutzeroberfläche des Datenbankoptimierungsratgebers dazu verwenden, alle Optimierungssitzungen anzuzeigen und neu zu laden, die für eine bestimmte Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt wurden. Dadurch, dass Ihnen alle vorhandenen Optimierungssitzungen zur Verfügung stehen, werden Ihnen die folgenden Operationen erleichtert: Klonen von Sitzungen auf der Grundlage vorhandener Sitzungen, Bearbeiten bestehender Optimierungsempfehlungen und Auswerten der bearbeiteten Sitzungen mit dem Datenbankoptimierungsratgeber sowie Ausführen von Optimierungen in regelmäßigen Abständen zur Überwachung des physischen Entwurfs der Datenbanken. So können Sie Datenbanken beispielsweise einmal im Monat optimieren.  
  
 Bevor Sie die Optimierungssitzungen für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]überprüfen können, müssen Sie durch das Optimieren von Arbeitsauslastungen mit dem Datenbankoptimierungsratgeber Optimierungssitzungen erstellen. Weitere Informationen finden Sie unter [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
### <a name="review-existing-tuning-sessions"></a>Überprüfen vorhandener Optimierungssitzungen  
 Führen Sie die folgenden Schritte aus, um die vorhandenen Optimierungssitzungen für eine vorhandene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu durchsuchen.  
  
##### <a name="to-review-existing-tuning-sessions"></a>So überprüfen Sie vorhandene Optimierungssitzungen  
  
1.  Starten Sie die grafische Benutzeroberfläche des Datenbankoptimierungsratgebers. Weitere Informationen finden Sie unter [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
2.  Alle vorhandenen Optimierungssitzungen werden in der oberen Hälfte des Fensters **Sitzungsmonitor** angezeigt. Die Anzahl der angezeigten Sitzungen ist davon abhängig, wie oft Sie Sitzungen für diese [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz optimiert haben. Verwenden Sie die Bildlaufleisten, um alle Optimierungssitzungen anzuzeigen.  
  
3.  Wenn Sie einmal auf den Namen einer Optimierungssitzung klicken, werden die zugehörigen Details in der unteren Hälfte des Fensters **Sitzungsmonitor** angezeigt.  
  
4.  Durch Doppelklicken auf den Namen einer Optimierungssitzung werden die Informationen in den Datenbankoptimierungsratgeber geladen. Nachdem die Sitzungsinformationen geladen wurden, können Sie eine beliebige der Registerkarten mit Informationen zur Optimierungssitzung auswählen.  
  
### <a name="evaluate-existing-tuning-sessions-as-hypothetical-configurations"></a>Auswerten vorhandener Optimierungssitzungen als hypothetische Konfigurationen  
 Führen Sie die folgenden Schritte aus, um eine vorhandene Optimierungssitzung auszuwerten. Das Auswerten einer vorhandenen Optimierungssitzung umfasst das Anzeigen und Bearbeiten der zugehörigen Empfehlungen und die anschließende erneute Optimierung. Wenn Sie beispielsweise nur Indizes für **table1**erstellen möchten, können Sie die Erstellung indizierter Sichten und die Partitionierung aus einer vorhandenen Optimierungsempfehlung löschen. Anschließend erstellt der Datenbankoptimierungsratgeber eine neue Optimierungssitzung und optimiert die Arbeitsauslastung für die Datenbanken auf Grundlage der bearbeiteten Empfehlungen als hypothetischer Konfiguration. Das bedeutet, dass der Datenbankoptimierungsratgeber die Arbeitsauslastung für die Datenbanken so optimiert, als wären die bearbeiteten Empfehlungen implementiert worden. Auf diese Weise steht Ihnen eine begrenzte Was-wäre-wenn-Analyse zur Verfügung. Es handelt sich deshalb nur um eine begrenzte Was-wäre-wenn-Analyse, weil Sie bei Verwendung der grafischen Benutzeroberfläche des Datenbankmodul-Optimierungsratgebers nur einen Teil einer vorhandenen Empfehlung auswählen können. Geben Sie eine vollständige neue hypothetische Konfiguration an, die nicht Teil einer vorherigen Optimierungssitzung ist, um eine umfassende Was-wäre-wenn-Analyse auszuführen. Sie müssen die XML-Eingabedatei des Datenbankoptimierungsratgebers zusammen mit dem Befehlszeilenprogramm **dta** verwenden.  
  
##### <a name="to-evaluate-an-existing-tuning-session"></a>So werten Sie eine vorhandene Optimierungssitzung aus  
  
1.  Doppelklicken Sie nach dem Starten des Datenbankoptimierungsratgebers auf eine Optimierungssitzung in der oberen Hälfte des Fensters **Sitzungsmonitor**. Daraufhin werden die Sitzungsinformationen in den Datenbankoptimierungsratgeber geladen.  
  
2.  Klicken Sie auf die Registerkarte **Status** , um das Optimierungsprotokoll anzuzeigen, das Fehlerinformationen zu allen Ereignissen in der Arbeitsauslastung enthält, die vom Datenbankoptimierungsratgeber nicht optimiert werden konnten. Diese Informationen können Ihnen bei der Auswertung der Effektivität der Arbeitsauslastung helfen.  
  
3.  Wenn Sie die Optimierungsergebnisse für diese Sitzung detaillierter überprüfen möchten, klicken Sie auf die Registerkarte **Berichte** . Dort können Sie eine Optimierungszusammenfassung anzeigen und einen Optimierungsbericht aus der Liste **Bericht auswählen** auswählen.  
  
4.  Klicken Sie auf die Registerkarte **Empfehlungen** , um die Optimierungsempfehlungen anzuzeigen.  
  
5.  Wenn Sie sich nicht sicher sind, ob Sie bestimmte Empfehlungen implementieren sollten, deaktivieren Sie diese.  
  
6.  Klicken Sie im Menü **Aktionen** auf **Empfehlungen bewerten**. Der Datenbankoptimierungsratgeber erstellt eine neue Optimierungssitzung, die die bearbeiteten Empfehlungen als eine hypothetische Konfiguration verwendet. Um die hypothetische Konfiguration in XML anzuzeigen, wählen Sie die Option **Klicken Sie hier, um den Konfigurationsabschnitt anzuzeigen**aus.  
  
7.  Geben Sie auf der Registerkarte **Allgemein** einen Namen im Feld **Sitzungsname**ein, und stellen Sie sicher, dass die richtige **Arbeitsauslastung** angegeben ist.  
  
8.  Legen Sie auf der Registerkarte **Optimierungsoptionen** eine Optimierungszeit oder eine beliebige andere der **Erweiterten Optionen**fest.  
  
9. Klicken Sie auf der Symbolleiste auf die Schaltfläche **Analyse starten** . Der Datenbankoptimierungsratgeber beginnt mit der Optimierung der Datenbanken auf Grundlage der hypothetischen Konfiguration. Nachdem der Datenbankoptimierungsratgeber den Vorgang beendet hat, können Sie die Ergebnisse dieser Sitzung wie für jede andere Sitzung anzeigen.  
  
### <a name="clone-existing-tuning-sessions"></a>Klonen vorhandener Optimierungssitzungen  
 Durch Auswahl der Option zum Klonen im Datenbankoptimierungsratgeber können Sie neue Optimierungssitzungen auf Grundlage vorhandener Sitzungen erstellen. Bei Verwendung der Klonoption basiert eine neue Optimierungssitzung auf einer vorhandenen Sitzung. Anschließend können Sie die Optimierungsoptionen für die neue Sitzung nach Bedarf ändern. Wenn Sie eine vorhandene Sitzung wie in der vorherigen Prozedur beschrieben auswerten, erstellt der Datenbankoptimierungsratgeber auch eine neue Optimierungssitzung. Sie können in diesem Fall aber nicht die Optimierungsoptionen ändern.  
  
##### <a name="to-create-new-tuning-sessions-by-cloning-existing-sessions"></a>So erstellen Sie neue Optimierungssitzungen durch Klonen vorhandener Sitzungen  
  
1.  Doppelklicken Sie nach dem Starten des Datenbankoptimierungsratgebers auf eine Optimierungssitzung in der oberen Hälfte des Fensters **Sitzungsmonitor**. Daraufhin werden die Sitzungsinformationen in den Datenbankoptimierungsratgeber geladen.  
  
2.  Klicken Sie im Menü **Aktionen** auf **Sitzung klonen**.  
  
3.  Geben Sie auf der Registerkarte **Allgemein** einen Namen im Feld **Sitzungsname**ein, und stellen Sie sicher, dass die richtige **Arbeitsauslastung** angegeben ist.  
  
4.  Auf der Registerkarte **Optimierungsoptionen** können Sie eine Optimierungszeit, die vom Datenbankoptimierungsratgeber ggf. zu erstellenden physischen Entwurfsstrukturen sowie die zu vernachlässigenden Empfehlungen angeben.  
  
5.  Klicken Sie auf **Erweiterte Optionen** , wenn Sie den Speicherplatz für Empfehlungen beschränken oder eine maximale Anzahl von Spalten je Index festlegen möchten oder wenn Sie angeben möchten, ob der Datenbankoptimierungsratgeber Empfehlungen generieren soll, die implementiert werden können, während [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] online ist.  
  
6.  Klicken Sie auf der Symbolleiste auf die Schaltfläche **Analyse starten** , um die Auswirkungen auf die Arbeitsauslastung wie bei jeder anderen Optimierungssitzung zu analysieren. Nachdem der Datenbankoptimierungsratgeber den Vorgang beendet hat, können Sie die Ergebnisse dieser Sitzung wie für jede andere Sitzung anzeigen.  
  
##  <a name="UI"></a> Benutzeroberflächenbeschreibungen  
  
### <a name="sessions-monitor"></a>Sitzungsmonitor  
 Der**Sitzungsmonitor** zeigt Informationen zu Sitzungen an, die im Datenbankoptimierungsratgeber geöffnet sind. Wählen Sie einen Sitzungsnamen in **Sitzungsmonitor**aus, um Informationen zur Sitzung im Eigenschaftenfenster anzuzeigen.  
  
### <a name="recommendations-tab"></a>Empfehlungen (Registerkarte)  
 Die Registerkarte **Empfehlungen** wird angezeigt, nachdem der Datenbankoptimierungsratgeber die Analyse einer Arbeitsauslastung abgeschlossen hat. Der Raster enthält die Empfehlungen für jedes berücksichtigte Objekt. Sofern Partitionsempfehlungen vorliegen, werden diese im oberen Raster angezeigt und die Indexempfehlungen im unteren Raster. Die Raster werden nicht angezeigt, wenn keine Empfehlungen vorhanden sind.  
  
 Die Spalte **Definition** enthält die Definition der empfohlenen Partition oder des empfohlenen Indexes als einen Link. In den meisten Fällen ist die Spalte für die Anzeige der gesamten Definition zu eng. Klicken Sie auf den Link, um ein Dialogfeld mit der vollständigen Definition und der Schaltfläche **In Zwischenablage kopieren** zu öffnen.  
  
#### <a name="partition-recommendations"></a>Partitionsempfehlungen  
 **Datenbankname**  
 Datenbank mit den Objekten, für die Änderungen empfohlen wurden.  
  
 **Empfehlung**  
 Empfohlene Aktion zur Steigerung der Leistung. Mögliche Werte sind Create und Drop.  
  
 **Empfehlungsziel**  
 Die von der Empfehlung betroffene Partitionsfunktion oder das Partitionsschema. Das Symbol in dieser Spalte steht für die Empfehlung, den Wert unter **Empfehlungsziel** zu löschen oder hinzuzufügen, und dafür, ob es sich um eine Partitionsfunktion oder ein Partitionsschema handelt.  
  
 **Details**  
 Eine Beschreibung der Werts unter **Empfehlungsziel**. Mögliche Werte sind: ein Bereich bei Partitionsfunktionen oder leer bei Partitionsschemas.  
  
 **Anzahl der Partitionen**  
 Anzahl der durch die empfohlenen Partitionierungsfunktionen definierten Partitionen. Wenn diese Funktion zusammen mit einem Schema verwendet und dann auf eine Tabelle angewendet wird, sind die Daten in der Tabelle in die entsprechende Anzahl von Partitionen unterteilt.  
  
 **Definition**  
 Die Definition für den Wert unter **Empfehlungsziel**. Klicken Sie auf die Spalte, um das Dialogfeld SQL-Skriptvorschau mit einem Skript für die empfohlene Aktion zu öffnen.  
  
##### <a name="index-recommendations"></a>Indexempfehlungen  
 **Datenbankname**  
 Datenbank mit den Objekten, für die Änderungen empfohlen wurden.  
  
 **Objektname**  
 Mit der Empfehlung verbundene Tabelle.  
  
 **Empfehlung**  
 Empfohlene Aktion zur Steigerung der Leistung. Mögliche Werte sind Create und Drop.  
  
 **Empfehlungsziel**  
 Der Index oder die Sicht, auf den/die sich die Empfehlung bezieht. Das Symbol in dieser Spalte steht für die Empfehlung, den Wert unter **Empfehlungsziel**zu löschen oder hinzuzufügen.  
  
 **Details**  
 Eine Beschreibung der Werts unter **Empfehlungsziel**. Mögliche Werte sind: gruppierte, indizierte Sicht oder leer bei einer nicht gruppierten Sicht. Gibt auch an, ob der Index eindeutig ist.  
  
 **Partitionsschema**  
 Das Partitionsschema wird in dieser Spalte bei empfohlener Partitionierung bereitgestellt.  
  
 **Größe (KB)**  
 Erwartete Größe des neuen Objekts, das empfohlen wird. Wenn diese Spalte leer ist, klicken Sie auf **Berichte für Größen von vorhandenen Objekten anzeigen**.  
  
 **Definition**  
 Die Definition für den Wert unter **Empfehlungsziel**. Klicken Sie auf die Spalte, um das Dialogfeld SQL-Skriptvorschau mit einem Skript für die empfohlene Aktion zu öffnen.  
  
 **Vorhandene Objekte anzeigen**  
 Wählen Sie diese Option, um alle im Raster vorhandenen Objekte anzuzeigen, auch wenn für die Objekte keine Empfehlungen durch den Datenbankoptimierungsratgeber vorliegen.  
  
 **Berichte für Größen von vorhandenen Objekten anzeigen**  
 Wählen Sie diese Option aus, um Berichte anzuzeigen, aus denen die Größe von vorhandenen Objekten im Empfehlungsraster hervorgeht.  
  
### <a name="actions-menuapply-recommendations-options"></a>Aktionen (Menü)/Empfehlungen anwenden (Optionen)  
 Klicken Sie, nachdem die Arbeitsauslastung analysiert und die Empfehlungen angezeigt wurden, im Menü **Aktionen** auf **Empfehlungen anwenden** , um das Dialogfeld **Empfehlungen anwenden** zu öffnen.  
  
 **Jetzt anwenden**  
 Generiert ein Skript für die Empfehlungen und führt das Skript aus, um die Empfehlungen zu implementieren.  
  
 **Spätere Ausführung planen**  
 Generiert ein Skript für die Empfehlungen und speichert die Aktionen als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrag.  
  
 **Datum**  
 Gibt das Datum für die Ausführung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrags an, mit dem die Empfehlungen angewendet werden.  
  
 **Uhrzeit**  
 Gibt die Uhrzeit für die Ausführung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrags an, mit dem die Empfehlungen angewendet werden.  
  
### <a name="reports-tab-options"></a>Optionen auf der Registerkarte "Berichte"  
 Die Registerkarte **Berichte** wird angezeigt, nachdem der Datenbankoptimierungsratgeber die Analyse einer Arbeitsauslastung abgeschlossen hat.  
  
 **Optimierungszusammenfassung**  
 Zeigt eine Zusammenfassung der Empfehlungen des Datenbankoptimierungsratgebers an.  
  
 **Datum**  
 Das Datum, an dem der Bericht durch den Datenbankoptimierungsratgeber erstellt wurde.  
  
 **Uhrzeit**  
 Die Uhrzeit, zu der der Bericht durch den Datenbankoptimierungsratgeber erstellt wurde.  
  
 **Server**  
 Der Server, der das Ziel der Arbeitsauslastungsanalyse durch den Datenbankoptimierungsratgeber war.  
  
 **Zu optimierende Datenbank(en)**  
 Die Datenbank, auf die sich die Empfehlungen des Datenbankoptimierungsratgebers beziehen.  
  
 **Arbeitsauslastungsdatei**  
 Wird angezeigt, wenn die Arbeitsauslastung eine Datei ist.  
  
 **Arbeitauslastungstabelle**  
 Wird angezeigt, wenn die Arbeitsauslastung eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle ist.  
  
 **Arbeitsauslastung**  
 Wird angezeigt, wenn die Arbeitsauslastung aus dem Abfrage-Editor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]importiert wurde.  
  
 **Maximale Optimierungszeit**  
 Die aufgrund der Konfiguration maximal verfügbare Zeit für die Analyse durch den Datenbankoptimierungsratgeber.  
  
 **Für die Optimierung benötigte Zeit**  
 Die vom Datenbankoptimierungsratgeber tatsächlich verwendete Zeit für die Analyse der Arbeitsauslastung.  
  
 **Prozentsatz für die erwartete Verbesserung**  
 Der zu erwartende Prozentsatz der Verbesserung bei der angestrebten Arbeitsauslastung, wenn alle Empfehlungen des Datenbankoptimierungsratgebers umgesetzt werden.  
  
 **Maximaler Speicherplatz für Empfehlung (MB)**  
 Der maximal vorgesehene Speicherplatz für die Empfehlungen. Dieser Wert wird vor der Analyse mithilfe der Schaltfläche **Erweiterte Optionen** auf der Registerkarte **Optimierungsoptionen** konfiguriert.  
  
 **Aktuell verwendeter Speicherplatz (MB)**  
 Der Speicherplatz, der aktuell von Indizes in der analysierten Datenbank verwendet wird.  
  
 **Von der Empfehlung verwendeter Speicherplatz (MB)**  
 Der ungefähre Speicherplatz, der voraussichtlich von Indizes verwendet wird, wenn alle Empfehlungen des Datenbankoptimierungsratgebers umgesetzt werden.  
  
 **Anzahl von Ereignissen der Arbeitsauslastung**  
 Anzahl der Ereignisse, die in der Arbeitsauslastung enthalten sind.  
  
 **Anzahl von optimierten Ereignissen**  
 Anzahl der Ereignisse, die in der Arbeitsauslastung optimiert wurden. Wenn ein Ereignis nicht optimiert werden kann, wird es im Optimierungsprotokoll aufgeführt, das auf der Registerkarte **Status** verfügbar ist.  
  
 **Anzahl von optimierten Anweisungen**  
 Anzahl der Anweisungen, die in der Arbeitsauslastung optimiert wurden. Wenn eine Anweisung nicht optimiert werden kann, wird sie im Optimierungsprotokoll aufgeführt, das auf der Registerkarte **Status** verfügbar ist.  
  
 **Prozentsatz der SELECT-Anweisungen in der optimierten Gruppe**  
 Prozentsatz der optimierten Anweisungen, die SELECT-Anweisungen sind. Wird nur angezeigt, wenn SELECT-Anweisungen optimiert wurden.  
  
 **Prozentsatz der UPDATE-Anweisungen in der optimierten Gruppe**  
 Prozentsatz der optimierten Anweisungen, die UPDATE-Anweisungen sind. Wird nur angezeigt, wenn UPDATE-Anweisungen optimiert wurden.  
  
 **Empfohlene Anzahl von zu [erstellenden | löschenden] Indizes**  
 Empfohlene Anzahl von Indizes, die in der optimierten Datenbank erstellt bzw. gelöscht werden sollen. Wird nur angezeigt, wenn Indizes Teil der Empfehlung sind.  
  
 **Empfohlene Anzahl von zu [erstellenden | löschenden] Indizes für Sichten**  
 Empfohlene Anzahl von Indizes für Sichten, die in der optimierten Datenbank erstellt bzw. gelöscht werden sollen. Wird nur angezeigt, wenn Indizes für Sichten Teil der Empfehlung sind.  
  
 **Empfohlene Anzahl von zu erstellenden Statistiken**  
 Empfohlene Anzahl der Statistiken, die in der optimierten Datenbank erstellt werden sollen. Wird nur angezeigt, wenn Statistiken empfohlen werden.  
  
 **Select Report**  
 Zeigt die Details des ausgewählten Berichts an. Die Spalten des Rasters sind in jedem Bericht unterschiedlich.  
  
## <a name="see-also"></a>Siehe auch  
 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [dta (Hilfsprogramm)](../../tools/dta/dta-utility.md)  
  
  
