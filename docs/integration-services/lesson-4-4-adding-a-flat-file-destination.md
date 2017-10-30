---
title: "Schritt 4: Hinzufügen eines Flatfileziels | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: f4088de3-16d8-419c-96a1-a2cd005d0a5b
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ff4badae70e5762f51003c0d3edae3ad1fb3907b
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-4-4---adding-a-flat-file-destination"></a>Lektion 4-4-Hinzufügen eines Flatfileziels
Die Fehlerausgabe der "Lookup Currency Key"-Transformation leitet alle Datenzeilen, für die im Suchvorgang keine Übereinstimmung gefunden wurde, zur Skripttransformation um. Um die zu den Fehlern angezeigten Informationen zu verbessern, führt die Skripttransformation ein Skript aus, mit dem die Fehlerbeschreibung abgerufen wird.  
  
In dieser Aufgabe speichern Sie alle Informationen zu den fehlerhaften Zeilen für eine spätere Verarbeitung in einer Datei mit Trennzeichen. Um die fehlerhaften Zeilen zu speichern, müssen Sie einen Flatfile-Verbindungs-Manager für die Textdatei, die die Fehlerdaten enthalten wird, und ein Flatfileziel hinzufügen und konfigurieren. Durch Festlegen von Eigenschaften im Verbindungs-Manager für Flatfiles, der vom Flatfileziel verwendet wird, können Sie angeben, wie das Flatfileziel die Textdatei formatiert und schreibt. Weitere Informationen finden Sie unter [Verbindungs-Manager für Flatfiles](../integration-services/connection-manager/flat-file-connection-manager.md) und [Flatfileziel](../integration-services/data-flow/flat-file-destination.md).  
  
### <a name="to-add-and-configure-a-flat-file-destination"></a>So fügen Sie ein Flatfileziel hinzu und konfigurieren es  
  
1.  Klicken Sie auf die Registerkarte **Datenfluss** .  
  
2.  Erweitern Sie in der **SSIS-Toolbox**die Option **Weitere**, und ziehen Sie **Flatfileziel** auf die Datenfluss-Entwurfsoberfläche. Setzen Sie das **Flatfileziel** direkt unter die **Get Error Description** -Transformation.  
  
3.  Klicken Sie auf die **Get Error Description** -Transformation, und ziehen Sie anschließend den grünen Pfeil auf das neue **Flatfileziel**.  
  
4.  Klicken Sie auf der **Datenfluss** -Entwurfsoberfläche in der neu hinzugefügten **Flatfileziel** -Transformation auf **Flatfileziel** , und ändern Sie den Namen in **Failed Rows**.  
  
5.  Klicken Sie mit der rechten Maustaste auf die Transformation **Failed Rows** , klicken Sie auf **Bearbeiten**und anschließend im **Ziel-Editor für Flatfiles**auf **Neu**.  
  
6.  Überprüfen Sie im Dialogfeld **Flatfileformat** , ob **Mit Trennzeichen** ausgewählt ist, und klicken Sie anschließend auf **OK**.  
  
7.  Geben Sie im **Verbindungs-Manager-Editor für Flatfiles**im Feld **Name des Verbindungs-Managers** die Zeichenfolge **Error Data**ein.  
  
8.  Klicken Sie im Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** auf **Durchsuchen**, und suchen Sie den Ordner, in dem die Datei gespeichert werden soll.  
  
9. Geben Sie im Dialogfeld **Öffnen** für **Dateiname**den Namen **ErrorOutput.txt**ein, und klicken Sie anschließend auf **Öffnen**.  
  
10. Prüfen Sie im Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** , ob das Feld **Gebietsschema** den Wert Englisch (USA) und das Feld **Codepage** den Wert 1252 (ANSI -Latin I) enthält.  
  
11. Klicken Sie im Optionen-Bereich auf **Spalten**.  
  
    Beachten Sie, dass zusätzlich zu den Spalten aus der Quelldatendatei drei neue Spalten vorhanden sind: ErrorCode, ErrorColumn und ErrorDescription. Diese Spalten werden von der Fehlerausgabe der Lookup Currency Key-Transformation und vom Skript in der Get Error Description-Transformation generiert und können dazu verwendet werden, die Ursache für das Fehlschlagen der Zeile zu beheben.  
  
12. Klicken Sie auf **OK**.  
  
13. Deaktivieren Sie im **Ziel-Editor für Flatfiles**das Kontrollkästchen **Daten in der Datei überschreiben** .  
  
    Wenn Sie dieses Kontrollkästchen deaktivieren, werden die Fehler über mehrere Paketausführungen beibehalten.  
  
14. Klicken Sie im **Ziel-Editor für Flatfiles**auf **Zuordnungen** um zu überprüfen, ob alle Spalten ordnungsgemäß sind. Optional können Sie die Spalten im Ziel umbenennen.  
  
15. Klicken Sie auf **OK**.  
  
## <a name="next-steps"></a>Nächste Schritte  
[Schritt 5: Testen des Lektion 4-Lernprogrammpakets](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
  
  

