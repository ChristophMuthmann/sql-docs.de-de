---
title: Erstellen einer Abgleichsrichtlinie | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dqs.kb.kbmatchingmap.f1
- sql13.dqs.kb.kbmatchingpolicy.f1
- sql13.dqs.kb.kbmatchingresults.f1
ms.assetid: cce77a06-ca31-47b6-8146-22edf001d605
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1fe1c8b25d8309d3984c70c31f5949a9724599a3
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="create-a-matching-policy"></a>Erstellen einer Abgleichsrichtlinie
  In diesem Thema wird beschrieben, wie eine Abgleichsrichtlinie eine Wissensdatenbank in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) erstellt wird. Sie bereiten den Abgleichsprozess in DQS vor, indem Sie die Abgleichsrichtlinienaktivität für Beispieldaten ausführen. In dieser Aktivität erstellen und testen Sie eine oder mehrere Abgleichsregeln in der Richtlinie und veröffentlichen dann die Wissensdatenbank, um die Abgleichsregeln zur Verwendung öffentlich verfügbar zu machen. Es kann nur eine Abgleichsrichtlinie in einer Wissensdatenbank geben, aber diese Richtlinie kann mehrere Abgleichsregeln enthalten.  
  
 Die Abgleichsrichtlinienerstellung wird in drei Phasen ausgeführt: ein Zuordnungsprozess, in dem Sie die Datenquelle identifizieren und Domänen zu Spalten zuordnen, ein Abgleichsrichtlinienprozess, in dem Sie eine oder mehrere Abgleichsregeln erstellen und jede Abgleichsregel separat testen, und ein Abgleichsergebnisseprozess, in dem Sie alle Abgleichsregeln zusammen ausführen und die Richtlinie der Wissensdatenbank hinzufügen, wenn Sie mit ihr zufrieden sind. Jeder dieser Prozesse wird auf einer separaten Seite des Abgleichsrichtlinienaktivitäts-Assistenten ausgeführt, sodass Sie zwischen den Seiten hin und her wechseln, den Prozess erneut auszuführen, einen bestimmten Abgleichsrichtlinienprozess schließen und dann zur gleichen Phase des Prozesses zurückkehren können. Nach dem gemeinsamen Testen aller Regeln können Sie, falls erforderlich, zur Seite **Abgleichsrichtlinie** zurückkehren, eine einzelne Regel ändern, sie wieder separat testen und zur Seite **Abgleichsergebnisse** zurückkehren, um alle Regeln erneut gemeinsam auszuführen. DQS stellt Ihnen Statistiken zu den Quelldaten, den Abgleichsregeln und den Abgleichsergebnissen bereit, die es Ihnen ermöglichen, informierte Entscheidungen zur Abgleichsrichtlinie zu treffen, damit Sie sie optimieren können.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Microsoft Excel muss auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Computer installiert sein, wenn sich die Quelldaten in einer Excel-Datei befinden. Andernfalls sind Sie nicht in der Lage, die Excel-Datei in der Zuordnungsphase auszuwählen. Die von Microsoft Excel erstellten Dateien können die Erweiterung .xlsx, .xls oder .csv haben. Wenn die 64-Bit-Version von Excel verwendet wird, werden nur Excel 2003-Dateien (.xls) unterstützt; Excel 2007- oder 2010-Dateien (.xlsx) werden nicht unterstützt. Wenn Sie die 64-Bit-Version von Excel 2007 oder 2010 verwenden, speichern Sie die Datei als XLS-Datei oder CSV-Datei, oder installieren Sie stattdessen eine 32-Bit-Version von Excel.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die Rolle „dqs_kb_editor“ oder „dqs_administrator“ in der DQS_MAIN-Datenbank verfügen, um eine Abgleichsrichtlinie zu erstellen.  
  
##  <a name="MatchingRules"></a> So legen Sie Abgleichsregelparameter fest  
 Das Erstellen einer Abgleichsregel ist ein iterativer Prozess, in dem Sie die Faktoren eingeben, der verwendet werden, um zu bestimmen, ob ein Datensatz mit einem anderen übereinstimmt. Sie können Bedingungen für eine beliebige Domäne in einer Tabelle eingeben. Wenn DQS zwei Datensätzen gegeneinander abgleicht, werden die Werte in den Feldern, die den Domänen zugeordnet sind, die in der Abgleichsregel enthalten sind, verglichen. DQS analysiert die Werte in jedem Feld der Regel, und verwendet dann die in der Regel eingegebenen Faktoren für jede Domäne, um eine abschließende Treffergenauigkeit zu berechnen. Wenn die Treffergenauigkeit für die zwei verglichenen Datensätze größer als die minimale Treffergenauigkeit ist, werden die zwei Felder als übereinstimmend angesehen.  
  
 Die Faktoren, die Sie in einer Abgleichsregel eingeben, schließen Folgendes ein:  
  
-   Gewichtung: Geben Sie für jede Domäne in der Regel eine numerische Gewichtung ein, die bestimmt, wie die Abgleichsanalyse für die Domäne mit der für jede andere Domäne in der Regel verglichen wird. Die Gewichtung gibt den Beitrag des Feldergebnisses zur Gesamttreffergenauigkeit zwischen zwei Datensätzen an. Die jedem Quellfeld zugewiesenen berechneten Ergebnisse werden für eine zusammengesetzte Treffergenauigkeit für die zwei Datensätze zusammengezählt. Legen Sie die Gewichtung zwischen 10 und 100 für jedes Feld fest, das keine erforderliche Komponente (mit einer genauen oder ähnlichen Entsprechung) ist. Die Summe der Gewichtungen der Domänen, die keine Voraussetzungen sind, muss gleich 100 sein. Wenn der Wert eine Voraussetzung ist, wird die Gewichtung auf 0 festgelegt und kann nicht geändert werden.  
  
-   Ähnlichkeit von Genau: Wählen Sie **Genau** aus, wenn die Werte im gleichen Feld von zwei verschiedenen Datensätzen für die Werte, die betrachtet werden sollen, identisch sein müssen, um als übereinstimmend angesehen zu werden. Falls die Werte identisch sind, wird die Treffergenauigkeit für diese Domäne auf „100“ festgelegt, und DQS verwendet dieses Ergebnis und die Ergebnisse für die anderen Domänen in der Regel, um die gesamte Treffergenauigkeit zu bestimmen. Falls die Werte nicht identisch sind, wird die Treffergenauigkeit für diese Domäne auf „0“ festgelegt, und die Verarbeitung der Regel schreitet zur nächsten Bedingung voran. Wenn Sie eine Abgleichsregel für eine numerische Domäne einrichten und **Ähnlich**auswählen, können Sie eine Toleranz als Prozentsatz oder als ganze Zahl eingeben. Für eine Domäne vom Typ Datum können Sie eine Toleranz als Tag, Monat oder Jahr (ganze Zahl) eingeben, wenn Sie **Ähnlich**auswählen; für eine Datumsdomäne gibt es keine Prozenttoleranz. Wenn Sie **Genau**auswählen, haben Sie diese Option nicht.  
  
-   Ähnlichkeit von Ähnlich: Wählen Sie **Ähnlich** aus, wenn zwei Werte im gleichen Feld von zwei verschiedenen Datensätzen auch dann als übereinstimmend angesehen werden können, wenn die Werte nicht identisch sind. Wenn DQS die Regel ausführt, wird eine Treffergenauigkeit für diese Domäne berechnet dieses Ergebnis und die Ergebnisse für die anderen Domänen in der Regel verwendet, um die gesamte Treffergenauigkeit zu bestimmen. Die minimale Ähnlichkeit zwischen den Werten eines Felds ist 60 %. Wenn die berechnete Treffergenauigkeit für ein Feld von zwei Datensätzen kleiner als 60 ist, wird das Ähnlichkeitsergebnis automatisch auf 0 festgelegt. Wenn Sie eine Abgleichsregel für ein numerisches Feld einrichten und **Ähnlich**auswählen, können Sie eine Toleranz als Prozentsatz oder als ganze Zahl eingeben. Wenn Sie eine Abgleichsregel für ein Datumsfeld einrichten und **Ähnlich**auswählen, können Sie eine numerische Toleranz eingeben.  
  
-   Voraussetzung: Wählen Sie **Voraussetzung** aus, um anzugeben, dass die Werte im gleichen Feld in zwei verschiedenen Datensätzen eine 100 %-Übereinstimmung zurückgeben müssen. Andernfalls werden die Datensätze nicht als Übereinstimmung angesehen, und die anderen Klauseln in der Regel werden ignoriert. Wenn **Voraussetzung** ausgewählt wird, wird das Gewichtungsfeld für die Domäne entfernt, sodass Sie keine Gewichtung für die Domäne definieren können. Sie müssen mindestens eine Domänengewichtung zurücksetzen, sodass die Summe der Gewichtungen gleich 100 ist. Voraussetzungsdomänen tragen nicht zur Datensatztreffergenauigkeit bei. Die Datensatztreffergenauigkeit wird durch das Vergleichen der Werte in Feldern, für die die Ähnlichkeit auf „Ähnlich“ oder „Genau“ festgelegt wurde, bestimmt. Wenn Sie ein Feld zu einer Voraussetzung machen, wird die Ähnlichkeit für diese Domäne automatisch auf „Genau“ festgelegt.  
  
 Die minimale Treffergenauigkeit ist der Schwellenwert ab dem zwei Datensätze als Übereinstimmung angesehen werden (der Status für die Datensätze wird auf „Matched“ festgelegt). Geben Sie einen ganzzahligen Wert in Schritten von „1“ ein, oder klicken Sie auf den Pfeil nach oben oder nach unten, um den Wert in Schritten von "10" zu vergrößern oder zu verringern. Der Mindestwert beträgt 80. Wenn die Treffergenauigkeit unter 80 liegt, werden die zwei Datensätze nicht als übereinstimmend angesehen. Sie können den Bereich der minimalen Treffergenauigkeit auf dieser Seite nicht ändern. Die niedrigste minimale Treffergenauigkeit ist 80. Sie können allerdings die niedrigste minimale Treffergenauigkeit auf der Verwaltungsseite ändern (wenn Sie DQS-Administrator sind).  
  
 Das Erstellen einer Abgleichsregel ist ein iterativer Prozess, da Sie möglicherweise die relativen Gewichtungen der Domänen in der Regel oder die Ähnlichkeit oder die erforderliche Eigenschaft für eine Domäne oder die minimale Treffergenauigkeit für die Regel ändern müssen, um die gewünschten Ergebnisse zu erzielen. Möglicherweise stellen Sie auch fest, dass Sie mehrere Regeln erstellen müssen, von denen jede ausgeführt wird, um die Treffergenauigkeit zu erstellen. Es ist möglicherweise schwierig, das benötigte Ergebnis mit nur einer Regel zu erzielen. Mehrere Regeln stellen andere Sichten einer erforderlichen Übereinstimmung bereit. Mit mehreren Regeln sind Sie möglicherweise in der Lage, weniger Domänen in die einzelnen Regeln einzuschließen, höhere Gewichtungen für die einzelnen Domänen zu verwenden und bessere Ergebnisse zu erzielen. Wenn die Daten weniger genau und weniger vollständig sind, benötigen Sie möglicherweise mehr Regeln, um erforderliche Übereinstimmungen zu finden. Wenn die Daten genauer und vollständiger sind, benötigen Sie weniger Regeln.  
  
 Die Profilerstellung gibt Einblicke in Vollständigkeit und Eindeutigkeit. Berücksichtigen Sie Vollständigkeit und Eindeutigkeit zusammen. Verwenden Sie Vollständigkeits- und Eindeutigkeitsdaten, um zu bestimmen, welche Gewichtung ein Feld im Abgleichsprozess erhalten soll. Wenn es einen hohen Eindeutigkeitsgrad in einem Feld gibt, können durch Verwenden des Felds in einer Abgleichsrichtlinie die Abgleichsergebnisse verringert werden. Daher sollten Sie die Gewichtung für dieses Feld auf einen relativ kleinen Wert festlegen. Wenn Sie für eine Spalte eine niedrige Eindeutigkeit, aber auch eine niedrige Vollständigkeit haben, sollten Sie keine Domäne für diese Spalte einschließen. Bei einer niedrigen Eindeutigkeit aber einer hohen Vollständigkeit sollten Sie die Domäne einschließen. Einige Spalten, z. B. Geschlecht, haben normalerweise einen niedrigen Eindeutigkeitsgrad. Weitere Informationen finden Sie unter [Profiler and Results Tabs](#Tabs).  
  
##  <a name="Starting"></a> Erster Schritt: Starten einer Abgleichsrichtlinie  
 Sie führen die Abgleichsrichtlinienaktivität im Wissensdatenbank-Verwaltungsbereich der Anwendung [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] aus.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Neue Wissensdatenbank** , um in einer neuen Wissensdatenbank eine Abgleichsrichtlinie zu erstellen. Geben Sie einen Namen für die Wissensdatenbank ein, geben Sie eine Beschreibung ein, und legen Sie **Wissensdatenbank erstellen aus** wie gewünscht fest. Klicken Sie für die Aktivität auf **Abgleichsrichtlinie** . Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  
  
3.  Klicken Sie auf **Wissensdatenbank öffnen** , um die Abgleichsrichtlinie in einer vorhandenen Wissensdatenbank zu erstellen oder zu ändern. Wählen Sie die Wissensdatenbank aus, wählen Sie **Abgleichsrichtlinie**aus, und klicken Sie dann auf **Weiter**. Sie können auch unter **Zuletzt verwendete Wissensdatenbank**auf eine Wissensdatenbank klicken. Wenn Sie eine Wissensdatenbank öffnen, die geschlossen wurde, während an einer Abgleichsrichtlinie gearbeitet wurde, fahren Sie mit der Phase fort, in der die Abgleichsrichtlinienaktivität geschlossen wurde (wie von der Spalte **Status** für die Wissensdatenbank in der Wissensdatenbanktabelle oder im Wissensdatenbanknamen unter **Zuletzt verwendete Wissensdatenbank**angegeben). Wenn Sie eine Wissensdatenbank öffnen, die eine Abgleichsrichtlinie enthält und abgeschlossen wurde, wechseln Sie zur Seite **Abgleichsrichtlinie** . Wenn Sie eine Wissensdatenbank öffnen, die keine Abgleichsrichtlinie enthält und abgeschlossen wurde, wechseln Sie zur Seite **Zuordnung** .  
  
##  <a name="MatchingStage"></a> Zuordnungsphase  
 In der Zuordnungsphase identifizieren Sie die Quelle der Daten, für die Sie die Abgleichsrichtlinie erstellen, und ordnen Domänen Quellspalten zu, um die Domänen für die Abgleichsrichtlinienaktivität verfügbar zu machen.  
  
1.  Behalten Sie auf der Seite **Struktur** zum Erstellen einer Richtlinie für eine Datenbank für **Datenquelle** die Option **SQL Server**bei, wählen Sie die Datenbank aus, für die Sie die Richtlinie in **Datenbank**erstellen möchten, und wählen Sie dann die Tabelle oder Sicht in **Tabelle/Sicht**aus. Die Quelldatenbank muss sich in der gleichen SQL Server-Instanz wie [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]befinden. Andernfalls wird sie nicht in der Dropdownliste angezeigt.  
  
2.  Um eine Richtlinie für die Daten in einem Excel-Arbeitsblatt zu erstellen, wählen Sie **Excel-Datei** für **Datenquelle**aus, klicken Sie auf **Durchsuchen** , und wählen Sie die Excel-Datei aus. Lassen Sie **Erste Zeile als Header verwenden** ggf. aktiviert. Wählen Sie in **Arbeitsblatt**das Arbeitsblatt in der Excel-Datei aus, das die Quelle der Daten ist. Microsoft Excel muss auf dem Data Quality-Clientcomputer installiert sein, um eine Excel-Datei auswählen zu können. Andernfalls ist die Schaltfläche „Durchsuchen“ nicht verfügbar, und Sie werden unter diesem Textfeld benachrichtigt, dass Microsoft Excel nicht installiert ist.  
  
3.  Wählen Sie unter **Zuordnungen**ein Feld für **Quellspalte**aus, und klicken Sie dann auf das Symbol **Domäne erstellen** .  
  
4.  Wählen Sie unter **Zuordnungen**ein Feld in der Datenquelle für **Quellspalte**aus, und wählen Sie dann die entsprechende Domäne aus. Wiederholen Sie den Vorgang für alle Domänen, die Sie im Abgleichsprozess verwenden. Erstellen Sie Domänen bei Bedarf durch Klicken auf **Domäne erstellen** oder **Verbunddomäne erstellen**.  
  
    > [!NOTE]  
    >  Sie können beim Erstellen einer Abgleichsrichtlinie Ihren Quelldaten nur dann einer DQS-Domäne zuordnen, wenn der Quelldatentyp in DQS unterstützt wird und mit dem DQS-Domänendatentyp übereinstimmt. Informationen zu in DQS unterstützten Datentypen finden Sie unter [Supported SQL Server and SSIS Data Types for DQS Domains](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
5.  Klicken Sie auf das Plussteuerelement **(+)** , um der Zuordnungstabellen eine Zeile hinzuzufügen, oder auf das Minussteuerelement **(-)** , um eine Zeile zu entfernen.  
  
6.  Klicken Sie auf **Vorschau der Datenquelle** , um die Daten in der ausgewählten SQL Server-Tabelle oder -Sicht oder im ausgewählten Excel-Arbeitsblatt anzuzeigen.  
  
7.  Klicken Sie auf **Verbunddomänen anzeigen/auswählen** , um eine Liste der in der Wissensdatenbank verfügbaren Verbunddomänen anzuzeigen und entsprechend für die Zuordnung auszuwählen.  
  
8.  Klicken Sie auf **Weiter** , um zur Abgleichsrichtlinienphase zu wechseln.  
  
    > [!NOTE]  
    >  Klicken Sie auf **Schließen** , um die Phase des Abgleichsprojekts zu speichern und zur DQS-Startseite zurückzukehren. Wenn Sie dieses Projekt das nächste Mal öffnen, befindet es sich in derselben Phase. Klicken Sie auf **Abbrechen** , um die Abgleichsaktivität zu beenden, ohne Ihre Arbeit zu speichern, und kehren Sie zur DQS-Startseite zurück.  
  
##  <a name="MatchingPolicyStage"></a> Abgleichsrichtlinienphase  
 Sie erstellen Abgleichsregeln und testen sie einzeln auf der Abgleichsrichtlinienseite. Wenn Sie eine Abgleichsregel auf der Seite **Abgleichsrichtlinie** testen, sehen Sie eine Abgleichsergebnistabelle, die die Cluster anzeigt, die DQS für die ausgewählte Regel identifiziert hat. In der Tabelle wird jeder Datensatz im Cluster mit den Zuordnungsdomänenwerten und der Treffergenauigkeit sowie der ursprüngliche Pivotdatensatz für den Cluster angezeigt. Sie können auch alle Profilerstellungsdaten für den Abgleichsprozess gemeinsam, die Bedingungen in den einzelnen Abgleichsregeln und die Statistiken zu den Ergebnissen für die einzelnen Abgleichsregeln separat anzeigen. Sie können nach den gewünschten Masterregeldaten filtern.  
  
 Weitere Informationen zur Funktionsweise von Abgleichsregeln finden Sie unter [So legen Sie Abgleichsregelparameter fest](#MatchingRules).  
  
1.  Klicken Sie auf der Seite **Abgleichsrichtlinie** auf das Symbol **Abgleichsregel erstellen** .  
  
2.  Geben Sie einen Namen und eine Beschreibung für die Regel ein.  
  
3.  Vergrößern Sie den Wert für **Minimale Treffergenauigkeit** , wenn Sie die Abgleichsanforderungen strenger machen möchten. Weitere Informationen zur minimalen Treffergenauigkeit finden Sie unter [So legen Sie Abgleichsregelparameter fest](#MatchingRules).  
  
4.  Klicken Sie auf das Symbol **Neues Domänenelement hinzufügen** .  
  
5.  Wählen Sie eine Domäne oder Verbunddomäne aus, für die Sie Regelwerte eingeben möchten.  
  
    > [!NOTE]  
    >  Sie können nur dann eine Verbunddomäne auswählen, wenn jede Einzeldomäne in der Verbunddomäne einer Quellspalte zugeordnet wurde.  
  
6.  Wählen Sie für **Ähnlichkeit**die Option **Ähnlich** aus, wenn zwei Werte im gleichen Feld von zwei verschiedenen Datensätzen auch dann als übereinstimmend angesehen werden können, wenn sie nicht identisch sind. Wählen Sie **Genau** aus, wenn zwei Werte im gleichen Feld von zwei verschiedenen Datensätzen identisch sein müssen, um als übereinstimmend angesehen zu werden. (Weitere Informationen finden Sie unter [So legen Sie Abgleichsregelparameter fest](#MatchingRules).)  
  
7.  Geben Sie für **Gewichtung**einen Wert ein, der den Beitrag der Treffergenauigkeit einer Domäne zur Gesamttreffergenauigkeit für zwei Datensätze bestimmt.  
  
    > [!NOTE]  
    >  Wenn Sie eine Gewichtung für eine Verbunddomäne definieren, können Sie eine andere Gewichtung für jede Einzeldomäne in der Verbunddomäne eingeben. In diesem Fall erhält die Verbunddomäne keine separate Gewichtung. Sie können auch eine einzelne Gewichtung für die Verbunddomäne eingeben, in der die Einzeldomänen keine separaten Gewichtungen erhalten.  
  
8.  Wählen Sie **Voraussetzung** aus, um anzugeben, dass die Werte für das Feld in den zwei Datensätzen eine 100 %-Übereinstimmung zurückgeben müssen. Andernfalls werden die Datensätze nicht als Übereinstimmung angesehen, und die anderen Klauseln in der Regel werden ignoriert. Wenn die **Ähnlichkeit** auf **Ähnlich**festgelegt wurde, wird sie zu **Genau**geändert, und die Gewichtung wird entfernt, da die Übereinstimmung 100 % betragen muss.  
  
9. Wiederholen Sie die Schritte 4 bis 8 für alle anderen Domänen, die Teil der Abgleichsregel sind. Stellen Sie sicher, dass die Summe der Gewichtungen für alle Domänen in der Regel 100 entspricht.  
  
10. Wählen Sie **Überlappende Cluster** aus der Dropdownliste aus, um die Pivotdatensätze und die folgenden Datensätze für alle Cluster anzuzeigen, wenn der Abgleich ausgeführt wird, auch wenn Gruppen von Clustern gemeinsame Datensätze aufweisen. Wählen Sie **Nicht überlappende Cluster** aus, um Cluster anzuzeigen, die als einzelne Cluster gemeinsame Datensätze aufweisen, wenn der Abgleich ausgeführt wird.  
  
11. Klicken Sie auf **Erneut aus Datenquelle laden** , um Daten aus der Datenquelle in die Stagingtabelle zu laden und neu zu indizieren, wenn Sie die Abgleichsrichtlinie ausführen. Klicken Sie auf **Für vorherige Daten ausführen** , um eine Abgleichsrichtlinie auszuführen, ohne die Daten in die Stagingtabelle zu kopieren und neu zu indizieren. **Für vorherige Daten ausführen** ist für die erste Ausführung der Abgleichsrichtlinie deaktiviert. Dies gilt auch, wenn Sie die Zuordnung auf der Seite **Struktur** ändern und in der folgenden Meldung auf **Ja** klicken. In beiden Fällen müssen Sie die Daten erneut indizieren. Die Neuindizierung ist nicht erforderlich, wenn die Abgleichsrichtlinie nicht geändert wurde. Durch die Ausführung für vorherige Daten kann die Leistung verbessert werden.  
  
12. Klicken Sie auf **Start** , um den Abgleichsprozess für die ausgewählte Regel auszuführen. Wenn der Prozess abgeschlossen wurde, werden in der Tabelle die Datensatz-ID, Clusternummer und Datenspalten (einschließlich derer, die sich nicht in der Abgleichsregel befinden) für jeden Datensatz in einem Cluster angezeigt. Die Pivotzeile im Cluster wird als erstklassiger Kandidat zum Verbleiben nach dem Deduplizierungsprozess angesehen. Jede zusätzliche Zeile in einem Cluster wird als Duplikat angesehen; seine Treffergenauigkeit (im Vergleich zum Pivotdatensatz) wird in der Ergebnistabelle bereitgestellt. Die Clusternummer ist mit der Datensatz-ID für den Pivotdatensatz im Cluster identisch.  
  
13. Sie können in der Tabelle **Abgleichsergebnisse** wie folgt mit den Daten arbeiten:  
  
    -   Wählen Sie unter **Filter**die Option **Matched** aus, um alle übereinstimmenden Zeilen und ihre Ergebnisse anzuzeigen. Zeilen, die nicht als übereinstimmend angesehen werden (die eine Treffergenauigkeit unterhalb der minimalen Treffergenauigkeit aufweisen), werden nicht in der Abgleichsergebnistabelle angezeigt. Wählen Sie **Keine Übereinstimmung** aus, um alle Zeilen ohne Übereinstimmung anzuzeigen, nicht die übereinstimmenden Zeilen.  
  
    -   Wählen Sie im Dropdownfeld **Prozent**einen Prozentwert (in Schritten von „5“) aus der Dropdownliste aus. Alle Zeilen mit einer Treffergenauigkeit, die größer oder gleich diesem Prozentwert ist, werden in der Abgleichsergebnistabelle angezeigt.  
  
    -   Wenn Sie auf einen Datensatz in der Abgleichsergebnistabelle doppelklicken, zeigt DQS das Popupfenster **Details zur Treffergenauigkeit** an, das den Pivotdatensatz und den Quelldatensatz anzeigt (und die Werte in allen ihren Feldern), das Ergebnis zwischen ihnen und einen Drilldown des Datensatzabgleichs. Der Drilldown zeigt die Werte in jedem Feld des Pivotdatensatzes und Quelldatensatzes an, damit Sie sie vergleichen können, und zeigt die Treffergenauigkeit an, die jedes Feld zur Gesamttreffergenauigkeit für die zwei Datensätze beiträgt.  
  
14. Zeigen Sie die Statistiken auf den Registerkarten **Profiler** und **Abgleichsergebnisse** an, um sicherzustellen, dass Sie die benötigten Ergebnisse erzielen. Weitere Informationen finden Sie unter [Profiler and Results Tabs](#Tabs).  
  
15. Wenn die Regel geändert werden muss, ändern Sie sie im Regel-Editor, und klicken Sie auf **Neustart**.  
  
    > [!NOTE]  
    >  Nachdem die erste Analyse abgeschlossen wurde, wird die Schaltfläche **Start** zur Schaltfläche **Neustart** . Wenn die Ergebnisse der vorherigen Analyse noch nicht gespeichert wurden, gehen beim Klicken auf **Neustart** die vorherigen Daten verloren. Verlassen Sie während der Ausführung der Analyse nicht die Seite, da ansonsten der Analyseprozess abgebrochen wird.  
  
16. Auf der Registerkarte **Abgleichsergebnisse** werden Statistiken für die letzten zwei Ausführungen der Regel angezeigt. Wenn Sie die Abgleichsregel mehr als einmal mit anderen Einstellungen ausgeführt haben, vergleichen Sie die Statistiken auf die aktuelle Regel und die vorherige Regel. Wenn Sie feststellen, dass die Ergebnisse der vorherigen Regel besser waren, klicken Sie auf **Vorherige Regel wiederherstellen** , um die Bedingungen der vorherigen Regel wiederherzustellen und die Regel auf den Status vor der Bearbeitung zurückzusetzen. Die aktuellen Regelbedingungen gehen verloren. Dies ermöglicht es Ihnen, die Richtlinie auf Grundlage der letzten zwei Abgleichsausführungen zu optimieren und die Zeit, die Sie zum Optimieren der Abgleichsrichtlinie aufgewendet haben, zu verringern.  
  
17. Wenn Sie der Abgleichsrichtlinie eine andere Regel hinzufügen möchten, wiederholen Sie den Vorgang ab Schritt 1.  
  
18. Klicken Sie auf **Weiter** , um zur Abgleichsergebnisphase zu wechseln.  
  
##  <a name="MatchingResultsStage"></a> Abgleichsergebnisphase  
 Sie testen alle Abgleichsregeln sofort auf der Seite **Abgleichsergebnisse** . Davor können Sie angeben, dass der Regeltestlauf überlappende oder nicht überlappende Cluster identifizieren soll. Wenn Sie die Regeln mehrfach ausführen, können Sie die Regel auf von der Quelle erneut geladenen Daten oder auf vorherigen Daten ausführen.  
  
 Wenn Sie die Abgleichsregeln auf der Seite **Abgleichsergebnisse** testen, sehen Sie eine Abgleichsergebnistabelle, die die Cluster anzeigt, die DQS für alle Regeln identifiziert hat. In der Tabelle wird jeder Datensatz im Cluster mit den Zuordnungsdomänenwerten und der Treffergenauigkeit sowie der ursprüngliche Pivotdatensatz für den Cluster angezeigt. Sie können auch alle Profilerstellungsdaten für die Abgleichsregeln gemeinsam, die Bedingungen in den einzelnen Abgleichsregeln und die Statistiken zu den Ergebnissen für alle Abgleichsregeln anzeigen.  
  
1.  Wählen Sie auf der Seite **Abgleichsergebnisse** aus der Dropdownliste die Option **Überlappende Cluster** aus, um die Pivotdatensätze und die folgenden Datensätze für alle Cluster anzuzeigen, wenn der Abgleich ausgeführt wird, auch wenn Gruppen von Clustern gemeinsame Datensätze aufweisen. Wählen Sie **Nicht überlappende Cluster** aus, um Cluster anzuzeigen, die als einzelne Cluster gemeinsame Datensätze aufweisen, wenn der Abgleich ausgeführt wird.  
  
2.  Klicken Sie auf **Erneut aus Datenquelle laden** , um Daten aus der Datenquelle in die Stagingtabelle zu laden und neu zu indizieren, wenn Sie die Abgleichsrichtlinie ausführen. Klicken Sie auf **Für vorherige Daten ausführen** , um eine Abgleichsrichtlinie auszuführen, ohne die Daten in die Stagingtabelle zu kopieren und neu zu indizieren. **Für vorherige Daten ausführen** ist für die erste Ausführung der Abgleichsrichtlinie deaktiviert. Dies gilt auch, wenn Sie die Zuordnung auf der Seite **Struktur** ändern und in der folgenden Meldung auf **Ja** klicken. In beiden Fällen müssen Sie die Daten erneut indizieren. Die Neuindizierung ist nicht erforderlich, wenn die Abgleichsrichtlinie nicht geändert wurde. Durch die Ausführung für vorherige Daten kann die Leistung verbessert werden.  
  
3.  Klicken Sie auf **Start** , um den Abgleichsprozess für alle von Ihnen definierten Regeln auszuführen. In der Tabelle **Abgleichsergebnisse** werden die Datensatz-ID, Clusternummer und Datenspalten (einschließlich derer, die sich nicht in der Abgleichsregel befinden) für jeden Datensatz in einem Cluster angezeigt. Der führende Datensatz im Cluster wird zufällig ausgewählt. (Sie bestimmen den überdauernden Datensatz durch Auswählen der Survivorship-Regel auf der Seite **Exportieren**, wenn Sie das Abgleichsprojekt ausführen.) Jede zusätzliche Zeile in einem Cluster wird als Duplikat angesehen; seine Treffergenauigkeit (im Vergleich zum Pivotdatensatz) wird in der Ergebnistabelle bereitgestellt.  
  
4.  Sie können in der Tabelle **Abgleichsergebnisse** wie folgt mit den Daten arbeiten:  
  
    -   Wählen Sie unter **Filter**die Option **Matched** aus, um alle übereinstimmenden Zeilen und ihre Ergebnisse anzuzeigen. Zeilen, die nicht als übereinstimmend angesehen werden (die eine Treffergenauigkeit unterhalb der minimalen Treffergenauigkeit aufweisen), werden nicht in der Abgleichsergebnistabelle angezeigt. Wählen Sie **Keine Übereinstimmung** aus, um alle Zeilen ohne Übereinstimmung anzuzeigen, nicht die übereinstimmenden Zeilen.  
  
    -   Wählen Sie im Dropdownfeld **Prozent**einen Prozentwert (in Schritten von „5“) aus der Dropdownliste aus. Alle Zeilen mit einer Treffergenauigkeit, die größer oder gleich diesem Prozentwert ist, werden in der Abgleichsergebnistabelle angezeigt.  
  
    -   Wenn Sie auf einen Datensatz in der Abgleichsergebnistabelle doppelklicken, zeigt DQS das Popupfenster **Details zur Treffergenauigkeit** an, das den Pivotdatensatz und den Quelldatensatz anzeigt (und die Werte in allen ihren Feldern), das Ergebnis zwischen ihnen und einen Drilldown des Datensatzabgleichs. Der Drilldown zeigt die Werte in jedem Feld des Pivotdatensatzes und Quelldatensatzes an, damit Sie sie vergleichen können, und zeigt die Treffergenauigkeit an, die jedes Feld zur Gesamttreffergenauigkeit für die zwei Datensätze beiträgt.  
  
5.  Zeigen Sie die Statistiken auf den Registerkarten **Profiler** und **Abgleichsergebnisse** an, um sicherzustellen, dass Sie die benötigten Ergebnisse erzielen. Klicken Sie auf die Registerkarte **Abgleichsregeln** , um die Domäneneinstellungen für die einzelnen Regeln anzuzeigen. Weitere Informationen finden Sie unter [Profiler and Results Tabs](#Tabs).  
  
6.  Wenn Sie mit den Ergebnissen aller Regeln nicht zufrieden sind, klicken Sie auf **Zurück** , um zur Seite **Abgleichsrichtlinie** zurückzukehren, ändern Sie ggf. eine oder mehrere Regeln, kehren Sie zur Seite **Abgleichsergebnisse** zurück, und klicken Sie dann auf **Neustart**.  
  
    > [!NOTE]  
    >  Nachdem die Analyse abgeschlossen wurde, wird die Schaltfläche **Start** zur Schaltfläche **Neustart** . Wenn die Ergebnisse der vorherigen Analyse noch nicht gespeichert wurden, gehen beim Klicken auf **Neustart** die vorherigen Daten verloren.  
  
7.  Wenn Sie mit den Ergebnissen aller Regeln zufrieden sind, klicken Sie auf **Fertig stellen** , um den Abgleichsrichtlinienprozess abzuschließen, und klicken Sie auf eine der folgenden Optionen:  
  
    -   **Ja – Wissensdatenbank veröffentlichen und beenden**: Die Wissensdatenbank wird veröffentlicht und kann vom aktuellen Benutzer oder von anderen Benutzern verwendet werden. Die Wissensdatenbank wird nicht gesperrt, der Status der Wissensdatenbank (in der Wissensdatenbanktabelle) wird auf leer festgelegt, und die Aktivitäten für die Domänenverwaltung sowie die Wissensermittlung sind verfügbar. Sie kehren zur Seite „Wissensdatenbank öffnen“ zurück.  
  
    -   **Nein – Arbeit in der Wissensdatenbank speichern und beenden**: Ihre Arbeit wird gespeichert, die Wissensdatenbank bleibt gesperrt, und der Status der Wissensdatenbank wird auf **In Arbeit**festgelegt. Sowohl die Domänenverwaltungs- als auch die Wissensermittlungsaktivitäten sind verfügbar. Sie kehren zur Startseite zurück.  
  
    -   **Abbrechen – Im aktuellen Fenster bleiben**: Das Popupfenster wird geschlossen, und Sie kehren zum Fenster „Domänenverwaltung“ zurück.  
  
8.  Klicken Sie auf **Schließen** , um die Arbeit zu speichern, und kehren Sie zur DQS-Startseite zurück. Der Status der Wissensdatenbank zeigt die Zeichenfolge „Abgleichsrichtlinie - “ und den aktuellen Status an. Wenn Sie auf **Schließen** klicken, während Sie auf dem Bildschirm **Abgleichsergebnis** sind, zeigt der Status Folgendes an: „Abgleichsrichtlinie - Ergebnisse“. Wenn Sie auf „Schließen“ klicken, während Sie auf dem Bildschirm **Abgleichsrichtlinie** sind, zeigt der Status Folgendes an: „Abgleichsrichtlinie - Abgleichsrichtlinie“. Nachdem Sie auf **Schließen**geklickt haben, um die **Wissensermittlungsaktivität** auszuführen, müssen Sie zur Aktivität **Abgleichsrichtlinie** zurückkehren, auf **Fertig stellen**klicken und dann auf **Ja** klicken, um die Wissensdatenbank zu veröffentlichen, oder auf **Nein** , um die Arbeit an der Wissensdatenbank zu speichern und zu beenden.  
  
    > [!NOTE]  
    >  Wenn Sie auf **Schließen** klicken, während ein Abgleichsprozess ausgeführt wird, wird der Abgleichsprozess nicht beendet, wenn Sie auf **Schließen**klicken. Sie können die Wissensdatenbank erneut öffnen und sehen, dass der Prozess immer noch ausgeführt wird oder dass die Ergebnisse angezeigt werden, falls er abgeschlossen wurde. Wenn der Prozess nicht abgeschlossen wurde, wird der Fortschritt auf dem Bildschirm angezeigt.  
  
9. Klicken Sie auf **Abbrechen** , um die Abgleichsrichtlinienaktivität abzubrechen, ohne die Ergebnisse zu speichern, und um zur DQS-Startseite zurückzukehren.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Erstellen einer Abgleichsrichtlinie  
 Nachdem Sie eine Abgleichsrichtlinie erstellt haben, können Sie ein Abgleichsprojekt basierend auf der Wissensdatenbank, die die Abgleichsrichtlinie enthält, ausführen. Weitere Informationen finden Sie unter [Run a Matching Project](../data-quality-services/run-a-matching-project.md).  
  
##  <a name="Tabs"></a> Profiler and Results Tabs  
 Die Registerkarten „Profiler“ und „Ergebnisse“ enthalten Statistiken für die Abgleichsrichtlinie und die Abgleichsergebnisseiten.  
  
###  <a name="Profiler"></a> Registerkarte „Profiler“  
 Klicken Sie auf die Registerkarte **Profiler** , um Statistiken für die Quelldatenbank und für alle in der Richtlinienregel enthaltenen Felder anzuzeigen. Die Statistiken werden aktualisiert, wenn die Richtlinienregel ausgeführt wird.  
  
 Weitere Informationen zum Interpretieren der folgenden Statistiken finden Sie unter [So legen Sie Abgleichsregelparameter fest](#MatchingRules).  
  
 Die Quelldatenbankstatistiken umfassen Folgendes:  
  
-   **Datensätze**: Die Gesamtzahl der Datensätze in der Quelldatenbank  
  
-   **Gesamtwerte**: Die Gesamtzahl der Werte in den Feldern der Datenquelle  
  
-   **Neue Werte**: Die Gesamtzahl der Werte, die seit der vorherigen Ausführung neu sind, und ihr prozentualer Anteil am Ganzen  
  
-   **Eindeutige Werte**: Die Gesamtzahl der eindeutigen Werte in den Feldern und ihr prozentualer Anteil am Ganzen  
  
-   **Neue eindeutige Werte**: Die Gesamtzahl der eindeutigen Werte, die neu in den Feldern sind, und ihr prozentualer Anteil am Ganzen  
  
 Die Feldstatistiken umfassen Folgendes:  
  
-   **Feldname**  
  
-   **Domänenname**  
  
-   **Neu**: Die Anzahl der neuen Werte und die Prozentzahlen neuer Werte im Vergleich zu vorhandenen Werten in der Domäne  
  
-   **Eindeutig**: Die Gesamtzahl der eindeutigen Datensätze in den Feldern und ihr prozentualer Anteil am Ganzen  
  
-   **Vollständigkeit**: Die Vollständigkeit jedes Quellfelds, das für den Abgleich zugeordnet ist  
  
###  <a name="Notifications"></a> Abgleichsrichtlinienbenachrichtigungen  
 Für die Abgleichsrichtlinienaktivität führen die folgenden Bedingungen zu Benachrichtigungen:  
  
-   Das Feld ist in allen Datensätzen leer; Sie sollten es aus der Zuordnung entfernen.  
  
-   Das Feldvollständigkeitsergebnis ist sehr niedrig; Sie sollten es aus der Zuordnung entfernen.  
  
-   Alle Werte in einem Feld sind ungültig; Sie sollten die Zuordnung und die Relevanz von Domänenregeln für den Feldinhalt überprüfen.  
  
-   Es gibt nur wenige gültige Werte im Feld; Sie sollten die Zuordnung und die Relevanz von Domänenregeln für den Feldinhalt überprüfen.  
  
-   Es gibt einen hohen Eindeutigkeitsgrad in diesem Feld. Das Verwenden dieses Felds in Abgleichsrichtlinien kann die Abgleichsergebnisse reduzieren.  
  
###  <a name="ResultsTab"></a> Registerkarte „Abgleichsergebnisse“  
 Klicken Sie auf die Registerkarte **Abgleichsergebnisse** , um Statistiken für die Ausführung der Abgleichsrichtlinienregel und der vorherigen Regel anzuzeigen. Wenn Sie die gleiche Regel mehrmals mit anderen Parametern ausgeführt haben, werden in der Abgleichsergebnistabelle Statistiken für beide Ausführungen angezeigt, sodass Sie sie miteinander vergleichen können. Sie können die vorherige Regel bei Bedarf auch wiederherstellen.  
  
 Die Statistiken umfassen Folgendes:  
  
-   Die Gesamtzahl der Datensätze in der Datenbank  
  
-   Die Gesamtzahl der übereinstimmenden Datensätze in der Datenbank  
  
-   Die Anzahl von Datensätzen in der Datenbank, die nicht als Duplikate angesehen werden  
  
-   Die Anzahl der ermittelten Cluster  
  
-   Die durchschnittliche Clustergröße (die Anzahl doppelter Datensätze geteilt durch die Anzahl der Cluster)  
  
-   Die geringste Anzahl von Duplikaten in einem Cluster  
  
-   Die größte Anzahl von Duplikaten in einem Cluster  
  
  
