# KiCad Vacuum Tube Library

This library provides symbols for various vacuum (electron) tubes (or as the
Brits call 'em, valves). It also contains generic symbols for different tube
circuits.

## Symbol Design Decisions

### Pin Locations

Generally, symbols follow these rules:

- *Plate/Anode* is on the top
- *Control grid* is on the left
- *Cathode* is on the right
- Additional grids are on the right

### Symbol Units

If present, the heater is separated into a separate unit. Although this breaks
KiCad library conventions, vacuum tube circuit diagrams will often have all the
heaters in the same place, somewhere off to the side, in order to reduce
clutter.

Each logical element of the tube is split into symbol units, **even if they
share some elements**. For example, the **6AV6** tube contains a triode and two
diodes with a shared cathode. It is structured into four units:

- Unit A - Triode
- Unit B - First diode
- Unit C - Second diode
- Unit D - Heater

Note that the KiCad 9.0 ERC does complain about duplicate cathode pins between
Units A, B, C. It's possible to share a pin between all units, but that
typically is not good enough for tube schematics, so for now, the error needs to
manually supressed in the ERC.

### Generic Components

`Device_Vacuum_Tube` provides generic vacuum tube symbols analogous to the
generic transistors in the standard `Device` library. Versions with heaters and
without heaters are provided. These symbols can and should be used as templates
for creating new symbols.

The naming pattern for these symbols is:

```
VT_<type>_[variation]_[heater]
```

For example:

- `VT_Pentode` - Generic pentode, no heater
- `VT_Pentode_G3K` - Generic pentode, G3 internally connected to K, no heater
- `VT_Triode_H` - Generic triode, with heater
- `VT_Diode_F` - Generic diode, directly heated cathode
