---
title: "Konvertieren von Daten in einen anderen Datentyp mithilfe der Transformation f&#252;r Datenkonvertierung | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Konvertieren von Datentypen [Integration Services]"
  - "Transformation für Datenkonvertierung"
  - "Datentypen [Integration Services], Konvertieren"
ms.assetid: 4aabbe4f-7666-4672-865a-9627bd25fbfd
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 41
---
# Konvertieren von Daten in einen anderen Datentyp mithilfe der Transformation f&#252;r Datenkonvertierung
  Um eine Transformation für Datenkonvertierung hinzuzufügen und zu konfigurieren, muss das Paket bereits mindestens einen Datenflusstask und eine Quelle enthalten.  
  
### So konvertieren Sie Daten in einen anderen Datentyp  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Datenfluss** , und ziehen Sie dann aus dem Bereich **Toolbox**die Transformation für Datenkonvertierung auf die Entwurfsoberfläche.  
  
4.  Verbinden Sie die Transformation für Datenkonvertierung mit dem Datenfluss, indem Sie einen Konnektor von der Quelle oder der vorherigen Transformation auf die Transformation für Datenkonvertierung ziehen.  
  
5.  Doppelklicken Sie auf die Transformation für Datenkonvertierung.  
  
6.  Aktivieren Sie im Dialogfeld **Transformations-Editor für Datenkonvertierung** in der Tabelle **Verfügbare Eingabespalten** das Kontrollkästchen neben den Spalten, deren Datentyp Sie konvertieren möchten.  
  
    > [!NOTE]  
    >  Für eine Eingabespalte können mehrere Datenkonvertierungen angewendet werden.  
  
7.  Optional können die Standardwerte in der **Ausgabealias** -Spalte geändert werden.  
  
8.  Wählen Sie in der Liste **Datentyp** den neuen Datentyp für die Spalte aus. Der Standarddatentyp ist der Datentyp der Eingabespalte.  
  
9. Aktualisieren Sie optional in Abhängigkeit vom ausgewählten Datentyp die Werte in den Spalten **Länge**, **Genauigkeit**, **Dezimalstellen**und **Codepage** .  
  
10. Um die Fehlerausgabe zu konfigurieren, klicken Sie auf **Fehlerausgabe konfigurieren**. Weitere Informationen finden Sie unter [Konfigurieren einer Fehlerausgabe in einer Datenflusskomponente](../../../integration-services/troubleshooting/configure-an-error-output-in-a-data-flow-component.md).  
  
11. Klicken Sie auf **OK**.  
  
12. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## Siehe auch  
 [Transformation für Datenkonvertierung](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [SQL Server Integration Services-Pfade](../../../integration-services/data-flow/integration-services-paths.md)   
 [SQL Server Integration Services-Datentypen](../../../integration-services/data-flow/integration-services-data-types.md)   
 [Datenflusstask](../../../integration-services/control-flow/data-flow-task.md)  
  
  