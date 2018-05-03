---
title: 'Schritt 1: Konfigurieren der Entwicklungsumgebung für Ruby-Entwicklung | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ruby
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c7052fce85e035a0c4bff543ccbf994d7dd5f44d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>Schritt 1: Konfigurieren der Entwicklungsumgebung für Ruby-Entwicklung
Sie müssen Ihre Entwicklungsumgebung mit den Voraussetzungen zu konfigurieren, um die Entwicklung einer Anwendung mithilfe der Ruby-Treiber für SQL Server.    
  
Beachten Sie, dass der Ruby-Treiber das TDS-Protokoll verwendet, die standardmäßig in SQL Server und Azure SQL-Datenbank aktiviert ist.  Es ist keine zusätzliche Konfiguration erforderlich.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Herunterladen der Ruby-Installer**  
Wenn Ihr Computer keinen Ruby, installieren Sie es. Für neue Benutzer Ruby wird empfohlen, dass Sie Ruby 2.2.X Installationsprogramme verwenden. Diese enthalten eine stabile Sprache und eine umfassende Liste der Pakete (Gems), die aktualisierte und kompatibel sind. Wechseln Sie die [Ruby Downloadseite](http://rubyinstaller.org/downloads/) und entsprechenden 2.1.x Installationsprogramm herunterzuladen. Für das Beispiel auf einem 64-Bit-Computer herunterladen Installationsprogramm Ruby 2.1.6 (x 64).   
  
2.  **Installieren von Ruby**  
Sobald das Installationsprogramm heruntergeladen wurde, führen Sie folgende Schritte aus:  
A. Doppelklicken Sie auf die Datei, um das Installationsprogramm zu starten.  
B. Wählen Sie Ihre Sprache aus, und akzeptieren.  
c.  Wählen Sie auf der Seite Installation Einstellungen die Kontrollkästchen neben sowohl den Pfad und ordnen RB und .rbw-Dateien mit dieser Installation Ruby ausführbaren Dateien Ruby hinzufügen.  
  
3.  **Ruby DevKit herunterladen**  
DevKit von der Seite "RubyInstaller" herunterladen  
  
4.  **Installieren von Ruby DevKit**  
Nachdem der Download abgeschlossen ist, führen Sie folgende Schritte aus:  
A. Doppelklicken Sie auf die Datei. Sie aufgefordert, wo die Dateien zu extrahieren.  
B. Klicken Sie auf die Schaltfläche "...", und wählen Sie "C:\DevKit". Sie benötigen wahrscheinlich in diesem Ordner zuerst zu erstellen, indem Sie auf "Neuen Ordner erstellen".  
c. Klicken Sie auf "OK", und klicken Sie dann "extrahieren", um die Dateien zu extrahieren.  
  
5. **Öffnen von cmd.exe**  
  
6. **Initialisieren von Ruby DevKit**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **Installieren Sie TinyTDS Kugel**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Geöffneten Terminaldienste**  
  
2. **Installieren von Ruby-Versions-Manager (Rvm) und erforderliche Komponenten**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Verwenden Sie Rvm Ruby installieren**  
Installieren Sie z. B. Version 2.3.0 des Ruby:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Stellen Sie sicher, dass die Ausgabe mit dem letzten Befehl gibt an, dass Sie Version 2.3.0 ausgeführt werden.  
  
4.  **Installieren von FreeTDS**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **Installieren von TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
Beachten Sie, dass die Mac OS X wurde bereits vorinstalliert, Ruby, wie das Betriebssystem abhängig ist.    
  
1.  **Geöffneten Terminaldienste**  
  
2. **Installieren von Homebrew-Paket-manager**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **Installieren von FreeTDS**  
```  
> brew install FreeTDS  
```  
  
4.  **Installieren Sie TinyTDS Kugel**  
```  
> gem install tiny_tds  
```
