---
title: Практическое руководство. Анимация объекта вдоль контура (матричная анимация)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], objects along paths (matrix animation)
- matrix animation [WPF]
ms.assetid: 7000e697-1414-468c-b915-cf66062fc49e
ms.openlocfilehash: 3c90d20cac60004aa9876d9fe8d213d33c5a6883
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64651437"
---
# <a name="how-to-animate-an-object-along-a-path-matrix-animation"></a>Практическое руководство. Анимация объекта вдоль контура (матричная анимация)
В этом примере показано, как использовать <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> класс для анимации объекта вдоль пути, который определяется <xref:System.Windows.Media.PathGeometry>.  
  
## <a name="example"></a>Пример  
 Следующий пример анимирует объект вдоль пути следующим образом:  
  
- Применяет <xref:System.Windows.Media.MatrixTransform> к объекту, чтобы переместить его.  
  
- Определяет путь с помощью <xref:System.Windows.Media.PathGeometry>.  
  
- Создает <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> и использует его для анимации <xref:System.Windows.Media.Matrix> свойство <xref:System.Windows.Media.MatrixTransform>. <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> Принимает <xref:System.Windows.Media.PathGeometry> и использует их для создания <xref:System.Windows.Media.Matrix> значения.  
  
 [!code-xaml[PathAnimationGallery_snippet#MatrixAnimationUsingPathWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/matrixanimationusingpathexample.xaml#matrixanimationusingpathwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/MatrixAnimationUsingPathExample.cs#matrixanimationusingpathwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/MatrixAnimationUsingPathExample.vb#matrixanimationusingpathwholepage)]  
  
 Полный пример см. в разделе [Пример анимации вдоль пути](https://go.microsoft.com/fwlink/?LinkID=160028). Дополнительные сведения о геометрических путях см. в разделе [Общие сведения о геометрии](geometry-overview.md).  
  
## <a name="see-also"></a>См. также

- [Общие сведения об эффектах анимации](animation-overview.md)
- [Пример анимации вдоль пути](https://go.microsoft.com/fwlink/?LinkID=160028)
- [Практические руководства, посвященные анимации по контуру](path-animation-how-to-topics.md)
