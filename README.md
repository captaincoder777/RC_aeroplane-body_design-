# RC_aeroplane(body_design)
RC aeroplane using sun board which is completely focused on body design and aerodynamics

Designe custom , scratch built fixed wing remote controlled aircraft engineered in AutoDesk Fusion 360 and constructed from 5mm sun board. 

Powered by An A2212 1200KV brushless propulsion system and controlled via a FlySky FS-i6S / FS-iA10B radio link. 

This project focuses on practical aerodynamics , airframe design , and interactive flight testing. 

## Project Motivation

Rather than assembling a pre-molded foam kit, I wanted to engineer a fixed-wing aircraft from first principles—starting from airfoil selection and 3D CAD modeling in Fusion 360 to hand-forming 5mm Sun Board, configuring channel mixing, and troubleshooting real crash and flight-test data. Through iterative prototyping, I learned how airfoil camber, center of gravity (CG), motor thrust angles, and power distribution directly govern flight stability.

## Airframe Dimensions & Wing Design

I used **5mm Sun Board** instead of 2mm because it holds its shape much better against wind and rough landings. The catch is that 5mm board snaps cleanly in half if you try to bend it cold, so I used a heat gun to soften the sheet gradually while curving the wing camber.

| Section | Material | Measurements | Notes |
| :--- | :--- | :--- | :--- |
| **Main Wing** | 5mm Sun Board (Heat-formed) | **90 cm** span, **15 cm** chord | High-wing mount; left hollow inside for aileron servo wires |
| **Airfoil** | **NACA 4412** | 4% camber at 40% chord, 12% thickness | Flat bottom with curved top for solid lift at slow speeds |
| **Fuselage** | 5mm Sun Board | **60 cm** long, **5 cm** wide (tapers to **3 cm** at tail) | Removable nose for motor access; wing sits at the 15 cm mark |
| **Ailerons** | 5mm Sun Board + Duct Tape | **32 cm × 3 cm** each | Hinged with duct tape so they can be replaced fast if torn |
| **Elevator & Rudder** | 5mm Sun Board | Full-span tail surfaces | Driven by steel pushrods routed through the tail section |

<img width="1600" height="624" alt="image" src="https://github.com/user-attachments/assets/4c5dff4b-11f3-4b58-8bfa-72b2b76f4caf" />


### Build Choices That Mattered
* **Modular Wing Attachment:** Instead of glue the wing permanently, I fixed it onto the fuselage saddle with wooden skewers and rubber bands during crashes, the bands absorb the shock and let the wing free instead of ripping the fuselage .
* **Motor Offset Angle:** I tilted the A2212 1400KV motor mount **3°** to counter propeller torque so the plane wouldn't roll to one side right after launch.

## CAD Modeling (Autodesk Fusion 360)

Before touching a blade to the Sun Board i modeled the full airframe in Fusion 360:
* **Fuselage & Tail:** Sketched one side wall , mirrored it , and angled the tail base upward so the plane sits at a positive angle of attack on the ground.

  <img width="291" height="354" alt="image" src="https://github.com/user-attachments/assets/4e10ae2c-a8d4-461c-91c1-9b3e07a1aafc" />


<img width="807" height="508" alt="image" src="https://github.com/user-attachments/assets/fa8c6847-ab9c-4d64-9a29-069ea0adcbbf" />

  
* **NACA 4412 Wing:** Used arcs and splines to trace the curved upper airfoil and flat bottom , extruded it out to 90 cm, and cut pockets into the underside so the two aileron servos sit half inside the wing.

<img width="705" height="638" alt="image" src="https://github.com/user-attachments/assets/952376e2-a9bb-4c0e-9026-325e320a7a60" />


<img width="453" height="359" alt="image" src="https://github.com/user-attachments/assets/3bdbbad8-96a3-4572-8b16-5db1de6bbcdf" />

  
* **Custom 3D-Printed Parts:** Downloaded control horn STLs kept failing on two different printers, so I designed my own flat-base clip-on horns and motor firewall mount from scratch in Fusion 360.

# Full CAD assembly along with Electronics

<img width="914" height="271" alt="image" src="https://github.com/user-attachments/assets/f4c096e5-ff36-42e6-9b0a-788dd17e5355" />


<img width="479" height="389" alt="image" src="https://github.com/user-attachments/assets/60f605cf-6500-481d-8c0f-b4697692283a" />


<img width="466" height="708" alt="image" src="https://github.com/user-attachments/assets/9942337e-3b96-4d4a-aae2-4e19a4af65c3" />


<img width="495" height="192" alt="image" src="https://github.com/user-attachments/assets/0c58ad78-47c1-409d-b0a4-c17c4591a34f" />

## Electronics & FlySky FS-i6S Setup

The power system pairs a **3S 11.1V 2200mAh 35C LiPo** (`~200 g`) with an **A2212 1400KV** brushless motor (`1400 × 11.1V = 15,540 RPM` unloaded) and a **30A ESC**.

### Receiver Wiring (`FlySky FS-iA10B`)

| Receiver Port | Connected Part | What It Controls |
| :--- | :--- | :--- |
| **CH1** | Left Aileron Servo (`MG90S`) | Roll (Master channel) |
| **CH2** | Elevator Servo (`MG90S`) | Pitch (hidden servo inside tail) |
| **CH3** | 30A Brushless ESC | Motor throttle + supplies `5V` BEC power to receiver |
| **CH4** | Rudder Servo (`MG90S`) | Yaw |
| **CH5** | Right Aileron Servo (`MG90S`) | Roll (Slave channel mixed from CH1) |
| **CH6–CH10** | Empty | Not used |

### Transmitter Tuning & Safety Settings

* **Aileron Mix (`CH1 → CH5`):** Because the left and right wing servos are mounted mirrored to each other plugging them into a standard setup makes both flaps move the same way i cleared `CH5` from the top knob (`Aux. channels → Nul`) and set up **Mix 1** with `CH1` as Master and `CH5` as Slave at **100%** so one aileron goes up while the other goes down.
  
* **90% Throttle Limit:** Bench tests showed full 100% throttle pushed current draw right to the 30A ESC's thermal limit, so I capped the throttle endpoint at **90%**.
  
* **Kill Switch & Fail-Safe:** Programmed the FS-iA10B fail-safe so `CH3` drops immediately to **`-100%`** (motor off) if the signal drops or I flip the emergency kill switch.

## Bill of Materials

| Part | Details | Qty | Price |Source |
| :--- | :--- | :--- | :--- | :--- |
| **Brushless Motor** | A2212 1400KV | 1 | $ 4 | https://robu.in/product/a2212-10t-13t-1400kv-brushless-motor-with-soldered-connector/ |
| **ESC** | 30A Brushless ESC (with 5V BEC) | 1 | $ 4 | https://robu.in/product/30a-bldc-esc-electronic-speed-controller/ |
| **Propeller** | 10×4.5 / 9×4.5 | 2 | $ 3 | https://robu.in/product/orange-hd-propellers-90459x4-5-glass-fiber-nylon-1cw1ccw-1pair-grey/ |
| **Battery** | 3S 11.1V 2200mAh 35C LiPo | 1 | $21 | https://robocraze.com/products/bonka-2200mah-35c-3s1p-11-1v-lipo-battery?srsltid=AYCX9vLNrhRPwrTPco0temPQehwEhiwKgbKT7DRJzPEuJOA4HpuxUuzz |
| **Radio System** | FlySky FS-i6S Transmitter + FS-iA10B 10-Ch Receiver | 1 Set | $96 | https://robu.in/product/flysky-fs-i6s-2-4ghz-10ch-afhds-2a-rc-transmitter-with-fs-ia10b-10ch-receiver/?gad_source=1&gad_campaignid=17419548928&gbraid=0AAAAADvLFWdtac96sDBsSiEi0dJVB5eJ_&gclid=CjwKCAiAquDXBhApEiwAoyNqBMhySPPs9hCK_4_34ef8c7B5dS2-AB6sF9ZG4XoIhrKGFzlSfo_XEhoCfAkQAvD_BwE |
| **Servos** | MG90S Metal Gear (9g) | 4 | $13 | https://robu.in/product/mg90s-9g-servo-metal-gear/|
| **Airframe Sheet** | 5mm Sun Board | 3 Sheet | $11| https://www.amazon.in/Lakeer-Lightweight-Signboard-Reflector-Photography/dp/B0BRXZ2QLX/ref=sr_1_49_sspa?dib=eyJ2IjoiMSJ9.JoZNfAEZchBht5AMQqKGXctRhkha-jbXLEAHmiZBSz0wLaT6mE6YAJ0KG9KB7jK3uNLznQ1zxxPl5la94EbzxcA34Xg_mDRt-1heTWfznM2JOLCoDsOzdIjJCssm2xRYUL5guT12VfMOK-Qz6OJLTVljk0iMxcsnG4j9PvHSBCh5Bql0lA__srS0BTO-ZhsViPUrv7J6ooFm-Nh-aGGnF-WvuLWZcgcHcpIIVwTMbnRssFsUeOxfGA-mRKizECax1nYwBLQF_fKSFml6ZFBLFEcFVAKN7yeuNheyEctcQpQ.e-5ClYDClobF5hywvikH2SgqCFdCmGsFSSAzZDMRvNY&dib_tag=se&keywords=sun%2Bboard%2Bsheet%2B5mm%2Blarge%2Bsize&qid=1794669053&sr=8-49-spons&aref=f8QedCN2ao&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGZfbmV4dA&th=1|
| **Linkages & Hardware** | Steel pushrods, 3D-printed horns & motor mount(self printed) , skewers(self sourced) , rubber bands(self sourced) , duct tape | 1 Set | $10 |https://www.amazon.in/FlyingMachines-Airplane-Push-Rod-Linkage/dp/B0GL88P6G1/ref=sr_1_4?dib=eyJ2IjoiMSJ9.6M45WJEj5z5qOvmxpTzVYEu-Xvh0BhidOIm0OK0YmkgEfsoGTNu45G0F1CBXnKC_I9otP65zT-xu_rsJP5Xs8g4Md68ptcf1nsI54vajwyl-_QU22tFQFwUul0wXu3ENbojnCqer-YyLZH1YmXGibmc6pVqiwYLRbeXEN4hD3D2vP6cxD3CyNtqV7M1AWt_3kxWnJzEK7XCW4FZTTPVaMP-_rkglAgvLVDUYtIwHjkMsht8BX3ukzeH0iddQegHiWcIliAWW-CLXxDnU5aCIs0SMyE5X6l6qFiX2dz5Y580.zGQ7mH99hjP3IhjrFcBo1XPhzetbSdNyuLoEdnKMhE4&dib_tag=se&keywords=pushrods+for+rc+plane&qid=1794669201&sr=8-4|


## Test Flights, Crashes & What I Fixed

Every test session showed me  something I missed on the workbench:

1. **Snapping the First Wing:** Trying to bend 5mm Sun Board cold cracked the sheet straight down the middle warming it slowly with a heat gun let me form the NACA 4412 curve cleanly and I spliced the two halves together with an internal Sun Board joiner and duct tape.
2. **Loose Prop Adapter on Bench Run:** During early throttle test the prop mount wasn't spinning according to the motor shaft tightly enough caused the prop to slip out of sync. Tightened the collet properly and kept spares after a nose-in landing snapped the first adapter.
3. **High-Throttle Rudder Shake:** Ground throttle runs caused the 5mm vertical fin to vibrate rapidly reinforcing the fin base and hinge line with duct tape stopped the flutter completely.
4. **Unstrapped Battery Shift:** On an early hand launch into wind, the plane pitched up too steep, stalled, and the loose battery slid forward sending it straight into the ground on its nose and cracking the mid-fuselage. Glued and taped the fuselage spine back together and locked the battery down tightly right at the **CG mark**.
5. **Control Surface Sync Issues:** Initially the servos jumped to the wrong directions and channels didn't match my stick inputs Re-mapped the receiver pins dialed in the `CH1 → CH5` mix and verified every surface angle on the ground before flying again.


# Test videos

* **First crash: ** https://youtube.com/shorts/VGiG9RxfIqw?feature=share
* **Second crash: ** https://youtu.be/t4nsS9l1lS4

## Tools & Resources Used
* * **Autodesk Fusion 360** — Airframe CAD, custom motor mount, and clip-on control horns
* * **[GrabCAD](https://grabcad.com/library)** - CAD electronic models for full CAD assembly
* * **Hack Club Forge** — Build documentation and dev log tracking
