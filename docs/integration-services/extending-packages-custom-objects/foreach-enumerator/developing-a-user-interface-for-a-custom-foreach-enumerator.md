---
title: "Entwickeln einer Benutzeroberfläche für einen benutzerdefinierten foreach-Enumerator | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom user interface [Integration Services], custom foreach enumerators
- custom foreach enumerators [Integration Services], developing custom user interface
ms.assetid: 8aa4aa80-c9ba-42b3-ba87-ae5ea5d3cac3
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e743464fcf482ea51f0cde78d692b367c2be525b
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="developing-a-user-interface-for-a-custom-foreach-enumerator"></a>Entwickeln einer Benutzeroberfläche für einen benutzerdefinierten ForEach-Enumerator
  Nachdem Sie die Implementierung der Eigenschaften und Methoden der Basisklasse überschrieben haben, um benutzerdefinierte Funktionen bereitzustellen, möchten Sie vielleicht eine benutzerdefinierte Benutzeroberfläche für den Foreach-Enumerator erstellen. Wenn Sie keine individuelle Benutzeroberfläche erstellen, können die Benutzer den neuen benutzerdefinierten ForEach-Enumerator nur über das Eigenschaftenfenster konfigurieren.  
  
 Erstellen Sie in einem benutzerdefinierten Benutzeroberflächenprojekt oder einer entsprechenden Assembly eine Klasse, die den <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI> implementiert. Diese Klasse leitet sich von System.Windows.Forms.UserControl, in der Regel dient zum Erstellen eines zusammengesetzten Steuerelements, um andere Windows Forms-Steuerelemente zu hosten. Die von Ihnen erstellte Steuerelement wird angezeigt, der **enumeratorkonfiguration** Clientbereich der **Auflistung** auf der Registerkarte die **foreach-Schleifen-Editor**.  
  
> [!IMPORTANT]  
>  Nach dem Signieren und Erstellen der benutzerdefinierten Oberfläche und im globalen Assemblycache zu installieren, wie in beschrieben [erstellen, bereitstellen und Debuggen von benutzerdefinierten Objekten](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md), denken Sie daran, geben Sie den vollqualifizierten Namen dieser Klasse in der <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A> Eigenschaft von der <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>.  
  
## <a name="coding-the-user-interface-control-class"></a>Codieren der Benutzeroberflächen-Steuerelementklasse  
  
### <a name="initializing-the-user-interface"></a>Initialisieren der Benutzeroberfläche  
 Sie überschreiben die <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.Initialize%2A>-Methode, um Verweise auf das Hostobjekt sowie die im Paket definierten Auflistungen von Verbindungs-Managern und Variablen zwischenzuspeichern.  
  
### <a name="setting-properties-on-the-user-interface-control"></a>Festlegen von Eigenschaften für das Benutzeroberflächensteuerelement  
 UserControl-Klasse, von der die Benutzeroberflächenklasse abgeleitet wird, dient zur Verwendung als zusammengesetztes Steuerelement zum Hosten von anderen Windows Forms-Steuerelemente. Da diese Klasse als Host für andere Steuerelemente dient, können Sie Ihre benutzerdefinierte Oberfläche durch Ziehen und Ablegen von Steuerelementen entwerfen. Sie können diese wie bei jeder Windows Forms-Anwendung anordnen, ihre Eigenschaften festlegen und zur Ausführungszeit auf ihre Ereignisse reagieren.  
  
### <a name="saving-settings"></a>Speichern von Einstellungen  
 Sie überschreiben die <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.SaveSettings%2A>-Methode, um die vom Benutzer festgelegten Werte beim Beenden des Editors aus den Steuerelementen in die Eigenschaften des Enumerators zu kopieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines benutzerdefinierten ForEach-Enumerators](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/creating-a-custom-foreach-enumerator.md)   
 [Codieren eines benutzerdefinierten ForEach-Enumerators](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/coding-a-custom-foreach-enumerator.md)  
  
  

