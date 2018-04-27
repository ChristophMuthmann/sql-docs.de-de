---
title: Tabellenwertobjekt (Spalte)-Eigenschaften (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- vdt.designers.properties.QueryViewColumn
ms.assetid: 212d9bcd-aded-4313-a6b9-d7e2270e5954
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 76843a03de3223aa1f64ccb1ab012f4b9093a157
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="table-valued-object-column-properties-visual-database-tools"></a>Tabellenwertobjekt (Spalte) Eigenschaften (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Diese Eigenschaften erscheinen, wenn Sie im Abfrage- und Sicht-Designer im Bereich **Diagramm** eine Spalte in einem Tabellenwertobjekt auswählen.  
  
> [!NOTE]  
> Die in diesem Thema behandelten Eigenschaften sind nicht alphabetisch, sondern nach Kategorie angeordnet.  
  
> [!NOTE]  
> Die angezeigten Dialogfelder und Menübefehle können von den in der Hilfe beschriebenen abweichen. Dies hängt von Ihren aktiven Einstellungen oder Ihrer Edition ab. Um Ihre Einstellungen zu ändern, wählen Sie **Einstellungen importieren und exportieren** im Menü **Extras** aus.  
  
**Kategorie Identität**  
Wird erweitert, um die Eigenschaft **Name** anzuzeigen.  
  
**Name**  
Zeigt den Namen der ausgewählten Spalte an.  
  
**Abfrage-Designer – Kategorie**  
Wird erweitert und zeigt die Eigenschaften für **NULL-Werte zulassen**, **Sortierung**, **Datentyp**, **Länge**, **Genauigkeit**, **Dezimalstellen**und **Größe**an.  
  
**NULL-Werte zulassen**  
Zeigt an, ob der Datentyp der Spalte NULL-Werte zulässt.  
  
**Sortierung**  
Zeigt die Sortierungseinstellung der ausgewählten Spalte an. Die Sortierung kann auf der Registerkarte Spalteneigenschaften des Tabellen-Designers festgelegt werden.  
  
**Datentyp**  
Zeigt den Datentyp der ausgewählten Spalte an.  
  
**Länge**  
Zeigt die Anzahl der Zeichen oder Stellen an, die der Datentyp der ausgewählten Spalte zulässt. Diese Eigenschaft ist nur für zeichenbasierte Datentypen verfügbar.  
  
> [!NOTE]  
> Die Größe in Byte wird darunter in der Eigenschaft **Größe** angezeigt.  
  
**Genauigkeit**  
Zeigt die maximale Anzahl der für numerische Datentypen zulässigen Stellen. Bei nicht numerischen Datentypen wird diese Eigenschaft mit **0** angegeben.  
  
**Dezimalstellen**  
Zeigt die maximale Anzahl von Stellen an, die bei numerischen Datentypen rechts vom Dezimalkomma erscheinen können. Dieser Wert muss kleiner oder gleich der Genauigkeit sein. Bei nicht numerischen Datentypen wird diese Eigenschaft mit **0** angegeben.  
  
**Größe**  
Zeigt die für den Datentyp der Spalte zulässige Größe in Byte an. Beispiel: Ein nchar-Datentyp kann eine Länge von 10 besitzen (die Anzahl der Zeichen), wegen der Unicode-Zeichensätze aber eine Größe von 20 Byte besitzen.  
  
