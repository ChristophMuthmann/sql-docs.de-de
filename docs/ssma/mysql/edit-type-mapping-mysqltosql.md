---
title: Bearbeiten der Zuordnung (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
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
ms.assetid: 184f7ab2-725f-491e-a15b-b889f2fb6a68
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8a504400ffe402f3066404538f17d840c44cc04d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="edit-type-mapping-mysqltosql"></a>Bearbeiten der Zuordnung (MySQLToSQL)
Die **bearbeiten Type Mapping** Dialogfeld können Sie angeben, wie Datentypen zwischen Quelle und Ziel-Datenbankobjekten zugeordnet sind.  
  
Sie können dieses Dialogfeld an mehreren Stellen zuzugreifen:  
  
-   Bei der Auswahl einer Quelldatenbank oder ein Datenbankobjekt, das **Type Mapping** -Registerkarte wird rechts neben dem Metadaten-Explorer angezeigt. Klicken Sie auf **hinzufügen** fügen Sie eine neue Zuordnung hinzu, oder klicken Sie auf **bearbeiten** so ändern Sie eine vorhandene Zuordnung.  
  
-   Auf der **Tools** klicken Sie im Menü **Projekteinstellungen** oder **Projekt Standardeinstellungen**. Wählen Sie im daraufhin angezeigten Dialogfeld **Type Mapping**. Klicken Sie auf **hinzufügen** fügen Sie eine neue Zuordnung hinzu, oder klicken Sie auf **bearbeiten** so ändern Sie eine vorhandene Zuordnung.  
  
-   Tabelle-spezifische Zuordnungen datentypzuordnungen für Projekte und Datenbank zu überschreiben. Datenbank-spezifische Zuordnungen überschreiben Projekt Zuordnungen.  
  
## <a name="options"></a>enthalten  
  
##### <a name="source-type"></a>Quelltyp  
Wählen Sie den Quelltyp für die Daten in einen SQL Server-Datentyp zugeordnet.  
  
Wenn der Datentyp mit variabler Länge ist, erscheint die folgenden Felder unter **Sourcetype**:  
  
##### <a name="from"></a>Von  
Geben Sie die minimale Länge für diese Zuordnung. Z. B. für die **Nchar** -Datentyp, können Sie 10, um anzugeben, dass diese Zuordnung für einen Bereich beginnend ist eingeben **nchar(10).**  
  
##### <a name="to"></a>Aktion  
Geben Sie die maximale Länge für diese Zuordnung. Z. B. für die **Nchar** -Datentyp, können Sie 20, um anzugeben, dass diese Zuordnung für einen Bereich endet am eingeben **nchar(20).**  
  
##### <a name="target-type"></a>Zieltyp  
Wählen Sie den SQL Server-Datentyp, der der Quelltyp der Daten zugeordnet ist. Wenn SSMA die Tabelle erstellt oder in der SQL Server ändert sich der Quelldatentyp auf diesen Datentyp.  
  
Wenn der Datentyp mit variabler Länge ist, erscheint das folgende Feld unter **Zieltyp**:  
  
##### <a name="replace-with"></a>Ersetzen durch  
Geben Sie die Ziellänge für diese Zuordnung. Z. B. für die **Nvarchar** -Datentyp, können Sie 20, um anzugeben, dass die angegebene Quelle-Datentyp zugeordnet werden sollte eingeben **Nvarchar (20).**  
  
