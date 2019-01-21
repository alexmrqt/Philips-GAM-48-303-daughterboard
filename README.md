# Philips GAM 48-303 fix

## Presentation
I am, since many years, the proud owner of a Philips GAM 48-303 soldering station.
This is an old piece of hardware, that works well nonetheless, and can even drive a brand new Hakko 907.

On the inside, it is only based around four main components:
 - A mains transformer that step down 230V AC to 24V AC,
 - A TIC225A triac to deliver (or not) power to the iron,
 - A CA3140 op-amp to compute an error signal from the temperature set point and the iron temperature,
 - A U106BS "monolithic integrated zero voltage", which is used to drive the triac (TIC225A) based on the error signal computed by the CA3140A op-amp (proportional controller).

Of these four components, the TIC225A triac and the U106BS are not produced any more. Finding a pin-compatible replacement for the TIC225A triac is easy, but none are available for the U106BS.

Unfortunately for me, the latter component ended up faulty in my soldering station. Thus, this project provides a KiCAD project for a daughter board that can be easily mounted on top of the existing board in the Philips GAM 48-303, and provide the features of the U106BS.

This daughter board is based on a UAA2016 "zero voltage switch power controller" and an additional CA3140 (to replace the internal op amp of the U106BS, any other op amp should do the job, by the way).

## Repository layout
This repository is organized as follows:
 - docs/ contains datasheet for the various components used in the project, as well as pictured of the original PCB present in the soldering station.
 - soldering-station-hat/ is a KiCAD project containing all the files to create and modify the daughter board.

 - soldering-station-pcb/ is a KiCAD project used for reverse-engineering purposes. Its schematics draws components and connection over a picture of the PCB.
 - soldering-station/ is a KiCAD project used for reverse-engineering purposes. Its schematics splits the original circuits into functional units. It also contains the way the UAA2016 and CA3140 should be connected with the original board.

## Final thoughts
Overall, after calibrating the circuit using the potentiometer of the error amplifier, this circuit works like a charm!

Be aware that I realized the circuit on a proto-board, and never had the occasion to make the PCB present in soldering-station-hat/ fabricated. Thus, it may or may not fit properly on top of the original circuit.

Finally, if I had to make a v2 of this project, I would add the necessary circuitry to adjust the hysteresis off the UAA2016, because the soldering station switch ON and OFF a bit too often for my taste.
