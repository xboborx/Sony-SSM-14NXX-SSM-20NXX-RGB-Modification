Данный форк является вольным переводом оригинала статьи:
https://github.com/phrederick/Sony-SSM-14NXX-SSM-20NXX-RGB-Modification
Спасибо автору за труд!

# SSM-14NXX / SSM-20NXX RGB модификация

- [Введение](#введение)
- [Для кого это руководство](#для-кого-это-руководство)
    - [Модели PVM](#pvm-models)
- [Список инструментов](#tools-list)
    - [Необходимые](#required)
    - [Рекомендуемые](#highly-recommended)
- [Список деталей](#parts-list)
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
Это руководство предназначено специально для вас, если вы собираетесь модифицировать какой-либо из следующих мониторов для поддержки RGB:
|14" модели|20" модели|
|----------|----------|
|SSM-14N5A|SSM-20N5A|
|SSM-14N5E|SSM-20N5E|
|SSM-14N5U|SSM-20N5U|

### Модели PVM
This guide may also be useful to you if you own any of the monitors from the table below, as they are also based on the same chassis as the aforementioned 'SSM-XXXXX' monitors.
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

Modifying the PVM models is slightly different, and perhaps even easier depending on your perspective. The mod differences specific to PVM models that I am aware of are:
Модификация моделей PVM немного отличается и, возможно, даже проще в зависимости от вашей точки зрения. Различия в модификациях, характерные для моделей PVM, о которых я знаю, следующие:

1. **Important** - Your PVM may or may not have a connector and wiring harness pre-installed at connector CN403 on the A board. If your monitor does not have this connector + harness, then you will need to route your own wires between the A and Q boards, but **be aware** that Sony made a mistake with the PCB labelling for this connector and it is reversed. On the PCB, the red pin is labelled as being closest to the front of the monitor, but the red pin is actually the one closest to the corner of the PCB; all other inputs are respectively reversed too. Therefore, from the corner of the PCB to the front, the pinouts are: R, GND, G, GND, B, GND, and Audio. See the images section below for a picture with the corrected pinout.

2. You may not need to make the same jumper cuts on the A board as noted in the instructions below, as they may already be absent.

3. The BA7604N and MC14052BCP ICs may already be present on your model, which means you will not need to add them.

4. If your monitor already has a connector and wiring harness between CN402 on the A board and CN1302 on the Q board (which it likely will if your monitor has Line B), then you can route your RGB sync pin to the emitter pin at Q1312 which is equivalent to jumping a wire to ESYNC at CN1302. See the images section below for a picture showing where to make the connection.

5. In the case of the PVM-14N5MDE, you may not need to add the 10 ohm resistor at R032, as it may already be present.

|Image|Notes|
|-----|-----|
|<img src="https://i.imgur.com/FmWPSVE.jpg" width="300">| As per point 1 above, this image illustrates the corrected pinout for CN403. If you are wiring CN403 yourself because your PVM does not have a connector and wiring harness, keep this in mind. If you want to install your own pin header (as opposed to just soldering wires directly into the PCB holes), the type of header you need is one with a 2.54mm pitch.
|<img src="https://i.imgur.com/OgMdGZ5.jpg" width="300">|As per point 4 above, if your PVM already has a connector between CN402 on the A board and CN1302 on the Q board, you can put a jumper wire between these two points instead of running a wire between A board and Q board which is necessary for models without aforementioned wiring harness between CN402 & CN1302.

## Tools List
### Required
* Screwdriver
* Soldering iron (I used a TS100)
* Desoldering braid / Desoldering tool
* Solder (I used 0.7mm)
* Insulated wire

### Highly Recommended
* Multimeter
* Flux
* Side cutters

## Parts List
|Component|Description|Qty|Links|
|---------|-----------|---|-----|
|Ceramic capacitor|Surface mount, non-polarised - 0.1µF|3|[Digi-Key - 445-1418-1-ND](https://www.digikey.com.au/product-detail/en/tdk-corporation/C2012X7R2A104K125AA/445-1418-1-ND/569084)|
|Resistor|Through hole - 75 ohm 0.25W|6|[Digi-Key - S75CACT-ND](https://www.digikey.com.au/product-detail/en/stackpole-electronics-inc/RNMF14FTC75R0/S75CACT-ND/2617815)|
|Resistor|Through hole - 10 ohm 0.25W|2|[Digi-Key - CF14JT10R0CT-ND](https://www.digikey.com.au/product-detail/en/stackpole-electronics-inc/CF14JT10R0/CF14JT10R0CT-ND/1830306)|
|Switch|Side actuated, through hole, right angle|2|[Digi-Key - P12233SCT-ND](https://www.digikey.com.au/product-detail/en/panasonic-electronic-components/EVQ-PC105K/P12233SCT-ND/593537)|
|BNC Connectors|Female socket|4|[Digi-Key - 2057-RF1-106-D-00-50-HDW-ND](https://www.digikey.com.au/product-detail/en/adam-tech/RF1-106-D-00-50-HDW/2057-RF1-106-D-00-50-HDW-ND/9830449)<br>[Jaycar - PS0658 (Australia)](https://www.jaycar.com.au/bnc-panel-socket-single-hole-mount/p/PS0658)|
|MC14052BCP|Integrated circuit|1|[eBay](https://www.ebay.com/sch/i.html?_from=R40&_trksid=p2380057.m570.l1313&_nkw=MC14052BCP&_sacat=0)|
|BA7604N|Integrated circuit|1|[eBay](https://www.ebay.com/sch/i.html?_from=R40&_trksid=p2334524.m570.l1313&_nkw=BA7604N&_sacat=0)|

## Step 1 - Dismantling the monitor
A note on safety: It goes without saying that working on CRTs has an element of risk as high voltages are involved. You can get a nasty zap or worse if you are not careful. There are lots of guides on YouTube on CRT safety and how to discharge them. I encourage you to educate yourself further on CRT safety so you're prepared for doing this mod.

At the high level, dismantling the monitor for this modification involves the following steps:
1. Removing the case
2. Removing the Q board (i.e. the panel + PCB with the connectors on it), and releasing the Q board from the connector mounting plate
4. Removing the A board (i.e. the main board that sits at the bottom of the monitor)

### Step 1.1 - Removing the case
1. Remove the 4 screws (2 per side) on the sides of the monitor.
2. Remove the 4 screws on the rear of the monitor, all of which are located near the bottom. Two on the outer perimeter of the case, and two on the connector panel.
3. Using the carry handles, pull the outer case off to the rear.

### Step 1.2 - Detaching the Q board and releasing the Q board from the connector mounting plate
1. Looking at the rear of the monitor, note that there are markings that suggest that you need to push down on the plastic frame below the input board.
2. Gently press down in the designated areas while pulling the Q board outward to release it.
3. This procedure is best illustrated in Steve @ Retro Tech's video [here](https://www.youtube.com/watch?t=320&v=-ifKYeq9aC4).
4. Disconnect the ribbon cables and ground wires.
5. Using a soldering iron + desoldering braid, or a desoldering tool, desolder all of the points where the Q board attaches to the connector mounting plate. Note that this includes 4 ground tab sections on the perimeter of the board.

### Step 1.3 - Removing the A board
1. Take a note / photo of all the connector locations.
2. Discharge and remove the anode cap. An example of how to remove and discharge the anode cap for PVM's is illustrated and explained in Steve @ Retro Tech's video [here](https://www.youtube.com/watch?t=184&v=AZBh8YaPbQg). You may also wish to review [this video](https://www.youtube.com/watch?v=JeX5Y7Amk0o) if you prefer to use the discharge tool method.
3. Disconnect the remaining connectors.
4. Hold the A board firmly at the back and pull it outwards. There are no screws or tabs holding it down.

## Step 2 - Q board and mounting panel modifications
Now that the Q board has been released from the mounting plate, you can add the required components. I did it by first adding the BNC connectors to the mounting plate and soldering wire into the solder cup terminals which I then fed through the appropriate holes in the Q board. I then used insulated wires on the BNC ground lugs that wrapped around and attached to a single ground terminal on the Q board / mounting plate.

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

### Q board and mounting panel modification images
Image|Notes|
-----|-----|
|<img src="https://i.imgur.com/7zH86tG.jpg" width="300">|Q board, showing all component modification locations.|
|<img src="https://i.imgur.com/0IfgGnd.jpg" width="300">|Q board, showing an example of how to attach the BNC connectors.|
|<img src="https://i.imgur.com/40ZhIf3.jpg" width="300">|Q board and A board, showing an example of how to connect the sync wire.|

## Step 3 - A board modifications
Modifying the A board is pretty straight-forward. It's just a matter of removing and adding a few components. As noted earlier, some of these changes are not necessary if you are modifying the **non-SSM** variants based on the same chassis.

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

### Case / enclosure modification images
Image|Notes|
-----|-----|
|<img src="https://i.imgur.com/GO5K9MK.jpg" width="300">|Rear panel, showing an example of how to modify the rear panel.|

### 3D-printed front panel buttons
If you have access to a 3D printer, then you can print yourself some face buttons using the STL file here: https://www.thingiverse.com/thing:5029004. The STL file is also available on this GitHub page in the '..\Faceplate Button' directory. Kudos to 'galaxius' for kindly designing and printing the buttons for my own modified monitors.

Alternatively, for a small fee, I can provide you with two 3D printed buttons for switching between RGB and Line A. If you are interested, you can drop me an email: oo2@outlook.com. The cost is $5 AUD + shipping for 2 buttons. I can also sand and paint them for you for an additional $5 AUD - I will paint them with three coats of Tamiya Acrylic.

If you are using the suggested switches (or ones with very similar dimensions), the 3D printed buttons should remain captive in the hole and rest neatly against the switch acutator. Note that you will still need to punch or cut a square hole in the vinyl sticker so the button can protrude through.

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
