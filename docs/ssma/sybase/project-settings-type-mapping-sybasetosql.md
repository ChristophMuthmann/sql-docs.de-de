---
title: Projekteinstellungen (Zuordnung) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 411cb12d17399e43ebdc454f5f55a5c5595972a2
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="project-settings-type-mapping-sybasetosql"></a>Projekteinstellungen (Zuordnung) (SybaseToSQL)
Die Seite "Type Mapping", der die **Projekteinstellungen** Dialogfeld enthält Einstellungen, anpassen, wie SSMA für Sybase Adaptive Server Enterprise (ASE)-Datentypen in konvertiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentypen.  
  
Die Seite "Type Mapping" steht in der **Projekteinstellungen** und **Projekt Standardeinstellungen** Dialogfelder.  
  
-   Angeben der Einstellungen für die Zuordnung für alle zukünftigen SSMA-Projekte, auf die **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**, wählen Sie die Migration-Projekttyp, die für die Einstellungen sind erforderlich, angezeigt oder geändert werden **Migration Zielversion** Dropdown-Liste, und wählen Sie dann **Typzuordnung** unten im linken Bereich.  
  
-   Zum Angeben von Einstellungen für das aktuelle Projekt auf die **Tools** klicken Sie im Menü **Projekteinstellungen**, und wählen Sie dann **Type Mapping** unten im linken Bereich.  
  
## <a name="options"></a>enthalten  
**Quelltyp**  
Der zugeordnete ASE-Datentyp.  
  
**Zieltyp**  
Das Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datentyp für den angegebenen ASE-Datentyp.  
  
Siehe die Tabelle im folgenden Abschnitt für den standardmäßigen SSMA für Sybase-Typzuordnung.  
  
**Hinzufügen**  
Klicken Sie auf diese Option, um einen Datentyp der Zuordnungsliste hinzuzufügen.  
  
**Bearbeiten**  
Klicken Sie auf diese Option, um den ausgewählten Datentyp in der Zuordnungsliste zu bearbeiten.  
  
**Entfernen**  
Klicken Sie auf diese Option, um die ausgewählte Zuordnung aus der Zuordnungsliste zu entfernen.  
  
**Standard wiederherstellen**  
Klicken Sie auf diese Option, um die Liste ' datentypzuordnung ' auf die SSMA-Standardwerte zurückzusetzen.  
  
## <a name="default-type-mapping"></a>Standardtypmapping  
Die folgende Tabelle enthält die Standard-Typzuordnung zwischen ASE und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentypen.  
  
|ASE-Datentyp|SQL Server-Datentyp|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binary**|**binary**|  
|**Binary [\*... 8000]**|**binary[\*]**|  
|**binary[8001..\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**Char varying [\*... 8000]**|**varchar[\*]**|  
|**char varying[8001..\*]**|**varchar(max)**|  
|**Char [\*... 8000]**|**char[\*]**|  
|**char[8001..\*;]**|**varchar(max)**|  
|**character**|**char**|  
|**unterschiedliche Zeichen**|**varchar**|  
|**unterschiedliche Zeichen [\*... 8000]**|**varchar[\*]**|  
|**character varying[8001..\*]**|**varchar(max)**|  
|**Zeichen [\*... 8000]**|**char[\*]**|  
|**character[8001..\*]**|**varchar(max)**|  
|**Datum**|**Datum**|  
|**datetime**|**datetime2[3]**|  
|**dec**|**decimal**|  
|**dec[\*..\*]**|**decimal[\*]**|  
|**dec[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**decimal**|**decimal**|  
|**decimal[\*..\*]**|**decimal[\*]**|  
|**decimal[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**mit doppelter Genauigkeit**|**float[53]**|  
|**float**|**float[53]**|  
|**float[\*..15]**|**float[24]**|  
|**float[16..\*]**|**float[53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**nvarchar[255]**|  
|**money**|**money**|  
|**National char**|**nchar**|  
|**National Char [\*... 4000]**|**nchar[\*]**|  
|**National Char varying**|**nvarchar**|  
|**National Char varying [\*... 4000]**|**nvarchar[\*]**|  
|**National Char varying [4001..\*]**|**nvarchar(max)**|  
|**National Char [4001..\*]**|**nvarchar(max)**|  
|**nationale Zeichensätze**|**nchar**|  
|**nationale Zeichensätze [\*... 4000]**|**nchar[\*]**|  
|**nationale Zeichensätze [4001..\*]**|**nvarchar(max)**|  
|**nationale Zeichensätze varying**|**nvarchar**|  
|**nationale Zeichensätze varying [\*... 4000]**|**nvarchar[\*]**|  
|**nationale Zeichensätze varying [4001..\*]**|**nvarchar(max)**|  
|**National varchar**|**nvarchar**|  
|**National Varchar [\*... 4000]**|**nvarchar[\*]**|  
|**National Varchar [4001..\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**NCHAR varying**|**nvarchar**|  
|**NCHAR varying [\*... 4000]**|**nvarchar[\*]**|  
|**nchar varying[4001..\*]**|**nvarchar(max)**|  
|**NCHAR [\*... 4000]**|**nchar[\*]**|  
|**nchar[4001..\*]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**numeric[\*..\*]**|**numeric[\*]**|  
|**numeric[\*..\*][\*..\*]**|**numeric[\*][\*]**|  
|**nvarchar**|**nvarchar**|  
|**Nvarchar [\*... 4000]**|**nvarchar[\*]**|  
|**nvarchar[4001..\*]**|**nvarchar(max)**|  
|**real**|**float[24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar[128]**|  
|**sysname[\*..\*]**|**nvarchar[255]**|  
|**text**|**text**|  
|**Uhrzeit**|**time[3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**unichar**|**nchar**|  
|**UNICHAR-varying**|**nvarchar**|  
|**UNICHAR-varying [\*... 4000]**|**nvarchar[\*]**|  
|**unichar varying[4001..\*]**|**nvarchar(max)**|  
|**UNICHAR [\*... 4000]**|**nchar[\*]**|  
|**unichar[4001..\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar[\*..4000]**|**nvarchar[\*]**|  
|**univarchar[4001..\*]**|**nvarchar(max)**|  
|**unsigned bigint**|**numeric[20][0]**|  
|**Int ohne Vorzeichen**|**bigint**|  
|**ohne Vorzeichen "smallint"**|**int**|  
|**unsigned tinyint**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary[\*..8000]**|**varbinary[\*]**|  
|**varbinary[8001..\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**Varchar [\*... 8000]**|**varchar[\*]**|  
|**varchar[8001..\*]**|**varchar(max)**|  
  
