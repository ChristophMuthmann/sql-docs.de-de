---
title: Projekteinstellungen (Zuordnung) (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
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
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
caps.latest.revision: 16
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f1fbca03968ed7257cd7b65a42a6fff5180dbedc
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-type-mapping-accesstosql"></a>Projekteinstellungen (Zuordnung) (AccessToSQL)
Die projekteinstellungen Type Mapping können Sie die standardtypmappings für das SSMA-Projekt festgelegt. Sie können auch Zuordnungen für einzelne Datenbankobjekte angeben. Weitere Informationen finden Sie unter [Zuordnen von Quelle und Ziel-Datentypen](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9).  
  
Typzuordnung finden Sie in der **Projekteinstellungen** und **Projekt Standardeinstellungen** Dialogfelder:  
  
-   Verwenden der **Projekteinstellungen** (Dialogfeld), Konfigurationsoptionen für das aktuelle Projekt festzulegen. Einstellungen für die Zuordnung, für den Zugriff auf die **Tools** klicken Sie im Menü **Projekteinstellungen**, und klicken Sie dann auf **Typzuordnung** im linken Bereich.  
  
-   Verwenden der **Projekt Standardeinstellungen** (Dialogfeld), Konfigurationsoptionen für alle Projekte festzulegen. Zum Zugriff auf die Einstellungen für die Zuordnung, in der **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**, wählen Sie die Migration-Projekttyp, die für die Einstellungen angezeigt oder geändert werden, erforderlich sind **Migration-Zielversion** Dropdown-Liste, und klicken Sie dann auf **Typzuordnung** im linken Bereich.  
  
## <a name="options"></a>enthalten  
**Quelltyp**  
Der Access-Datentyp zugeordnet werden soll.  
  
**Zieltyp**  
Das Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datentyp für den angegebenen Access-Datentyp.  
  
Die folgende Tabelle zeigt die Zuordnung zwischen Quelle und Ziel-Datentypen.  
  
|Access-Datentyp|SQL Server-Datentyp|  
|--------------------|------------------------|  
|**Binary [\*... \*]**|**Varbinary [\*]**|  
|**boolean**|**bit**|  
|**Byte**|**tinyint**|  
|**Währung**|**money**|  
|**Datum**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**GUID**|**uniqueidentifier**|  
|**integer**|**smallint**|  
|**lange**|**int**|  
|**LONGBINARY**|**varbinary(max)**|  
|**Memo**|**nvarchar(max)**|  
|**Memo** – Access 97|**varchar(max)**|  
|**einzelne**|**real**|  
|**text[\*..\*]**|**Nvarchar [\*]**|  
|**text[\*.. \*]** – für Access 97|**Varchar [\*]**|  
  
**Hinzufügen**  
Klicken Sie auf diese Option, um einen Datentyp der Zuordnungsliste hinzuzufügen.  
  
**Bearbeiten**  
Klicken Sie auf diese Option, um einen Datentyp in der Zuordnungsliste zu bearbeiten.  
  
**Entfernen**  
Klicken Sie auf diese Option, um die ausgewählte Zuordnung aus der Zuordnungsliste zu entfernen.  
  
**Standard wiederherstellen**  
Klicken Sie auf diese Option, um alle datentypzuordnungen auf die SSMA-Standardwerte zurückzusetzen.  
  
## <a name="see-also"></a>Siehe auch  
[Zuordnen von Quell- und Ziel-Datentypen](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)  
[Benutzer-Schnittstelle Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  

