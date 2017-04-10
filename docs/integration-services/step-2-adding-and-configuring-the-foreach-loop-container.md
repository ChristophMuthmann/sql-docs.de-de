---
title: "Schritt 2: Hinzuf&#252;gen und Konfigurieren des Foreach-Schleifencontainers | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 88a973cc-0f23-4ecf-adb6-5b06279c2df6
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Schritt 2: Hinzuf&#252;gen und Konfigurieren des Foreach-Schleifencontainers
In dieser Aufgabe fügen Sie die Möglichkeit zum Schleifendurchlauf für einen Ordner von Flatfiles hinzu und wenden die auch in Lektion 1 verwendete Datenflusstransformation auf jede dieser Flatfiles an. Dies geschieht durch das Hinzufügen eines Foreach-Schleifencontainers zur Ablaufsteuerung und dessen Konfigurierung.  
  
Für den von Ihnen hinzugefügten Foreach-Schleifencontainer muss es möglich sein, eine Verbindung mit jeder Flatfile im Ordner herzustellen. Da alle Dateien im Ordner das gleiche Format aufweisen, kann vom Foreach-Schleifencontainer der gleiche Flatfile-Verbindungs-Manager zum Herstellen einer Verbindung mit jeder dieser Dateien verwendet werden. Der vom Container verwendete Flatfile-Verbindungs-Manager ist der gleiche Flatfile-Verbindungs-Manager, den Sie in Lektion 1 erstellt haben.  
  
Zurzeit wird vom Flatfile-Verbindungs-Manager aus der Lektion 1 nur eine Verbindung mit einer bestimmten Flatfile hergestellt. Um iterativ Verbindungen mit jedem Flatfile im Ordner herzustellen, müssen Sie sowohl den Foreach-Schleifencontainer als auch den Flatfile-Verbindungs-Manager wie folgt konfigurieren:  
  
-   **Foreach-Schleifencontainer:** Sie ordnen den aufgezählten Wert des Containers einer benutzerdefinierten Paketvariable zu. Der Container verwendet diese benutzerdefinierte Variable dann, um die **ConnectionString**-Eigenschaft des Verbindungs-Managers für Flatfiles dynamisch zu ändern und iterativ Verbindungen mit jeder Flatfile im Ordner herzustellen.  
  
-   **Verbindungs-Manager für Flatfiles:** Sie ändern den Verbindungs-Manager, der in Lektion 1 erstellt worden ist, indem Sie eine benutzerdefinierte Variable zum Auffüllen der **ConnectionString**-Eigenschaft des Verbindungs-Managers verwenden.  
  
Die Vorgänge in diesem Task verdeutlichen, wie Sie den Foreach-Schleifencontainer erstellen und ändern, um eine benutzerdefinierte Paketvariable zu verwenden, und wie der Schleife der Datenflusstask hinzugefügt wird. Sie lernen, wie der Flatfile-Verbindungs-Manager geändert wird, um eine benutzerdefinierte Variable in der nächsten Aufgabe zu verwenden.  
  
Nachdem Sie diese Änderungen am Paket vorgenommen haben, iteriert der Foreach-Schleifencontainer beim Ausführen des Pakets durch die Auflistung der Dateien im Ordner Sample Data. Jedes Mal, wenn eine mit den Kriterien übereinstimmende Datei gefunden wird, wird die benutzerdefinierte Variable vom Foreach-Schleifencontainer mit dem Dateinamen aufgefüllt, die benutzerdefinierte Variable der **ConnectionString**-Eigenschaft des Flatfile-Verbindungs-Managers für Sample Currency Data zugeordnet und der Datenfluss anschließend gegen diese Datei ausgeführt. Dadurch wird in jeder Iteration der Foreach-Schleife vom Datenflusstask eine andere Flatfile verarbeitet.  
  
> [!NOTE]  
> Weil [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] die Ablaufsteuerung vom Datenfluss trennt, erfordert keine der Schleifen, die Sie der Ablaufsteuerung hinzufügen, Änderungen am Datenfluss. Deshalb muss der von Ihnen in Lektion 1 erstellte Datenfluss nicht geändert werden.  
  
### So fügen Sie einen Foreach-Schleifencontainer hinzu  
  
1.  Klicken Sie in **SQL Server Data Tools** auf die Registerkarte **Ablaufsteuerung**.  
  
2.  Erweitern Sie **Container** in der **SSIS-Toolbox**, und ziehen Sie anschließend **Foreach-Schleifencontainer** auf die Entwurfsoberfläche der Registerkarte **Ablaufsteuerung**.  
  
3.  Klicken Sie mit der rechten Maustaste auf den neu hinzugefügten **Foreach-Schleifencontainer**, und wählen Sie **Bearbeiten** aus.  
  
4.  Geben Sie auf der Seite **Allgemein** im Dialogfeld **Foreach-Schleifen-Editor** für **Name** **Foreach File in Folder** (Foreach-Datei in Ordner) ein. Klicken Sie auf **OK**.  
  
5.  Klicken Sie mit der rechten Maustaste auf den Foreach-Schleifencontainer, klicken Sie auf **Eigenschaften**, und prüfen Sie im Eigenschaftenfenster, ob die Eigenschaft **LocaleID** auf **Englisch (USA)** festgelegt ist.  
  
### So konfigurieren Sie den Enumerator für den Foreach-Schleifencontainer  
  
1.  Doppelklicken Sie auf „Foreach File in Folder“, um den **Foreach-Schleifen-Editor** erneut zu öffnen.  
  
2.  Klicken Sie auf **Sammlung**.  
  
3.  Wählen Sie auf der Seite **Sammlung** **Foreach-Dateienumerator** aus.  
  
4.  Klicken Sie in der Gruppe **Enumeratorkonfiguration** auf **Durchsuchen**.  
  
5.  Suchen Sie im Dialogfeld **Nach Ordner suchen** den Ordner auf dem Computer, der die „Currency_*.txt“-Dateien enthält.  
  
    Die Beispieldaten sind in den [!INCLUDE[ssIS](../includes/ssis-md.md)]-Lektionspaketen enthalten. Um die Beispieldaten und die Lektionspakete herunterzuladen, gehen Sie wie folgt vor.  
  
    1.  Klicken Sie [hier](http://go.microsoft.com/fwlink/?LinkId=275027), um zur Seite Integration Services Product Samples zu gelangen  
  
    2.  Klicken Sie auf die Registerkarte **DOWNLOADS**.  
  
    3.  Klicken Sie auf die ZIP-Datei „SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample“.  
  
6.  Geben Sie im Feld **Dateien** **Currency_\*.txt** ein.  
  
### So ordnen Sie den Enumerator einer benutzerdefinierten Variablen zu  
  
1.  Klicken Sie auf **Variablenzuordnungen**.  
  
2.  Klicken Sie auf der Seite **Variablenzuordnungen** in der Spalte **Variable** auf die leere Zelle, und wählen Sie **\<Neue Variable…>** aus.  
  
3.  Geben Sie im Dialogfeld **Variable hinzufügen** für **Name** **varFileName** ein.  
  
    > [!IMPORTANT]  
    > Bei Variablennamen wird nach Groß-/Kleinschreibung unterschieden.  
  
4.  Klicken Sie auf **OK**.  
  
5.  Klicken Sie erneut auf **OK**, um das Dialogfeld **Foreach-Schleifen-Editor** zu schließen.  
  
### So fügen Sie der Schleife den Datenflusstask hinzu  
  
-   Ziehen Sie den Datenflusstask **Extract Sample Currency Data** (Beispielwährungsdaten extrahieren) in Foreach-Schleifencontainer, der jetzt **Foreach File in Folder** (Foreach-Datei in Ordner) heißt.  
  
## Aufgabe in der nächsten Lektion  
[Schritt 3: Ändern des Flatfile-Verbindungs-Managers](../integration-services/step-3-modifying-the-flat-file-connection-manager.md)  
  
## Siehe auch  
[Konfigurieren eines Foreach-Schleifencontainers](../Topic/Configure%20a%20Foreach%20Loop%20Container.md)  
[Verwenden von Variablen in Paketen](../Topic/Use%20Variables%20in%20Packages.md)  
  
  
  
