---
title: "Langsam veränderliche Dimension Transformation | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.slowlychangingdimtrans.f1
helpviewer_keywords:
- Slowly Changing Dimension transformation
- slowly changing dimensions
- SCD transformation
- updating slowly changing dimensions
ms.assetid: f8849151-c171-4725-bd25-f2c33a40f4fe
caps.latest.revision: 55
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 59f467f9aee0637bc9463c39b51b30e47eeaff47
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="slowly-changing-dimension-transformation"></a>Transformation für langsam veränderliche Dimensionen
  Die Transformation für langsam veränderliche Dimensionen koordiniert das Aktualisieren und Einfügen von Datensätzen in Data Warehouse-Dimensionstabellen. Beispielsweise können Sie mit dieser Transformation die Transformationsausgaben konfigurieren, die Datensätze in der DimProduct-Tabelle der [!INCLUDE[ssSampleDBDWobject](../../../includes/sssampledbdwobject-md.md)] -Datenbank mit Daten aus der Production.Products-Tabelle in der AdventureWorks-OLTP-Datenbank aktualisieren und ersetzen.  
  
> [!IMPORTANT]  
>  Der Assistent für langsam veränderliche Dimensionen unterstützt nur Verbindungen mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Die Transformation für langsam veränderliche Dimensionen stellt die folgende Funktionalität zum Verwalten langsam veränderlicher Dimensionen bereit:  
  
-   Suchen übereinstimmender Zeilen in der Nachschlagetabelle für eingehende Zeilen, um neue und vorhandene Zeilen zu identifizieren.  
  
-   Identifizieren eingehender Zeilen, die Änderungen enthalten, obwohl keine Änderungen zulässig sind.  
  
-   Identifizieren von Datensätzen für abgeleitete Elemente, die aktualisiert werden müssen.  
  
-   Identifizieren eingehender Zeilen mit Verlaufsänderungen, die das Einfügen neuer Datensätze und das Aktualisieren abgelaufener Datensätze erfordern.  
  
-   Erkennen eingehender Zeilen mit Änderungen, die das Aktualisieren vorhandener Datensätze, einschließlich abgelaufener Datensätze, erfordern.  
  
 Die Transformation für langsam veränderliche Dimensionen unterstützt vier Änderungstypen: Veränderliches Attribut, Verlaufsattribut, Festes Attribut und Abgeleitetes Element.  
  
-   Veränderliches Attribut überschreibt vorhandene Datensätze. Diese Art von Änderung ist mit einer Änderung vom Typ 1 identisch. Die Transformation für langsam veränderliche Dimensionen leitet diese Zeilen an die Ausgabe **Ausgabe: Updates von veränderlichen Attributen**weiter.  
  
-   Verlaufsattribut erstellt neue Datensätze, statt vorhandene Datensätze zu aktualisieren. Als einzige Änderung in einem vorhandenen Datensatz ist das Update einer Spalte zulässig, die angibt, ob der Datensatz aktuell oder abgelaufen ist. Diese Art von Änderung ist mit einer Änderung vom Typ 2 identisch. Die Transformation für langsam veränderliche Dimensionen leitet diese Zeilen an zwei Ausgaben weiter: **Ausgabe der Einfügevorgänge im Verlaufsattribut** und **Neue Ausgabe**.  
  
-   Festes Attribut gibt an, dass der Spaltenwert nicht geändert werden darf. Die Transformation für langsam veränderliche Dimensionen erkennt Änderungen und kann die Zeilen mit Änderungen an die Ausgabe **Ausgabe des festen Attributs**weiterleiten.  
  
-   Abgeleitetes Element gibt an, dass es sich bei der Zeile um einen Datensatz für abgeleitete Elemente in der Dimensionstabelle handelt. Ein abgeleitetes Element ist vorhanden, wenn eine Faktentabelle auf ein Dimensionselement verweist, das noch nicht geladen ist. Ein minimaler Datensatz für abgeleitete Elemente wird unter Vorwegnahme von relevanten Dimensionsdaten erstellt, die nachfolgend beim Laden der Dimensionsdaten bereitgestellt werden. Die Transformation für langsam veränderliche Dimensionen leitet diese Zeilen an die Ausgabe **Ausgabe der Updates abgeleiteter Elemente**weiter. Wenn für das abgeleitete Element Daten geladen sind, können Sie den vorhandenen Datensatz aktualisieren, aber keinen neuen erstellen.  
  
> [!NOTE]  
>  Die Transformation für langsam veränderliche Dimensionen unterstützt keine Änderungen vom Typ 3, für die Änderungen an der Dimensionstabelle erforderlich sind. Durch das Identifizieren von Spalten mit dem Updatetyp Festes Attribut können Sie die Datenwerte aufzeichnen, die für Änderungen vom Typ 3 in Frage kommen.  
  
 Zur Laufzeit versucht die Transformation für langsam veränderliche Dimensionen zuerst, für die eingehende Zeile einen übereinstimmenden Datensatz in der Nachschlagetabelle zu finden. Falls keine Übereinstimmung gefunden wird, ist die eingehende Zeile ein neuer Datensatz. Deshalb führt die Transformation für langsam veränderliche Dimensionen keine zusätzlichen Schritte aus und leitet die Zeile an **Neue Ausgabe**weiter.  
  
 Falls eine Übereinstimmung gefunden wird, erkennt die Transformation für langsam veränderliche Dimensionen, ob die Zeile Änderungen enthält. Falls die Zeile Änderungen enthält, identifiziert die Transformation für langsam veränderliche Dimensionen den Updatetyp für jede Spalte und leitet die Zeile an **Ausgabe: Updates von veränderlichen Attributen**, **Ausgabe des festen Attributs**, **Ausgabe der Einfügevorgänge im Verlaufsattribut**oder **Ausgabe der Updates abgeleiteter Elemente**weiter. Wenn die Zeile unverändert ist, leitet die Transformation für langsam veränderliche Dimensionen die Zeile an **Nicht geänderte Ausgabe**weiter.  
  
## <a name="slowly-changing-dimension-transformation-outputs"></a>Ausgaben der Transformation für langsam veränderliche Dimensionen  
 Die Transformation für langsam veränderliche Dimensionen weist eine Eingabe und bis zu sechs Ausgaben auf. Eine Ausgabe leitet eine Zeile an die Teilmenge des Datenflusses weiter, der den Update- und Einfügeanforderungen der Zeile entspricht. Eine Fehlerausgabe wird von dieser Transformation nicht unterstützt.  
  
 In der folgenden Tabelle werden die Transformationsausgaben und die Anforderungen der nachfolgenden Datenflüsse beschrieben. Für die Anforderungen wird der Datenfluss beschrieben, den der Assistent für langsam veränderliche Dimensionen erstellt.  
  
|Ausgabe|Description|Datenflussanforderungen|  
|------------|-----------------|----------------------------|  
|**Ausgabe: Updates von veränderlichen Attributen**|Der Datensatz in der Nachschlagetabelle wird aktualisiert. Diese Ausgabe wird für veränderliche Attributzeilen verwendet.|Eine Transformation für OLE DB-Befehl aktualisiert den Datensatz mithilfe einer UPDATE-Anweisung.|  
|**Ausgabe des festen Attributs**|Die Werte in Zeilen, die nicht geändert werden dürfen, stimmen nicht mit Werten in der Nachschlagetabelle überein. Diese Ausgabe wird für feste Attributzeilen verwendet.|Es wird kein Standarddatenfluss erstellt. Falls für die Transformation konfiguriert ist, dass sie fortgesetzt wird, wenn Änderungen an Spalten fester Attribute gefunden werden, sollten Sie einen Datenfluss zum Aufzeichnen dieser Zeilen erstellen.|  
|**Ausgabe der Einfügevorgänge im Verlaufsattribut**|Die Nachschlagetabelle enthält mindestens eine übereinstimmende Zeile. Die als "aktuell" markierte Zeile muss jetzt als "abgelaufen" markiert werden. Diese Ausgabe wird für Verlaufsattributzeilen verwendet.|Transformationen für abgeleitete Spalten erstellen Spalten für die Indikatoren abgelaufener Zeilen und aktueller Zeilen. Eine OLE DB-Befehlstransformation aktualisiert den Datensatz, der jetzt als "abgelaufen" markiert werden muss. Die Zeile mit den neuen Spaltenwerten wird an die neue Ausgabe geleitet, wo die Zeile eingefügt und als "aktuell" markiert wird.|  
|**Ausgabe der Updates abgeleiteter Elemente**|Zeilen für abgeleitete Dimensionselemente werden eingefügt. Diese Ausgabe wird für abgeleitete Elementzeilen verwendet.|Eine Transformation für OLE DB-Befehl aktualisiert den Datensatz mithilfe einer UPDATE-Anweisung von SQL.|  
|**Neue Ausgabe**|Die Nachschlagetabelle enthält keine übereinstimmenden Zeilen. Die Zeile wird der Dimensionstabelle hinzugefügt. Diese Ausgabe wird für neue Zeilen und Änderungen an Verlaufsattributzeilen verwendet.|Eine Transformation für abgeleitete Spalten legt den Indikator für die aktuelle Zeile fest, und ein OLE DB-Ziel fügt die Zeile ein.|  
|**Nicht geänderte Ausgabe**|Die Werte in der Nachschlagetabelle stimmen mit den Zeilenwerten überein. Diese Ausgabe wird für nicht geänderte Zeilen verwendet.|Es wird kein Standarddatenfluss erstellt, weil die Transformation für langsam veränderliche Dimensionen keine Schritte ausführt. Wenn Sie diese Zeilen aufzeichnen möchten, sollten Sie einen Datenfluss für diese Ausgabe erstellen.|  
  
## <a name="business-keys"></a>Geschäftsschlüssel  
 Für die Transformation für langsam veränderliche Dimensionen ist mindestens eine Geschäftsschlüsselspalte erforderlich.  
  
 Die Transformation für langsam veränderliche Dimensionen unterstützt keine Geschäftsschlüssel mit einem NULL-Wert. Falls die Daten Zeilen einschließen, in denen die Geschäftsschlüsselspalte gleich NULL ist, sollten diese Zeilen aus dem Datenfluss entfernt werden. Mit der Transformation für bedingtes Teilen können Sie Zeilen filtern, deren Geschäftsschlüsselspalten NULL-Werte enthalten. Weitere Informationen finden Sie unter [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md).  
  
## <a name="optimizing-the-performance-of-the-slowly-changing-dimension-transformation"></a>Optimieren der Leistung der Transformation für langsam veränderliche Dimensionen  
 Vorschläge zum Optimieren der Leistung der Transformation für langsam veränderliche Dimensionen finden Sie unter [Funktionen für die Datenflussleistung](../../../integration-services/data-flow/data-flow-performance-features.md).  
  
## <a name="troubleshooting-the-slowly-changing-dimension-transformation"></a>Problembehandlung der Transformation für langsam veränderliche Dimensionen  
 Sie können die von der Transformation für langsam veränderliche Dimensionen an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktionen können Sie Probleme bei Verbindungen mit externen Datenquellen, bei Befehlen an externe Datenquellen sowie bei an externe Datenquellen gerichteten Abfragen durch die Transformation für langsam veränderliche Dimensionen behandeln. Aktivieren Sie zum Protokollieren der von der Transformation für langsam veränderliche Dimensionen an externe Datenanbieter gerichteten Aufrufe die Paketprotokollierung, und wählen Sie das **Diagnostic** -Ereignis auf Paketebene aus. Weitere Informationen finden Sie unter [Behandeln von Problemen mit Paketausführungstools](../../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-slowly-changing-dimension-transformation"></a>Konfigurieren der Transformation für langsam veränderliche Dimensionen  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="configuring-the-slowly-changing-dimension-transformation-outputs"></a>Konfigurieren der Ausgaben der Transformation für langsam veränderliche Dimensionen  
 Das Koordinieren der Updates und der Einfügungen von Datensätzen in Dimensionstabellen kann eine komplexe Aufgabe sein, insbesondere wenn Änderungen vom Typ 1 und Typ 2 verwendet werden. [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer stellt zwei Möglichkeiten bereit, um die Unterstützung langsam veränderlicher Dimensionen zu konfigurieren:  
  
-   Das Dialogfeld **Erweiterter Editor** , in dem Sie eine Verbindung auswählen, allgemeine und benutzerdefinierte Komponenteneigenschaften festlegen, Eingabespalten auswählen und Spalteneigenschaften für die sechs Ausgaben festlegen. Um die Konfiguration der Unterstützung für eine langsam veränderliche Dimension abzuschließen, müssen Sie manuell den Datenfluss für die Ausgaben erstellen, die die Transformation für langsam veränderliche Dimensionen verwendet. Weitere Informationen finden Sie unter [Data Flow](../../../integration-services/data-flow/data-flow.md).  
  
-   Der Assistent zum Laden einer Dimension, der Sie durch die Schritte zum Konfigurieren der Transformation für langsam veränderliche Dimensionen und zum Erstellen des Datenflusses für Transformationsausgaben führt. Führen Sie den Assistenten zum Laden einer Dimension erneut aus, um die Konfiguration für langsam veränderliche Dimensionen zu ändern. Weitere Informationen finden Sie unter [Konfiguration von Ausgaben mithilfe des Assistenten für langsam veränderliche Dimensionen](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md).  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   Blogeintrag, [Optimizing the Slowly Changing Dimension Wizard](http://go.microsoft.com/fwlink/?LinkId=199481)(Optimieren des Assistenten für langsam veränderliche Dimensionen), auf blogs.msdn.com.  
  
  

