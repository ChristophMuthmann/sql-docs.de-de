---
title: "Erstellen von Paketkonfigurationen | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server Integration Services-Pakete, Konfigurationen"
  - "Paketkonfigurationsplaner (Dialogfeld)"
  - "SSIS-Pakete, Konfigurationen"
  - "Integration Services-Pakete, Konfigurationen"
  - "Konfigurationen [Integration Services]"
  - "Pakete [Integration Services], Konfigurationen"
  - "Bereitstellen von Paketen [Integration Services], Konfigurationen"
ms.assetid: 91ac0347-f908-44f5-bd3d-115790223af4
caps.latest.revision: 72
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 72
---
# Erstellen von Paketkonfigurationen
  Erstellen Sie im Dialogfeld **Paketkonfigurationsplaner** und im Paketkonfigurations-Assistenten entsprechende Paketkonfigurationen. Um auf diese Tools zuzugreifen, klicken Sie in **im Menü** SSIS **auf** Paketkonfigurationen [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
  
 **HINWEISE:**
>Sie können auch durch Klicken auf die Schaltfläche mit den Auslassungspunkten neben der Eigenschaft **Konfiguration** auf den **Paketkonfigurationsplaner** zugreifen. Die Eigenschaft Konfiguration wird im Eigenschaftenfenster für das Paket angezeigt.  
  
>Konfigurationen sind für das Paketbereitstellungsmodell verfügbar. Parameter werden für das Projektbereitstellungsmodell anstelle von Konfigurationen verwendet. Mithilfe des Projektbereitstellungsmodells können Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekte auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitstellen. Weitere Informationen zu Bereitstellungsmodellen finden Sie unter [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).  
  
>Im Dialogfeld **Paketkonfigurationsplaner** können Sie Pakete zum Verwenden von Konfigurationen aktivieren, Konfigurationen hinzufügen und löschen sowie die bevorzugte Reihenfolge festlegen, in der die Konfigurationen geladen werden sollten. 
 
>Wenn Paketkonfigurationen in der bevorzugten Reihenfolge geladen werden, werden die Konfigurationen in der Reihenfolge geladen, in der sie im Dialogfeld **Paketkonfigurationsplaner** angezeigt werden, wobei mit der Konfiguration am Anfang der Liste begonnen wird. Zur Laufzeit werden Paketkonfigurationen möglicherweise aber nicht in der bevorzugten Reihenfolge geladen. Beispielsweise werden übergeordnete Paketkonfigurationen nach Konfigurierungen anderer Typen geladen.  
  
>Wenn mehrere Konfigurationen dieselbe Objekteigenschaft festlegen, wird der zuletzt geladene Wert zur Laufzeit verwendet.  
  
 Im Dialogfeld **Paketkonfigurationsplaner** führen Sie den Paketkonfigurations-Assistenten aus, der Sie durch die Schritte zum Erstellen einer Konfiguration führt. Um den Paketkonfigurations-Assistenten auszuführen, fügen Sie im Dialogfeld **Paketkonfigurationsplaner** eine neue Konfiguration hinzu, oder bearbeiten Sie eine vorhandene Konfiguration. Auf den Seiten des Assistenten wählen Sie den Konfigurationstyp aus. Sie legen fest, ob Sie direkt auf die Konfiguration zugreifen oder Umgebungsvariablen verwenden möchten, und Sie wählen die in der Konfiguration zu speichernden Eigenschaften aus.  
  
 Im folgenden Beispiel werden die Zieleigenschaften einer Variablen und eines Pakets gezeigt, so wie sie auf der Seite Assistenten abschließen des Paketkonfigurations-Assistenten angezeigt werden:  
  
 \Package.Variables[User::TodaysDate].Properties[RaiseChangedEvent]  
  
 \Package.Properties[MaximumErrorCount]  
  
 \Package.Properties[LoggingMode]  
  
 \Package.Properties[LocaleID]  
  
 \Package\My SQL Task.Variables[User::varTableName].Properties[Value]  
  
 In diesem Beispiel werden diese Eigenschaften von der Konfiguration aktualisiert:  
  
-   Die RaiseChangedEvent-Eigenschaft der benutzerdefinierten Variablen `TodaysDate`.  
  
-   Die Eigenschaften MaximumErrorCount, LoggingMode und LocaleID des Pakets.  
  
-   Die Value-Eigenschaft der benutzerdefinierten Variablen `varTableName` im Bereich des Tasks My SQL Task.  
  
 "\Package" stellt den Stamm dar, und Punkte (.) trennen die Objekte, die den Pfad für die von der Konfiguration aktualisierten Eigenschaft definieren. Die Namen von Variablen und Eigenschaften werden in eckigen Klammern eingeschlossen. Der Begriff Package wird immer in der Konfiguration verwendet, unabhängig vom Paketnamen. Für alle anderen Objekte im Pfad werden jedoch die benutzerdefinierten Namen verwendet.  
  
 Nachdem der Assistent beendet ist, wird die neue Konfiguration der Konfigurationsliste im Dialogfeld **Paketkonfigurationsplaner** hinzugefügt.  
  
> **HINWEIS:** Auf der letzten Seite des Paketkonfigurations-Assistenten, der Seite Assistenten abschließen, werden die Zieleigenschaften der Konfiguration aufgelistet. Wenn Sie beim Ausführen von Paketen mithilfe des Eingabeaufforderungs-Hilfsprogramms **dtexec** die Eigenschaften aktualisieren möchten, können Sie die Zeichenfolgen, die die Eigenschaftspfade darstellen, generieren. Führen Sie hierzu den Paketkonfigurations-Assistenten aus, kopieren Sie dann die Zeichenfolgen, und fügen Sie diese im Eingabeaufforderungsfenster für die Verwendung mit der festgelegten Option von **dtexec** ein.  
  
 In der folgenden Tabelle werden die Spalten der Konfigurationsliste im Dialogfeld **Paketkonfigurationsplaner** beschrieben.  
  
|Column|Description|  
|------------|-----------------|  
|**Konfigurationsname**|De Name der Konfiguration.|  
|**Konfigurationstyp**|Der Konfigurationstyp.|  
|**Konfigurationszeichenfolge**|Der Speicherort der Konfiguration. Beim Speicherort kann es sich um einen Pfad, eine Umgebungsvariable, einen Registrierungsschlüssel, den Namen einer Variablen eines übergeordneten Pakets oder eine Tabelle in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank handeln.|  
|**Zielobjekt**|Der Name des Objekts mit einer Eigenschaft, die eine Konfiguration besitzt. Wenn es sich bei der Konfiguration um eine XML-Konfigurationsdatei handelt, ist die Spalte leer, da die Konfiguration mehrere Objekte aktualisieren kann.|  
|**Zieleigenschaft**|Der Name der Eigenschaft. Wenn die Konfiguration in eine XML-Konfigurationsdatei oder in eine SQL Server-Tabelle schreibt, ist die Spalte leer, da die Konfiguration mehrere Objekte aktualisieren kann.|  
  
### So erstellen Sie eine Paketkonfiguration  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer auf die Registerkarte **Ablaufsteuerung**, **Datenfluss**, **Ereignishandler**oder **Paket-Explorer** .  
  
4.  Klicken Sie im Menü **SSIS** auf **Paketkonfigurationen**.  
  
5.  Wählen Sie im Dialogfeld **Paketkonfigurationsplaner** die Option **Paketkonfigurationen aktivieren**aus, und klicken Sie dann auf **Hinzufügen**.  
  
6.  Klicken Sie auf der Willkommensseite des Paketkonfigurationsassistenten auf **Weiter**.  
  
7.  Geben Sie auf der Seite "Konfigurationstyp auswählen" den Konfigurationstyp an, und legen Sie dann die für den Konfigurationstyp relevanten Eigenschaften fest. Weitere Informationen finden Sie unter [Package Configuration Wizard UI Reference](../../integration-services/packages/package-configuration-wizard-ui-reference.md).  
  
8.  Wählen Sie auf der Seite zum Auswählen der zu exportierenden Eigenschaften die Eigenschaften von Paketobjekten aus, die in der Konfiguration enthalten sein sollen. Wenn der Konfigurationstyp nur eine Eigenschaft unterstützt, lautet die Überschrift dieser Assistentenseite Zieleigenschaft auswählen. Weitere Informationen finden Sie unter [Package Configuration Wizard UI Reference](../../integration-services/packages/package-configuration-wizard-ui-reference.md).  
  
    > **HINWEIS:** Nur die Konfigurationstypen **XML-Konfigurationsdatei** und **SQL Server** unterstützen die Berücksichtigung von mehreren Eigenschaften in einer Konfiguration.  
  
9. Geben Sie auf der Seite "Assistenten abschließen" den Namen der Konfiguration ein, und klicken Sie dann auf **Fertig stellen**.  
  
10. Zeigen Sie die Konfiguration im Dialogfeld **Paketkonfigurationsplaner** an.  
  
11. Klicken Sie auf **Schließen**.  
  
## Externe Ressourcen  
  
-   Technischer Artikel [Grundlegendes zu Integration Services-Paketkonfigurationen](http://go.microsoft.com/fwlink/?LinkId=165643)auf msdn.microsoft.com.  
  
-   Blogeintrag zu [Codebasiertes Erstellen von Paketen – Paketkonfigurationen](http://go.microsoft.com/fwlink/?LinkId=217663)auf www.sqlis.com.  
  
-   Blogeintrag zu [API-Beispiel – Programmgesteuertes Hinzufügen einer Konfigurationsdatei zu einem Paket](http://go.microsoft.com/fwlink/?LinkId=217664)auf blogs.msdn.com.  
  
## Siehe auch  
 [Paketkonfigurationen](../../integration-services/packages/package-configurations.md)   
 [Legacy-Paketbereitstellung &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)   
 [Programmgesteuertes Arbeiten mit Variablen](../../integration-services/building-packages-programmatically/working-with-variables-programmatically.md)  
  
  