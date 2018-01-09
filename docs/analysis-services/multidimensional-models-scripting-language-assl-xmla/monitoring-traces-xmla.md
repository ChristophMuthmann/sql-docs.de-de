---
title: "Überwachen von Ablaufverfolgungen (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- XML for Analysis, traces
- XMLA, traces
- monitoring traces [XMLA]
- traces [Analysis Services]
ms.assetid: cdbfb984-18bd-4c4e-8fb7-d64ce298ed35
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3ae92fd24e3e9d5abbf3084472eac09a0e2d59fb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="monitoring-traces-xmla"></a>Überwachen von Ablaufverfolgungen (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Sie können die [abonnieren](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md) -Befehl in XML for Analysis (XMLA) zum Überwachen einer vorhandenen Ablaufverfolgungs definiert, die auf einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Die **abonnieren** Befehl gibt die Ergebnisse einer Ablaufverfolgung als Rowset zurück.  
  
## <a name="specifying-a-trace"></a>Festlegen einer Ablaufverfolgung  
 Die [Objekt](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) Eigenschaft von der **abonnieren** -Befehls muss einen Objektverweis auf entweder enthalten eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz oder eine Ablaufverfolgung auf eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz. Wenn die **Objekt** Eigenschaft wurde nicht angegeben oder ein ablaufverfolgungsbezeichner ist nicht angegeben, der **Objekt** -Eigenschaft, die **abonnieren** Befehl überwacht die Ablaufverfolgung der standardsitzung für die explizite Sitzung in den SOAP-Header für den Befehl angegeben.  
  
## <a name="returning-results"></a>Zurückgeben von Ergebnissen  
 Die **abonnieren** Befehl gibt ein Rowset mit der Ablaufverfolgungsereignisse, die durch die angegebene Ablaufverfolgung aufgezeichnet. Die **abonnieren** -Befehl gibt Ablaufverfolgungsergebnisse zurück, bis der Befehl abgebrochen wird, indem Sie die ["Abbrechen"](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md) Befehl.  
  
 Das Rowset enthält die in der folgenden Tabelle aufgeführten Spalten.  
  
|Spalte|Datentyp|Description|  
|------------|---------------|-----------------|  
|EventClass|Integer|Die von der Ablaufverfolgung empfangene Ereignisklasse des Ereignisses.|  
|EventSubclass|Lange ganze Zahl|Die von der Ablaufverfolgung empfangene Ereignisunterklasse des Ereignisses.|  
|CurrentTime|DATETIME|Der Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|DATETIME|Der Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|DATETIME|Zeitpunkt, zu dem das Ereignis beendet wurde (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".<br /><br /> Diese Spalte wird nicht für Ereignisklassen aufgefüllt, die den Beginn eines Prozesses oder einer Aktion beschreiben.|  
|Duration|Lange ganze Zahl|Die Gesamtzeitspanne (in Millisekunden), die für das Ereignis vergangen ist.|  
|CPUTime|Lange ganze Zahl|Die Prozessorzeit (in Millisekunden), die für das Ereignis vergangen ist.|  
|JobID|Lange ganze Zahl|Der Auftragsbezeichner für den Prozess.|  
|SessionID|Zeichenfolge|Der Bezeichner der Sitzung, für die das Ereignis aufgetreten ist.|  
|SessionType|Zeichenfolge|Der Typ der Sitzung, für die das Ereignis aufgetreten ist.|  
|ProgressTotal|Lange ganze Zahl|Der Gesamtfortschritt, der von dem Ereignis gemeldet wurde.|  
|IntegerData|Lange ganze Zahl|Die diesem Ereignis zugeordneten ganzzahligen Daten. Der Inhalt dieser Spalte ist von der Ereignisklasse und der Unterklasse des Ereignisses abhängig.|  
|ObjectID|Zeichenfolge|Der Bezeichner des Objekts, für das das Ereignis aufgetreten ist.|  
|ObjectType|Zeichenfolge|Der Typ des in ObjectName festgelegten Objekts.|  
|ObjectName|Zeichenfolge|Der Name des Objekts, für das das Ereignis aufgetreten ist.|  
|ObjectPath|Zeichenfolge|Der hierarchische Pfad des Objekts, für das das Ereignis aufgetreten ist. Der Pfad wird als kommagetrennte Zeichenfolge von Objektbezeichnern für die übergeordneten Elemente des in ObjectName festgelegten Objekts dargestellt.|  
|ObjectReference|Zeichenfolge|Die XML-Darstellung des Objektverweises für das in ObjectName festgelegte Objekt.|  
|NestLevel|Integer|Die Ebene der Transaktion, für die das Ereignis aufgetreten ist.|  
|NumSegments|Lange ganze Zahl|Die Anzahl der Datensegmente, die von dem Befehl, für den das Ereignis aufgetreten ist, betroffen ist, oder auf die zugegriffen wurde.|  
|Schweregrad|Integer|Der Schweregrad einer Ausnahme für das Ereignis. Die Spalte kann einen der folgenden Werte enthalten:<br /><br /> <br /><br /> 0: Erfolg<br /><br /> <br /><br /> 1: Informationen<br /><br /> <br /><br /> 2: Warnung<br /><br /> <br /><br /> 3: Fehler|  
|Success|Boolean|Gibt an, ob ein Befehl erfolgreich war oder zu einem Fehler geführt hat.|  
|Fehler|Lange ganze Zahl|Die Fehlernummer des Ereignisses (falls zutreffend).|  
|ConnectionID|Zeichenfolge|Der Bezeichner der Verbindung, für die das Ereignis aufgetreten ist.|  
|DatabaseName|Zeichenfolge|Der Name der Datenbank, für die das Ereignis aufgetreten ist.|  
|NTUserName|Zeichenfolge|Der Windows-Benutzername des Benutzers, der dem Ereignis zugeordnet ist.|  
|NTDomainName|Zeichenfolge|Die Windows-Domäne des Benutzers, der dem Ereignis zugeordnet ist.|  
|ClientHostName|Zeichenfolge|Der Name des Computers, auf dem die Clientanwendung ausgeführt wird. Diese Spalte wird mit den von der Clientanwendung übergebenen Werten aufgefüllt.|  
|ClientProcessID|Lange ganze Zahl|Der Prozessbezeichner der Clientanwendung.|  
|ApplicationName|Zeichenfolge|Der Name der Clientanwendung, die die Verbindung mit der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Clientanwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|  
|NTCanonicalUserName|Zeichenfolge|Der kanonische Windows-Benutzername des Benutzers, der dem Ereignis zugeordnet ist.|  
|SPID|Zeichenfolge|Die Serverprozess-ID (SPID) der Sitzung, für die das Ereignis aufgetreten ist. Der Wert dieser Spalte entspricht direkt der Sitzungs-ID, die im SOAP-Header der XMLA-Nachricht festgelegt wurde, für die das Ereignis aufgetreten ist.|  
|TextData|Zeichenfolge|Die diesem Ereignis zugeordneten Textdaten. Der Inhalt dieser Spalte ist von der Ereignisklasse und der Unterklasse des Ereignisses abhängig.|  
|ServerName|Zeichenfolge|Der Name der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz, für die das Ereignis aufgetreten ist.|  
|RequestParameters|Zeichenfolge|Die Parameter der parametrisierten Abfrage oder des XMLA-Befehls, für die oder den das Ereignis aufgetreten ist.|  
|RequestProperties|Zeichenfolge|Die Eigenschaften der XMLA-Methode, für die das Ereignis aufgetreten ist.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
