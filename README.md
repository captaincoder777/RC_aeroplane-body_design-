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




<img width="466" height="708" alt="image" src="https://github.com/user-attachments/assets/9942337e-3b96-4d4a-aae2-4e19a4af65c3" />


