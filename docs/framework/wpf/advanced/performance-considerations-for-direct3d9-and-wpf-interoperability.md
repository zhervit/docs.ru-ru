---
title: Вопросы производительности, связанные с взаимодействием Direct3D9 и WPF
ms.date: 03/30/2017
helpviewer_keywords:
- WPF [WPF], Direct3D9 interop performance
- Direct3D9 [WPF interoperability], performance
ms.assetid: ea8baf91-12fe-4b44-ac4d-477110ab14dd
ms.openlocfilehash: 02a91c1824c5d6374f37b0af66a3308d33210c4a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69932482"
---
# <a name="performance-considerations-for-direct3d9-and-wpf-interoperability"></a>Вопросы производительности, связанные с взаимодействием Direct3D9 и WPF
Содержимое Direct3D9 можно разместить с помощью <xref:System.Windows.Interop.D3DImage> класса. Размещение содержимого Direct3D9 может повлиять на производительность приложения. В этом разделе описываются рекомендации по оптимизации производительности при размещении содержимого Direct3D9 в приложении Windows Presentation Foundation (WPF). Эти рекомендации включают использование <xref:System.Windows.Interop.D3DImage> и рекомендации при использовании Windows Vista, Windows XP и нескольких мониторов.  
  
> [!NOTE]
> Примеры кода, демонстрирующие эти рекомендации, см. в разделе [взаимодействие WPF и Direct3D9](wpf-and-direct3d9-interoperation.md).  
  
## <a name="use-d3dimage-sparingly"></a>Использовать D3DImage с осторожностью  
 Содержимое Direct3D9, размещенное <xref:System.Windows.Interop.D3DImage> в экземпляре, не отображается так быстро, как в чистом приложении Direct3D. Копирование поверхности и очистка буфера команд может быть дорогостоящими операциями. По мере увеличения числа <xref:System.Windows.Interop.D3DImage> экземпляров увеличивается и снижается производительность. Поэтому следует использовать <xref:System.Windows.Interop.D3DImage> с осторожностью.  
  
## <a name="best-practices-on-windows-vista"></a>Рекомендации по использованию Windows Vista  
 Чтобы обеспечить наилучшую производительность Windows Vista с отображением, настроенным на использование модели Windows дисплея (WDDM), создайте на `IDirect3DDevice9Ex` устройстве поверхность Direct3D9. Это обеспечивает общий доступ к поверхности. Видеоадаптер должен поддерживать `D3DDEVCAPS2_CAN_STRETCHRECT_FROM_TEXTURES` возможности драйверов и `D3DCAPS2_CANSHARERESOURCE` в Windows Vista. Другие параметры приводят к тому, что поверхность копируется в программное обеспечение, что значительно снижает производительность.  
  
> [!NOTE]
> Если в Windows Vista имеется дисплей, настроенный на использование модели Windows XP дисплея (КСДДМ), поверхность всегда копируется через программное обеспечение независимо от параметров. Благодаря правильным параметрам и видеоадаптеру в Windows Vista вы увидите лучшую производительность при использовании WDDM, поскольку копирование поверхностей выполняется на оборудовании.  
  
## <a name="best-practices-on-windows-xp"></a>Рекомендации по Windows XP  
 Для лучшей производительности в Windows XP, которая использует модель видеодрайверов Windows XP (ксддм), создайте блокируемую поверхность, которая правильно работает при `IDirect3DSurface9::GetDC` вызове метода. На `BitBlt` внутреннем уровне метод передает поверхность между устройствами в оборудовании. `GetDC` Метод всегда работает на поверхностях ксргб. Однако если клиентский компьютер работает под управлением Windows XP с пакетом обновления 3 (SP3) или с пакетом обновления 2 (SP2), а также если у клиента есть исправление для функции многоуровневого окна, этот метод работает только на поверхностях ARGB. Видеоадаптер должен поддерживать `D3DDEVCAPS2_CAN_STRETCHRECT_FROM_TEXTURES` возможности драйвера.  
  
 16-разрядная глубина экрана может значительно снизить производительность. Рекомендуется использовать 32-разрядный компьютер.  
  
 При разработке для Windows Vista и Windows XP следует протестировать производительность Windows XP. В Windows XP возникает проблема, связанная с нехваткой видеопамяти. Кроме того, <xref:System.Windows.Interop.D3DImage> в Windows XP используется больше памяти и пропускной способности, чем в Windows Vista WDDM из-за необходимости в дополнительной копии видеопамяти. Таким образом, производительность может быть хуже в Windows XP, чем в Windows Vista для одного и того же видеооборудования.  
  
> [!NOTE]
> КСДДМ доступен как в Windows XP, так и в Windows Vista; Однако WDDM доступен только в Windows Vista.  
  
## <a name="general-best-practices"></a>Общие рекомендации  
 При создании устройства используйте `D3DCREATE_MULTITHREADED` флаг создания. Это снижает производительность, но система отрисовки WPF вызывает методы на этом устройстве из другого потока. Не забудьте правильно следовать протоколу блокировки, чтобы ни один из двух потоков не одновременно выполнял доступ к устройству.  
  
 Если отрисовка выполняется в управляемом потоке WPF, настоятельно рекомендуется создать устройство с `D3DCREATE_FPU_PRESERVE` флагом создания. Без этого параметра визуализация D3D может снизить точность операций двойной точности WPF и вызвать проблемы отрисовки.  
  
 Мозаичное заполнение <xref:System.Windows.Media.DrawingBrush> <xref:System.Windows.Media.VisualBrush> <xref:System.Windows.Interop.D3DImage>выполняется быстро, если не pow2 поверхность без поддержки оборудования или если плитка или содержит. <xref:System.Windows.Interop.D3DImage>  
  
## <a name="best-practices-for-multi-monitor-displays"></a>Рекомендации по отображению нескольких мониторов  
 Если вы используете компьютер с несколькими мониторами, следуйте приведенным выше рекомендациям. Кроме того, для конфигурации с несколькими мониторами также необходимо учитывать некоторые дополнительные факторы.  
  
 При создании заднего буфера он создается на определенном устройстве и адаптере, но WPF может отображать передний буфер на любом адаптере. Копирование между адаптерами для обновления внешнего буфера может быть очень дорогим. В Windows Vista, настроенном для использования WDDM с несколькими видеоадаптерами и `IDirect3DDevice9Ex` устройством, если передний буфер находится на другом адаптере, но по-прежнему один видеоадаптер, производительность не снижается. Однако в Windows XP и КСДДМ с несколькими видеоадаптерами значительно снижается производительность при отображении внешнего буфера на адаптере, отличном от адаптера заднего буфера. Дополнительные сведения см. в разделе [взаимодействие WPF и Direct3D9](wpf-and-direct3d9-interoperation.md).  
  
## <a name="performance-summary"></a>Сводка по производительности  
 В следующей таблице показана производительность обновления переднего буфера в виде функции операционной системы, формата пикселей и блокировки поверхности. Предполагается, что интерфейсный буфер и задний буфер находятся на одном адаптере. В зависимости от конфигурации адаптера обновления оборудования обычно выполняются гораздо быстрее, чем обновления программного обеспечения.  
  
|Формат пиксельной поверхности|Windows Vista, WDDM и 9Ex|Другие конфигурации Windows Vista|Исправление для Windows XP SP3 или с пакетом обновления 2 (SP2)|Windows XP с пакетом обновления 2 (SP2)|  
|--------------------------|---------------------------------|----------------------------------------|--------------------------------------|--------------------|  
|D3DFMT_X8R8G8B8 (не блокируемый)|**Обновление оборудования**|Обновление программного обеспечения|Обновление программного обеспечения|Обновление программного обеспечения|  
|D3DFMT_X8R8G8B8 (блокируемый)|**Обновление оборудования**|Обновление программного обеспечения|**Обновление оборудования**|**Обновление оборудования**|  
|D3DFMT_A8R8G8B8 (не блокируемый)|**Обновление оборудования**|Обновление программного обеспечения|Обновление программного обеспечения|Обновление программного обеспечения|  
|D3DFMT_A8R8G8B8 (блокируемый)|**Обновление оборудования**|Обновление программного обеспечения|**Обновление оборудования**|Обновление программного обеспечения|  
  
## <a name="see-also"></a>См. также

- <xref:System.Windows.Interop.D3DImage>
- [Взаимодействие WPF и Direct3D9](wpf-and-direct3d9-interoperation.md)
- [Пошаговое руководство: Создание содержимого Direct3D9 для размещения в WPF](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)
- [Пошаговое руководство: Размещение содержимого Direct3D9 в WPF](walkthrough-hosting-direct3d9-content-in-wpf.md)
