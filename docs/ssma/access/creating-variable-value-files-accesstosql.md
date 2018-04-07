---
title: Erstellen von Variablenwert-Dateien (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c9e2d86d94c8e49c2aa54e431e5b2c2c4a1ba43
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="creating-variable-value-files-accesstosql"></a>Erstellen von Variablenwert-Dateien (AccessToSQL)
Ein Wert Variablendatei ist eine XML-Datei mit den Parameterwerten für Befehle (z. B. den Servernamen Quelle bzw. zum Ziel), die häufig für Migrationen zu ändern. Wenn eine große Anzahl von Datenbank-Migrationen auftreten, mehrere Dateien zum Speichern des Wert der einzelnen Quellserver erstellt und in einer master Skriptdatei mit referenziert werden die **– V** zur Befehlszeile wechseln. Dieses Verhalten hilft dabei, die statische Werte in ein paar Skriptdateien mit den Variablen Werten in mehreren Dateien.  
  
> [!NOTE]  
> -  Variablennamen sind mit dem Präfix und Suffix ein Symbol, das $ (Dollar). Wenn eine Variable einen Wert in der Datei der Wert der Variablen nicht zugewiesen ist, tritt ein Fehler während der Analyse der Skriptdatei, resultierende, in der Konsole Ausführungsprozess führte.  
> -  The escape character for **$** is **$$**. Wenn der Wert, der eine Variable oder ein statischer Wert eines Parameters enthält eine **$** Symbol (Dollar), klicken Sie dann **$$** muss angegeben werden, um es als ein Zeichen anstatt einer Variablen zu behandeln.  
> -  Aus Gründen der Verwaltbarkeit können Variablen deklariert werden in `‘variable-group’` Elemente logische Trennung von benutzerdefinierten Variablen.  Verwendung dieses Elements ist nicht obligatorisch.  
  
**Beispiele:**  
  
**Beispiel 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$type$" value="MyProject"/>  
  
    <variable name="$project_folder$" value=".\$project_name$"/>  
  
    <variable name="$project_name$" value="$type$ConsoleProject"/>  
  
    <variable name="$project_overwrite$" value="true"/>  
  
    <variable name="$project_type$" value="sql-server-2008"/>  
  
  </variable-group>  
  
</variables>  
```  
**Beispiel 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="xxx"/>  
  
      <variable name="$TargetDB$" value="xxx"/>  
  
      <variable name="$TargetUserName$" value="xxx"/>  
  
      <variable name="$TargetPassword$" value="xxx"/>  
  
      <variable name="$TargetIsTrusted$" value="xxx"/>  
  
      <variable name="$TrustedConnection$" value="xxx"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="TestTable1"/>  
  
      <variable name="$ObjectName2$" value="TestProc1"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>Variablenwert-dateiüberprüfung  
Benutzer kann problemlos überprüfen Benutzervoreinstellung Variablenwert-Datei anhand der Schemadefinitionsdatei **ConsoleScriptVariablesSchema.xsd** in den Ordner "Schemas" verfügbar.  
  
## <a name="next-step"></a>Nächster Schritt  
Im nächsten Schritt in der Konsole funktioniert [erstellen die Server-Verbindungsdateien &#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen die Server-Verbindungsdateien (Access)](http://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  
