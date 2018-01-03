---
title: Bearbeiten der Zuordnung (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7078b4ed-c779-4bf3-8db8-f9dcb3edd50f
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: b737d23608fa538019d55cc4825a29001238ee1e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="edit-type-mapping-oracletosql"></a>Bearbeiten der Zuordnung (OracleToSQL)
Die **bearbeiten Type Mapping** Dialogfeld können Sie angeben, wie Datentypen zwischen Quelle und Ziel-Datenbankobjekten zugeordnet sind.  
  
Sie können dieses Dialogfeld an mehreren Stellen zuzugreifen:  
  
-   Bei der Auswahl einer Quelldatenbank oder ein Datenbankobjekt, das **Type Mapping** -Registerkarte wird rechts neben dem Metadaten-Explorer angezeigt. Klicken Sie auf **hinzufügen** fügen Sie eine neue Zuordnung hinzu, oder klicken Sie auf **bearbeiten** so ändern Sie eine vorhandene Zuordnung.  
  
-   Auf der **Tools** klicken Sie im Menü **Projekteinstellungen** oder **Projekt Standardeinstellungen**. Wählen Sie im daraufhin angezeigten Dialogfeld **Type Mapping**. Klicken Sie auf **hinzufügen** fügen Sie eine neue Zuordnung hinzu, oder klicken Sie auf **bearbeiten** so ändern Sie eine vorhandene Zuordnung.  
  
Tabelle-spezifische Zuordnungen datentypzuordnungen für Projekte und Datenbank zu überschreiben. Datenbank-spezifische Zuordnungen überschreiben Projekt Zuordnungen.  
  
## <a name="options"></a>Tastatur  
**Quelltyp**  
Wählen Sie den Quelltyp für die Daten zum Zuweisen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentyp.  
  
Wenn der Datentyp mit variabler Länge ist, erscheint die folgenden Felder unter **Datenquellentyp**:  
  
**From**  
Geben Sie die minimale Länge für diese Zuordnung. Z. B. für die **Nchar** -Datentyp, können Sie 10, um anzugeben, dass diese Zuordnung für einen Bereich beginnend ist eingeben **nchar(10)**.  
  
**Aktion**  
Geben Sie die maximale Länge für diese Zuordnung. Z. B. für die **Nchar** -Datentyp, können Sie 20, um anzugeben, dass diese Zuordnung für einen Bereich endet am eingeben **nchar(20)**.  
  
**Zieltyp**  
Wählen Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentyp, dem der Quelldatentyp zugeordnet ist. Wenn SSMA erstellt, die Tabelle oder eine gespeicherte Prozedur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], ändert sich der Quelldatentyp auf diesen Datentyp.  
  
Wenn der Datentyp mit variabler Länge ist, erscheint das folgende Feld unter **Zieltyp**:  
  
**Replace with**  
Geben Sie die Ziellänge für diese Zuordnung. Z. B. für die **Nvarchar** -Datentyp, können Sie 20, um anzugeben, dass die angegebene Quelle-Datentyp zugeordnet werden sollte eingeben **nvarchar(20)**.  
  
