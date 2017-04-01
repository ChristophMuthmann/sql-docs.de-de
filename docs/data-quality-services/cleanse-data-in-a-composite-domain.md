---
title: "Bereinigen von Daten in einer Verbunddom&#228;ne | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7d1076e0-7710-469a-9107-e293e4bd80ac
caps.latest.revision: 14
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 14
---
# Bereinigen von Daten in einer Verbunddom&#228;ne
  Dieses Thema enthält Informationen zur Bereinigung von Verbunddomänen in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Eine Verbunddomäne besteht aus einer oder mehreren Einzeldomänen und ist einem Datenfeld zugeordnet, das sich aus mehreren verwandten Begriffen zusammensetzt. Die einzelnen Domänen in einer Verbunddomäne müssen einen gemeinsamen Wissensbereich haben. Ausführliche Informationen zu Verbunddomänen finden Sie unter [Managing a Composite Domain](../data-quality-services/managing-a-composite-domain.md).  
  
##  <a name="Mapping"></a> Zuordnen einer Verbunddomäne zu den Quelldaten  
 Es gibt zwei Methoden, mit denen Sie die Quelldaten einer Verbunddomäne zuordnen können:  
  
-   Bei den Quelldaten handelt es sich um ein einzelnes Feld (beispielsweise „Vollständiger Name“), das einer Verbunddomäne zugeordnet wird.  
  
    -   Wenn die Verbunddomäne einem Verweisdatendienst zugeordnet wird, werden die Quelldaten zur Korrektur und Analyse unverändert an den Verweisdatendienst gesendet.  
  
    -   Wenn die Verbunddomäne keinem Verweisdatendienst zugeordnet wird, werden die Quelldaten basierend auf der für die Verbunddomäne definierten Methode analysiert. Weitere Informationen zum Angeben einer Analysemethode für Verbunddomänen finden Sie unter [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md)  
  
-   Die Quelldaten bestehen aus mehreren Feldern (z. B. „Vorname“, „Weitere Vornamen“ und „Nachname“), die einzelnen Domänen innerhalb einer Verbunddomäne zugeordnet werden.  
  
 Ein Beispiel zum Zuordnen von verbunddomänen zu Quelldaten, finden Sie unter [Domäne anfügen oder Verbunddomäne an Verweisdaten](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
##  <a name="CDCorrection"></a> Datenkorrektur mit definitiven domänenübergreifenden Regeln  
 Domänenübergreifende Regeln in Verbunddomänen ermöglichen es Ihnen, Regeln zu erstellen, die die Beziehung zwischen einzelnen Domänen in einer Verbunddomäne angeben. Domänenübergreifende Regeln werden berücksichtigt, wenn Sie die Bereinigungsaktivität für die Quelldaten von Verbunddomänen ausführen. Außer dass Sie erfahren, ob eine domänenübergreifende Regel, die endgültige *dann* domänenübergreifende Regel **Wert ist gleich**, auch die Daten während der datenbereinigungsaktivität korrigiert.  
  
 Beachten Sie das folgende Beispiel: Es gibt eine Verbunddomäne namens „Product“ mit drei einzelnen Domänen: ProductName, CompanyName und ProductVersion. Erstellen Sie die folgende definitive domänenübergreifende Regel:  
  
 IF Domain ‘CompanyName’ Value contains *Microsoft* and Domain ‘ProductName’ Value is equal to *Office* and ‘ProductVersion’ Value is equal to *2010* THEN Domain ‘ProductName’ Value is equal to *Microsoft Office 2010*.  
  
 Wenn diese domänenübergreifende Regel ausgeführt wird, werden die Quelldaten (ProductName) nach der Bereinigungsaktivität wie folgt korrigiert:  
  
 **Quelldaten**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Office|Microsoft Inc.|2010|  
  
 **Ausgabedaten**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Microsoft Office 2010|Microsoft Inc.|2010|  
  
 Beim Testen der endgültige *dann* domänenübergreifende Regel **Wert ist gleich**,  **Verbunddomänenregel testen** Dialogfeld enthält eine neue Spalte, **korrigieren in**, in dem die richtigen Daten angezeigt. In einem Data Quality-Projekte, ändert diese definitive domänenübergreifende Regel die Daten mit 100 % Zuverlässigkeit und die **Grund** Spalte wird die folgende Meldung angezeigt: korrigiert von Regel '*\< domänenübergreifende Regelname >*'. Weitere Informationen zu domänenübergreifenden Regeln finden Sie unter [Erstellen Sie eine domänenübergreifende Regel](../data-quality-services/create-a-cross-domain-rule.md).  
  
> [!NOTE]  
>  Die definitive domänenübergreifende Regel funktioniert nicht für Verbunddomänen, die an einen Verweisdatendienst angefügt wurden.  
  
##  <a name="DataProfiling"></a> Datenprofilerstellung für Verbunddomänen  
 DQS-profilerstellung stellt zwei Data Quality-Dimensionen: *Vollständigkeit* (das Ausmaß, zu dem Daten vorhanden sind) und *Genauigkeit* (das Ausmaß, in dem Daten für den beabsichtigten Zweck verwendet werden können) während der bereinigungsaktivität. Die Profilerstellung kann keine zuverlässigen Vollständigkeitsstatistiken für Verbunddomänen bereitstellen. Wenn Sie Vollständigkeitsstatistiken benötigen, verwenden Sie Einzeldomänen anstatt Verbunddomänen. Wenn Sie Verbunddomänen verwenden möchten, sollten Sie eine Wissensdatenbank mit Einzeldomänen für die Profilerstellung erstellen, um die Vollständigkeit zu bestimmen, und eine weitere Domäne mit einer Verbunddomäne für die Bereinigungsaktivität erstellen. Die Profilerstellung kann z. B. 95 % Vollständigkeit für Adressendatensätze anzeigen, die eine Verbunddomäne verwenden, aber es kann einen viel höheren Grad der Unvollständigkeit für eine der Spalten geben, z. B. für eine Postleitzahlspalte. In diesem Beispiel möchten Sie die Vollständigkeit der Postleitzahlspalte mit einer Einzeldomäne messen.  
  
 Die Profilerstellung stellt wahrscheinlich zuverlässige Genauigkeitsstatistiken für Verbunddomänen bereit, da Sie die Genauigkeit für mehrere Spalten gemeinsam messen können. Der Wert dieser Daten liegt in der zusammengesetzten Aggregation, daher sollten Sie die Genauigkeit mit einer Verbunddomäne messen.  
  
 Ausführliche Informationen zur datenprofilerstellung während der bereinigungsaktivität finden Sie unter [Profiler-Statistik](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Profiler) in [Bereinigen von Daten mithilfe von DQS & #40; intern & #41; Knowledge](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
  