---
title: "Überwachen von Ablaufverfolgungen (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XML for Analysis, traces
- XMLA, traces
- monitoring traces [XMLA]
- traces [Analysis Services]
ms.assetid: cdbfb984-18bd-4c4e-8fb7-d64ce298ed35
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d63e2b7e07c01d0f937618cfc521921e9d16dc43
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="monitoring-traces-xmla"></a>Überwachen von Ablaufverfolgungen (XMLA)
  Sie können die [abonnieren](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md) -Befehl in XML for Analysis (XMLA) zum Überwachen einer vorhandenen Ablaufverfolgungs definiert, die auf einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Die **abonnieren** Befehl gibt die Ergebnisse einer Ablaufverfolgung als Rowset zurück.  
  
## <a name="specifying-a-trace"></a>Festlegen einer Ablaufverfolgung  
 Die [Objekt](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) Eigenschaft von der **abonnieren** -Befehls muss einen Objektverweis auf entweder enthalten eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz oder eine Ablaufverfolgung auf eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz. Wenn die **Objekt** Eigenschaft wurde nicht angegeben oder ein ablaufverfolgungsbezeichner ist nicht angegeben, der **Objekt** -Eigenschaft, die **abonnieren** Befehl überwacht die Ablaufverfolgung der standardsitzung für die explizite Sitzung in den SOAP-Header für den Befehl angegeben.  
  
## <a name="returning-results"></a>Zurückgeben von Ergebnissen  
 Die **abonnieren** Befehl gibt ein Rowset mit der Ablaufverfolgungsereignisse, die durch die angegebene Ablaufverfolgung aufgezeichnet. Die **abonnieren** -Befehl gibt Ablaufverfolgungsergebnisse zurück, bis der Befehl abgebrochen wird, indem Sie die ["Abbrechen"](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md) Befehl.  
  
 Das Rowset enthält die in der folgenden Tabelle aufgeführten Spalten.  
  
|Column|Datentyp|Description|  
|------------|---------------|-----------------|  
|EventClass|Integer|Die von der Ablaufverfolgung empfangene Ereignisklasse des Ereignisses.|  
|EventSubclass|Lange ganze Zahl|Die von der Ablaufverfolgung empfangene Ereignisunterklasse des Ereignisses.|  
|CurrentTime|Datetime|Der Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|Datetime|Der Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|Datetime|Zeitpunkt, zu dem das Ereignis beendet wurde (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".<br /><br /> Diese Spalte wird nicht für Ereignisklassen aufgefüllt, die den Beginn eines Prozesses oder einer Aktion beschreiben.|  
|Dauer|Lange ganze Zahl|Die Gesamtzeitspanne (in Millisekunden), die für das Ereignis vergangen ist.|  
|CPUTime|Lange ganze Zahl|Die Prozessorzeit (in Millisekunden), die für das Ereignis vergangen ist.|  
|JobID|Lange ganze Zahl|Der Auftragsbezeichner für den Prozess.|  
|SessionID|String|Der Bezeichner der Sitzung, für die das Ereignis aufgetreten ist.|  
|SessionType|String|Der Typ der Sitzung, für die das Ereignis aufgetreten ist.|  
|ProgressTotal|Lange ganze Zahl|Der Gesamtfortschritt, der von dem Ereignis gemeldet wurde.|  
|IntegerData|Lange ganze Zahl|Die diesem Ereignis zugeordneten ganzzahligen Daten. Der Inhalt dieser Spalte ist von der Ereignisklasse und der Unterklasse des Ereignisses abhängig.|  
|ObjectID|String|Der Bezeichner des Objekts, für das das Ereignis aufgetreten ist.|  
|ObjectType|String|Der Typ des in ObjectName festgelegten Objekts.|  
|ObjectName|String|Der Name des Objekts, für das das Ereignis aufgetreten ist.|  
|ObjectPath|String|Der hierarchische Pfad des Objekts, für das das Ereignis aufgetreten ist. Der Pfad wird als kommagetrennte Zeichenfolge von Objektbezeichnern für die übergeordneten Elemente des in ObjectName festgelegten Objekts dargestellt.|  
|ObjectReference|String|Die XML-Darstellung des Objektverweises für das in ObjectName festgelegte Objekt.|  
|NestLevel|Integer|Die Ebene der Transaktion, für die das Ereignis aufgetreten ist.|  
|NumSegments|Lange ganze Zahl|Die Anzahl der Datensegmente, die von dem Befehl, für den das Ereignis aufgetreten ist, betroffen ist, oder auf die zugegriffen wurde.|  
|Severity|Integer|Der Schweregrad einer Ausnahme für das Ereignis. Die Spalte kann einen der folgenden Werte enthalten:<br /><br /> <br /><br /> 0: Erfolg<br /><br /> <br /><br /> 1: Informationen<br /><br /> <br /><br /> 2: Warnung<br /><br /> <br /><br /> 3: Fehler|  
|Success|Boolean|Gibt an, ob ein Befehl erfolgreich war oder zu einem Fehler geführt hat.|  
|Fehler|Lange ganze Zahl|Die Fehlernummer des Ereignisses (falls zutreffend).|  
|ConnectionID|String|Der Bezeichner der Verbindung, für die das Ereignis aufgetreten ist.|  
|DatabaseName|String|Der Name der Datenbank, für die das Ereignis aufgetreten ist.|  
|NTUserName|String|Der Windows-Benutzername des Benutzers, der dem Ereignis zugeordnet ist.|  
|NTDomainName|String|Die Windows-Domäne des Benutzers, der dem Ereignis zugeordnet ist.|  
|ClientHostName|String|Der Name des Computers, auf dem die Clientanwendung ausgeführt wird. Diese Spalte wird mit den von der Clientanwendung übergebenen Werten aufgefüllt.|  
|ClientProcessID|Lange ganze Zahl|Der Prozessbezeichner der Clientanwendung.|  
|ApplicationName|String|Der Name der Clientanwendung, die die Verbindung mit der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Clientanwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|  
|NTCanonicalUserName|String|Der kanonische Windows-Benutzername des Benutzers, der dem Ereignis zugeordnet ist.|  
|SPID|String|Die Serverprozess-ID (SPID) der Sitzung, für die das Ereignis aufgetreten ist. Der Wert dieser Spalte entspricht direkt der Sitzungs-ID, die im SOAP-Header der XMLA-Nachricht festgelegt wurde, für die das Ereignis aufgetreten ist.|  
|TextData|String|Die diesem Ereignis zugeordneten Textdaten. Der Inhalt dieser Spalte ist von der Ereignisklasse und der Unterklasse des Ereignisses abhängig.|  
|ServerName|String|Der Name der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz, für die das Ereignis aufgetreten ist.|  
|RequestParameters|String|Die Parameter der parametrisierten Abfrage oder des XMLA-Befehls, für die oder den das Ereignis aufgetreten ist.|  
|RequestProperties|String|Die Eigenschaften der XMLA-Methode, für die das Ereignis aufgetreten ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

