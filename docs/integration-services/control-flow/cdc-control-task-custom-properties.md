---
title: "Benutzerdefinierte Eigenschaften des CDC-Steuerungstasks | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2a073699-79a2-4ea1-a68e-fc17a80b74ba
caps.latest.revision: 9
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Benutzerdefinierte Eigenschaften des CDC-Steuerungstasks
  In der folgenden Tabelle werden die benutzerdefinierten Eigenschaften des CDC-Steuerungstasks beschrieben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftsname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|Verbindung|ADO.NET-Verbindung|Eine ADO.NET-Verbindung zur [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -CDC-Datenbank für Zugriff auf die Änderungstabellen und den CDC-Status, falls diese Daten in derselben Datenbank gespeichert werden.<br /><br /> Die Verbindung muss zu einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank hergestellt werden, die für CDC aktiviert ist und in der sich die ausgewählte Änderungstabelle befindet.|  
|TaskOperation|Ganze Zahl (Enumeration)|Der ausgewählte Vorgang für den CDC-Steuerungstask. Die möglichen Werte sind **Mark Initial Load Start**, **Mark Initial Load End**, **Mark CDC Start**, **Get Processing Range**, **Mark Processed Range**und **Reset CDC State**.<br /><br /> Wenn Sie beim Arbeiten mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC (also nicht mit Oracle) die Option **MarkCdcStart**, **MarkInitialLoadStart** oder **MarkInitialLoadEnd** auswählen, muss im Verbindungs-Manager ein Benutzer mit der Berechtigung **db_owner** oder **sysadmin** angegeben werden.<br /><br /> Weitere Informationen zu diesen Vorgängen finden Sie unter [CDC Control Task Editor](../../integration-services/control-flow/cdc-control-task-editor.md) und [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md).|  
|OperationParameter|String|Wird momentan mit dem **MarkCdcStart** -Vorgang verwendet. Dieser Parameter ermöglicht eine zusätzliche Eingabe, die für den jeweiligen Vorgang erforderlich ist. Beispiel: Für den **MarkCdcStart** -Vorgang erforderliche LSN-Nummer|  
|StateVariable|String|Eine SSIS-Paketvariable, die den CDC-Status des aktuellen CDC-Kontexts speichert. Der CDC-Steuerungstask liest und schreibt den Status in die **StateVariable** und führt das Laden oder das Speichern in einem persistenten Speicher nur durch, wenn **AutomaticStatePersistence** ausgewählt wird. Weitere Informationen finden Sie unter [Definieren einer Statusvariablen](../../integration-services/data-flow/define-a-state-variable.md).|  
|AutomaticStatePersistence|Boolean|Der CDC-Steuerungstask liest den CDC-Status aus der CDC-Statuspaketvariablen. Nach einem Vorgang aktualisiert der CDC-Steuerungstask den Wert der CDC-Statuspaketvariablen. Die **AutomaticStatePersistence** -Eigenschaft teilt dem CDC-Steuerungstask mit, wer zwischen den Ausführungen des SSIS-Pakets für das Beibehalten des CDC-Statuswerts zuständig ist.<br /><br /> Wenn diese Eigenschaft den Wert **true**hat, lädt der CDC-Steuerungstask den Wert der CDC-Statusvariablen automatisch aus einer Statustabelle. Wenn der CDC-Steuerungstask den Wert der CDC-Statusvariablen aktualisiert, wird auch der dazugehörige Wert von **table.stores**mit dem gleichen Status aktualisiert, der Status in einer speziellen Tabelle gespeichert und die Statusvariable aktualisiert. Der Entwickler kann steuern, welche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank diese Statustabelle und ihren Namen enthält. Die Struktur dieser Statustabelle wird vordefiniert.<br /><br /> Wenn **false**gilt, führt der CDC-Steuerungstask das Beibehalten seines Werts nicht durch. Wenn true gilt, speichert der CDC-Steuerungstask den Status in einer speziellen Tabelle und aktualisiert die StateVariable.<br /><br /> Der Standardwert ist **true**und gibt an, dass die Statusbeibehaltung automatisch aktualisiert wird.|  
|StateConnection|ADO.NET-Verbindung|Eine ADO.NET-Verbindung zur Datenbank, in der sich bei Verwendung von **AutomaticStatePersistence**die Statustabelle befindet. Der Standardwert ist der gleiche Wert für **Verbindung**.|  
|StateName|String|Der dem persistenten Status zugeordnete Name. In den Paketen für das vollständige Laden und den CDC-Paketen, die denselben CDC-Kontext verwenden, wird ein gemeinsamer CDC-Kontextname angegeben. Dieser Name wird zum Nachschlagen der Statuszeile in der Statustabelle verwendet.<br /><br /> Diese Eigenschaft gilt nur, wenn **AutomaticStatePersistence** auf **true**festgelegt ist.|  
|StateTable|String|Gibt den Namen der Tabelle an, in der der CDC-Kontextstatus gespeichert ist. Auf diese Tabelle muss der Zugriff mit der für diese Komponente konfigurierten Verbindung möglich sein. Diese Tabelle muss varchar-Spalten mit den Namen **name** und **state**enthalten. (Die Spalte **state** muss mindestens 256 Zeichen aufweisen.)<br /><br /> Diese Eigenschaft gilt nur, wenn **AutomaticStatePersistence** auf **true**festgelegt ist.|  
|CommandTimeout|integer|Dieser Wert gibt beim Kommunizieren mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank das Timeout (in Sekunden) an. Dieser Wert wird verwendet, wenn die Antwortzeit der Datenbank sehr langsam ist und der Standardwert (30 Sekunden) nicht ausreicht.|  
  
## Siehe auch  
 [CDC-Steuerungstask](../../integration-services/control-flow/cdc-control-task.md)   
 [Task-Editor für CDC-Steuerelement](../../integration-services/control-flow/cdc-control-task-editor.md)  
  
  