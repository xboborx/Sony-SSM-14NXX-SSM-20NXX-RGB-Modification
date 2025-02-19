Данный форк является вольным переводом оригинала статьи:
https://github.com/phrederick/Sony-SSM-14NXX-SSM-20NXX-RGB-Modification
Спасибо автору за труд!

# SSM-14NXX / SSM-20NXX RGB модификация

- [Введение](#введение)
- [Для кого это руководство](#для-кого-это-руководство)
    - [Модели PVM](#модели-pvm)
- [Список инструментов](#список-инструментов)
    - [Необходимые](#required)
    - [Рекомендуемые](#highly-recommended)
- [Список деталей](#список-деталей)
- [Шаг 1 - Dismantling the monitor](#step-1---dismantling-the-monitor)
    - [Step 1.1 - Removing the case](#step-11---removing-the-case)
    - [Step 1.2 - Detaching the Q board and releasing the Q board from the connector mounting plate](#step-12---detaching-the-q-board-and-releasing-the-q-board-from-the-connector-mounting-plate)
    - [Step 1.3 - Removing the A board](#step-13---removing-the-a-board)
- [Step 2 - Q board and mounting panel modifications](#step-2---q-board-and-mounting-panel-modifications)
    - [Q board and mounting panel modification images](#q-board-and-mounting-panel-modification-images)
- [Step 3 - A board modifications](#step-3---a-board-modifications)
    - [A board modification images](#a-board-modification-images)
- [Step 4 - Case / enclosure modifications](#step-4---case--enclosure-modifications)
    - [Case / enclosure modification images](#case--enclosure-modification-images)
    - [3D-printed front panel buttons](#3d-printed-front-panel-buttons)
    - [Reproduction faceplate decals](#reproduction-faceplate-decals)
- [References and acknowledgements](#references-and-acknowledgements)

## Введение
Цель этого документа - показать, как можно расширить функционал монитора Sony SSM, чтобы он мог поддерживать RGB-вход. В качестве оговорки хочу отметить, что я никоим образом не являюсь инженером-электронщиком, и вся информация, содержащаяся здесь, собрана из различных онлайн-источников. Эта документация в основном предназначена для моего собственного ознакомления, но я надеюсь, что другие тоже найдут ее полезной. Хотя я и производил эти модификации собственноручнчо, я все время опираюсь на плечи других.

Пожалуйста, обратите внимание, что на самом деле существует несколько способов создания этого мода, и что более правильным способом почти наверняка будет заполнить все недостающие компоненты, но эта документация служит для того, чтобы поведать конкретный маршрут, который я выбрал для его достижения.

## Для кого это руководство
Это руководство предназначено специально для тех, кто собирается модифицировать один из следующих мониторов для поддержки RGB:
|14" модели|20" модели|
|----------|----------|
|SSM-14N5A|SSM-20N5A|
|SSM-14N5E|SSM-20N5E|
|SSM-14N5U|SSM-20N5U|

### Модели PVM
Это руководство также может оказаться полезным, если вы являетесь владельцем одного из мониторов из таблицы, приведенной ниже, поскольку они основаны на том же шасси, что и вышеупомянутые мониторы «SSM-XXXXX».

|14" модель|20" модель|Комментарии|
|----------|----------|-----|
|PVM-14N5A|PVM-20N5A|Возможно модифицировать — см. примечания ниже.
|PVM-14N5E|PVM-20N5E|Возможно модифицировать — см. примечания ниже.
|PVM-14N5MDE|--|Возможно модифицировать — см. примечания ниже.
|PVM-14N5U|PVM-20N5U|Возможно модифицировать — см. примечания ниже.
|PVM-14N6A|PVM-20N6A|В этом мониторе уже имеется RGB
|PVM-14N6E|PVM-20N6E|В этом мониторе уже имеется RGB
|PVM-14N6U|PVM-20N6U|В этом мониторе уже имеется RGB

Модификация моделей PVM немного отличается и, может быть проще в зависимости от вашей цели. Различия в модификациях, характерные для моделей PVM, которые известны:

1. **Important** - Your PVM may or may not have a connector and wiring harness pre-installed at connector CN403 on the A board. If your monitor does not have this connector + harness, then you will need to route your own wires between the A and Q boards, but **be aware** that Sony made a mistake with the PCB labelling for this connector and it is reversed. On the PCB, the red pin is labelled as being closest to the front of the monitor, but the red pin is actually the one closest to the corner of the PCB; all other inputs are respectively reversed too. Therefore, from the corner of the PCB to the front, the pinouts are: R, GND, G, GND, B, GND, and Audio. See the images section below for a picture with the corrected pinout.
1. **Важно** - Ваш PVM может иметь или не иметь разъем и жгут проводов, предварительно установленные на разъеме CN403 на плате A. Если ваш монитор не имеет этого разъема + жгута, то вам нужно будет проложить собственные провода между платами A и Q, но **имейте в виду**, что Sony допустила ошибку с маркировкой печатной платы для этого разъема, и он перевернут. На печатной плате красный контакт обозначен как ближайший к передней части монитора, но на самом деле красный контакт является ближайшим к углу печатной платы; все остальные входы соответственно также перевернуты. Таким образом, от угла печатной платы к передней части, расположение выводов следующее: R, GND, G, GND, B, GND и Audio. Смотрите раздел изображений ниже для изображения с исправленным расположением выводов.

2. You may not need to make the same jumper cuts on the A board as noted in the instructions below, as they may already be absent.
2. Возможно, вам не придется делать те же самые разрезы перемычек на плате А, как указано в инструкциях ниже, поскольку они могут отсутствовать.

3. The BA7604N and MC14052BCP ICs may already be present on your model, which means you will not need to add them.
3. Микросхемы BA7604N и MC14052BCP могут уже присутствовать в вашей модели, поэтому вам не потребуется их добавлять.   

4. If your monitor already has a connector and wiring harness between CN402 on the A board and CN1302 on the Q board (which it likely will if your monitor has Line B), then you can route your RGB sync pin to the emitter pin at Q1312 which is equivalent to jumping a wire to ESYNC at CN1302. See the images section below for a picture showing where to make the connection.
4. Если у вашего монитора уже есть разъем и жгут проводов между CN402 на плате A и CN1302 на плате Q (что, скорее всего, так и будет, если у вашего монитора есть линия B), то вы можете направить свой контакт синхронизации RGB на контакт эмиттера на Q1312, что эквивалентно перемычке провода к ESYNC на CN1302. Смотрите раздел изображений ниже, где показано, где сделать подключение.

5. In the case of the PVM-14N5MDE, you may not need to add the 10 ohm resistor at R032, as it may already be present.
5. В случае PVM-14N5MDE вам, возможно, не придется добавлять резистор сопротивлением 10 Ом в R032, так как он уже может присутствовать.

|Изображение|Описание|
|-----|-----|
|<img src="https://i.imgur.com/FmWPSVE.jpg" width="300">| As per point 1 above, this image illustrates the corrected pinout for CN403. If you are wiring CN403 yourself because your PVM does not have a connector and wiring harness, keep this in mind. If you want to install your own pin header (as opposed to just soldering wires directly into the PCB holes), the type of header you need is one with a 2.54mm pitch.
|<img src="https://i.imgur.com/OgMdGZ5.jpg" width="300">|As per point 4 above, if your PVM already has a connector between CN402 on the A board and CN1302 on the Q board, you can put a jumper wire between these two points instead of running a wire between A board and Q board which is necessary for models without aforementioned wiring harness between CN402 & CN1302.

## Список инструментов
### Обязательные
* Отвёртка
* Паяльник
* Инструмент для демонтажа компонентов и медная оплетка
* Оловянный припой (толщина 0.7мм)
* Изолированный кабель

### Рекомендуемые
* Мультиметр
* Паяльный флюс
* Бокорезы

## Список деталей
|Компонент|Описание|Количество|Ссылка|
|---------|-----------|---|-----|
|Керамический конденсатор|Поверхностный монтаж, неполярный - 0.1 мкф|3|[Digi-Key - 445-1418-1-ND](https://www.digikey.com.au/product-detail/en/tdk-corporation/C2012X7R2A104K125AA/445-1418-1-ND/569084)|
|Резистор|Выводной монтаж - 75 Ом 0.25 Вт|6|[Digi-Key - S75CACT-ND](https://www.digikey.com.au/product-detail/en/stackpole-electronics-inc/RNMF14FTC75R0/S75CACT-ND/2617815)|
|Резистор|Выводной монтаж - 10 Ом 0.25 Вт|2|[Digi-Key - CF14JT10R0CT-ND](https://www.digikey.com.au/product-detail/en/stackpole-electronics-inc/CF14JT10R0/CF14JT10R0CT-ND/1830306)|
|Переключатель|Выводной монтаж, угловой|2|[Digi-Key - P12233SCT-ND](https://www.digikey.com.au/product-detail/en/panasonic-electronic-components/EVQ-PC105K/P12233SCT-ND/593537)|
|BNC |Розетка типа "мама"|4|[Digi-Key - 2057-RF1-106-D-00-50-HDW-ND](https://www.digikey.com.au/product-detail/en/adam-tech/RF1-106-D-00-50-HDW/2057-RF1-106-D-00-50-HDW-ND/9830449)<br>[Jaycar - PS0658 (Australia)](https://www.jaycar.com.au/bnc-panel-socket-single-hole-mount/p/PS0658)|
|MC14052BCP|Микросхема|1|[eBay](https://www.ebay.com/sch/i.html?_from=R40&_trksid=p2380057.m570.l1313&_nkw=MC14052BCP&_sacat=0)|
|BA7604N|Микросхема|1|[eBay](https://www.ebay.com/sch/i.html?_from=R40&_trksid=p2334524.m570.l1313&_nkw=BA7604N&_sacat=0)|

## Step 1 - Dismantling the monitor
A note on safety: It goes without saying that working on CRTs has an element of risk as high voltages are involved. You can get a nasty zap or worse if you are not careful. There are lots of guides on YouTube on CRT safety and how to discharge them. I encourage you to educate yourself further on CRT safety so you're prepared for doing this mod.

At the high level, dismantling the monitor for this modification involves the following steps:
1. Removing the case
2. Removing the Q board (i.e. the panel + PCB with the connectors on it), and releasing the Q board from the connector mounting plate
4. Removing the A board (i.e. the main board that sits at the bottom of the monitor)

## Шаг 1 — Разборка монитора
Замечание по технике безопасности: Само собой разумеется, что работа с ЭЛТ-мониторами несет в себе элемент риска, поскольку задействованы высокие напряжения. Вы можете получить неприятный удар или что-то похуже, если не будете осторожны. На YouTube есть множество руководств по технике безопасности при работе с ЭЛТ и по их разрядке. Я рекомендую вам узнать больше о технике безопасности при работе с ЭЛТ, чтобы вы были готовы к этой модификации.

На высоком уровне разборка монитора для этой модификации включает в себя следующие шаги:
1. Снятие корпуса
2. Снятие платы Q (т. е. панели + печатной платы с разъемами на ней) и освобождение платы Q от монтажной пластины разъема
4. Снятие платы A (т. е. основной платы, которая находится в нижней части монитора)

### Step 1.1 - Removing the case
1. Remove the 4 screws (2 per side) on the sides of the monitor.
2. Remove the 4 screws on the rear of the monitor, all of which are located near the bottom. Two on the outer perimeter of the case, and two on the connector panel.
3. Using the carry handles, pull the outer case off to the rear.

### Шаг 1.1 — Снятие корпуса
1. Открутите 4 винта (по 2 с каждой стороны) по бокам монитора.
2. Открутите 4 винта на задней панели монитора, все они расположены в нижней части. Два по внешнему периметру корпуса и два на панели разъемов.
3. Используя ручки для переноски, потяните внешний корпус назад.

### Step 1.2 - Detaching the Q board and releasing the Q board from the connector mounting plate
1. Looking at the rear of the monitor, note that there are markings that suggest that you need to push down on the plastic frame below the input board.
2. Gently press down in the designated areas while pulling the Q board outward to release it.
3. This procedure is best illustrated in Steve @ Retro Tech's video [here](https://www.youtube.com/watch?t=320&v=-ifKYeq9aC4).
4. Disconnect the ribbon cables and ground wires.
5. Using a soldering iron + desoldering braid, or a desoldering tool, desolder all of the points where the Q board attaches to the connector mounting plate. Note that this includes 4 ground tab sections on the perimeter of the board.

### Шаг 1.2. Отсоединение платы Q и освобождение платы Q от монтажной пластины разъема
1. Глядя на заднюю часть монитора, обратите внимание, что есть маркировки, которые указывают на то, что вам нужно нажать на пластиковую рамку под платой ввода.
2. Аккуратно нажмите в обозначенных областях, одновременно вытягивая плату Q наружу, чтобы освободить ее.
3. Эта процедура лучше всего проиллюстрирована в видео Стива @ Retro Tech [здесь](https://www.youtube.com/watch?t=320&v=-ifKYeq9aC4).
4. Отсоедините ленточные кабели и провода заземления.
5. Используя паяльник + оплетку для распайки или инструмент для распайки, распаяйте все точки, где плата Q крепится к монтажной пластине разъема. Обратите внимание, что это включает в себя 4 секции заземляющих выводов по периметру платы.

### Step 1.3 - Removing the A board
1. Take a note / photo of all the connector locations.
2. Discharge and remove the anode cap. An example of how to remove and discharge the anode cap for PVM's is illustrated and explained in Steve @ Retro Tech's video [here](https://www.youtube.com/watch?t=184&v=AZBh8YaPbQg). You may also wish to review [this video](https://www.youtube.com/watch?v=JeX5Y7Amk0o) if you prefer to use the discharge tool method.
3. Disconnect the remaining connectors.
4. Hold the A board firmly at the back and pull it outwards. There are no screws or tabs holding it down.

### Шаг 1.3 - Снятие платы A
1. Запишите / сфотографируйте все места расположения разъемов.
2. Разрядите и снимите анодный колпачок. Пример того, как снять и разрядить анодный колпачок для ФЭМ, проиллюстрирован и объяснен в видео Стива @ Retro Tech [здесь](https://www.youtube.com/watch?t=184&v=AZBh8YaPbQg). Вы также можете просмотреть [это видео](https://www.youtube.com/watch?v=JeX5Y7Amk0o), если вы предпочитаете использовать метод с инструментом для разрядки.
3. Отсоедините оставшиеся разъемы.
4. Крепко держите плату A сзади и потяните ее наружу. На ней нет винтов или фиксаторов, удерживающих ее.

## Step 2 - Q board and mounting panel modifications
Now that the Q board has been released from the mounting plate, you can add the required components. I did it by first adding the BNC connectors to the mounting plate and soldering wire into the solder cup terminals which I then fed through the appropriate holes in the Q board. I then used insulated wires on the BNC ground lugs that wrapped around and attached to a single ground terminal on the Q board / mounting plate.

## Шаг 2 — Модификации платы Q и монтажной панели
Теперь, когда плата Q снята с монтажной пластины, можно добавить необходимые компоненты. Я сделал это, сначала добавив разъемы BNC к монтажной пластине и припаяв провод к клеммам для припоя, которые затем пропустил через соответствующие отверстия в плате Q. Затем я использовал изолированные провода на заземляющих наконечниках BNC, которые обернули вокруг и прикрепили к одной заземляющей клемме на плате Q/монтажной пластине.

Action|Part|Location / Notes|
------|----|----------------|
Add component|75 ohm resistor|R1339|
Add component|75 ohm resistor|R1344|
Add component|75 ohm resistor|R1346|
Add component|75 ohm resistor|Tieing BNC pin directly to ANA-R at CN1303. You can attach to the emitter pin at Q1308|
Add component|75 ohm resistor|Tieing BNC pin directly to ANA-G at CN1303. You can attach to the emitter pin at Q1309|
Add component|75 ohm resistor|Tieing BNC pin directly to ANA-B at CN1303. You can attach to the emitter pin at Q1310|
Add component|Insulated wire|Tieing the Sync BNC pin to EXT SYNC at CN402 on A board|
Add component|Insulated wire|**Optional** - Tieing AUDIO at CN1303 to emitter pin at Q1305|

The optional jumper wire for the Audio means that the RGB and Line A will share the same 'Audio In' jack.
Дополнительная перемычка для аудиосигнала означает, что RGB и линия A будут использовать один и тот же разъем «Аудиовход».

### Q board and mounting panel modification images
### Изображения модификации платы Q и монтажной панели
Image|Notes|
-----|-----|
|<img src="https://i.imgur.com/7zH86tG.jpg" width="300">|Q board, showing all component modification locations.|
|<img src="https://i.imgur.com/0IfgGnd.jpg" width="300">|Q board, showing an example of how to attach the BNC connectors.|
|<img src="https://i.imgur.com/40ZhIf3.jpg" width="300">|Q board and A board, showing an example of how to connect the sync wire.|

## Step 3 - A board modifications
Modifying the A board is pretty straight-forward. It's just a matter of removing and adding a few components. As noted earlier, some of these changes are not necessary if you are modifying the **non-SSM** variants based on the same chassis.

## Шаг 3 — Модификации платы A
Модификация платы A довольно проста. Это всего лишь вопрос удаления и добавления нескольких компонентов. Как отмечалось ранее, некоторые из этих изменений не нужны, если вы модифицируете варианты **не-SSM** на основе того же шасси.

Action|Part|Location / Notes|
------|----|----------------|
Remove component|Jumper wire|JW401|
Remove component|Jumper wire|JW402|
Remove component|Jumper wire|JW403|
Add component|10 ohm resistor|R030|
Add component|10 ohm resistor|R032|
Add component|SMD capacitor|C310|
Add component|SMD capacitor|C311|
Add component|SMD capacitor|C312|
Add component|MC14052BCP|IC401|
Add component|BA7604N|IC402|
Add component|Tactile switch|S006|
Add component|Tactile switch|S008|

### A board modification images
### Изображения модификации платы A
Image|Notes|
-----|-----|
|<img src="https://i.imgur.com/1zPY3th.jpg" width="300">|A board, showing all component modification locations.|
|<img src="https://i.imgur.com/retnfXi.jpg" width="300">|A board, detailed image showing where the ICs and jumper wire cuts / removals are to be made.|
|<img src="https://i.imgur.com/zdiLlXD.jpg" width="300">|A board, detailed image showing where to attach the SMD capacitors.|
|<img src="https://i.imgur.com/5jClN18.jpg" width="300">|A board, detailed image showing where to attach the 10 ohm resistors.|
|<img src="https://i.imgur.com/mKp8iDQ.jpg" width="300">|A board, detailed image showing where to attach the tactile switches.|

## Step 4 - Case / enclosure modifications
You will need to make some minor finishing touches to the case. Specifically:
1. Cutting holes in the rear panel plastic so the BNC connectors can poke through. One way you can do this is by using a scalpel to cut a rough but slightly smaller diameter circle out from behind and then roll up some 240 grit sandpaper and sand down the remaining overlap.
2. Cutting holes in the front panel plastic so you can reach the tactile buttons used for switching between your two inputs (Line A and RGB).
3. Adding labels for your new inputs and buttons.

## Шаг 4 — Модификации корпуса/корпуса
Вам нужно будет сделать несколько небольших завершающих штрихов в корпусе. А именно:
1. Вырезать отверстия в пластике задней панели, чтобы можно было продеть разъемы BNC. Один из способов сделать это — вырезать скальпелем грубый, но немного меньшего диаметра круг сзади, а затем скатать немного наждачной бумаги зернистостью 240 и отшлифовать оставшееся перекрытие.
2. Вырезать отверстия в пластике передней панели, чтобы можно было достать тактильные кнопки, используемые для переключения между двумя входами (линия A и RGB).
3. Добавить метки для новых входов и кнопок.

### Case / enclosure modification images
Image|Notes|
-----|-----|
|<img src="https://i.imgur.com/GO5K9MK.jpg" width="300">|Rear panel, showing an example of how to modify the rear panel.|

### 3D-printed front panel buttons
If you have access to a 3D printer, then you can print yourself some face buttons using the STL file here: https://www.thingiverse.com/thing:5029004. The STL file is also available on this GitHub page in the '..\Faceplate Button' directory. Kudos to 'galaxius' for kindly designing and printing the buttons for my own modified monitors.

Alternatively, for a small fee, I can provide you with two 3D printed buttons for switching between RGB and Line A. If you are interested, you can drop me an email: oo2@outlook.com. The cost is $5 AUD + shipping for 2 buttons. I can also sand and paint them for you for an additional $5 AUD - I will paint them with three coats of Tamiya Acrylic.

If you are using the suggested switches (or ones with very similar dimensions), the 3D printed buttons should remain captive in the hole and rest neatly against the switch acutator. Note that you will still need to punch or cut a square hole in the vinyl sticker so the button can protrude through.

### Кнопки передней панели, напечатанные на 3D-принтере
Если у вас есть доступ к 3D-принтеру, вы можете напечатать несколько кнопок на лицевой панели, используя файл STL здесь: https://www.thingiverse.com/thing:5029004. Файл STL также доступен на этой странице GitHub в каталоге '..\Faceplate Button'. Спасибо 'galaxius' за любезное проектирование и печать кнопок для моих собственных модифицированных мониторов.

В качестве альтернативы, за небольшую плату, я могу предоставить вам две кнопки, напечатанные на 3D-принтере, для переключения между RGB и Line A. Если вы заинтересованы, вы можете написать мне по электронной почте: oo2@outlook.com. Стоимость составляет 5 австралийских долларов + доставка за 2 кнопки. Я также могу отшлифовать и покрасить их для вас за дополнительные 5 австралийских долларов - я покрашу их тремя слоями акрила Tamiya.

Если вы используете предлагаемые переключатели (или те, которые имеют очень похожие размеры), 3D-печатные кнопки должны оставаться в отверстии и аккуратно прилегать к активатору переключателя. Обратите внимание, что вам все равно нужно будет пробить или вырезать квадратное отверстие в виниловой наклейке, чтобы кнопка могла выступать.

Image|Notes|
-----|-----|
|<img src="https://i.imgur.com/hqXKFIL.png" width="300">|An example of how these buttons can look once they are installed after the necessary modifications are done to the vinyl sticker.|
|<img src="https://i.imgur.com/lDalRr7.jpg" width="300">|Buttons unpainted / unsanded.|
|<img src="https://i.imgur.com/ctR6LBL.jpg" width="300">|Buttons painted / face sanded.|
|<img src="https://i.imgur.com/xH0grE9.gif" width="300">|Button video - view from inside case.|
|<img src="https://i.imgur.com/JDGMtNc.gif" width="300">|Button video - view from front (unsanded + painted prototype button)|

### Reproduction faceplate decals
With gracious thanks to Industrial Designer, Evan Twyford, we now have templates for creating reproduction faceplate decals to suit monitors with the following configurations:

* Modified monitors with 7mm x 7mm button holes for Line A, and RGB. Suitable for monitors using 3D-printed buttons available on this GitHub page - Note: **currently untested** - if you have created a panel with this configuration, please let me know your results!
* Modified monitors with 10mm x 10mm button holes for Line A, and RGB. Suitable for monitors where you have your own solution for faceplate buttons and / or desire the original 10mm x 10mm hole.
* Original N6 monitors with 10mm x 10mm button holes for Line A, Line B, and RGB. Suitable for monitors where Line B is also present, as is the case for original, unmodified N6 models.

The decals are available on this GitHub page in the '..\Faceplate Decals' directory. As advised by Evan, the PDF drawing will have just about all the info you need to know to have these decals recreated. Separate DXF file for the die-cut pattern is also provided if needed, but it is included in a layer in the PDF.

If you are based in the US, you may find the following information provided by Evan regarding printers / vendors useful:

* [Gamma Ray Graphics](https://www.gammaraygraphics.com/) - cheaper option (~$20 ea), colour matching not perfect, thinner labels.
* [MPC - Metalphoto of Cincinnati](https://www.mpofcinci.com/) - $400 setup cost, polyester nameplates are an accurate reproduction. This company, or similar, should have no problem meeting OEM spec.

  ### Репродукция наклеек на лицевую панель
С благодарностью промышленному дизайнеру Эвану Твайфорду у нас теперь есть шаблоны для создания репродукций наклеек на лицевую панель, подходящих для мониторов со следующими конфигурациями:

* Модифицированные мониторы с отверстиями для кнопок 7 мм x 7 мм для линии A и RGB. Подходит для мониторов с кнопками, напечатанными на 3D-принтере, доступными на этой странице GitHub. Примечание: **в настоящее время не протестировано** — если вы создали панель с этой конфигурацией, сообщите мне о своих результатах!
* Модифицированные мониторы с отверстиями для кнопок 10 мм x 10 мм для линии A и RGB. Подходит для мониторов, где у вас есть собственное решение для кнопок лицевой панели и/или вы хотите оригинальное отверстие 10 мм x 10 мм.
* Оригинальные мониторы N6 с отверстиями для кнопок 10 мм x 10 мм для линии A, линии B и RGB. Подходит для мониторов, где также присутствует линия B, как в случае с оригинальными, немодифицированными моделями N6.

Наклейки доступны на этой странице GitHub в каталоге '..\Faceplate Decals'. Как советует Эван, чертеж PDF будет содержать практически всю информацию, которую вам нужно знать, чтобы воссоздать эти наклейки. Отдельный файл DXF для шаблона высечки также предоставляется при необходимости, но он включен в слой в PDF.

Если вы находитесь в США, вам может быть полезна следующая информация, предоставленная Эваном относительно принтеров / поставщиков:

* [Gamma Ray Graphics](https://www.gammaraygraphics.com/) - более дешевый вариант (~$20 за штуку), неидеальное соответствие цветов, более тонкие этикетки.
* [MPC - Metalphoto of Cincinnati](https://www.mpofcinci.com/) - стоимость установки 400 $, полиэстеровые таблички являются точной репродукцией. У этой компании или аналогичной ей не должно возникнуть проблем с соблюдением спецификаций OEM.

Image|Notes|
-----|-----|
|<img src="https://i.imgur.com/JRme1tc.jpg" width="300">|An example image provided by Evan Twyford showing 2 PVM-14N6U monitors with reproduction faceplate decals produced by Gamma Ray Graphics|

## References and acknowledgements
* nrq for his additional notes on modding the PVM-14N5MDE; specifically regarding the R032 resistor, and the pin-header size.
* Sam Theodore Byrd for PVM model-specific note on where to connect the external sync pin.
* Evan Twyford, Industrial Designer - for creating and providing faceplate decal design files to suit original and modified monitors.
* galaxius for designing and printing 3D-printable face buttons.
* The official service manual for the 'SIIA' chassis: http://diagramas.diagramasde.com/otros/SSM-20N5U_9976686010-00e.pdf
* freakaftr8's 'Sony SSM-20N5U RGB mod!' guide on the Shmups forum: https://shmups.system11.org/viewtopic.php?f=6&t=66067&p=1400712#p1400712
* freakaftr8 for his patience with answering my questions on Reddit and providing additional guidance.
* santiis2010's 'PVM 14N5U to 14N6U' guide on Reddit: https://www.reddit.com/r/crtgaming/comments/i36ydq/re_doing_the_post_of_rgb_modding_for_pvm_14n5u_to/
* santiis2010 for his help with answering my questions on Facebook.
* Steve @ Retro Tech for his excellent videos on a broad range of CRT-related topics.
* Keith Gable for his 'Cap list and RGB mod part list' spreadsheet: https://onedrive.live.com/view.aspx?resid=780863C57629ADCC!1093221&ithint=file%2cxlsx&authkey=!APah2XIIKrw75wk
* The 'Professional & Broadcast CRT Monitors' and 'The CRT Collective' Facebook groups.
* The '/r/crtgaming' subreddit.
