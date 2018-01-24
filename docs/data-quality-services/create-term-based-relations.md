---
title: Erstellen von begriffsbasierten Beziehungen | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/08/2011
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dqs.dm.kbtermsbased.f1
ms.assetid: 66db9277-d892-4dae-8a82-060fd3ba6949
caps.latest.revision: "27"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fef7b422366598e1974a07e4ee36e0100157dfa2
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="create-term-based-relations"></a>Erstellen von begriffsbasierten Beziehungen
  In diesem Thema wird die Erstellung von begriffsbasierten Beziehungen für eine Domäne in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) beschrieben. Mithilfe von begriffsbasierten Beziehungen (Term-based Relation, TBR) können Sie eine Korrektur an einem Begriff vornehmen, der Teil eines Werts in einer Domäne ist. Mehrere Werte, die abgesehen von der Schreibweise eines gemeinsamen Teils identisch sind, werden als identische Synonyme angesehen. Sie können z. B. eine begriffsbasierte Beziehung einrichten, die den Begriff „Inc.“ in „Incorporated“ ändert. Der Begriff „Inc.“ wird jedes Mal geändert, wenn er in der Domäne vorkommt. Instanzen von „Contoso, Inc.“ werden in „Contoso, Incorporated“ geändert, und die beiden Werte werden als exakte Synonyme angesehen.  
  
 Um begriffsbasierte Beziehungen zu verwenden, erstellen Sie eine Liste mit Wert-/Ersetzungswertpaaren, z. B. „Inc.“ und „Incorporated“ oder „Senior“ und „Sr.“. Durch die Verwendung einer begriffsbasierten Beziehung können Sie einen Begriff in der gesamten Domäne ändern, ohne manuell einzelne Domänenwerte als Synonyme festzulegen. Sie können angeben, dass ein Wert korrigiert wird, auch wenn er nicht zuvor von der Wissensermittlung erkannt wurde. Wenn eine Transformation aufgrund einer begriffsbasierten Beziehung dazu führt, dass zwei Werte identisch sind, erstellt DQS zwischen ihnen eine Synonymbeziehung (in der Wissensermittlung), eine Korrekturbeziehung (in der Datenkorrektur) oder eine genaue Übereinstimmung (beim Abgleich).  
  
 Transformationen aufgrund einer begriffsbasierten Beziehung und Symboltransformationen (Sonderzeichen werden durch ein Leerzeichen oder einen NULL-Wert ersetzt) werden in einer Vorverarbeitungsphase vor der Analyse durchgeführt. Wenn eine Verbunddomänenanalyse angefordert wird, erfolgt diese vor den beiden Transformationen, da für die Trennzeichenanalyse Symbole erforderlich sind. Andere Vorgänge, z. B. Änderungen an Domänenregeln und Domänenwerten, werden nach den Transformationen ausgeführt. Beim Abgleich werden begriffsbasierte Beziehungen vor der Abgleichsaktivität auf die Quelldaten angewendet, unabhängig davon, ob die Bereinigung ausgeführt wird.  
  
 **Begriffsbasierte Beziehungen und Domänenverwaltung**  
  
 Wenn Sie in der Domänenverwaltung eine begriffsbasierte Beziehung anwenden, wendet DQS die Änderungen in den Prozessen zur Wissensermittlung, Bereinigung oder zum Abgleich an. DQS ändert jedoch nicht den Domänenwert selbst, um der begriffsbasierten Beziehung zu entsprechen. Anders ausgedrückt, wenn Sie auf der Registerkarte **Begriffsbasierte Beziehungen** der Seite **Domänenverwaltung** eine begriffsbasierte Beziehung eingeben und annehmen, wird die Änderung nicht auf der Registerkarte **Domänenwerte** der gleichen Seite vorgenommen. Dies ermöglicht es Ihnen, die begriffsbasierte Beziehung anschließend zu ändern.  
  
 **Begriffsbasierte Beziehungen und Datenbereinigung**  
  
 Wenn Sie eine begriffsbasierte Beziehung in einer Domäne anwenden und dann den Datenbereinigungsprozess ausführen, wendet DQS die Änderungen während der Bereinigung an, übernimmt jedoch die Änderungen nicht für Begriffe in der Wissensdatenbank.  
  
-   Wenn sich ein Wert, wie von einer begriffsbasierten Beziehung geändert, in der Domäne befindet, aber kein Synonym ist, wird er in der Spalte **Korrigieren in** auf der Registerkarte **Korrigiert** auf der Seite **Ergebnisse verwalten und anzeigen** angezeigt, wobei der Grund auf Begriffsbasierte Beziehung festgelegt ist.  
  
-   Wenn sich ein Wert, wie von einer begriffsbasierten Beziehung geändert, nicht in der Domäne befindet und DQS einen übereinstimmenden Wert findet, wird der Wert entsprechend korrigiert und auf der Registerkarte Korrigiert oder der Registerkarte Vorgeschlagen angezeigt, abhängig vom Vertrauensgrad. Wenn keine Übereinstimmung gefunden wird, wird der Wert unter Neu mit einer TBR-Korrektur angezeigt. Dies geschieht, weil eine TBR-Korrektur nicht bedeutet, dass der Wert korrekt ist.  
  
-   Wenn sich ein Wert, wie von einer begriffsbasierten Beziehung geändert, in der Domäne befindet, der Wert mit der vorhandenen Korrektur jedoch Fehler/Ungültig lautet, wird der Wert auf der Registerkarte Korrigiert mit seiner Korrektur und dem Grund Domänenwert angezeigt.  
  
-   Wenn sich ein Wert, wie von einer begriffsbasierten Beziehung geändert, in der Domäne befindet, der Wert ohne Korrektur jedoch Fehler/Ungültig lautet, wird der Wert auf der Registerkarte Ungültig mit dem Grund Domänenwert angezeigt.  
  
 **Begriffsbasierte Beziehungen und Wissensermittlung**  
  
 Wenn Sie eine begriffsbasierte Beziehung anwenden und dann den Wissensermittlungsprozess ausführen, werden alle Werte, die dem TBR entsprechen, nicht geändert und als richtiger Wert identifiziert. Alle Werte, die durch einen TBR geändert werden, werden als richtiger Wert importiert und als Synonym zu einem Wert identifiziert, der dem TBR entspricht.  
  
 **Begriffsbasierte Beziehungen und Importieren von Bereinigungswerten in eine Domäne**  
  
 Wenn Sie während des Bereinigungsprozesses gesammeltes Datenqualitätswissen in eine Domäne importieren, wird ein durch einen TBR geänderter Wert als richtiger Wert importiert.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Um begriffsbasierte Beziehungen zu erstellen, ist es erforderlich, dass eine Domäne in der Domänenverwaltungsaktivität geöffnet ist.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die dqs_kb_editor- oder dqs_administrator-Rolle in der DQS_MAIN-Datenbank verfügen, um begriffsbasierte Beziehungen zu erstellen.  
  
##  <a name="Create"></a> Erstellen von begriffsbasierten Beziehungen  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Öffnen oder erstellen Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm eine Wissensdatenbank. Wählen Sie **Domänenverwaltung** als Aktivität aus, und klicken Sie dann auf **Öffnen** oder **Erstellen**. Weitere Informationen finden Sie unter [Erstellen einer Wissensdatenbank](../data-quality-services/create-a-knowledge-base.md) oder [Öffnen einer Wissensdatenbank](../data-quality-services/open-a-knowledge-base.md).  
  
    > [!NOTE]  
    >  Die Domänenverwaltung wird auf einer Seite des Data Quality Service-Clients ausgeführt, der fünf Registerkarten für separate Domänenverwaltungsvorgänge enthält. Es ist kein assistentengesteuerter Prozess; jeder Verwaltungsvorgang kann getrennt ausgeführt werden.  
  
3.  Wählen Sie aus der **Domänenliste** auf der Seite **Domänenverwaltung** die Domäne aus, für die Sie eine Domänenregel erstellen möchten, oder erstellen Sie eine neue Domäne. Wenn Sie eine neue Domäne erstellen müssen, finden Sie unter [Domäne erstellen](../data-quality-services/create-a-domain.md)weitere Informationen.  
  
4.  Klicken Sie auf die Registerkarte **Begriffsbasierte Beziehungen** .  
  
5.  Sie können begriffsbasierte Beziehungen wie folgt erstellen:  
  
    1.  Klicken Sie auf **Neue Beziehung hinzufügen** , um eine Zeile in der Tabelle Beziehungen hinzuzufügen.  
  
    2.  Geben Sie in der Spalte **Wert** der hinzugefügten Zeile einen Begriff ein, der jedes Mal geändert werden soll, wenn er in einem Wert in der ausgewählten Domäne vorkommt.  
  
        > [!NOTE]  
        >  Wenn der Begriff als ganzer Wert in der Domäne vorkommt oder bereits als korrigierender Wert in der Domäne vorhanden ist, tritt ein Fehler auf.  
  
    3.  Geben Sie in der Spalte **Korrigieren in** einen Begriff ein, in den der Begriff in der Spalte **Wert** geändert werden soll.  
  
    4.  Klicken Sie erneut auf **Neue Beziehung hinzufügen** , um eine weitere begriffsbasierte Beziehung hinzuzufügen.  
  
    5.  Klicken Sie auf **Ausgewählte Beziehungen löschen** , um die ausgewählten Zeilen aus der Tabelle Beziehungen zu löschen. Sie können mehrere Zeilen auswählen, indem Sie die STRG-TASTE drücken und auf eine nicht ausgewählte Zeile klicken.  
  
    6.  Suchen Sie einen Wert in der Tabelle Beziehungen, indem Sie eine oder mehrere Ziffern im Textfeld **Suchen** eingeben. Die gefundenen Werte für die Zeichenfolge werden hervorgehoben. Wechseln Sie mithilfe der NACH-OBEN- und NACH-UNTEN-TASTE zu verschiedenen Instanzen der Zeichenfolge in der Tabelle.  
  
    7.  **Rechtschreibprüfung**: Wenn ein Wert in der Spalte **Wert** oder **Korrigieren in** eine wellige rote Unterstreichung aufweist, schlägt die Rechtschreibprüfung eine Korrektur für den Wert vor. Klicken Sie mit der rechten Maustaste auf den unterstrichenen Wert, und wählen Sie einen der von der Rechtschreibprüfung vorgeschlagenen Werte aus. Alternativ können Sie im Kontextmenü auf **Hinzufügen** klicken, um mit dem ursprünglichen Wert fortzufahren. Weitere Informationen finden Sie unter [Verwenden der DQS-Rechtschreibprüfung](../data-quality-services/use-the-dqs-speller.md) und [Domain-Eigenschaften festlegen](../data-quality-services/set-domain-properties.md).  
  
        > [!NOTE]  
        >  Um die Rechtschreibprüfung zu verwenden, können Sie diese auf der Seite **Domäneneigenschaften** aktivieren. Wenn sie auf der Seite **Domäneneigenschaften** deaktiviert ist, können Sie auf das Symbol **Rechtschreibprüfung aktivieren/deaktivieren** auf der Seite **Begriffsbasierte Beziehungen** klicken, um sie auf dieser Seite zu aktivieren.  
  
6.  Klicken Sie auf **Änderungen anwenden** , um die begriffsbasierten Beziehungen auf die Domäne anzuwenden.  
  
7.  Klicken Sie auf **Fertig stellen** , um die Domänenverwaltungsaktivität abzuschließen, wie in [End the Domain Management Activity](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)beschrieben.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Erstellen von begriffsbasierten Beziehungen  
 Nachdem Sie die begriffsbasierten Beziehungen erstellt haben, können Sie andere Domänenverwaltungsaufgaben in der Domäne ausführen. Sie können die Wissensermittlung durchführen, um der Domäne Wissen hinzuzufügen, oder Sie können der Domäne eine Abgleichsrichtlinie hinzufügen. Weitere Informationen finden Sie unter [Durchführen der Wissensermittlung](../data-quality-services/perform-knowledge-discovery.md), [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md) oder [Erstellen einer Abgleichsrichtlinie](../data-quality-services/create-a-matching-policy.md).  
  
  
