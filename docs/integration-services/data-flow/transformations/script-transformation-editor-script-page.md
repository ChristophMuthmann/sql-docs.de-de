---
title: "Transformations-Editor f&#252;r Skripterstellung (Seite Skript) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.scriptcomponent.script.f1"
helpviewer_keywords: 
  - "Transformations-Editor für Skripterstellung"
ms.assetid: 4c6d1901-ef21-4aa7-9d0a-6bbeb7fadf1c
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# Transformations-Editor f&#252;r Skripterstellung (Seite Skript)
  Auf der Registerkarte **Skript** des Dialogfelds **Transformations-Editor für Skripterstellung** können Sie ein Skript und verknüpfte Eigenschaften angeben.  
  
 Weitere Informationen zur Skriptkomponente finden Sie unter [Script Component](../../../integration-services/data-flow/transformations/script-component.md) und [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Weitere Informationen zur Programmierung der Skriptkomponente finden Sie unter [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
## enthalten  
 **Eigenschaften**  
 Zeigt die Skripttransformationseigenschaften an und ermöglicht Änderungen. Viele dieser Eigenschaften sind schreibgeschützt. Die folgenden Eigenschaften können Sie ändern:  
  
|Wert|Description|  
|-----------|-----------------|  
|**Description**|Beschreibt den Zweck der Skripttransformation.|  
|**LocaleID**|Gibt das Gebietsschema für die Bereitstellung regionsspezifischer Informationen für das Bestellen sowie für Datums- und Zeitformate an.|  
|**Name**|Geben Sie einen aussagekräftigen Namen für die Komponente ein.|  
|**ValidateExternalMetadata**|Zeigt an, ob von der Skripttransformation zur Entwurfszeit Spaltenmetadaten mithilfe externer Datenquellen überprüft werden. Bei dem Wert **false** wird die Überprüfung bis zur Ausführungszeit verzögert.|  
|**ReadOnlyVariables**|Geben Sie eine durch Trennzeichen getrennte Liste von Variablen für den schreibgeschützten Zugriff durch die Skripttransformation ein.<br /><br /> Hinweis: Bei Variablennamen wird nach Groß-/Kleinschreibung unterschieden.|  
|**ReadWriteVariables**|Geben Sie eine durch Trennzeichen getrennte Liste von Variablen für den Lese-/Schreibzugriff durch die Skripttransformation ein.<br /><br /> Hinweis: Bei Variablennamen wird nach Groß-/Kleinschreibung unterschieden.|  
|**ScriptLanguage**|Wählen Sie die Skriptsprache aus, die von der Skriptkomponente verwendet werden soll.<br /><br /> Um die Standardskriptsprache für Skriptkomponenten und Skripttasks festzulegen, verwenden Sie im Dialogfeld **Optionen** auf der Seite **Allgemein** die Option **Skriptsprache** .|  
|**UserComponentTypeName**|Gibt die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost>-Klasse und die **Microsoft.SqlServer.TxScript**-Assembly an, die die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Infrastruktur unterstützen.|  
  
 **Skript bearbeiten**  
 Verwenden Sie [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]-Tools für Anwendungen (VSTA), um ein Skript zu erstellen oder zu ändern.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Skriptkomponententyp auswählen](../../../integration-services/data-flow/transformations/select-script-component-type.md)   
 [Transformations-Editor für Skripterstellung &#40;Seite Eingabespalten&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)   
 [Transformations-Editor für Skripterstellung &#40;Seiten Eingaben und Ausgaben&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)   
 [Transformations-Editor für Skripterstellung &#40;Seite Verbindungs-Manager&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md)   
 [Zusätzliche Skriptkomponentenbeispiele](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
  
  