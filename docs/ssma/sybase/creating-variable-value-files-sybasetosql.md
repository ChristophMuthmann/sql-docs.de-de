---
title: Erstellen von Variablenwert-Dateien (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Creating Variable Value Files
- Sybase Console,Variable Value File Validation
ms.assetid: 395be464-4b19-44f7-91e5-b8876d6743dc
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e23cffcc79e0276f5003537b4ecc724efe76b36d
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="creating-variable-value-files-sybasetosql"></a>Erstellen von Variablenwert-Dateien (SybaseToSQL)
Variablendatei Wert ist eine XML-Datei mit den Parameterwerten für Befehle wie die Quelle oder Ziel-Servernamen, die häufig von der Migration von einem Server auf einen anderen ändern. Wenn eine große Anzahl von Datenbank-Migrationen auftreten, mehrere Dateien zum Speichern des Wert der einzelnen Quellserver werden erstellt und in master Skriptdatei mit verwiesen die **– V** zur Befehlszeile wechseln. Dadurch erhalten Sie statische Werte in ein paar Skriptdateien mit den Variablen Werten in mehreren Dateien.  
  
> [!NOTE]  
> 1.  Variablennamen sind mit dem Präfix und Suffix ein Symbol, das $ (Dollar). Wenn einen Wert in der Datei Variablenwert in der Variablen nicht zugewiesen sind, treten einen Fehler während der Analyse der Skriptdatei an, was in der Konsole Ausführungsprozess führte.  
> 2.  The escape character for **$** is **$$**. Wenn der Wert, der eine Variable oder ein statischer Wert eines Parameters enthält  **$**  Symbol (Dollar), klicken Sie dann  **$$**  muss angegeben werden, um es als ein Zeichen anstatt einer Variablen zu behandeln.  
> 3.  Aus Gründen der Verwaltbarkeit können Variablen deklariert werden in `‘variable-group’` Elemente logische Trennung von Benutzer definierte Variablen.  Verwendung dieses Elements ist nicht obligatorisch.  
  
**Beispiele:**  
  
**Beispiel 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$project_folder$" value="<project-folder>"/>  
  
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
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
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
Benutzer kann problemlos überprüfen Benutzervoreinstellung Variablenwert-Datei anhand der Schemadefinitionsdatei **ConsoleScriptVariablesSchema.xsd** in den Ordner "Schemas" verfügbar.  
  
## <a name="next-step"></a>Nächster Schritt  
Im nächsten Schritt in der Konsole funktioniert [erstellen, die Server-Connection-Dateien &#40; SybaseToSQL &#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen die Server-Datenbankdateien (Sybase)](http://msdn.microsoft.com/en-us/35ef396f-9f98-429d-9fc5-4f413d08fb37)  
  

