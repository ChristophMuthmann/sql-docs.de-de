---
title: "Paketkonfigurationsplaner | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.packageconfigurationorganizer.f1"
helpviewer_keywords: 
  - "Paketkonfigurationsplaner (Dialogfeld)"
ms.assetid: f20ae6cb-9e6a-4d24-88ff-d7a903a4e8d3
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# Paketkonfigurationsplaner
  Mithilfe des Dialogfelds **Paketkonfigurationsplaner** können Sie Paketkonfigurationen aktivieren, eine Liste der Konfigurationen für das aktuelle Paket anzeigen und die bevorzugte Reihenfolge angeben, in der die Konfigurationen geladen werden sollten.  
  
> **HINWEIS:** Konfigurationen sind für das Paketbereitstellungsmodell verfügbar. Parameter werden für das Projektbereitstellungsmodell anstelle von Konfigurationen verwendet. Mithilfe des Projektbereitstellungsmodells können Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekte auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitstellen. Weitere Informationen zu Bereitstellungsmodellen finden Sie unter [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).  
  
 Wenn mehrere Konfigurationen dieselbe Eigenschaft aktualisieren, ersetzen Werte aus Konfigurationen weiter unten in der Konfigurationsliste die Werte aus Konfigurationen weiter oben in der Liste. Der letzte in die Eigenschaft geladene Wert ist der Wert, der verwendet wird, wenn das Paket ausgeführt wird. Auch muss die indirekte Konfiguration, die auf den Speicherort der direkten Konfiguration verweist, weiter oben in der Liste stehen, wenn das Paket eine Kombination aus direkter Konfiguration, z. B. XML-Konfigurationsdatei, und indirekter Konfiguration, z. B. Umgebungsvariable, verwendet.  
  
> **HINWEIS:** Wenn Paketkonfigurationen in der bevorzugten Reihenfolge geladen werden, werden die Konfigurationen in der Reihenfolge geladen, in der sie im Dialogfeld **Paketkonfigurationsplaner** angezeigt werden, wobei mit der Konfiguration am Anfang der Liste begonnen wird. Zur Laufzeit werden Paketkonfigurationen möglicherweise aber nicht in der bevorzugten Reihenfolge geladen. Beispielsweise werden übergeordnete Paketkonfigurationen nach Konfigurationen anderer Typen geladen.  
  
 Paketkonfigurationen aktualisieren die Werte der Eigenschaften von Paketobjekten zur Laufzeit. Beim Laden eines Pakets werden die beim Entwickeln des Pakets festgelegten Werte durch die Werte der Konfigurationen ersetzt. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] unterstützt unterschiedliche Konfigurationstypen. Beispielsweise können Sie eine XML-Datei mit mehreren möglichen Konfigurationen oder eine Umgebungsvariable mit einer einzigen enthaltenen Konfiguration verwenden. Weitere Informationen finden Sie unter [Package Configurations](../../integration-services/packages/package-configurations.md).  
  
## enthalten  
 **Paketkonfigurationen aktivieren**  
 Wählen Sie diese Option aus, um mit dem Paket Konfigurationen zu verwenden.  
  
 **Konfigurationsname**  
 Zeigt den Namen der Konfiguration an.  
  
 **Konfigurationstyp**  
 Zeigt den Typ des Speicherorts von Konfigurationen an.  
  
 **Konfigurationszeichenfolge**  
 Zeigt den Speicherort der Konfigurationswerte an. Der Speicherort kann der Pfad einer Datei, der Name einer Umgebungsvariablen, der Name einer Variablen für das übergeordnete Paket, ein Registrierungsschlüssel oder der Name einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle sein.  
  
 **Zielobjekt**  
 Zeigt den Namen des Objekts an, das von der Konfiguration aktualisiert wird. Wenn es sich bei der Konfiguration um eine XML-Konfigurationsdatei oder eine SQL Server-Tabelle handelt, ist die Spalte leer, da die Konfiguration mehrere Objekte enthalten kann.  
  
 **Zieleigenschaft**  
 Zeigt den Namen der durch die Konfiguration geänderten Eigenschaft an. Diese Spalte ist leer, wenn der Konfigurationstyp mehrere Konfigurationen unterstützt.  
  
 **Hinzufügen**  
 Fügt mithilfe des Paketkonfigurationsassistenten eine Konfiguration hinzu.  
  
 **Bearbeiten**  
 Bearbeitet eine vorhandene Konfiguration, indem der Paketkonfigurationsassistent erneut ausgeführt wird.  
  
 **Entfernen**  
 Wählen Sie eine Konfiguration aus, und klicken Sie auf **Entfernen**.  
  
 **Pfeile**  
 Wählen Sie eine Konfiguration aus, und verschieben Sie sie mithilfe der Pfeile in der Liste nach oben oder nach unten. Konfigurationen werden in der Reihenfolge geladen, in der sie in der Liste angezeigt werden.  
  
## Siehe auch  
 [Erstellen von Paketkonfigurationen](../../integration-services/packages/create-package-configurations.md)  
  
  