---
title: "Zugreifen auf benutzerdefinierte Assemblys über Ausdrücke | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- expressions [Reporting Services], custom assemblies
- static member calls
- instance member calls [Reporting Services]
- calling class members
- custom assemblies [Reporting Services], expressions
ms.assetid: 917c4d47-1a95-4f54-98b1-e8cb2165d90f
caps.latest.revision: 32
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 70ff488827e5289d401bf62b67a82a08ecc25f70
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="accessing-custom-assemblies-through-expressions"></a>Zugriff auf benutzerdefinierte Assemblys über Ausdrücke
  Sobald Sie eine benutzerdefinierte Assembly erstellt, diese im Berichts-Designer oder Berichtsserver zur Verfügung gestellt, die entsprechende Sicherheitsrichtlinie und in der Berichtsdefinition einen Verweis auf die benutzerdefinierte Assembly hinzugefügt haben, können Sie mit Berichtsausdrücken auf Klassenelemente in der Assembly zugreifen. Wenn Sie in einem Ausdruck auf benutzerdefinierten Code verweisen möchten, müssen Sie das Klassenelement in der Assembly aufrufen. Die Vorgehensweise hängt davon ab, ob es sich um eine statische oder um eine instanzbasierte Methode handelt.  
  
## <a name="calling-static-members-from-a-report-definition-file"></a>Aufruf statischer Elemente aus einer Berichtsdefinitionsdatei  
 Statische Elemente gehören zur Klasse oder zum Typ selbst und nicht zu einem instanziierten Objekt. Auf diese Elemente kann zugegriffen werden, indem sie direkt von der Klasse aus aufgerufen werden. Wenn möglich, sollten Sie statische Elemente verwenden, um benutzerdefinierte Funktionen in einem Bericht aufzurufen, da die Leistung von statischen Elementen am besten ist. Um ein statisches Element aufzurufen, müssen Sie es als Ausdruck verweisen, die der Form =*Namespace.Class.Method*.  
  
#### <a name="to-call-static-members"></a>So rufen Sie statische Elemente auf  
  
-   Um ein statisches Element aufzurufen, stellen Sie den Ausdruck auf den vollqualifizierten Namen des Elements ein, der Namespace, den Klassennamen und den Elementnamen umfasst. Im folgenden Beispiel wird die **ToGBP** -Methode, die konvertiert die **StandardCost** Feld-Felds von Dollar in Pfund Sterling und in einem Bericht angezeigt wird:  
  
    ```  
    =CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
    ```  
  
### <a name="important-information-regarding-static-fields-and-properties"></a>Wichtige Informationen für statische Felder und Eigenschaften  
 Derzeit werden alle Berichte in der gleichen Anwendungsdomäne ausgeführt. Das bedeutet, dass Berichte mit benutzerdefinierten, statischen Daten diese Daten in anderen Instanzen desselben Berichts zur Verfügung stellen. Dies kann dazu führen, dass die statischen Daten eines Benutzers allen Benutzern, die einen bestimmten Bericht ausführen, zur Verfügung gestellt werden. Aus diesem Grund wird dringend empfohlen, keine statische Felder oder Eigenschaften in benutzerdefinierten Assemblys oder im Verwenden der **Code** Element; stattdessen Instanzfelder bzw.-Eigenschaften in Ihren Berichten verwenden. Statische Methoden können trotzdem verwendet werden, da sie weder Status noch Daten speichern.  
  
## <a name="calling-instance-members-from-a-report-definition-file"></a>Aufruf von Instanzelementen aus einer Berichtsdefinitionsdatei  
 Wenn die benutzerdefinierte Assembly Instanzelemente enthält, auf die Sie in einer Berichtsdefinition zugreifen müssen, müssen Sie einen Instanznamen für die Klasse des Berichts hinzufügen. Sie können einen Instanznamen für eine Klasse mit Hinzufügen der **Code** auf der Registerkarte die **Berichtseigenschaften** Dialogfeld. Weitere Informationen zum Hinzufügen von Klasseninstanzen zu einem Bericht finden Sie unter [benutzerdefinierter Code und Assemblyverweise in Ausdrücken in Berichts-Designer &#40; SSRS &#41; ](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
 Um ein statisches Element aufzurufen, müssen Sie es als Ausdruck verweisen, die der Form = Code*. InstanceName.Method*.  
  
#### <a name="to-call-instance-members"></a>So rufen Sie Instanzelemente auf  
  
-   Um einen Instanzmember einer benutzerdefinierten Assembly aufzurufen, müssen Sie den Verweisen der **Code** Schlüsselwort, gefolgt von den Instanznamen und die Methode. Im folgenden Beispiel wird eine Instanzmethode **ToEUR** welche konvertiert die **StandardCost** Feldwert von Dollar in Euro und in einem Bericht angezeigt wird:  
  
    ```  
    =Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von benutzerdefinierten Assemblys mit Berichten](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
