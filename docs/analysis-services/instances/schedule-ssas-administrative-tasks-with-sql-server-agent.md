---
title: Planen von administrativen Tasks in SSAS mit SQL Server-Agent | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2d1484b3-51d9-48a0-93d2-0c3e4ed22b87
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 28be70a8fe43d1c22ba3e7787d507c694b09750a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="schedule-ssas-administrative-tasks-with-sql-server-agent"></a>Planen von administrativen Tasks in SSAS mithilfe von SQL Server-Agent
  Mithilfe des SQL Server-Agent-Diensts können Sie die gewünschte Reihenfolge und die erforderlichen Zeitpunkte für die Ausführung von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Verwaltungsaufgaben planen. Mit geplanten Tasks können Sie Vorgänge automatisieren, die in regelmäßigen oder vorhersagbaren Abständen ausgeführt werden müssen. Dabei können Sie administrative Tasks wie z. B. die Cubeverarbeitung so planen, dass sie zu Zeiten ausgeführt werden, in denen die geschäftliche Auslastung des Servers niedrig ist. Sie können auch die Reihenfolge bestimmen, in der die Tasks ausgeführt werden sollen, indem Sie innerhalb eines SQL Server-Agent-Auftrags Auftragsschritte erstellen. Beispielsweise können Sie einen Cube verarbeiten und dann eine Sicherung des Cubes durchführen lassen.  
  
 Mit Auftragsschritten können Sie den Ausführungsprozess steuern. Sie können SQL Server-Agent so konfigurieren, dass im Fall eines Fehlers bei einem Auftrag mit der Ausführung der restlichen Tasks fortgefahren wird, oder die Ausführung angehalten wird. Sie können in SQL Server-Agent auch das Senden von Benachrichtigungen über die erfolgreiche bzw. fehlerhafte Ausführung eines Auftrags konfigurieren.  
  
 Dieses Thema ist eine exemplarische Vorgehensweise, in der zwei Methoden erläutert werden, wie Sie XMLA-Skript mithilfe des SQL Server-Agents ausführen. Im ersten Beispiel wird veranschaulicht, wie die Verarbeitung einer einzelnen Dimension geplant wird. Im zweiten Beispiel wird gezeigt, wie Verarbeitungstasks in ein einzelnes Skript kombiniert werden, das nach einem Zeitplan ausgeführt wird. Wenn Sie diese exemplarische Vorgehensweise abschließen möchten, müssen folgende Voraussetzungen erfüllt sein.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 Der SQL Server-Agent-Dienst muss installiert sein.  
  
 Standardmäßig werden Aufträge unter demselben Dienstkonto ausgeführt. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], SQL Server-Agent das Standardkonto ist NT Service\SQLAgent$\<Instanzname >. Um einen Sicherungs- oder Verarbeitungstask auszuführen, muss dieses Konto Systemadministrator auf der Analysis Services-Instanz sein. Weitere Informationen finden Sie unter [Erteilen von serverweiten Administratorrechten für eine Analysis Services-Instanz](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
 Sie sollten außerdem eine Testdatenbank haben, um damit zu arbeiten. Sie können die mehrdimensionale AdventureWorks-Beispieldatenbank oder ein Projekt aus dem mehrdimensionalen Analysis Services-Lernprogramm bereitstellen, um es in dieser exemplarischen Vorgehensweise zu verwenden. Weitere Informationen finden Sie unter [Installieren von Beispieldaten und -projekten für das Analysis Services-Tutorial zur mehrdimensionalen Modellierung](../../analysis-services/install-sample-data-and-projects.md).  
  
## <a name="example-1-processing-a-dimension-in-a-scheduled-task"></a>Beispiel 1: Verarbeiten einer Dimension in einem geplanten Task  
 In diesem Beispiel wird veranschaulicht, wie Sie einen Auftrag erstellen und planen, um eine Dimension zu verarbeiten.  
  
 Ein geplanter [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Task ist ein in einem SQL Server-Agent-Auftrag eingebettetes XMLA-Skript. Dieser Auftrag ist geplant, d. h. er wird zu den festgelegten Zeiten und mit der festgelegten Häufigkeit ausgeführt. SQL Server-Agent ist Teil von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], daher benötigen Sie zum Erstellen und Planen von administrativen Tasks sowohl das Datenbankmodul als auch [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
###  <a name="bkmk_CreateScript"></a> Erstellen eines Skripts zum Verarbeiten einer Dimension in einem SQL Server-Agent-Auftrag  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung zu [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her. Öffnen Sie einen Datenbankordner, und suchen Sie eine Dimension. Klicken Sie mit der rechten Maustaste auf die Dimension, und wählen Sie **Verarbeiten**aus.  
  
2.  Überprüfen Sie im Dialogfeld **Dimension aufbereiten** in der Spalte **Verarbeitungsoptionen** unter **Objektliste**, ob die Option für diese Spalte **Vollständig verarbeiten**lautet. Falls dies nicht der Fall ist, klicken Sie auf die Option unter **Verarbeitungsoptionen**, und wählen Sie anschließend **Vollständig verarbeiten** aus der Dropdownliste aus.  
  
3.  Klicken Sie auf **Skript**.  
  
     Dieser Schritt öffnet ein **XML-Abfragefenster** , welches das XMLA-Skript enthält, das die Dimension verarbeitet.  
  
4.  Klicken Sie im Dialogfeld **Dimension aufbereiten** auf **Abbrechen** , um das Dialogfeld zu schließen.  
  
5.  Markieren Sie im **XMLA-Abfragefenster** das XMLA-Skript, klicken Sie mit der rechten Maustaste auf das markierte Skript, und wählen Sie **Kopieren**aus.  
  
     Dieser Schritt kopiert das XMLA-Skript in die Windows-Zwischenablage. Sie können das XMLA-Skript in der Zwischenablage lassen oder es in Editor oder einen anderen Text-Editor einfügen. Unten ist ein Beispiel für das XMLA-Skript angegeben.  
  
    ```  
    <Batch xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Account</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
###  <a name="bkmk_ProcessJob"></a> Erstellen und Planen des Dimensionsverarbeitungsauftrags  
  
1.  Stellen Sie eine Verbindung mit einer Instanz des Datenbankmoduls her, und öffnen Sie dann den Objekt-Explorer.  
  
2.  Erweitern Sie **SQL Server-Agent**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Aufträge** , und wählen Sie **Neuer Auftrag**aus.  
  
4.  Geben Sie im Dialogfeld **Neuer Auftrag** unter **Name**einen Auftragsnamen ein.  
  
5.  Wählen Sie unter **Seite auswählen**die Option **Schritte**aus, und klicken Sie dann auf **Neu**.  
  
6.  Geben Sie im Dialogfeld **Neuer Auftragsschritt** unter **Schrittname**einen Schrittnamen ein.  
  
7.  Geben Sie in **Server** **localhost** für eine Standardinstanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] und **localhost\\**\<*Instanzname*> für eine benannte Instanz ein.  
  
     Wenn Sie den Auftrag von einem Remotecomputer ausführen, verwenden Sie den Namen des Servers und der Instanz, wo der Auftrag ausgeführt wird. Verwenden Sie das Format \< *Servernamen*> für eine Standardinstanz und \< *Servernamen*>\\<*Instanz Namen*> für eine benannte Instanz.  
  
8.  Wählen Sie unter **Typ**die Option **SQL Server Analysis Services-Befehl**aus.  
  
9. Klicken Sie unter **Befehl**mit der rechten Maustaste, und wählen Sie **Einfügen**aus. Das XMLA-Skript, das Sie im vorherigen Schritt generiert haben, sollte im Befehlsfenster angezeigt werden.  
  
10. Klicken Sie auf **OK**.  
  
11. Wählen Sie unter **Seite auswählen**die Option **Zeitpläne**aus, und klicken Sie dann auf **Neu**.  
  
12. Geben Sie im Dialogfeld **Neuer Auftragszeitplan** einen Namen für den Zeitplan in das Feld **Name**ein, und klicken Sie auf **OK**.  
  
     Dieser Schritt erstellt einen Zeitplan für Sonntag 00:00 Uhr. Im nächsten Schritt sehen Sie, wie der Auftrag manuell ausgeführt wird. Sie können auch einen Zeitplan angeben, der den Auftrag ausführt, wenn Sie ihn überwachen.  
  
13. Klicken Sie im Dialogfeld **Neuer Auftrag** auf **OK**.  
  
14. Erweitern Sie im **Objekt-Explorer**den Eintrag **Aufträge**, klicken Sie mit der rechten Maustaste auf den erstellten Auftrag, und wählen Sie anschließend **Auftrag starten bei Schritt**aus.  
  
     Da der Auftrag nur einen Schritt hat, wird der Auftrag sofort ausgeführt. Wenn der Auftrag aus mehr als einem Schritt besteht, können Sie angeben, mit welchem Schritt der Auftrag beginnen soll.  
  
15. Klicken Sie nach Abschluss des Auftrags auf **Schließen**.  
  
## <a name="example-2-batch-processing-a-dimension-and-a-partition-in-a-scheduled-task"></a>Beispiel 2: Batchverarbeitung einer Dimension und einer Partition in einem geplanten Task  
 Die Prozeduren in diesem Beispiel veranschaulichen, wie Sie einen Auftrag erstellen und planen, der eine Batchverarbeitung für eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankdimension ausführt und zur gleichen Zeit eine Cubepartition verarbeitet, deren Aggregation von der Dimension abhängt. Weitere Informationen zur Batchverarbeitung von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Objekten finden Sie unter [Batchverarbeitung &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md).  
  
###  <a name="bkmk_BatchProcess"></a> Erstellen eines Skripts zur Batchverarbeitung einer Dimension und einer Partition in einem SQL Server-Agent-Auftrag  
  
1.  Erweitern Sie unter Verwendung der gleichen Datenbank den Eintrag **Dimensionen**, klicken Sie mit der rechten Maustaste auf die **Customer** -Dimension, und wählen Sie **Verarbeiten**aus.  
  
2.  Überprüfen Sie im Dialogfeld **Dimension aufbereiten** in der Spalte **Verarbeitungsoptionen** unter **Objektliste**, ob die Option für diese Spalte **Vollständig verarbeiten**lautet.  
  
3.  Klicken Sie auf **Skript**.  
  
     Dieser Schritt öffnet ein **XML-Abfragefenster** , welches das XMLA-Skript enthält, das die Dimension verarbeitet.  
  
4.  Klicken Sie im Dialogfeld **Dimension aufbereiten** auf **Abbrechen** , um das Dialogfeld zu schließen.  
  
5.  Erweitern Sie **Cubes**, erweitern Sie **Adventure Works**, erweitern Sie **Measuregruppen**, erweitern Sie **Internet Sales**, erweitern Sie **Partitionen**, klicken Sie mit der rechten Maustaste in der Liste auf die letzte Partition, und wählen Sie anschließend **Verarbeiten**aus.  
  
6.  Überprüfen Sie im Dialogfeld **Partition verarbeiten** in der Spalte **Verarbeitungsoptionen** unter **Objektliste**, ob die Option für diese Spalte **Vollständig verarbeiten**lautet.  
  
7.  Klicken Sie auf **Skript**.  
  
     Dieser Schritt öffnet ein zweites **XML-Abfragefenster** , welches das XMLA-Skript enthält, das die Partition verarbeitet.  
  
8.  Klicken Sie im Dialogfeld **Partition verarbeiten** auf **Abbrechen** , um den Editor zu schließen.  
  
     An diesem Punkt müssen Sie die zwei Skripts zusammenführen und sicherstellen, dass die Dimension zuerst verarbeitet wird.  
  
    > [!WARNING]  
    >  Wenn die Partition zuerst verarbeitet wird, bewirkt die nachfolgende Dimensionsverarbeitung, dass die Partition nicht mehr verarbeitet ist. Die Partition würde dann eine zweite Verarbeitung erfordern, um den Status "Verarbeitet" aufzuweisen.  
  
9. Markieren Sie im **XMLA-Abfragefenster** , das das XMLA-Skript enthält, das die Partition verarbeitet, den Code in den Tags `Batch` und `Parallel` , klicken Sie mit der rechten Maustaste auf das markierte Skript, und wählen Sie **Kopieren**aus.  
  
    ```  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID> Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID> Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
    ```  
  
10. Öffnen Sie das **XMLA-Abfragefenster** , welches das XMLA-Skript enthält, das die Dimension verarbeitet. Klicken Sie mit der rechten Maustaste innerhalb des Skripts links vom `</Process>` -Tag, und wählen Sie **Einfügen**aus.  
  
     Im folgenden Beispiel sehen Sie das überarbeitete XMLA-Skript.  
  
    ```  
    <Batch xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Customer</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
11. Markieren Sie das überarbeitete XMLA-Skript, klicken Sie mit der rechten Maustaste auf das markierte Skript, und wählen Sie **Kopieren**.  
  
12. Dieser Schritt kopiert das XMLA-Skript in die Windows-Zwischenablage. Sie können das XMLA-Skript in der Zwischenablage lassen, in einer Datei speichern oder es in Editor oder einen anderen Text-Editor einfügen.  
  
###  <a name="bkmk_Scheduling"></a> Erstellen und Planen des Batchverarbeitungsauftrags  
  
1.  Stellen Sie eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]her, und öffnen Sie den Objekt-Explorer.  
  
2.  Erweitern Sie **SQL Server-Agent**. Starten Sie den Dienst, wenn er nicht bereits ausgeführt wird.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Aufträge** , und wählen Sie **Neuer Auftrag**aus.  
  
4.  Geben Sie im Dialogfeld **Neuer Auftrag** unter **Name**einen Auftragsnamen ein.  
  
5.  Klicken Sie in **Schritte**auf **Neu**.  
  
6.  Geben Sie im Dialogfeld **Neuer Auftragsschritt** unter **Schrittname**einen Schrittnamen ein.  
  
7.  Wählen Sie unter **Typ**die Option **SQL Server Analysis Services-Befehl**aus.  
  
8.  Wählen Sie unter **Ausführen als**das **SQL Server-Agent-Dienstkonto**aus. Aus dem Abschnitt zu Voraussetzungen wissen Sie bereits, dass dieses Konto über Administratorberechtigungen für Analysis Services verfügen muss.  
  
9. Geben Sie unter **Server**den Servernamen der Analysis Services-Instanz an.  
  
10. Klicken Sie unter **Befehl**mit der rechten Maustaste, und wählen Sie **Einfügen**aus.  
  
11. Klicken Sie auf **OK**.  
  
12. Klicken Sie auf der Seite **Zeitpläne** auf **Neu**.  
  
13. Geben Sie im Dialogfeld **Neuer Auftragszeitplan** einen Namen für den Zeitplan in das Feld **Name**ein, und klicken Sie auf **OK**.  
  
     Dieser Schritt erstellt einen Zeitplan für Sonntag 00:00 Uhr. Im nächsten Schritt sehen Sie, wie der Auftrag manuell ausgeführt wird. Sie können auch einen Zeitplan auswählen, der den Auftrag ausführt, wenn Sie ihn überwachen.  
  
14. Klicken Sie auf **OK** , um das Dialogfeld zu schließen.  
  
15. Erweitern Sie im **Objekt-Explorer**den Eintrag **Aufträge**, klicken Sie mit der rechten Maustaste auf den erstellten Auftrag, und wählen Sie **Auftrag starten bei Schritt**aus.  
  
     Da der Auftrag nur einen Schritt hat, wird der Auftrag sofort ausgeführt. Wenn der Auftrag aus mehr als einem Schritt besteht, können Sie angeben, mit welchem Schritt der Auftrag beginnen soll.  
  
16. Klicken Sie nach Abschluss des Auftrags auf **Schließen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Verarbeiten von Optionen und Einstellungen &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)   
  
  
