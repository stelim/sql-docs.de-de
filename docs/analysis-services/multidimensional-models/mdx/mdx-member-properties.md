---
title: Verwenden von Elementeigenschaften (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DIMENSION PROPERTIES keyword
- Properties function
- member properties [MDX]
- members [MDX], properties
ms.assetid: 26b5ad08-3799-4a5e-89f3-dca25e637d45
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1c3f560f0be83b17b31db8cfd46bc0b7939ee05d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-member-properties"></a>MDX-Elementeigenschaften
  Elementeigenschaften enthalten die grundlegenden Informationen zu jedem Element in jedem Tupel. Zu den grundlegenden Informationen gehören der Elementname, die übergeordnete Ebene, die Anzahl der untergeordneten Elemente usw. Elementeigenschaften sind für alle Elemente auf der jeweiligen Ebene verfügbar. Organisatorisch werden Elementeigenschaften als in Dimensionen organisierte Daten behandelt, die in einer einzigen Dimension gespeichert werden.  
  
> [!NOTE]  
>  In [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]werden Elementeigenschaften als Attributbeziehungen bezeichnet. Weitere Informationen finden Sie unter [Attributbeziehungen](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
 Eine Elementeigenschaft ist entweder *systemintern* oder *benutzerdefiniert*:  
  
 Systeminterne Elementeigenschaften  
 Alle Elemente unterstützen systeminterne Elementeigenschaften, wie z. B. den formatierten Wert eines Elements. Dimensionen und Ebenen stellen dagegen zusätzliche systeminterne dimensions- und ebenenspezifische Elementeigenschaften, wie die ID eines Elements, bereit.  
  
 Weitere Informationen finden Sie unter [Integrierte Elementeigenschaften &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md).  
  
 Benutzerdefinierte Elementeigenschaften  
 Elemente haben häufig weitere ihnen zugeordnete Eigenschaften. Die Products-Ebene kann z. B. die Eigenschaften SKU (Stock Keeping Unit), SRP (Suggested Retail Price), Weight und Volume für jedes Produkt bieten. Diese Eigenschaften sind keine Elemente, sondern enthalten zusätzliche Informationen zu Elementen auf der Products-Ebene.  
  
 Weitere Informationen finden Sie unter [Benutzerdefinierte Elementeigenschaften &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
 Sowohl intrinsische als auch benutzerdefinierte Elementeigenschaften können mithilfe des **PROPERTIES**-Schlüsselworts oder der [Properties](../../../mdx/properties-mdx.md)-Funktion abgerufen werden.  
  
## <a name="using-the-properties-keyword"></a>Verwenden des PROPERTIES-Schlüsselworts  
 Das **PROPERTIES** -Schlüsselwort gibt die Elementeigenschaften an, die für eine bestimmte Achsendimension verwendet werden müssen. Das **PROPERTIES** -Schlüsselwort wird in der `<axis specification>` -Klausel der MDX- [SELECT](../../../mdx/mdx-data-manipulation-select.md) -Anweisung verwendet:  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
```  
  
 Die `<axis_specification>` -Klausel enthält eine optionale `<dim_props>` -Klausel (siehe folgende Syntax):  
  
```  
<axis_specification> ::= <set> [<dim_props>] ON <axis_name>  
```  
  
> [!NOTE]  
>  Weitere Informationen zu den Werten `<set>` und `<axis_name>` finden Sie unter [Angeben des Inhalts einer Abfrageachse &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
 Das `<dim_props>` -Klausel ermöglicht es Ihnen, mithilfe des **PROPERTIES** -Schlüsselworts Dimensions-, Ebenen- und Elementeigenschaften abzufragen. Nachstehend ist die Syntax der `<dim_props>` -Klausel definiert:  
  
```  
<dim_props> ::= [DIMENSION] PROPERTIES <property> [,<property>...]  
```  
  
 Die Aufteilung der Syntax von `<property>` variiert abhängig davon, welche Eigenschaft abgefragt wird:  
  
-   Bei einer kontextabhängigen systeminternen Elementeigenschaft muss der Name der Dimension oder der Ebene vor der Eigenschaft stehen. Nicht kontextabhängige systeminterne Elementeigenschaften können dagegen nicht durch den Dimensions- oder Ebenennamen qualifiziert werden. Weitere Informationen zum Verwenden des **PROPERTIES**-Schlüsselworts mit integrierten Elementeigenschaften finden Sie unter [Integrierte Elementeigenschaften &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md).  
  
-   Bei einer benutzerdefinierten Elementeigenschaft sollte der Name der Ebene vorangestellt werden, in der sie sich befindet. Weitere Informationen zum Verwenden des **PROPERTIES**-Schlüsselworts mit benutzerdefinierten Elementeigenschaften finden Sie unter [Benutzerdefinierte Elementeigenschaften &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Verwenden von Eigenschaftswerten &#40;MDX&#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)  
  
  