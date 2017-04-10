---
title: "Editor f&#252;r den Task &#39;Dateisystem&#39; (Seite Allgemein) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.filesystemtask.general.f1"
helpviewer_keywords: 
  - "Editor für den Task Dateisystem"
ms.assetid: 51fe6614-3418-4eff-a28d-02ea31cc9aa9
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Editor f&#252;r den Task &#39;Dateisystem&#39; (Seite Allgemein)
  Mithilfe der Seite **Allgemein** des Dialogfelds **Editor für den Task 'Dateisystem'** können Sie den Dateisystemvorgang konfigurieren, der durch den Task ausgeführt wird.  
  
 Informationen, um sich mit diesem Thema vertraut zu machen, finden Sie unter [File System Task](../../integration-services/control-flow/file-system-task.md).  
  
 Sie müssen durch Festlegen der Eigenschaften SourceConnection und DestinationConnection einen Quell- und einen Zielverbindungs-Manager angeben. Sie können entweder die Namen von Dateiverbindungs-Managern bereitstellen, die auf die Dateien zeigen, die der Task als Quelle oder Ziel verwendet. Wenn die Pfade der Dateien in Variablen gespeichert sind, können Sie alternativ auch die Namen der Variablen bereitstellen. Wenn Sie Variablen zum Speichern der Dateipfade verwenden möchten, müssen Sie zuerst die Option IsSourcePathVariable für die Quellverbindung und die Option IsDestinationPathVariable für die Zielverbindung auf **True** festlegen. Sie können dann die vorhandenen System- oder benutzerdefinierten Variablen zur Verwendung auswählen oder neue Variablen erstellen. Im Dialogfeld **Variable hinzufügen** können Sie den Bereich der Variablen konfigurieren und angeben. Der Bereich muss der Task Dateisystem oder ein übergeordneter Container sein. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) und [Verwenden von Variablen in Paketen](../Topic/Use%20Variables%20in%20Packages.md).  
  
> [!NOTE]  
>  Um die für die **SourceConnection** -Eigenschaft und die **DestinationConnection** -Eigenschaft ausgewählten Variablen zu überschreiben, geben Sie einen Ausdruck für die **Source** -Eigenschaft und einen für die **Destination** -Eigenschaft ein. Die Ausdrücke werden im **Editor für den Task 'Dateisystem'** auf der Seite **Ausdrücke**eingegeben. Wenn Sie beispielsweise den Pfad der Dateien, die vom Task verwendet werden, als Ziel festlegen möchten, kann in einigen Fällen die Variable A und in anderen die Variable B besser geeignet sein.  
  
> [!NOTE]  
>  Der Task Dateisystem wird in einer einzelnen Datei oder in einem einzelnen Verzeichnis ausgeführt. Daher unterstützt dieser Task nicht die Verwendung von Platzhalterzeichen, um denselben Vorgang in mehreren Dateien oder Verzeichnissen auszuführen. Damit der Task Dateisystem einen Vorgang in mehreren Dateien oder Verzeichnissen wiederholt, platzieren Sie den Task Dateisystem in einem Foreach-Schleifencontainer. Weitere Informationen finden Sie unter [File System Task](../../integration-services/control-flow/file-system-task.md).  
  
 Sie können Ausdrücke verwenden, um verschiedene Variablen einzusetzen.  
  
## enthalten  
 **IsDestinationPathVariable**  
 Geben Sie an, ob der Zielpfad in einer Variablen gespeichert ist. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Wahr**|Der Zielpfad ist in einer Variablen gespeichert. Wenn Sie diesen Wert auswählen, wird die dynamische Option **DestinationVariable**angezeigt.|  
|**False**|Der Zielpfad wird in einem Dateiverbindungs-Manager angegeben. Bei Auswahl dieses Wertes wird die dynamische Option **DestinationConnection**angezeigt.|  
  
 **OverwriteDestination**  
 Geben Sie an, ob der Vorgang Dateien im Zielverzeichnis überschreiben kann.  
  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Task Dateisystem an. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Description**  
 Geben Sie eine Beschreibung des Tasks Dateisystem ein.  
  
 **Vorgang**  
 Wählen Sie den auszuführenden Dateisystemvorgang aus. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Verzeichnis kopieren**|Kopieren Sie ein Verzeichnis. Bei Auswahl dieses Wertes werden die dynamischen Optionen für eine Quelle und ein Ziel angezeigt.|  
|**Datei kopieren**|Kopieren Sie eine Datei. Bei Auswahl dieses Wertes werden die dynamischen Optionen für eine Quelle und ein Ziel angezeigt.|  
|**Verzeichnis erstellen**|Erstellen Sie ein Verzeichnis. Bei Auswahl dieses Wertes werden die dynamischen Optionen für ein Quell- und ein Zielverzeichnis angezeigt.|  
|**Verzeichnis löschen**|Löschen Sie ein Verzeichnis. Bei Auswahl dieses Wertes werden die dynamischen Optionen für eine Quelle angezeigt.|  
|**Verzeichnisinhalt löschen**|Löschen Sie den Inhalt eines Verzeichnisses. Bei Auswahl dieses Wertes werden die dynamischen Optionen für eine Quelle angezeigt.|  
|**Datei löschen**|Löschen Sie eine Datei. Bei Auswahl dieses Wertes werden die dynamischen Optionen für eine Quelle angezeigt.|  
|**Verzeichnis verschieben**|Verschieben Sie ein Verzeichnis. Bei Auswahl dieses Wertes werden die dynamischen Optionen für eine Quelle und ein Ziel angezeigt.|  
|**Datei verschieben**|Verschieben Sie eine Datei. Bei Auswahl dieses Wertes werden die dynamischen Optionen für eine Quelle und ein Ziel angezeigt. Schließen Sie beim Verschieben einer Datei keinen Dateinamen in den Verzeichnispfad ein, den Sie als Ziel angeben.|  
|**Datei umbenennen**|Benennen Sie eine Datei um. Bei Auswahl dieses Wertes werden die dynamischen Optionen für eine Quelle und ein Ziel angezeigt. Schließen Sie beim Umbenennen einer Datei den neuen Dateinamen in den Verzeichnispfad ein, den Sie als Ziel angeben.|  
|**Attribute festlegen**|Legen Sie die Attribute einer Datei oder eines Verzeichnisses fest. Bei Auswahl dieses Wertes werden die dynamischen Optionen für eine Quelle und einen Vorgang angezeigt.|  
  
 **IsSourcePathVariable**  
 Geben Sie an, ob der Zielpfad in einer Variablen gespeichert ist. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert||  
|-----------|-|  
|**True**|Der Zielpfad ist in einer Variablen gespeichert. Bei Auswahl dieses Wertes wird die dynamische Option **SourceVariable**angezeigt.|  
|**False**|Der Zielpfad wird in einem Dateiverbindungs-Manager angegeben. Wenn Sie diesen Wert auswählen, wird die dynamische Option **DestinationVariable**angezeigt.|  
  
## IsDestinationPathVariable (dynamische Optionen)  
  
### IsDestinationPathVariable = True  
 **DestinationVariable**  
 Wählen Sie den Variablennamen aus der Liste aus, oder klicken Sie auf \<**Neue Variable…**>, um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](../Topic/Add%20Variable.md)  
  
### IsDestinationPathVariable = False  
 **DestinationConnection**  
 Wählen Sie einen Dateiverbindungs-Manager aus der Liste aus, oder klicken Sie auf \<**Neue Verbindung...**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## IsSourcePathVariable (dynamische Optionen)  
  
### IsSourcePathVariable = True  
 **SourceVariable**  
 Wählen Sie den Variablennamen aus der Liste aus, oder klicken Sie auf \<**Neue Variable…**>, um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](../Topic/Add%20Variable.md)  
  
### IsSourcePathVariable = False  
 **SourceConnection**  
 Wählen Sie einen Dateiverbindungs-Manager aus der Liste aus, oder klicken Sie auf \<**Neue Verbindung...**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## Operation (dynamische Optionen)  
  
### Operation = Set Attributes  
 **Hidden**  
 Geben Sie an, ob die Datei oder das Verzeichnis angezeigt wird.  
  
 **ReadOnly**  
 Geben Sie an, ob die Datei schreibgeschützt ist.  
  
 **Archive**  
 Geben Sie an, ob die Datei oder das Verzeichnis archiviert werden kann.  
  
 **System**  
 Geben Sie an, ob die Datei eine Betriebssystemdatei ist.  
  
### Operation = Create directory  
 **UseDirectoryIfExists**  
 Gibt an, ob der Vorgang **Verzeichnis erstellen** ein vorhandenes Verzeichnis mit dem angegebenen Namen verwendet, statt ein neues Verzeichnis zu erstellen.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
  