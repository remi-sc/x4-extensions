# vol_fog_optmized #

The aim of this extension is to optimize the very poor performance of volumetric fog
while trying to preserve the looks as best as possible.
Additionally volumetric fog is not possible to disable
(the corresponding option in graphics setting does not disable it even when set to "off")

This was kicked off from forum posts starting from:
https://forum.egosoft.com/viewtopic.php?f=180&t=414524&start=720#p5197757
There is more context there

## Installation ##

copy the `extensions/vol_fog_optmized` to your game/extensions dir

## Current status ##

```
--------+-----------------------------------------+--------+-------+---------------------------------------------------+
        |                                         | fps    | fps   |                                                   |
source  | region                                  | before | after | notes                                             |
--------+-----------------------------------------+--------+-------+---------------------------------------------------+
vanilla |empty (reference)                        | 225    |       |                                                   |
vanilla |testregion                               | 200    |       |                                                   |
vanilla |region_grav                              | 205    |       |                                                   |
vanilla |p1_40km_hydrogen_field                   | 95     |       |                                                   |
vanilla |p1_80km_hydrogen_field                   | 25     |       |                                                   |
vanilla |p1_40km_helium_field                     | 80     |       |                                                   |
vanilla |p1_40km_helium_highyield_field           | 80     |       |                                                   |
vanilla |p1_40km_methane_field                    | 82     |       |                                                   |
vanilla |p1_40km_methane_highyield_field          | 84     |       |                                                   |
vanilla |p1_wreckfield_xenon_battle_60km          | 99     |       |                                                   |
vanilla |p1_wreckfield_xenon_teladi_battle_200km  | 105    |       |                                                   |
vanilla |p1_wreckfield_xenon_teladi_10km          | 176    |       |                                                   |
vanilla |p1_wreckfield_xenon_split_cluster32      | 154    |       |                                                   |
vanilla |region_cluster_01_sector_001_a           | 187    |       |                                                   |
vanilla |region_cluster_01_sector_001_b           | 199    |       |                                                   |
vanilla |region_cluster_01_sector_001_c           | 196    |       |                                                   |
vanilla |region_cluster_01_sector_002_a           | 155    |       |                                                   |
vanilla |region_cluster_01_sector_002_b           | 189    |       |                                                   |
vanilla |region_cluster_01_sector_002_c           | 209    |       |                                                   |
vanilla |region_cluster_01_sector_002_d           | 179    |       |                                                   |
vanilla |region_cluster_01_sector_002_e           | 209    |       |                                                   |
vanilla |region_cluster_01_sector_002_f           | 191    |       |                                                   |
vanilla |region_cluster_01_sector_002_g           | 171    |       |                                                   |
vanilla |region_cluster_01_sector_002_h           | 206    |       |                                                   |
vanilla |region_cluster_01_sector_003_a           | 225    |       |                                                   |
vanilla |region_cluster_01_sector_003_b           | 212    |       |                                                   |
vanilla |region_cluster_01_sector_003_c           | 225    |       |                                                   |
vanilla |region_cluster_01_sector_003_d           | 223    |       | invisible spline                                  |
vanilla |region_cluster_01_sector_003_e           | 207    |       |                                                   |
vanilla |region_cluster_01_sector_003_f           | 211    |       |                                                   |
vanilla |region_cluster_02_sector_001b            | 136    |       |                                                   |
vanilla |region2_cluster_04_sector_001            | 203    |       |                                                   |
vanilla |region_cluster_07_sector_001             | 125    |       |                                                   |
vanilla |region_cluster_08_sector_001             | 82     |       |                                                   |
vanilla |region_cluster_14_sector_001             | 168    |       |                                                   |
vanilla |region_cluster_17_sector_001             | 86     |       |                                                   |
vanilla |region_cluster_25_sector_001             | 95     |       |                                                   |
vanilla |region_cluster_25_sector_002             | 118    |       |                                                   |
vanilla |region_cluster_26_sector_001             | 127    |       |                                                   |
vanilla |region_cluster_26_sector_002             | 140    |       |                                                   |
vanilla |region2_cluster_27_sector_001            | 87     |       |                                                   |
vanilla |region_cluster_31_sector_001             | 56     | 110   | heretic's end                                     |
vanilla |region_cluster_32_sector_001             | 133    |       |                                                   |
vanilla |region_cluster_32_sector_002             | 106    |       |                                                   |
vanilla |region_cluster_33_sector_001             | 156    |       | example of significant fog that performs well     |
vanilla |region_cluster_35_sector_001_a           | 79     |       |                                                   |
vanilla |region_cluster_37_sector_001             | 57     |       |                                                   |
vanilla |region_cluster_38_sector_001             | 168    |       |                                                   |
vanilla |region_cluster_38_sector_001_b           | 206    |       |                                                   |
vanilla |region_cluster_40_sector_001             | 156    |       |                                                   |
vanilla |region_cluster_41_sector_001             | 126    |       |                                                   |
vanilla |region_cluster_43_sector_001             | 102    |       |                                                   |
vanilla |region_cluster_44_sector_001             | 116    |       |                                                   |
vanilla |region_cluster_45_sector_001             | 121    |       |                                                   |
vanilla |region_cluster_46_sector_001             | 184    |       |                                                   |
vanilla |region_cluster_47_sector_001             | 50     |       |                                                   |
vanilla |region_cluster_47_sector_001b            | 41     | 135   |                                                   |
vanilla |region_cluster_48_sector_001             | 93     |       |                                                   |
vanilla |region_cluster_50_sector_001             | 54     |       |                                                   |
vanilla |region_cluster_50_sector_002             | 54     |       |                                                   |
vanilla |region_bigasteroids                      | 106    |       |                                                   |
vanilla |specialregion_cluster_14_sector_001      | 209    |       |                                                   |
vanilla |audioregion_cluster_14_sector_001        | 129    |       |                                                   |
--------+-----------------------------------------+--------+-------+---------------------------------------------------+
terran  | TODO                                    |        |       |                                                   |
pirate  | TODO                                    |        |       |                                                   |
split   | TODO                                    |        |       |                                                   |
boron   | TODO                                    |        |       |                                                   |
--------+-----------------------------------------+--------+-------+---------------------------------------------------+
```

# development #

- Testing in flight school universe for no universe simulation load - which means much less chance to be cpu-bound and 
much faster load times
- savegame used: `quicksave.xml.gz`
- to test in the flight school sector the region of that sector is replaced with target one. For example
```
<?xml version='1.0' encoding='utf-8'?>
<diff>
  <!-- Remove default flight school sector -->
  <remove sel="/regions/region[@name='audioregion_cluster_40_sector_001']"/>
  
  <!-- insert replacement - copy <region section >from .cat/libraries/region_definitions.xml
       and remember to replace the name with "audioregion_cluster_40_sector_001" -->
  <add sel="/regions">
  
  ... PASTE TARGET REGION HERE ...
  
  </region>
  
  </add>
</diff>
```

for example for Heretic's End:
```
<?xml version='1.0' encoding='utf-8'?>
<diff>
  <remove sel="/regions/region[@name='audioregion_cluster_40_sector_001']"/>
  <add sel="/regions">

  <region name="region_cluster_31_sector_001" density="1.5" rotation="0" noisescale="10000" seed="32" minnoisevalue="0.15" maxnoisevalue="1">
    <boundary class="cylinder">
      <size r="250000" linear="50000" />
    </boundary>
    <falloff>
      <lateral>
        <step position="0.0" value="0.0" />
        <step position="0.1" value="1.0" />
        <step position="0.9" value="1.0" />
        <step position="1.0" value="0.0" />
      </lateral>
      <radial>
        <step position="0.0" value="1.0" />
        <step position="0.3" value="1.0" />
        <step position="0.5" value="0.9" />
        <step position="0.9" value="0.4" />
        <step position="1.0" value="0.0" />
      </radial>
    </falloff>
    <fields>
      <!--positional ref="fog_outside_set1_lightorange_macro" lodrule="nebula" densityfactor="0.50" rotation="0" rotationvariation="0.5" noisescale="10000" seed="2001" minnoisevalue="0.90" maxnoisevalue="1.0" distancefactor="0.5"/-->
      <!--positional ref="fog_outside_set1_lightbrown_macro" densityfactor="0.30" rotation="0" rotationvariation="0.05" noisescale="25000" seed="26021984" minnoisevalue="0.90" maxnoisevalue="1.0" distancefactor="0.5"/-->
      <!--positional ref="fog_outside_set1_green_macro" lodrule="nebula" densityfactor="0.50" rotation="0" rotationvariation="0.5" noisescale="25000" seed="26021984" minnoisevalue="0.8" maxnoisevalue="1.0" distancefactor="0.25"/-->
      <volumetricfog multiplier="0.20" medium="fog_lightgreen" texture="assets/textures/environments/volumefog/vf_structured_01_diff" lodrule="nebula" size="22000" sizevariation="0.75" densityfactor="0.5" rotation="0" rotationvariation="0.5" noisescale="25000" seed="26021984" minnoisevalue="0.8" maxnoisevalue="0.9" distancefactor="0.250"/>

      <asteroid groupref="asteroid_ore_l" densityfactor="1.5" rotation="360" rotationvariation="4" noisescale="25000" seed="26021984" minnoisevalue="0.8" maxnoisevalue="1"/>
      <asteroid groupref="asteroid_ore_m" densityfactor="6" rotation="360" rotationvariation="8" noisescale="25000" seed="26021984" minnoisevalue="0.75" maxnoisevalue="1"/>
      <asteroid groupref="asteroid_ore_s" densityfactor="6" rotation="360" rotationvariation="16" noisescale="25000" seed="26021984" minnoisevalue="0.7" maxnoisevalue="1"/>
      <asteroid groupref="asteroid_ore_xs" densityfactor="6" rotation="360" rotationvariation="32" noisescale="25000" seed="26021984" minnoisevalue="0.65" maxnoisevalue="1"/>
      <!-- TODO @Alexei: add ambient sounds -->
    </fields>
    <resources>
      <resource ware="ore" yield="medium" />
    </resources>
  </region>

  </add>
</diff>
```
- change the parameters in `<volumetricfog`
- start the game and set graphic preset to "low", 3840x2160, no AA, no upscale
 (Add `<showfps>true</showfps>` and `<skipintro>true</skipintro>` to `config.xml` to expedite launching
- load the save 
- check fps without moving the camera
- rince and repeat until going through all problematic sectors
- when performance is satisfactory, take the `<volumetricfog>` tags and covert them into corresponding
`<replace>` ones and add to `extensions/vol_fog_optmized/libraries/region_definitions.xml`

# notes #

Tests performed in following environment:
- Ryzen 3700x
- RX 6700 10G
- 128GB ECC-DDR4 3200Mhz
- Linux kernel 6.4.4
- amdvlk vulkan userspace driver (mesa/radv is a bit faster but radeon GPU profiler does not support it)
- no upscale
- X4 version 6.10 
- all DLCs installed

Random thoughts:
- some sectors have seemingly invisible spline fogs lines (this may be a bug?)
- on some sectors the testing positon from the save is not that representative but
there that's a compromise to have consistent testing.

