---
title: Tabellen und Spalten (Dialogfeld) (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vdt.dlgbox.tablesandcolumns
ms.assetid: 8cf27be1-e66d-4735-a428-9ab4b33af4f5
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0be03d94210fc596bb0902ea130af731b1dadf92
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="tables-and-columns-dialog-box-visual-database-tools"></a>Tabellen und Spalten (Dialogfeld) (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] In diesem Dialogfeld können Sie einen Primärschlüssel in einer Tabelle einem Fremdschlüssel in einer anderen Tabelle zuordnen. Sie können dieses Dialogfeld aufrufen, indem Sie im Menü **Tabellen-Designer** auf **Beziehungen**klicken. Klicken Sie im Dialogfeld **Fremdschlüsselbeziehungen** auf **Tabellen- und Spaltenspezifikation** , und klicken Sie anschließend auf die Auslassungspunkte **(…)** , die rechts neben der Eigenschaft angezeigt werden.  
  
> [!NOTE]  
> Wenn die Tabelle zur Replikation veröffentlicht ist, müssen Sie mit der Transact-SQL-Anweisung [ALTER TABLE](http://msdn.microsoft.com/en-us/f1745145-182d-4301-a334-18f799d361d1) oder mit SMO (SQL Server Management Objects) Schemaänderungen ausführen. Wenn die Schemaänderungen mit dem Tabellen-Designer oder dem Datenbankdiagramm-Designer ausgeführt werden, wird versucht, die Tabelle zu entfernen und erneut zu erstellen. Da veröffentlichte Objekte nicht gelöscht werden können, schlägt die Schemaänderung fehl.  
  
## <a name="options"></a>Tastatur  
**Beziehungsname**  
Zeigt den Namen der Beziehung an.  
  
**Primärschlüsseltabelle**  
Listet die in der Datenbank enthaltenen Tabellen auf. Wählen Sie die Tabelle für die Primärschlüsselseite der Beziehung aus.  
  
**Fremdschlüsseltabelle**  
Zeigt die Tabelle an, die der Fremdschlüsselseite der Beziehung zugeordnet ist. Dabei handelt es sich um die aktuell im Tabellen-Designer ausgewählte Tabelle.  
  
**Datenblatt unter der Primärschlüsseltabelle**  
Listet die Spalten der in der Liste **Primärschlüsseltabelle** ausgewählten Tabelle auf. Geben Sie die Spalten ein, die für den Primärschlüssel dieser Tabelle verwendet werden sollen.  
  
**Datenblatt unter der Fremdschlüsseltabelle**  
Listet die Spalten der in der Liste **Fremdschlüsseltabelle** ausgewählten Tabelle auf. Geben Sie die Fremdschlüsselspalte der Fremdschlüsseltabelle ein, die der Primärschlüsselspalte entspricht.  
  
> [!NOTE]  
> Die Spalten, die Sie für den Fremdschlüssel auswählen, müssen denselben Datentyp wie die entsprechenden Primärspalten aufweisen. Die Anzahl der Spalten muss in den jeweiligen Schlüsseln gleich sein. Wenn beispielsweise der Primärschlüssel der Tabelle auf der Primärseite der Beziehung aus zwei Spalten besteht, müssen Sie für jede Spalte eine entsprechende Spalte in der Tabelle für die Fremdschlüsselseite der Beziehung auswählen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Vorgehensweise: Erstellen von Beziehungen zwischen Tabellen (Visual Database Tools)](http://msdn.microsoft.com/en-us/867a54b8-5be4-46e6-9702-49ae6dabf67c)  
  
