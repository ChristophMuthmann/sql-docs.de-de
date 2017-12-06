---
title: Problembehandlung bei der Verarbeitung von Reporting Services-Berichten | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: troubleshooting
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bb309231-68be-4d68-a44c-c098999c67a2
caps.latest.revision: "4"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b379a4a9cb342c96e23be750ff4c8c1df08a6dff
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="troubleshoot-processing-of-reporting-services-reports"></a>Problembehandlung bei der Verarbeitung von Reporting Services-Berichten
Nachdem die Berichtsdaten abgerufen wurden, kombiniert der Berichtsprozessor die Daten mit den Layoutinformationen. Jede Berichtselementeigenschaft, die über einen Ausdruck verfügt, wird im Kontext der mit dem Layout kombinierten Daten ausgewertet. Dieses Thema soll Ihnen beim Behandeln der folgenden Probleme helfen.   
  
## <a name="my-report-definition-is-not-valid"></a>Meine Berichtsdefinition ist ungültig.  
Zur Laufzeit kombiniert der Berichtsprozessor Daten- und Layoutelemente in der Berichtsdefinition und wertet Ausdrücke für Berichtselementeigenschaften aus.   
  
Der Berichtsprozessor überprüft, ob die Berichtsdefinition (RDL-Datei) mit dem Schema übereinstimmt, das in der Namespacedeklaration am Anfang der RDL-Datei angegeben wird. Weitere Informationen zu RDL-Schemas finden Sie unter [Suchen der Berichtsdefinitions-Schemaversion (SSRS)](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  
  
Zudem müssen die Berichtsausdrücke, die zur Laufzeit ausgewertet werden, mit einer Reihe von Regeln übereinstimmen, die sicherstellen, dass die Daten und das Layout des Berichts ordnungsgemäß kombiniert werden können. Wenn der Berichtsprozessor ein Problem feststellt, wird eventuell die folgende Meldung angezeigt: Die Definition des Berichts `<report name>` ist ungültig.  
  
### <a name="report-item-expressions-can-only-refer-to-fields-within-the-current-dataset-scope-or-if-inside-an-aggregate-the-specified-dataset-scope"></a>Ein Ausdruck für ein Berichtselement kann nur auf Felder verweisen, die sich im aktuellen Datasetbereich oder, wenn der Ausdruck zu einer Aggregatfunktion gehört, im angegebenen Datasetbereich befinden.  
  
Bestimmen Sie die Ursache des Fehlers mithilfe der folgenden Liste:  
* Wenn ein Bericht mehrere Datasets aufweist, muss ein Aggregatausdruck in einem Textfeld des Berichtshauptteils einen Bereichsparameter angeben. Beispiel: `=First(Fields!FieldName.Value, "DataSet1")`.  
  
Um einen Bereichsparameter anzugeben, stellen Sie den Namen eines Datasets, eines Datenbereichs oder einer Gruppe bereit, die im Bereich für das Berichtselement liegt. Weitere Informationen finden Sie unter [Grundlegendes zum Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Auflistungen (Berichts-Generator 3.0 und SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) und [Ausdrucksverweis (Berichts-Generator 3.0 und SSRS)](../../reporting-services/report-design/expression-reference-report-builder-and-ssrs.md).  
  
### <a name="names-of-objects-must-be-greater-than-0-and-less-than-or-equal-to-256-characters"></a>Namen von Objekten müssen länger als 0 Zeichen sein und dürfen höchstens 256 Zeichen lang sein.  
Die Länge der Objektbezeichner in einer Berichtsdefinition ist auf 256 Zeichen beschränkt. Bei Bezeichnern muss die Groß- und Kleinschreibung beachtet werden, und Bezeichner müssen CLS-kompatibel sein. Namen müssen mit einem Buchstaben beginnen und Buchstaben, Zahlen oder einen Unterstrich (_) enthalten. Sie dürfen keine Leerzeichen enthalten. Beispielsweise müssen Textfeldnamen und Datenbereichsnamen diesen Richtlinien entsprechen.   
  
Um den Namen eines Objekts zu ändern, wählen Sie auf der Symbolleiste des Bereichs Eigenschaften das Element in der Dropdownliste aus, führen Sie einen Bildlauf zu **Name** aus, und geben Sie einen gültigen Objektnamen ein.   
  
## <a name="a-text-box-displays-error-how-do-i-fix-it"></a>In einem Textfeld wird "#Error" angezeigt. Wie behebe ich das Problem?  
Die Meldung "#Error" tritt auf, wenn der Berichtsprozessor zur Laufzeit Ausdrücke in Berichtselementeigenschaften auswertet und einen Datentypkonvertierungsfehler, Bereichsfehler oder anderen Fehler feststellt.   
  
Ein Datentypfehler tritt normalerweise auf, wenn der Standarddatentyp oder der angegebene Datentyp nicht unterstützt wird. Ein Bereichsfehler tritt auf, wenn der angegebene Bereich zu dem Zeitpunkt, zu dem der Ausdruck ausgewertet wurde, nicht verfügbar war.   
  
Um die Meldung "#Error" zu vermeiden, müssen Sie den Ausdruck neu schreiben, durch den sie verursacht wurde. Um weitere Informationen über das Problem zu erhalten, zeigen Sie die ausführliche Fehlermeldung an.   
  
Zeigen Sie in der Vorschau in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull.md)]das Ausgabefenster an. Zeigen Sie auf dem Berichtsserver die Aufrufliste an. 
  
  
## <a name="see-also"></a>Siehe auch  
[Fehler und Ereignisse (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)
[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]

