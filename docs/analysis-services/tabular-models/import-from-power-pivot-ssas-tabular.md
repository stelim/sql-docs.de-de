---
title: Importieren aus PowerPivot | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 63a1619b09475bfa0ec8d4a1f21aaf88791a5b6c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/10/2018
ms.locfileid: "34041708"
---
# <a name="import-from-power-pivot"></a>Importieren aus PowerPivot 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  In diesem Artikel wird beschrieben, wie ein neues tabellarisches Modellprojekt erstellt, durch das Importieren von Metadaten und Daten aus einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Arbeitsmappe mithilfe des Imports von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Projektvorlage in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="create-a-new-tabular-model-from-a-power-pivot-for-excel-file"></a>Erstellen eines neuen tabellarischen Modells aus einer PowerPivot für Excel-Datei  
 Wenn Sie ein neues Projekt für tabellarische Modelle erstellen, indem Sie Daten aus einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe importieren, werden die Metadaten zur Definition der Arbeitsmappenstruktur verwendet, um die Struktur des tabellarischen Modellprojekts in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]zu erstellen und zu definieren. Objekte wie Tabellen, Spalten, Measures und Beziehungen werden beibehalten und im tabellarischen Modellprojekt genauso dargestellt wie in der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe. An der XLSX-Arbeitsmappendatei werden keine Änderungen vorgenommen.  
  
> [!NOTE]  
>  Verknüpfte Tabellen werden in tabellarischen Modellen nicht unterstützt. Wenn Daten aus einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe importiert werden, die eine verknüpfte Tabelle enthält, werden die Daten der verknüpften Tabelle wie kopierte/eingefügte Daten behandelt und in der Datei „Model.bim“ gespeichert. Wenn Sie Eigenschaften für eine kopierte/eingefügte Tabelle anzeigen, sind die Eigenschaft **Quelldaten** und das Dialogfeld **Tabelleneigenschaften** im Menü **Tabelle** deaktiviert.  
>   
>  Die Anzahl der Zeilen, die den im Modell eingebetteten Daten hinzugefügt werden können, ist auf 10.000 Zeilen beschränkt. Wenn Sie ein Modell aus [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] importieren und der Fehler „Daten wurden abgeschnitten. Eingefügte Tabellen dürfen nicht mehr als 10.000 Zeilen umfassen“ angezeigt wird, überprüfen Sie das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Modell, indem Sie die eingebetteten Daten in eine andere Datenquelle verschieben, beispielsweise eine Tabelle in SQL Server, und einen Neuimport ausführen.  
  
 Abhängig davon, ob die Arbeitsbereichsdatenbank auf einer Analysis Services-Instanz auf demselben Computer (lokal) wie [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oder auf einer Analysis Services-Remoteinstanz gespeichert ist, müssen bestimmte Punkte berücksichtigt werden.  
  
 Wenn die Arbeitsbereichsdatenbank auf einer lokalen Instanz von Analysis Services gespeichert ist, können Sie sowohl die Metadaten als auch die Daten aus der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe importieren. Die Metadaten werden aus der Arbeitsmappe kopiert und zum Erstellen des tabellarischen Modellprojekts verwendet. Anschließend werden die Daten aus der Arbeitsmappe kopiert und in der Arbeitsbereichsdatenbank des Projekts gespeichert (mit Ausnahme von kopierten/eingefügten Daten, die in der Datei Model.bim gespeichert werden).  
  
 Wenn die Arbeitsbereichsdatenbank auf einer Analysis Services-Remoteinstanz gespeichert ist, können Sie keine Daten aus einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für Excel-Arbeitsmappe importieren. Sie können jedoch die Metadaten der Arbeitsmappe importieren. Zu diesem Zweck wird ein Skript auf der Analysis Services-Remoteinstanz ausgeführt. Sie sollten nur Metadaten aus vertrauenswürdigen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen importieren. Die Daten müssen aus den in den Datenquellenverbindungen definierten Quellen importiert werden. Kopierte/eingefügte Daten und Daten aus verknüpften Tabellen in der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe müssen kopiert und in das tabellarische Modellprojekt eingefügt werden.  
  
#### <a name="to-create-a-new-tabular-model-project-from-a-power-pivot-for-excel-file"></a>So erstellen Sie ein neues tabellarisches Modellprojekt aus einer PowerPivot für Excel-Datei  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]auf das Menü **Datei** , auf **Neu**und dann auf **Projekt**.  
  
2.  Klicken Sie im Dialogfeld **Neues Projekt** unter **Installierte Vorlagen** auf **Business Intelligence** und dann auf **Von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] importieren**.  
  
3.  Geben Sie unter **Name**einen Namen für das Projekt ein. Geben Sie dann einen Speicherort und einen Projektmappennamen an, und klicken Sie auf **OK**.  
  
4.  Wählen Sie im Dialogfeld **Öffnen** die [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] -Datei aus, die die zu importierenden Modellmetadaten und -daten enthält, und klicken Sie dann auf **Öffnen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Arbeitsbereichsdatenbank](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md)   
 [Kopieren und Einfügen von Daten](../../analysis-services/tabular-models/ssas-import-data-copy-and-paste-data.md)  
  
  
