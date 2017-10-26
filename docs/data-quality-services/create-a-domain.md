---
title: "Erstellen einer Domäne | Microsoft-Dokumentation"
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
- sql13.dqs.kb.createdomain.f1
ms.assetid: 5c4828f5-bd51-4c29-b3de-87b7d2f2d3e5
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 777b6f8a914aeea942399ee1291b569f12a419d6
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="create-a-domain"></a>Domäne erstellen
  In diesem Thema wird beschrieben, wie Sie eine Domäne in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) erstellen. Die Werte in der Domäne sind eine semantische Darstellung der Daten in einem Feld. Weitere Informationen zu Domänen finden Sie unter [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md).  
  
 Es gibt zwei Möglichkeiten, eine neue Domäne zu erstellen. Erstens während des Zuordnungsschritts der Wissensermittlungsaktivität, wenn Sie gerade ein Datenbeispiel analysieren, um einer neuen oder vorhandenen Wissensdatenbank Wissen hinzuzufügen. Zweitens während der Domänenverwaltungsaktivität, wenn Sie eine neue Domäne erstellen, anstatt eine vorhandene zu ändern.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Voraussetzungen  
 Um eine Domäne zu erstellen, müssen Sie eine Wissensdatenbank erstellt und geöffnet haben.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die dqs_kb_editor- oder dqs_administrator-Rolle in der DQS_MAIN-Datenbank verfügen, um eine Domäne zu erstellen.  
  
##  <a name="Discovery"></a> Erstellen einer Domäne in der Wissensermittlungsaktivität  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Wissensdatenbank öffnen** , und wählen Sie dann eine Wissensdatenbank aus, oder klicken Sie auf **Neue Wissensdatenbank** , und geben Sie Eigenschaften für die neue Wissensdatenbank ein.  
  
3.  Wählen Sie die Aktivität **Wissensermittlung** aus, und klicken Sie dann auf **Erstellen** , um die neue Wissensdatenbank zu erstellen, oder auf **Öffnen** , um eine vorhandene Wissensdatenbank zu öffnen.  
  
4.  Geben Sie auf der Seite **Zuordnen** eine Verbindung zur Datenquelle an. Weitere Informationen finden Sie unter [Perform Knowledge Discovery](../data-quality-services/perform-knowledge-discovery.md).  
  
5.  Wählen Sie in der Tabelle **Zuordnungen** eine Quellspalte aus der Dropdownliste für die Spalte **Quellspalte** einer leeren Zeile aus. Wenn keine entsprechenden Domänen vorhanden ist, klicken Sie auf das Symbol **Domäne erstellen** .  
  
##  <a name="DomainManagement"></a> Erstellen einer Domäne in der Domänenverwaltungsaktivität  
  
1.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Wissensdatenbank öffnen** , und wählen Sie dann eine Wissensdatenbank aus, oder klicken Sie auf **Neue Wissensdatenbank** , und geben Sie Eigenschaften für die neue Wissensdatenbank ein.  
  
2.  Wählen Sie die Aktivität **Domänenverwaltung** aus, und klicken Sie dann auf **Erstellen** , um die neue Wissensdatenbank zu erstellen, oder auf **Öffnen** , um eine vorhandene Wissensdatenbank zu öffnen.  
  
3.  Klicken Sie auf der Seite **Domänenverwaltung** über der Domänenliste auf das Symbol **Domäne erstellen** .  
  
##  <a name="Properties"></a> Festlegen von Domäneneigenschaften  
  
1.  Geben Sie im Dialogfeld **Domäne erstellen** einen eindeutigen Namen für die Wissensdatenbank und eine Beschreibung mit maximal 256 Zeichen ein.  
  
    > [!NOTE]  
    >  Weitere Informationen zu den Domäneneigenschaften finden Sie unter [Set Domain Properties](../data-quality-services/set-domain-properties.md).  
  
2.  Wählen Sie in der Liste **Datentyp** einen Datentyp für die Werte in der Domäne aus. Der Datentyp kann **Zeichenfolge** (Standard), **Datum**, **Ganze Zahl**oder **Dezimal**sein.  
  
3.  Wählen Sie **Führende Werte verwenden** aus, um anzugeben, dass der führende Wert in einer Gruppe von Synonymen statt eines Werts ausgegeben wird, der ein Synonym dafür ist. Deaktivieren Sie **Führende Werte verwenden** , um anzugeben, dass jeder Synonymwert in seinem richtigen oder korrigierten Format ausgegeben und nicht durch den führenden Wert für die zugehörige Gruppe ersetzt wird.  
  
4.  Wenn der Datentyp **Zeichenfolge**angegeben ist, wählen Sie **Zeichenfolge normalisieren** aus, um Sonderzeichen in den Domänenwerten zu entfernen. Dies kann die Wahrscheinlichkeit von Übereinstimmungen erhöhen.  
  
5.  Wählen Sie in der Dropdownliste **Formatausgabe** die Formatierung aus, die beim Ausgeben der Datenwerte in der Domäne angewendet wird. Die Formatierung ist für den in Schritt 2 ausgewählten Datentyp spezifisch, wie in der folgenden Liste gezeigt:  
  
    -   Für einen Zeichenfolgenwert können Sie angeben, dass die Zeichenfolge in Großbuchstaben, in Kleinbuchstaben oder in Großschreibung ausgegeben wird.  
  
    -   Für einen Datumswert können Sie das Format von Tag, Monat und Jahr angeben.  
  
    -   Für einen ganzzahligen Wert können Sie den Typ der Formatmaske angeben, die angewendet werden soll.  
  
    -   Für einen Dezimalwert können Sie die Genauigkeit und den Typ der Formatmaske angeben, die angewendet werden soll.  
  
     Wenn Sie **Keine** in der Dropdownliste **Formatausgabe** auswählen, bedeutet dies, dass keines der Formate in der Liste angewendet wird.  
  
6.  Wenn der Datentyp **Zeichenfolge**angegeben ist, wählen Sie in der Dropdownliste **Sprache** die Sprachversion der Rechtschreibprüfung aus, die verwendet werden soll, wenn die Rechtschreibprüfung aktiviert ist.  
  
7.  Wählen Sie für den Datentyp **Zeichenfolge**die Option **Rechtschreibprüfung aktivieren** aus, um die Rechtschreibprüfung beim Auffüllen der Domäne für alle Zeichenfolgenwerte auszuführen.  
  
8.  Wählen Sie für den Datentyp **Zeichenfolge**die Option **Syntaxfehleralgorithmen deaktivieren** aus, um die Domäne aufzufüllen, ohne die Zeichenfolgenwerte auf Syntaxfehler zu überprüfen.  
  
9. Klicken Sie auf **OK**.  
  
10. Klicken Sie auf **Fertig stellen** , um die Domänenverwaltungsaktivität abzuschließen, wie in [End the Domain Management Activity](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)beschrieben.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Erstellen einer Domäne  
 Nachdem Sie eine Domäne erstellt haben, können Sie andere Domänenverwaltungsaufgaben in der Domäne ausführen. Sie können die Wissensermittlung durchführen, um der Domäne Wissen hinzuzufügen, oder Sie können der Domäne eine Abgleichsrichtlinie hinzufügen. Weitere Informationen finden Sie unter [Durchführen der Wissensermittlung](../data-quality-services/perform-knowledge-discovery.md), [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md) oder [Erstellen einer Abgleichsrichtlinie](../data-quality-services/create-a-matching-policy.md).  
  
  

