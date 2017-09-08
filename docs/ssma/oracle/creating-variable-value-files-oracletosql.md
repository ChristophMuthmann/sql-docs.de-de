---
title: Erstellen von Variablenwert-Dateien (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Variable Value File Creation
- Variable Value File, Variable Value File Validation
ms.assetid: f583d81a-8e34-41b1-8100-ee3a6a82213b
caps.latest.revision: 26
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3ba4def7c054b0d5a65a8ac93698cf6cb432845a
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="creating-variable-value-files-oracletosql"></a>Erstellen von Variablenwert-Dateien (OracleToSQL)
Variablendatei Wert ist eine XML-Datei mit den Parameterwerten für Befehle wie die Quelle oder Ziel-Servernamen, die häufig von der Migration von einem Server auf einen anderen ändern. Wenn eine große Anzahl von Datenbank-Migrationen auftreten, mehrere Dateien zum Speichern des Wert der einzelnen Quellserver werden erstellt und in master Skriptdatei mit verwiesen die **– V** zur Befehlszeile wechseln. Dadurch erhalten Sie statische Werte in ein paar Skriptdateien mit den Variablen Werten in mehreren Dateien.  
  
> [!NOTE]  
> 1.  Variablennamen sind mit dem Präfix und Suffix ein Symbol, das $ (Dollar). Wenn einen Wert in der Datei Variablenwert in der Variablen nicht zugewiesen sind, treten einen Fehler während der Analyse der Skriptdatei an, was in der Konsole Ausführungsprozess führte.  
> 2.  The escape character for **$** is **$$**. Wenn der Wert, der eine Variable oder ein statischer Wert eines Parameters enthält  **$**  Symbol (Dollar), klicken Sie dann  **$$**  muss angegeben werden, um es als ein Zeichen anstatt einer Variablen zu behandeln.  
> 3.  Aus Gründen der Verwaltbarkeit können Variablen deklariert werden in `‘variable-group’` Elemente logische Trennung von Benutzer definierte Variablen.  Verwendung dieses Elements ist nicht obligatorisch.  
  
**Beispiele:**  
  
**Beispiel 1:**  
  
```  
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
  
```  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
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
  
## <a name="next-step"></a>Nächster Schritt  
Im nächsten Schritt in der Konsole funktioniert [erstellen, die Server-Connection-Dateien &#40; OracleToSQL &#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen die Server-Datenbankdateien (Oracle)](http://msdn.microsoft.com/en-us/002f129e-0868-48ad-a4b4-c68b5007e12e)  
  

