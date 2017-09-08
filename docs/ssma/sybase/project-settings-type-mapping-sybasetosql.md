---
title: Projekteinstellungen (Zuordnung) (SybaseToSQL) | Microsoft Docs
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
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 77c02b875a22fefec54c59518f4972cbd7aefd4b
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

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
|**Binary [\*..8000]**|**Binary [\*]**|  
|**Binary [8001..\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**Char varying**|**varchar**|  
|**Char varying [\*..8000]**|**Varchar [\*]**|  
|**Char varying [8001..\*]**|**varchar(max)**|  
|**char[\*..8000]**|**char[\*]**|  
|**Char [8001..\& #42;]**|**varchar(max)**|  
|**Zeichen**|**char**|  
|**unterschiedliche Zeichen**|**varchar**|  
|**unterschiedliche Zeichen [\*..8000]**|**Varchar [\*]**|  
|**unterschiedliche Zeichen [8001..\*]**|**varchar(max)**|  
|**Zeichen [\*..8000]**|**char[\*]**|  
|**Zeichen [8001..\*]**|**varchar(max)**|  
|**Datum**|**Datum**|  
|**datetime**|**datetime2 [3]**|  
|**DEC**|**decimal**|  
|**dec[\*..\*]**|**Dezimal [\*]**|  
|**dec[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**decimal**|**decimal**|  
|**Dezimal [\*..\*]**|**Dezimal [\*]**|  
|**Dezimal [\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**mit doppelter Genauigkeit**|**"float" [53]**|  
|**float**|**"float" [53]**|  
|**"float" [\*... 15]**|**"float" [24]**|  
|**"float" [16..\*]**|**"float" [53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**Nvarchar [255]**|  
|**money**|**money**|  
|**National char**|**nchar**|  
|**National Char [\*..4000]**|**NCHAR [\*]**|  
|**National Char varying**|**nvarchar**|  
|**National Char varying [\*..4000]**|**Nvarchar [\*]**|  
|**National Char varying [4001..\*]**|**nvarchar(max)**|  
|**National Char [4001..\*]**|**nvarchar(max)**|  
|**nationale Zeichensätze**|**nchar**|  
|**nationale Zeichensätze [\*..4000]**|**NCHAR [\*]**|  
|**nationale Zeichensätze [4001..\*]**|**nvarchar(max)**|  
|**nationale Zeichensätze varying**|**nvarchar**|  
|**nationale Zeichensätze varying [\*..4000]**|**Nvarchar [\*]**|  
|**nationale Zeichensätze varying [4001..\*]**|**nvarchar(max)**|  
|**National varchar**|**nvarchar**|  
|**National Varchar [\*..4000]**|**Nvarchar [\*]**|  
|**National Varchar [4001..\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**NCHAR varying**|**nvarchar**|  
|**NCHAR varying [\*..4000]**|**Nvarchar [\*]**|  
|**NCHAR varying [4001..\*]**|**nvarchar(max)**|  
|**NCHAR [\*..4000]**|**NCHAR [\*]**|  
|**NCHAR [4001..\*]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**numerische [\*..\*]**|**numerische [\*]**|  
|**numerische [\*..\*][\*..\*]**|**numeric[\*][\*]**|  
|**nvarchar**|**nvarchar**|  
|**Nvarchar [\*..4000]**|**Nvarchar [\*]**|  
|**Nvarchar [4001..\*]**|**nvarchar(max)**|  
|**real**|**"float" [24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**Nvarchar [128]**|  
|**Sysname [\*..\*]**|**Nvarchar [255]**|  
|**text**|**text**|  
|**Uhrzeit**|**Zeit [3]**|  
|**timestamp**|**RowVersion**|  
|**tinyint**|**tinyint**|  
|**UNICHAR**|**nchar**|  
|**UNICHAR-varying**|**nvarchar**|  
|**UNICHAR-varying [\*..4000]**|**Nvarchar [\*]**|  
|**UNICHAR-varying [4001..\*]**|**nvarchar(max)**|  
|**UNICHAR [\*..4000]**|**NCHAR [\*]**|  
|**UNICHAR [4001..\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**Univarchar [\*..4000]**|**Nvarchar [\*]**|  
|**Univarchar [4001..\*]**|**nvarchar(max)**|  
|**ohne Vorzeichen "bigint"**|**numerische [20] [0]**|  
|**Int ohne Vorzeichen**|**bigint**|  
|**ohne Vorzeichen "smallint"**|**int**|  
|**ohne Vorzeichen "tinyint"**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**Varbinary [\*..8000]**|**Varbinary [\*]**|  
|**Varbinary [8001..\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**Varchar [\*..8000]**|**Varchar [\*]**|  
|**Varchar [8001..\*]**|**varchar(max)**|  
  

