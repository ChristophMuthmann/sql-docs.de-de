---
title: Verwalten einer Wissensdatenbank | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/04/2013
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27f306f4-d67c-47f5-b35c-4260cc5d36e3
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e725235e961b2f40765525d4812ddb7160657361
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="manage-a-knowledge-base"></a>Verwalten einer Wissensdatenbank
  In diesem Thema wird beschrieben, wie Verwaltungsfunktionen für eine Wissensdatenbank in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) ausgeführt werden. Sie können eine Wissensdatenbank löschen, entsperren, umbenennen, vorgenommene Anpassungen verwerfen und die Eigenschaften der Wissensdatenbank anzeigen.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Voraussetzungen  
 Um eine Wissensdatenbank zu verwalten, muss die Wissensdatenbank bereits erstellt und entweder veröffentlicht (wenn sie eine andere Person erstellt hat) oder geschlossen (wenn Sie sie erstellt haben) worden sein.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die Rolle "dqs_kb_editor" oder "dqs_administrator" in der DQS_MAIN-Datenbank verfügen, um eine Wissensdatenbank zu öffnen.  
  
##  <a name="Manage"></a> Verwalten einer Wissensdatenbank  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Wissensdatenbank öffnen**.  
  
3.  Klicken Sie mit der rechten Maustaste auf eine Wissensdatenbank in der Wissensdatenbanktabelle.  
  
4.  Im Kontextmenü können Sie folgende Schritte ausführen:  
  
    1.  **Öffnen**: Klicken Sie auf diese Option, um die Wissensdatenbank in der Aktivität zu öffnen, die im Bereich **Aktivität auswählen** ausgewählt ist.  
  
    2.  **Entsperren**: Sie können die Wissensdatenbank entsperren, wenn Sie die Wissensdatenbank im Rahmen der Domänenverwaltungs-, Wissensermittlungs- und Abgleichsrichtlinienaktivitäten bearbeitet und die Wissensdatenbank geschlossen haben. Wenn Sie die Wissensdatenbank entsperren, kann sie von einer anderen Person geöffnet und bearbeitet werden. Dieser Befehl ist nicht verfügbar, wenn sich die Wissensdatenbank nicht in einem Aktivitätszustand befindet. Weitere Informationen finden Sie unter [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md).  
  
    3.  **Arbeit verwerfen**: Klicken Sie auf diese Option, wenn die Wissensdatenbank bearbeitet wird, wie durch einen Eintrag im Feld Status in der Tabelle angezeigt wird. Dieser Befehl ist nicht verfügbar, wenn sich die Wissensdatenbank nicht in einem Aktivitätszustand befindet oder wenn die Wissensdatenbank gesperrt ist. Weitere Informationen finden Sie unter [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md).  
  
    4.  **Umbenennen**: Klicken Sie auf diese Option, um das Wissensdatenbankfeld der Tabelle für die Wissensdatenbank, auf die Sie mit der rechten Maustaste geklickt haben, bearbeiten zu können. Ändern Sie den Namen, und klicken Sie dann auf diese Wissensdatenbank und eine andere Wissensdatenbank in dem Feld, um die Namensänderung zu bestätigen.  
  
    5.  **Löschen**: Klicken Sie auf diese Option, um die Wissensdatenbank aus der DQS_MAIN-Datenbank auf dem [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]zu entfernen.  
  
    6.  **Eigenschaften**: Klicken Sie auf diese Option, um die Eigenschaften für die Datenbank im schreibgeschützten Modus anzuzeigen.  
  
        1.  **Quell-Wissensdatenbank**: Wissensdatenbank, auf der diese Datenbank basiert. Diese Eingabe ist optional.  
  
        2.  **Status**: Gibt an, ob sich die Wissensdatenbank **In Arbeit** und in einer bestimmten Wissensverwaltungsaktivität befindet. Dabei gilt der Status, als sie zum letzten Mal geschlossen wurde. Die Wissensdatenbank kann den Status **In Arbeit**haben – in dem Fall ist sie in einer Wissensverwaltungssitzung, jedoch nicht in einer bestimmten Aktivität geöffnet -, oder sie kann sich im Status **In Arbeit** sowie in einer Wissensverwaltungsaktivität befinden. In dem Fall ist die Wissensdatenbank in einer Wissensverwaltungssitzung und in einer bestimmten Aktivität geöffnet.  
  
        3.  **Ist Gesperrt**: Der Wert ist **True** , wenn die Wissensdatenbank gesperrt wurde, und **False** , wenn sie nicht gesperrt wurde.  
  
        4.  **Enthält nicht veröffentlichten Inhalt**: Der Wert ist True, wenn die Wissensdatenbank Inhalt enthält, der nicht durch eine Veröffentlichung gespeichert wurde, und False, wenn dies nicht der Fall ist.  
  
        5.  **Gesperrt von**: Name des Benutzers, der die Wissensdatenbank geschlossen und dabei gesperrt hat.  
  
        6.  **Sperrdatum**: Datum der Sperrung.  
  
        7.  **Erstellt von**: Name des Benutzers, der die Wissensdatenbank erstellt hat, und das entsprechende Netzwerk.  
  
        8.  **Erstellungsdatum**: Datum der Erstellung.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Verwalten einer Wissensdatenbank  
 Der nächste Schritt nach dem Verwalten einer Wissensdatenbank hängt davon ab, welche Aktion Sie für die Wissensdatenbank durchgeführt haben:  
  
-   Wenn Sie die Wissensdatenbank geöffnet haben, fahren Sie mit der Aktivität fort, die Sie ausgewählt haben.  
  
-   Wenn Sie die Wissensdatenbank entsperrt haben, kann diese von einer anderen Person im angegebenen Status geöffnet und bearbeitet werden.  
  
-   Wenn Sie die Anpassungen der Wissensdatenbank verworfen haben, ist sie im zuletzt veröffentlichten Status verfügbar.  
  
-   Wenn Sie die Wissensdatenbank umbenannt haben, müssen Sie die Wissensdatenbank mit dem neuen Namen öffnen, um sie zu bearbeiten.  
  
-   Wenn Sie sie löschen, müssen Sie eine andere Wissensdatenbank für die Bearbeitung auswählen oder eine neue erstellen.  
  
  

