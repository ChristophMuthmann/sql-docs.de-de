---
title: "Erstellen einer Domänenregel | Microsoft-Dokumentation"
ms.custom: 
ms.date: 11/08/2011
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dqs.dm.testdomainrule.f1
- sql13.dqs.dm.rules.f1
ms.assetid: 339fa10d-e22c-4468-b366-080c33f1a23f
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dc02a0d982ceb08f631fbdf628dff293f1f8e5c7
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="create-a-domain-rule"></a>Erstellen einer Domänenregel
  In diesem Thema wird beschrieben, wie Sie eine Domänenregel in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) erstellen. Eine Domänenregel ist eine Bedingung, mit der Domänenwerte validiert, korrigiert und standardisiert werden. Eine Domänenregel muss über eine Domäne hinweg wahr sein, damit Domänenwerte als genau betrachtet werden und den Geschäftsanforderungen entsprechen. Domänenregeln können Überprüfungsregeln enthalten, die für die Überprüfung von Domänenwerten, aber nicht für die Korrektur von Daten in Data Quality-Projekten verwendet werden. Regeln umfassen auch Standardisierungsregeln, die auf gültige Daten angewendet und in der Datenkorrektur verwendet werden.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Um eine Domänenregel zu erstellen, müssen Sie eine Wissensdatenbank und eine Domäne in der Domänenverwaltungsaktivität geöffnet haben.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die dqs_kb_editor- oder dqs_administrator-Rolle in der DQS_MAIN-Datenbank verfügen, um eine Domänenregel zu erstellen.  
  
##  <a name="Build"></a> Erstellen von Domänenregeln  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Öffnen oder erstellen Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm eine Wissensdatenbank. Wählen Sie **Domänenverwaltung** als Aktivität aus, und klicken Sie dann auf **Öffnen** oder **Erstellen**. Weitere Informationen finden Sie unter [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md) oder [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md).  
  
    > [!NOTE]  
    >  Die Domänenverwaltung wird auf einer Seite des Data Quality Service-Clients ausgeführt, der fünf Registerkarten für separate Domänenverwaltungsvorgänge enthält. Es ist kein assistentengesteuerter Prozess; jeder Verwaltungsvorgang kann getrennt ausgeführt werden.  
  
3.  Wählen Sie aus der **Domänenliste** auf der Seite **Domänenverwaltung** die Domäne aus, für die Sie eine Domänenregel erstellen möchten, oder erstellen Sie eine neue Domäne. Wenn Sie eine neue Domäne erstellen müssen, finden Sie unter [Create a Domain](../data-quality-services/create-a-domain.md)weitere Informationen.  
  
4.  Klicken Sie auf die Registerkarte **Domänenregeln** .  
  
5.  Klicken Sie auf **Fügt eine neue Domänenregel hinzu**, und geben Sie dann einen eindeutigen Namen für die Wissensdatenbank und eine Beschreibung für die Regel ein.  
  
6.  Wählen Sie **Aktiv** aus, um anzugeben, dass die Regel ausgeführt wird (Standard), oder deaktivieren Sie Option, um zu verhindern, dass die Regel ausgeführt wird.  
  
7.  Wählen Sie im Bereich **Regel erstellen** aus der Dropdownliste im Feld der Regelklausel eine Bedingung aus.  
  
8.  Falls die Bedingung einen Wert erfordert, geben Sie den Wert im zugeordneten Textfeld ein.  
  
9. Klicken Sie auf das Symbol **Fügt der ausgewählten Klausel eine neue Bedingung hinzu** , wenn eine weitere Klausel erforderlich ist.  
  
10. Wählen Sie **AND** oder **OR** als Operator aus.  
  
11. Wählen Sie in der Dropdownliste eine Bedingung aus, und geben Sie ggf. einen Wert für den Operanden ein.  
  
12. Um die Reihenfolge der Klauseln in der Liste zu ändern, wählen Sie eine Klausel aus, und klicken Sie dann auf die NACH-OBEN- oder NACH-UNTEN-TASTE. Dadurch wird die Reihenfolge geändert, in der sie ausgeführt werden. Das kann Auswirkungen auf die Ergebnisse haben.  
  
13. Fügen Sie weitere Klauseln nach Bedarf hinzu. Wenn erforderlich, löschen Sie eine Klausel, indem Sie sie auswählen und auf **Löscht die ausgewählte Klausel**klicken.  
  
14. Wiederholen Sie ggf. diesen Vorgang, um neue Regeln hinzuzufügen.  
  
15. Um anzuzeigen, welche Auswirkungen eine Überprüfungsregel auf die Werte hat, wenn sie implementiert wird, klicken Sie auf **Analysiert die Auswirkung der Domänenregel auf die Domänenwerte** .  
  
16. Fahren Sie mit der nachfolgenden Testprozedur fort.  
  
##  <a name="Test"></a> Testen von Domänenregeln  
  
1.  Wählen Sie eine Regel aus, und klicken Sie auf das Symbol **Ausgewählte Domänenregel für Testdaten ausführen** .  
  
2.  Klicken Sie im Dialogfeld Domänenregel testen auf das Symbol **Fügt einen neuen Testbegriff für die Domänenregel hinzu** . Geben Sie einen Wert ein, um diesen zu testen. Geben Sie ggf. andere Werte ein. Wählen Sie einen Wert aus, und klicken Sie dann auf das Symbol **Entfernt den ausgewählten Testbegriff** , wenn erforderlich.  
  
3.  Klicken Sie auf das Symbol **Testet die Domänenregeln für alle Begriffe** .  
  
4.  Überprüfen Sie die Gültigkeit der einzelnen Begriffe. Eine Häkchen bedeutet "richtig", ein Kreuz bedeutet "Fehler" und ein Dreieck bedeutet "ungültig".  
  
5.  Klicken Sie auf **Schließen** , wenn Sie das Dialogfeld zum Testen nicht mehr benötigen.  
  
6.  Wiederholen Sie den Vorgang ggf. für andere Regeln.  
  
7.  Fahren Sie mit der nachfolgenden Anwendungsprozedur fort.  
  
##  <a name="Apply"></a> Anwenden von Domänenregeln  
  
1.  Klicken Sie auf **Alle Regeln anwenden** , um die Regeln auf die Werte in der Domäne anzuwenden. Nachdem Sie auf **Alle Regeln anwenden**geklickt haben, wird ein Popupfenster angezeigt, in dem angegeben ist, wie viele Werte in bestimmten Status von der Regel betroffen sind. Klicken Sie auf **Ja** , wenn Sie die Regel trotzdem anwenden möchten, oder auf **Nein** , um sie nicht anzuwenden. Wenn Sie auf **Ja**klicken, klicken Sie anschließend auf **OK** , um das Popupfenster mit den Ergebnissen zu schließen.  
  
    > [!NOTE]  
    >  Wenn Sie eine Regel erstellen oder ändern, müssen Sie die Änderungen nicht speichern. Sie müssen die Regel jedoch anwenden, damit die Änderungen wirksam werden.  
  
2.  Klicken Sie auf **Alle Änderungen verwerfen** , um alle Änderungen zu entfernen, die Sie an den Domänenregeln vorgenommen haben, und die zuvor angewendeten Regeln wiederherzustellen. Das führt dazu, dass alle Änderungen, die nach der letzten Anwendung der Regeln vorgenommen wurden, nicht mehr gelten. Die Gültigkeit jedes Werts in der Domäne wird dann nicht gemäß den verworfenen Änderungen, sondern gemäß den zuvor angewendeten Regeln aktualisiert.  
  
3.  Klicken Sie auf **Fertig stellen** , um die Domänenverwaltungsaktivität abzuschließen, wie in [End the Domain Management Activity](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)beschrieben.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Erstellen einer Domänenregel  
 Nachdem Sie eine Domänenregel erstellt haben, können Sie andere Domänenverwaltungsaufgaben in der Domäne ausführen. Sie können die Wissensermittlung durchführen, um der Domäne Wissen hinzuzufügen, oder Sie können der Domäne eine Abgleichsrichtlinie hinzufügen. Weitere Informationen finden Sie unter [Durchführen der Wissensermittlung](../data-quality-services/perform-knowledge-discovery.md), [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md) oder [Erstellen einer Abgleichsrichtlinie](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Conditions"></a> Domänenregelbedingungen  
 In der nachfolgenden Tabelle werden die Bedingungen beschrieben, die in der Domänenregel angewendet werden können. Die Tabelle enthält außerdem ein Beispiel zur Veranschaulichung, wie die Bedingungen angewendet werden können.  
  
 Wenn eine Domänenregel angewendet wird und ein Domänenwert nicht der Regel entspricht, wird der Wert auf Ungültig festgelegt. Ein Wert, für den Ungültig angegeben ist, wird in Richtig geändert, wenn die Regel, wegen der er ungültig ist, gelöscht oder deaktiviert wird bzw. so geändert wird, dass der Wert jetzt der Regel entspricht. Wenn Sie für einen Wert manuell Ungültig angegeben haben (auf der Registerkarte Domänenwerte der Aktivität Domänenverwaltung) und eine Regel, der der Wert nicht entspricht, gelöscht, deaktiviert oder geändert wird, bleibt der Wert trotzdem gemäß der manuellen Festlegung ungültig.  
  
 Eine Domänenregel mit einer definitiven Bedingung übernimmt die Regellogik für Synonyme des Werts in der Bedingung oder den Bedingungen sowie die Werte selbst. Die definitiven Bedingungen sind "Wert ist gleich", "Wert ist ungleich", "Wert ist in" oder "Wert ist nicht in". Angenommen, Sie haben die folgende Domänenregel: "Für 'Ort', Wert ist gleich 'Los Angeles'". Wenn "Los Angeles" und "LA" Synonyme sind, sind beide richtig. Wenn die Regel jedoch keine definitive Bedingung enthält, wie z. B. die Regel "Für 'Ort', Wert endet mit 's'", ist "Los Angeles" richtig, aber das Synonym "LA" ist falsch.  
  
 Beim Erstellen einer Domänenregel stehen verschiedene Alternativen zur Auswahl. Um beispielsweise zu überprüfen, ob Werte mit dem Buchstaben A, B oder C beginnen, können Sie eine einfache Regel mit einer komplexen Bedingung (z. B. ein regulärer Ausdruck mit Pipezeichen) erstellen, oder Sie können eine komplexe Regel erstellen, die mehrere einfache Bedingungen enthält. Beispiel für die erste Regel: "Wert enthält regulären Ausdruck (^A|^B|^C)". Beispiel für die zweite Regel: "'Wert beginnt mit A' OR 'Wert beginnt mit B' OR 'Wert beginnt mit C'".  
  
|Bedingung|Beschreibung|Beispiel|  
|---------------|-----------------|-------------|  
|Länge ist gleich|Nur die Werte, die die vom Operanden festgelegte Anzahl an Zeichen enthalten, sind gültig.|Beispieloperand: 3<br /><br /> Gültiger Wert: BB1<br /><br /> Ungültiger Wert: AA|  
|Länge ist größer als oder gleich|Nur die Werte, die mindestens die vom Operanden festgelegte Anzahl an Zeichen enthalten, sind gültig.|Beispieloperand: 3<br /><br /> Gültige Werte: BB1, BBAA<br /><br /> Ungültiger Wert: AA|  
|Länge ist kleiner als oder gleich|Nur die Werte, die höchstens die vom Operanden festgelegte Anzahl an Zeichen enthalten, sind gültig.|Beispieloperand: 3<br /><br /> Gültige Werte: BB1, AA<br /><br /> Ungültiger Wert: BBAA|  
|Wert ist gleich|Nur die Werte, die mit dem Operanden identisch sind, sind gültig.|Beispieloperand: BB1<br /><br /> Gültiger Wert: BB1<br /><br /> Ungültige Werte: BB, BB1#|  
|Wert ist ungleich|Nur die Werte, die mit dem Operanden nicht identisch sind, sind gültig.|Beispieloperand: BB1<br /><br /> Gültige Werte: BB, BB1#<br /><br /> Ungültiger Wert: BB1|  
|Wert enthält|Nur die Werte, von denen alle Zeichen in beliebiger Reihenfolge im Operanden enthalten sind, sind gültig.|Beispieloperand: A1<br /><br /> Gültige Werte: A1, AA1<br /><br /> Ungültige Werte: 1A, AA|  
|Wert enthält nicht|Nur die Werte, die nicht im Operanden enthalten sind, sind gültig.|Beispieloperand: A1<br /><br /> Gültige Werte: 1A, AA<br /><br /> Ungültige Werte: A1, AA1|  
|Wert beginnt mit|Nur die Werte, die mit den Zeichen im Operanden beginnen, sind gültig.|Beispieloperand: AA<br /><br /> Gültiger Wert: AA1<br /><br /> Ungültiger Wert: 1AAB|  
|Wert endet mit|Nur die Werte, die mit den Zeichen im Operanden enden, sind gültig.|Beispieloperand: AA<br /><br /> Gültiger Wert: 1AA<br /><br /> Ungültiger Wert: 1AAB|  
|Wert ist numerisch|Nur Werte eines numerischen SQL Server-Datentyps sind gültig. Dazu gehören "int", "decimal", "float" usw.|Beispieloperand: N/A<br /><br /> Gültige Werte: 1, 25, 345.1234<br /><br /> Nicht gültige Werte: 2b, bcdef|  
|Wert ist Datum\Uhrzeit|Nur Werte eines SQL Server-Datum\Uhrzeit-Datentyps sind gültig. Dazu gehören "datetime", "time", "date" usw.|Beispieloperand: N/A<br /><br /> Gültige Werte: 1916-06-04; 1916-06-04 18:24:24; March 21, 2001; 5/18/2011; 18:24:24<br /><br /> Ungültige Werte: 213. März 2006|  
|Wert ist in|Nur die Werte, die im Satz im Operanden enthalten sind, sind gültig.<br /><br /> Um die Werte im Satz einzugeben, klicken Sie in das Operandentextfeld, geben Sie den ersten Wert ein, drücken Sie die EINGABETASTE, geben Sie den zweiten Wert ein, und wiederholen Sie den Vorgang für alle Werte, die Sie im Satz eingeben möchten. Klicken Sie anschließend erneut in das Operandentextfeld. DQS fügt zwischen den Werten im Satz ein Komma hinzu. Wenn Sie eine einzelne Zeichenfolge mit Kommas und ohne Wagenrücklauf eingeben (z. B. "A1, B1"), wird diese Zeichenfolge in DQS als einzelner Wert im Satz angesehen.|Beispieloperand: [A1, B1]<br /><br /> Gültige Werte: A1, B1<br /><br /> Ungültige Werte: AA, 11|  
|Wert ist nicht in|Nur die Werte, die nicht im Satz im Operanden enthalten sind, sind gültig.|Beispieloperand: [A1, B1]<br /><br /> Gültige Werte: AA, 11<br /><br /> Ungültige Werte: A1, B1|  
|Wert entspricht Muster|Nur die Werte, die dem Muster der Zeichen, Ziffern oder Sonderzeichen im Operanden entsprechen, sind gültig.<br /><br /> Alle Buchstaben A (... Z) können als Muster für einen beliebigen Buchstaben verwendet werden; es wird Groß/Kleinschreibung unterschieden. Alle Ziffern (0... 9) können als Muster für eine beliebige Ziffer verwendet werden. Alle Sonderzeichen mit Ausnahme eines Buchstabes oder einer Ziffer können als Muster für sich selbst verwendet werden. Durch Klammern [] wird ein optionaler Abgleich definiert.|Beispieloperand: AA:000 (Muster von zwei *beliebigen* Zeichen, gefolgt von einem Doppelpunkt (:), wiederum gefolgt von drei *beliebigen* Ziffern.)<br /><br /> Gültige Werte: AB:012, df:257<br /><br /> Ungültige Werte: abc:123, FJ-369<br /><br /> Weitere Informationen zu Musterregeln in DQS und Beispiele finden Sie unter [Mustervergleich in DQS-Domänenregeln](http://blogs.msdn.com/b/dqs/archive/2012/10/08/pattern-matching-in-dqs-domain-rules.aspx).|  
|Wert entspricht keinem Muster|Nur die Werte, die dem Muster der Zeichen, Ziffern oder Sonderzeichen im Operanden nicht entsprechen, sind gültig.|Beispieloperand: A1 (Wert darf einem Muster eines *beliebigen* Zeichens, gefolgt von einer *beliebigen* Ziffer nicht entsprechen.)<br /><br /> Gültige Werte: AB1, A, A:5<br /><br /> Ungültige Werte: B7, c9|  
|Wert enthält Muster|Nur die Werte, die das Muster der Zeichen, Ziffern oder Sonderzeichen im Operanden enthalten, sind gültig.|Beispieloperand: AA-12 (Wert enthält ein Muster von zwei *beliebigen* Zeichen, gefolgt von einem Bindestrich (-), wiederum gefolgt von zwei *beliebigen* Ziffern.)<br /><br /> Gültige Werte: AAA-01, ab-975<br /><br /> Ungültiger Wert: A7, AA-6, C-45, aa;98|  
|Wert enthält kein Muster|Nur die Werte, die das Muster der Zeichen im Operanden nicht enthalten, sind gültig.|Beispieloperand: AB-12 (Wert darf ein Muster von zwei *beliebigen* Zeichen, gefolgt von einem Bindestrich (-), wiederum gefolgt von zwei *beliebigen* Ziffern nicht enthalten.)<br /><br /> Gültige Werte: A7, AA-6, C-45, aa;98<br /><br /> Ungültiger Wert: AAA-01, ab-975|  
|Der Wert stimmt mit dem regulären Ausdruck überein|Nur die Werte, die dem regulären Ausdruck im Operanden entsprechen, werden als gültig angesehen.<br /><br /> Der reguläre Ausdruck sollte nicht den Anker "^" oder "$" enthalten, da DQS diese Anker automatisch zu einer Klausel mit "Wert ist gleich regulärem Ausdruck" hinzufügt. (Alternativ können Sie den regulären Ausdruck, der die Anker "^" und "$" enthält, in Klammern einschließen.) Weitere Informationen zu regulären Ausdrücken finden Sie unter [Sprachelemente für reguläre Ausdrücke](http://go.microsoft.com/fwlink/?LinkId=225561).|Beispieloperand: [1-5] + (jedes Zeichen muss eine Ziffer von 1 bis 5 sein, die mindestens einmal vorkommt)<br /><br /> Gültige Werte: 123, 12345, 14352<br /><br /> Ungültige Werte: 456, ABC|  
|Der Wert stimmt nicht mit einem regulären Ausdruck überein|Nur die Werte, die nicht dem regulären Ausdruck im Operanden entsprechen, werden als gültig angesehen.|Beispieloperand: [1-5] + (die Zeichenfolge darf nicht nur Ziffern von 1 bis 5 enthalten)<br /><br /> Gültige Werte: 456, ABC<br /><br /> Ungültige Werte: 123, 123456, 14352|  
  
  
