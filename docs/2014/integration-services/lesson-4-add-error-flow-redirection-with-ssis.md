---
title: 'Lektion 4: Hinzufügen von Fehlerflussumleitungen | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 0c8dbda2-75e3-4278-9b4e-dcd220c92522
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 39fdc04590f6a5656e902794f4965ef53f21bfad
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48154430"
---
# <a name="lesson-4-adding-error-flow-redirection"></a>Lektion 4: Hinzufügen der Fehlerflussumleitung
  Um mögliche Fehler im Transformationsprozess zu behandeln, können Sie mithilfe von [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] auf der Grundlage von Komponenten oder Spalten entscheiden, wie Daten zu handhaben sind, die nicht transformiert werden können. Sie können einen Fehler in bestimmten Spalten ignorieren, die gesamte fehlgeschlagene Zeile umleiten, oder die gesamte Komponente als fehlerhaft behandeln. Standardmäßig sind alle Komponenten in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] so konfiguriert, dass sie bei Fehlern fehlschlagen. Das Behandeln einer Komponente als fehlerhaft verursacht wiederum die Behandlung des Pakets als fehlerhaft, und die gesamte nachfolgende Verarbeitung wird beendet.  
  
 Anstatt das Beenden durch Fehler der Paketausführung zuzulassen, ist es eine bewährte Vorgehensweise, potenzielle Verarbeitungsfehler zu konfigurieren und zu handhaben, wenn sie innerhalb der Transformation auftreten. Während das Ignorieren von Fehlern möglich ist, um die erfolgreiche Ausführung Ihrer Pakete sicherzustellen, ist es oft besser, die fehlgeschlagene Zeile zu einem anderen Verarbeitungspfad umzuleiten, wo die Daten und Fehler bestehen bleiben sowie zu einem späteren Zeitpunkt untersucht und erneut verarbeitet werden können.  
  
 In dieser Lektion erstellen Sie eine Kopie des Pakets, das Sie in [Lesson 3: Adding Logging](lesson-3-add-logging-with-ssis.md)entwickelt haben. Beim Arbeiten mit diesem neuen Paket werden Sie eine beschädigte Version einer der Beispieldatendateien erstellen. Durch die beschädigte Datei wird beim Ausführen des Pakets ein Verarbeitungsfehler erzwungen.  
  
 Zur Behandlung von Fehlerdaten fügen Sie ein Flatfileziel hinzu, und konfigurieren Sie es. Das Flatfileziel schreibt alle Zeilen, die keinen Suchwert in der Lookup Currency Key-Transformation finden, in eine Datei.  
  
 Bevor die Fehlerdaten in die Datei geschrieben werden, greift eine von Ihnen eingefügte Skriptkomponente ein, die mithilfe eines Skripts Fehlerbeschreibungen abruft. Sie konfigurieren dann die Lookup Currency Key-Transformation erneut, um alle Daten, die nicht verarbeitet werden konnten, an die Skripttransformation umzuleiten.  
  
> [!IMPORTANT]  
>  Dieses Lernprogramm erfordert die **AdventureWorksDW2012** -Beispieldatenbank. Weitere Informationen zum Installieren und Bereitstellen von **AdventureWorksDW2012**finden Sie unter [Reporting Services Produktbeispiel-Projekt auf CodePlex](http://go.microsoft.com/fwlink/p/?LinkId=526910).  
  
## <a name="tasks-in-lesson"></a>Aufgaben in der Lektion  
 Diese Lektion enthält die folgenden Aufgaben:  
  
-   [Schritt 1: Kopieren des Pakets aus Lektion 3](lesson-4-1-copying-the-lesson-3-package.md)  
  
-   [Schritt 2: Erstellen einer beschädigten Datei](lesson-4-2-creating-a-corrupted-file.md)  
  
-   [Schritt 3: Hinzufügen von Fehlerflussumleitungen](lesson-4-3-adding-error-flow-redirection.md)  
  
-   [Schritt 4: Hinzufügen eines Flatfileziels](lesson-4-4-adding-a-flat-file-destination.md)  
  
-   [Schritt 5: Testen des Tutorialpakets aus Lektion 4](lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Lektion beginnen  
 [Schritt 1: Kopieren des Pakets aus Lektion 3](lesson-4-1-copying-the-lesson-3-package.md)  
  
  
