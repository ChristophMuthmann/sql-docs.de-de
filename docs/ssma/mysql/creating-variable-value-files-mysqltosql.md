---
title: Erstellen von Variablenwert-Dateien (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Creating variable value files
- variable value file validation
ms.assetid: 1dc56a7b-8e3a-4576-ad4f-47050bf7e28a
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67d08fcef37c1fbb8e2c740233c0d84176c7f5bb
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="creating-variable-value-files-mysqltosql"></a>Erstellen von Variablenwert-Dateien (MySQLToSQL)
Variablendatei Wert ist eine XML-Datei mit den Parameterwerten für Befehle wie die Quelle oder Ziel-Servernamen, die häufig von der Migration von einem Server auf einen anderen ändern. Wenn eine große Anzahl von Datenbank-Migrationen auftreten, mehrere Dateien zum Speichern des Wert der einzelnen Quellserver werden erstellt und in master Skriptdatei mit verwiesen die **– V** zur Befehlszeile wechseln. Dadurch erhalten Sie statische Werte in ein paar Skriptdateien mit den Variablen Werten in mehreren Dateien.  
  
> [!NOTE]  
> 1.  Variablennamen sind mit dem Präfix und Suffix ein Symbol, das $ (Dollar). Wenn einen Wert in der Datei Variablenwert in der Variablen nicht zugewiesen sind, treten einen Fehler während der Analyse der Skriptdatei an, was in der Konsole Ausführungsprozess führte.  
> 2.  The escape character for **$** is **$$**. Wenn der Wert, der eine Variable oder ein statischer Wert eines Parameters enthält **$** Symbol (Dollar), klicken Sie dann **$$** muss angegeben werden, um es als ein Zeichen anstatt einer Variablen zu behandeln.  
> 3.  Aus Gründen der Verwaltbarkeit können Variablen deklariert werden in `‘variable-group’` Elemente logische Trennung von Benutzer definierte Variablen.  Verwendung dieses Elements ist nicht obligatorisch.  
  
**Beispiele:**  
  
**Beispiel 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$project_folder$" value="<folder-name>"/>  
  
    <variable name="$project_name$" value="<project-name>"/>  
  
    <variable name="$project_overwrite$" value="<true/false>"/>  
  
    <variable name="$project_type$" value="<project-type>"/>  
  
  </variable-group>  
  
</variables>  
```  
**Beispiel 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetUserName$ value="<user-name>"/>  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
      <variable name="$TargetPassword$" value="<password>"/>  
  
      <variable name="$TrustedConnection$" value="<true/false>"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="<object-name>"/>  
  
      <variable name="$ObjectName2$" value="<object-name>"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>Variablenwert-Dateiüberprüfung  
Benutzer kann problemlos überprüfen Benutzervoreinstellung Variablenwert-Datei anhand der Schemadefinitionsdatei **"ConsoleScriptVariablesSchema.xsd"** in den Ordner "Schemas" verfügbar.  
  
## <a name="next-step"></a>Nächster Schritt  
Im nächsten Schritt in der Konsole funktioniert [erstellen die Server-Verbindungsdateien &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen die Server-Connection-Dateien (MySQL)](http://msdn.microsoft.com/en-us/df0e970c-da0b-4118-b359-c9dcbbad16d6)  
  
