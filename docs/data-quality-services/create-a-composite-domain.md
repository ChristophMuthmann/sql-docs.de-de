---
title: "Erstellen einer Verbunddom&#228;ne | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2011"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.kb.createcd.f1"
  - "sql13.dqs.dm.cdproperties.f1"
ms.assetid: c7f0bd84-a02e-4a81-885d-985e6415c499
caps.latest.revision: 21
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 21
---
# Erstellen einer Verbunddom&#228;ne
  In diesem Thema wird beschrieben, wie eine Verbunddomäne in einer Wissensdatenbank in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) erstellt wird. Eine Verbunddomäne besteht aus einer oder mehreren Einzeldomänen, die für ein einzelnes Datenfeld gelten. Weitere Informationen zu verbunddomänen finden Sie unter [Verwalten einer Verbunddomäne](../data-quality-services/managing-a-composite-domain.md).  
  
 Es gibt zwei Möglichkeiten, eine neue Verbunddomäne zu erstellen. Erstens während des Strukturschritts der Wissensermittlungsaktivität, wenn Sie gerade ein Datenbeispiel analysieren, um einer neuen oder vorhandenen Wissensdatenbank Wissen hinzuzufügen. Zweitens während der Domänenverwaltungsaktivität, wenn Sie eine neue Domäne erstellen, anstatt eine vorhandene zu ändern. Um eine Verbunddomäne zu erstellen, müssen Sie bereits mindestens zwei Einzeldomänen erstellt haben, um die Verbunddomäne hinzufügen zu können. Nur die Einzeldomänen, die bereits erstellt wurden und keiner vorhandenen Verbunddomäne hinzugefügt wurden, sind verfügbar, wenn Sie eine neue Verbunddomäne erstellen. Eine Einzeldomäne kann nur genau einer Verbunddomäne hinzugefügt werden, und eine Verbunddomäne kann keiner anderen Verbunddomäne hinzugefügt werden.  
  
 Nach dem Erstellen einer Verbunddomäne können Sie die Eigenschaften der Verbunddomäne ändern, einen Verweisdatendienst an die Domäne anfügen, domänenübergreifende Regeln oder Wertebeziehungen erstellen. Wählen Sie hierzu die Verbunddomäne in der Liste **Domäne** auf der Seite **Domänenverwaltung** und dann die entsprechende Registerkarte aus.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Um eine Verbunddomäne zu erstellen, müssen Sie eine Wissensdatenbank erstellt und geöffnet und mindestens zwei Einzeldomänen erstellt haben, um die Verbunddomäne hinzufügen zu können.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die Rolle „dqs_kb_editor“ oder „dqs_administrator“ in der DQS_MAIN-Datenbank verfügen, um eine Verbunddomäne zu erstellen.  
  
##  <a name="ParsingKnowledgeDiscoveryActivity"></a> Erstellen einer Verbunddomäne in der Wissensermittlungsaktivität  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Wissensdatenbank öffnen** , und wählen Sie dann eine Wissensdatenbank aus, oder klicken Sie auf **Neue Wissensdatenbank** , und geben Sie Eigenschaften für die neue Wissensdatenbank ein.  
  
3.  Wählen Sie die Aktivität **Wissensermittlung** aus, und klicken Sie dann auf **Erstellen** , um die neue Wissensdatenbank zu erstellen, oder auf **Öffnen** , um eine vorhandene Wissensdatenbank zu öffnen.  
  
4.  Geben Sie auf der Seite **Zuordnen** eine Verbindung zur Datenquelle an. Weitere Informationen finden Sie unter [Perform Knowledge Discovery](../data-quality-services/perform-knowledge-discovery.md).  
  
5.  In der **Zuordnungen** table, wählen Sie eine Quellspalte aus der Dropdown-Liste für die **Quellspalte** Spalte einer leeren Zeile. Stellen Sie sicher, dass die Quellspalte eine Verbunddomäne enthält, die von zwei vorhandenen Einzeldomänen adressiert wird. Wenn keine entsprechenden Einzeldomänen vorhanden sind, klicken Sie auf das Symbol **Domäne erstellen** .  
  
6.  In der **Zuordnungen** table, wählen Sie eine Quellspalte aus der Dropdown-Liste für die **Quellspalte** Spalte einer leeren Zeile. Stellen Sie sicher, dass die Quellspalte Teile einer Verbunddomäne enthält, die von zwei vorhandenen Einzeldomänen adressiert wird. Wenn keine entsprechenden Einzeldomänen vorhanden sind, klicken Sie auf das Symbol **Domäne erstellen** , um sie zu erstellen. Weitere Informationen finden Sie unter [Create a Domain](../data-quality-services/create-a-domain.md).  
  
7.  Klicken Sie auf das Symbol **Verbunddomäne erstellen** .  
  
##  <a name="DomainManagementActivity"></a> Erstellen einer Verbunddomäne in der Domänenverwaltungsaktivität  
  
1.  Klicken Sie auf der Startseite des Data Quality Services-Clients auf **Wissensdatenbank öffnen** , und wählen Sie dann eine Wissensdatenbank aus, oder klicken Sie auf **Neue Wissensdatenbank** , und geben Sie Eigenschaften für die neue Wissensdatenbank ein.  
  
2.  Wählen Sie die Aktivität **Domänenverwaltung** aus, und klicken Sie dann auf **Erstellen** , um die neue Wissensdatenbank zu erstellen, oder auf **Öffnen** , um eine vorhandene Wissensdatenbank zu öffnen.  
  
3.  Stellen Sie sicher, dass mindestens zwei für die Verbunddomäne erforderliche Einzeldomänen vorhanden sind. Klicken Sie andernfalls auf das Symbol **Domäne erstellen** , und erstellen Sie die Domänen. Weitere Informationen finden Sie unter [Create a Domain](../data-quality-services/create-a-domain.md).  
  
4.  Klicken Sie auf der Seite **Domänenverwaltung** oberhalb der Domänenliste auf das Symbol **Verbunddomäne erstellen** .  
  
5.  Geben Sie einen Namen ein, der für die Wissensdatenbank eindeutig ist, und eine Beschreibung mit bis zu 256 Zeichen.  
  
6.  Wählen Sie in der **Domänenliste**die Domänen aus, die Teil der Verbunddomäne sein werden, und klicken Sie auf den Pfeil nach rechts, um sie in die Tabelle **Domänen in Verbunddomäne** zu verschieben.  
  
7.  Klicken Sie auf **OK**.  
  
##  <a name="CompositeDomainProperties"></a> Festlegen von Verbunddomäneneigenschaften  
  
1.  Geben Sie im Dialogfeld **Verbunddomäne erstellen** einen Namen ein, der für die Wissensdatenbank eindeutig ist, und eine Beschreibung mit bis zu 256 Zeichen.  
  
2.  Wählen Sie in der **Domänenliste**die Domänen aus, die Teil der Verbunddomäne sein werden, und klicken Sie auf den Pfeil nach rechts, um sie in die Tabelle **Domänen in Verbunddomäne** zu verschieben. Dies ist eine Liste von Einzeldomänen, die verfügbar sind, um der Verbunddomäne, die Sie erstellen, hinzugefügt zu werden. Nur die Einzeldomänen, die bereits erstellt wurden und keiner vorhandenen Verbunddomäne hinzugefügt wurden, sind verfügbar. Eine Einzeldomäne kann nur genau einer Verbunddomäne in der Wissensdatenbank hinzugefügt werden, und eine Verbunddomäne kann keiner anderen Verbunddomäne hinzugefügt werden.  
  
3.  Klicken Sie auf **Erweitert**.  
  
4.  Wählen Sie für **Analysemethode**eine der folgenden Optionen aus:  
  
    -   **Verweisen auf Daten**: Analysieren von Werten des Felds, wie die Daten von der Reference Data Service (RDS) formatiert ist. Data Quality Services sendet die Werte in der Verbunddomäne an den RDS, und der RDS gibt die gemäß der Domäne in der Verbunddomäne korrigierten und analysierten Daten zurück.  
  
    -   **Reihenfolge**: Analysieren Sie die Werte des Felds nach der Reihenfolge der Domänen in der Verbunddomäne. Der erste Wert wird in der ersten Domäne eingeschlossen, der zweite Wert in der zweiten Domäne usw.  
  
    -   **Trennzeichen**: Analysieren Sie die Werte des Felds auf Grundlage des Trennzeichens, das aus den Optionsfeldern ausgewählt wurde, wenn „Trennzeichen“ ausgewählt wird. Kann **Tabulator**, **Semikolon**, **Komma**, **Leerzeichen**oder **Anderes**sein. Geben für **Anderes**den Wert ein, der als Trennzeichen dienen soll.  
  
5.  Wenn Sie **Trennzeichen** als Analysemethode ausgewählt haben, können Sie auch **Analyse der Wissensdatenbank verwenden**auswählen. Weitere Informationen finden Sie unter [Analyse der Wissensdatenbank](#KnowledgeBaseParsing).  
  
6.  Klicken Sie auf **Fertig stellen** , um die Domänenverwaltungsaktivität abzuschließen, wie in [End the Domain Management Activity](../Topic/End%20the%20Domain%20Management%20Activity.md)beschrieben.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Erstellen einer Verbunddomäne  
 Nachdem Sie eine Verbunddomäne erstellt haben, können Sie andere Domänenverwaltungstasks in der Domäne ausführen, Sie können die Wissensermittlung durchführen, um der Domäne Wissen hinzuzufügen, oder Sie können der Domäne eine Abgleichsrichtlinie hinzufügen. Weitere Informationen finden Sie unter [Durchführen der Wissensermittlung](../data-quality-services/perform-knowledge-discovery.md), [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md), oder [Erstellen einer Abgleichsrichtlinie](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="KnowledgeBaseParsing"></a> Analyse der Wissensdatenbank  
 Data Quality Services ermöglicht es Ihnen, Daten auf Grundlage des Wissens, nicht nur nach Trennzeichen oder Reihenfolge, zu analysieren. Die Analyse der Wissensdatenbank wird verwendet, wenn einer Verbunddomäne komplexe Quelldaten zugeordnet werden und Sie keine Verweisdatendienste verwenden. Sie können die Analyse der Wissensdatenbank verwenden, um die Daten aus der Datenquelle in die relevanten Einzeldomänen zu analysieren. Mit der Analyse der Wissensdatenbank versucht DQS zunächst, Wissen zu verwenden, um komplexe Daten in einzelne Domänen zu analysieren. Wenn möglich identifiziert DQS Teile der Zeichenfolge wie in einer oder mehreren Domänen und analysiert die Zeichenfolge in seine verschiedenen Domänen. Beispiel: Sie haben „John B. Doe“ als komplexen Wert in einem Feld für den vollen Namen, das durch eine Verbunddomäne „Voller Name“ dargestellt wird. Wenn DQS „John“ als Teil der Vornamendomäne und „Doe“ als Teil der Nachnamendomäne identifiziert, fügt DQS auf Grundlage des Domänenwissens „B.“  zur Domäne für den zweiten Vornamen hinzu.  
  
 Sie können die Analyse der Wissensdatenbank nur verwenden, wenn Sie auch die auf Trennzeichen basierende Analyse auswählen. Die Analyse der Wissensdatenbank ersetzt nicht die Trennzeichenanalyse, sondern erweitert sie. Nur, wenn kein Wissen dafür vorhanden ist, verwendet DQS für die Analyse ein Trennzeichen. In einigen Fällen bestimmt DQS möglicherweise die eine Analyse durch die Analyse der Wissensdatenbank und bestimmt dann eine andere Analyse durch die auf Trennzeichen basierte Analyse.  
  
 Die Analyse der Wissensdatenbank kann verwendet werden, wenn die Verbunddomäne aus Zeichenfolgendomänen besteht oder wenn die Verbunddomäne aus einer Mischung verschiedener Domänentypen besteht (int, date, time usw.). Wenn die Datenquelle aus anderen Datentypen besteht, sollte die Analyse zuerst für die Nicht-Zeichenfolgen-Datentypen ausgeführt werden und dann für die restlichen Daten, wie oben beschrieben, auf Grundlage des Domänenwissens.  
  
 Wenn Sie die Analyse der Wissensdatenbank verwenden und es weniger Werte in den Quelldaten als Domänen in der Verbunddomäne gibt, fügt DQS eine NULL in der fehlenden Domäne ein. Wenn es mehr Werte in den Quelldaten als Domänen in der Verbunddomäne gibt, fügt DQS einer der Spalten die zusätzlichen Daten hinzu. Wenn mindestens zwei Domänen die gleichen Werte enthalten, wird die Datenquelle zur ersten abgeglichenen Domäne analysiert.  
  
  