---
title: "Verwenden der DQS-Rechtschreibprüfung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 11/08/2011
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 65e4e53e-2699-4cae-a9e0-fe78547755b5
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a14a9adc633e997fa9f8095d3d98a11bc9d386aa
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="use-the-dqs-speller"></a>Verwenden der DQS-Rechtschreibprüfung
  Die [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS)-Rechtschreibprüfung überprüft die Syntax, Rechtschreibung und Satzstruktur von Zeichenfolgenwerten in einer Domäne. Die Rechtschreibprüfung ist eine eigenständige, clientseitige Funktion, die nicht in serverseitige Module integriert ist und keine Auswirkungen auf aktuelle Abläufe oder Status hat. Mit der Rechtschreibprüfung werden die Zeichenfolgenwerte identifiziert, bei denen es sich möglicherweise um Fehler handelt. Diese werden an der gleichen Stelle, an der andere manuelle Änderungen an Domänenwerten vorgenommen werden, mit einem roten Unterstrich markiert. Dazu gehören die folgenden Stellen:  
  
-   Die Seite **Domänenwerte verwalten** der Aktivität **Wissensermittlung**  
  
-   Die Seite **Domänenwerte** oder die Seite **Begriffsbasierte Beziehungen** der Aktivität **Domänenverwaltung**  
  
-   Die Seite **Ergebnisse verwalten und anzeigen** der Aktivität **Bereinigung**  
  
 Die Rechtschreibprüfung funktioniert nur in einzelnen Domänen mit dem Datentyp Zeichenfolge. Alle Werte in einer einzelnen Domäne des Datentyps Zeichenfolge werden zur Überprüfung an die Rechtschreibprüfung gesendet. Die Rechtschreibprüfung funktioniert weder für eine Verbunddomäne noch für Domänen, die nicht vom Typ Zeichenfolge sind, oder kombinierte Werte (z. B. Buchstaben und Zahlen ohne Leerzeichen), römische Ziffern, einzelne Zeichen bzw. Werte, die nur aus Großbuchstaben bestehen.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Um die Rechtschreibprüfung ausführen zu können, ist es erforderlich, dass eine Wissensdatenbank und eine Domäne in der Wissensermittlungs- oder Domänenverwaltungsaktivität geöffnet sind, die Rechtschreibprüfung für die entsprechende Domäne und Seite aktiviert ist und die Spracheigenschaft für die Domäne angegeben ist.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die dqs_kb_editor- oder dqs_administrator-Rolle in der DQS_MAIN-Datenbank verfügen, um die Rechtschreibprüfung ausführen zu können.  
  
##  <a name="Enable"></a> Aktivieren der Rechtschreibprüfung  
  
1.  Um die Rechtschreibprüfung in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]zu aktivieren, öffnen Sie die Wissensdatenbank in der Aktivität **Domänenverwaltung** , wählen Sie die gewünschte Domäne aus, und klicken Sie auf der Seite **Domäneneigenschaften** auf **Rechtschreibprüfung aktivieren** . Wählen Sie unter **Sprache**die Sprache für die Rechtschreibprüfung aus.  
  
2.  Wenn die Rechtschreibprüfung in den Domäneneigenschaften aktiviert wird, gilt die Aktivierung für die Seite **Domänenwerte verwalten** , die Seite **Domänenwerte** oder die Seite **Begriffsbasierte Beziehungen** und die Seite **Ergebnisse verwalten und anzeigen** . Um die Rechtschreibprüfung für diese Seiten zu deaktivieren, klicken Sie auf das Symbol **Rechtschreibprüfung aktivieren/deaktivieren** . Durch Klicken auf das Symbol wird der Status der Rechtschreibprüfung für die Seite geändert. Wenn die Eigenschaft **Rechtschreibprüfung aktivieren** für die Domäne deaktiviert ist, wird dementsprechend die Rechtschreibprüfung durch Klicken auf das Symbol **Rechtschreibprüfung aktivieren/deaktivieren** für die Seite aktiviert. Wenn Sie die Seite schließen und wieder öffnen, wird der Status der Schaltfläche durch die Domäneneigenschaft **Rechtschreibprüfung aktivieren** bestimmt.  
  
##  <a name="Use"></a> Verwenden der Rechtschreibprüfung  
  
1.  Wechseln Sie zu einer der folgenden Seiten:  
  
    -   Die Seite **Domänenwerte verwalten** der Aktivität **Wissensermittlung**  
  
    -   Die Seite **Domänenwerte** oder die Seite **Begriffsbasierte Beziehungen** der Aktivität **Domänenverwaltung**  
  
    -   Die Seite **Ergebnisse verwalten und anzeigen** der Aktivität **Bereinigung**  
  
2.  Zeigen Sie die gewünschten Werte in der Tabelle **Wert** an, indem Sie einen Filter anwenden oder danach suchen.  
  
3.  Scannen Sie die Zeilen in der Tabelle **Wert** , um festzustellen, ob Werte in den Spalten **Wert** oder **Korrigieren in** mit einem welligen roten Unterstrich markiert sind.  
  
4.  Klicken Sie mit der rechten Maustaste auf einen Wert, der durch einen roten Unterstrich markiert ist. Klicken Sie auf einen der aufgelisteten Ersetzungswerte, wenn dieser dem ursprünglichen Wert vorzuziehen ist.  
  
5.  Wenn kein vorgeschlagener Wert besser ist und die Schaltfläche **Weitere Vorschläge** auf zusätzliche Werte hinweist, klicken Sie darauf. Wenn einer der zusätzlichen Werte dem ursprünglichen Wert vorzuziehen ist, klicken Sie darauf.  
  
6.  Wenn Sie den Wert dem Wörterbuch hinzufügen möchten, klicken Sie auf **Zum Wörterbuch hinzufügen**. Der Wert ist nicht mehr mit einem roten Unterstrich markiert.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Verwenden der Rechtschreibprüfung  
 Nachdem Sie die Rechtschreibprüfung ausgeführt haben, schließen Sie die Aktivität ab, in der sich die Domäne befindet, um die von der Rechtschreibprüfung vorgeschlagenen Korrekturen zu verwenden. Wenn die Wissensermittlungs-, Domänenverwaltungs- oder Abgleichsrichtlinienaktivität durchgeführt wird, veröffentlichen Sie die Wissensdatenbank, um die Ergebnisse der Rechtschreibprüfung für die Verwendung in der Wissensdatenbank verfügbar zu machen. Weitere Informationen finden Sie unter [Durchführen der Wissensermittlung](../data-quality-services/perform-knowledge-discovery.md), [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md) oder [Erstellen einer Abgleichsrichtlinie](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="How"></a> Funktionsweise der Rechtschreibprüfung  
 Die DQS-Rechtschreibprüfung markiert jeden potenziellen Zeichenfolgenwertfehler mit einem roten Unterstrich, der für den gesamten Wert angezeigt wird. Wenn "New York" falsch geschrieben wurde, z. B. "Neu York", zeigt die Rechtschreibprüfung einen roten Unterstrich unter "Neu York" und nicht nur unter "Neu" an. Wenn Sie mit der rechten Maustaste auf den Wert klicken, sehen Sie vorgeschlagene Korrekturen für den gesamten Wert. Wenn mehr als fünf Vorschläge vorhanden sind, können Sie auch auf **Weitere Vorschläge** klicken. Sie können einen der Vorschläge auswählen oder dem Wörterbuch einen Wert hinzufügen (auf Benutzerkontoebene), der für den ursprünglichen Wert angezeigt werden soll. Dem Wörterbuch hinzugefügte Werte gelten für alle Domänen. Nur wenn Sie einen Vorschlag explizit festlegen, wird die Korrektur in der Domäne vorgenommen. Wenn Sie einen Vorschlag im Kontextmenü der Rechtschreibprüfung auswählen, ändert sich der Werttyp in einen Fehler (oder bleibt ein Fehler). Der ausgewählte Vorschlag wird der Korrekturspalte hinzugefügt. Beachten Sie, dass der **Typ** eines Werts mit **Richtig** angegeben und trotzdem von der Rechtschreibprüfung als potenzieller Fehler markiert sein kann.  
  
 DQS stellt Vorschläge für Werte sowohl in der Spalte **Wert** als auch in der Spalte **Korrigieren in** der Tabelle **Wert** bereit. Wenn Sie einen Vorschlag in der Spalte **Wert** auswählen, wird der Werttyp auf **Fehler**festgelegt, und der Vorschlag wird in die Spalte **Korrigieren in** kopiert, so als hätten Sie den Wert manuell eingefügt. Eine bereits vorhandene Korrektur wird zu einem Vorschlag. Wenn Sie auf der Seite **Ergebnisse verwalten und anzeigen** der Aktivität **Bereinigung** einen Vorschlag in der Spalte **Korrigieren in** auswählen, ersetzt DQS den derzeit ausgewählten Wert durch die Auswahl, und der derzeit ausgewählte Wert wird ein Vorschlag. Auf der Seite **Ergebnisse verwalten und anzeigen** der Aktivität **Bereinigung** werden keine Vorschläge auf Datensatzebene (das untere Raster) gemacht.  
  
  

