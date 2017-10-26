---
title: SQLTables (Text-Datei-Treiber) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], SQLTables
- SQLTables function [ODBC], Text File Driver
ms.assetid: f47fd1a4-5bd8-4b2e-8ae3-e595e49f4f95
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 56fa0c8ea21d4cfb620acfb633b3a4297ccd27fd
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqltables-text-file-driver"></a>SQLTables (Text-Datei-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Textdatei treiberspezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argument|Kommentare|  
|--------------|--------------|  
|*szTableOwner*|Der einzige gültige Argument für *SzTableOwner* NULL ist, da keines der Treiber Besitzernamens unterstützt. Mit *SzTableOwner* auf NULL festgelegt, werden alle Tabellen zurückgegeben. In der Spalte TABLE_OWNER wird NULL zurückgegeben.|  
|*szTableQualifier*|In der Spalte TABLE_QUALIFIER **SQLTables** gibt den Pfad zu einem Verzeichnis zurück.|  
|*SzTableType*|"TABLE" ist der einzige Tabelle unterstützt.<br /><br /> Wenn der Text-Treiber verwendet wird, die Liste der Dateien, die zurückgegebene **SQLTables** richtet sich nach der Dateierweiterungen, die in der **Erweiterungsliste** im Feld der **ODBC Text-Setup** (Dialogfeld).|

